---
title: Указание механизма параметризации запросов с помощью структур плана | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: da60ceee93802b14b7d09392740a1f6b471e4ab1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148204"
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>Указание механизма параметризации запросов с помощью структур плана
  Если для параметра базы данных PARAMETERIZATION установлено значение SIMPLE, оптимизатор запросов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может выбрать параметризацию запросов. Это значит, что все литеральные значения, содержащиеся в запросе, заменяются параметрами. Этот процесс называется простой параметризацией. При применении простой (SIMPLE) параметризации невозможно контролировать, какие запросы параметризуются, а какие нет. Однако можно параметризовать все запросы в базе данных, присвоив параметру базы данных PARAMETERIZATION значение FORCED. Этот процесс называется принудительной параметризацией.  
  
 Механизм параметризации в базе данных можно переопределить с помощью структур планов следующим путем.  
  
-   Если значение параметра базы данных PARAMETERIZATION равно SIMPLE, можно указать, чтобы попытки принудительной параметризации выполнялись в определенном классе запросов. Это можно сделать путем создания структуры плана TEMPLATE для параметризованной формы запроса и задания указания запроса PARAMETERIZATION FORCED с помощью хранимой процедуры [sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) . Такая разновидность структуры плана представляет собой способ включения принудительной параметризации только для определенного класса запросов, а не для всех.  
  
-   Если значение параметра базы данных PARAMETERIZATION равно FORCED, можно указать, чтобы для определенного класса запросов выполнялись только попытки простой параметризации вместо принудительной. Это можно сделать путем создания структуры плана TEMPLATE для формы запроса с принудительной параметризацией и задания указания запроса PARAMETERIZATION SIMPLE с помощью хранимой процедуры **sp_create_plan_guide**.  
  
 Рассмотрим следующий запрос к базе данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 Администратор базы данных решил не включать принудительную параметризацию для всех запросов к базе данных. Однако необходимо избегать затрат на компиляцию для всех запросов, синтаксически эквивалентных предыдущему и различающихся только литеральными значениями констант. Иными словами, необходимо реализовать параметризацию запроса таким образом, чтобы план для данного вида запроса использовался повторно. В этом случае нужно выполнить следующее.  
  
1.  Получить параметризованную форму запроса. Единственным безопасным путем получения этого значения для последующего использования в процедуре **sp_create_plan_guide** является использование системной хранимой процедуры [sp_get_query_template](/sql/relational-databases/system-stored-procedures/sp-get-query-template-transact-sql) .  
  
2.  Создать структуру плана для параметризованной формы запроса, задав указание запроса PARAMETERIZATION FORCED.  
  
    > [!IMPORTANT]  
    >  В ходе параметризации запроса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] присваивает параметрам, заменяющим литеральные значения, определенный тип данных в зависимости от значения и размера литерала. Подобный процесс выполняется и для значений констант-литералов, передаваемых в качестве выходного параметра **@stmt** процедуры **sp_get_query_template**. Так как тип данных, указанный в аргументе **@params** процедуры **sp_create_plan_guide** , должен соответствовать типу данных в запросе после его параметризации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], может потребоваться создание нескольких структур планов для охвата всего диапазона возможных значений параметров запроса.  
  
 Следующий скрипт можно использовать как для получения параметризированного запроса, так и для дальнейшего создания по нему структуры плана:  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 Подобным образом в базе данных, в которой уже включена принудительная параметризация, можно гарантировать, что указанный в качестве примера запрос и другие синтаксически ему эквивалентные, в которых различаются только литеральные значения констант, будут параметризованы согласно правилам простой параметризации. Для этого следует указать PARAMETERIZATION SIMPLE вместо PARAMETERIZATION FORCED в предложении OPTION.  
  
> [!NOTE]  
>  С помощью структур плана TEMPLATE осуществляется сопоставление инструкций с запросами, поступающими в пакетах, каждый из которых состоит только из одной инструкции. Инструкции, находящиеся в пакетах с несколькими инструкциями, не подлежат сопоставлению со структурами планов TEMPLATE.  
  
  
