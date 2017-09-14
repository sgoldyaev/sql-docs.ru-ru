---
title: "Чтение данных из таблицы (учебник) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4f808355e765cb54fa973fce76af98ae56dbdc5
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-4---reading-the-data-in-a-table"></a>Занятие 1-4-чтение данных в таблице
Для чтения данных в таблице используется инструкция SELECT. Инструкция SELECT является одной из наиболее важных инструкций [!INCLUDE[tsql](../includes/tsql-md.md)] , и для нее существует много разновидностей синтаксиса. В этом учебнике будет показана работа с пятью простыми вариантами.  
  
### <a name="to-read-the-data-in-a-table"></a>Чтение данных из таблицы  
  
1.  Чтобы прочитать данные из таблицы `Products` , введите и выполните следующие инструкции.  
  
    ```  
    -- The basic syntax for reading data from a single table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
    GO  
  
    ```  
  
2.  Чтобы выбрать все столбцы в таблице, можно использовать звездочку. Такой способ часто используется в нерегламентированных запросах. Необходимо предоставить список всех столбцов в постоянном коде, чтобы инструкция возвращала нужные столбцы, даже если какой-то столбец будет добавлен в таблицу позднее.  
  
    ```  
    -- Returns all columns in the table  
    -- Does not use the optional schema, dbo  
    SELECT * FROM Products  
    GO  
  
    ```  
  
3.  Если нет необходимости возвращать определенные столбцы, их можно опустить. Столбцы возвращаются в том порядке, в котором они перечислены.  
  
    ```  
    -- Returns only two of the columns from the table  
    SELECT ProductName, Price  
        FROM dbo.Products  
    GO  
  
    ```  
  
4.  Чтобы ограничить количество строк, возвращаемых пользователю, используйте предложение `WHERE` .  
  
    ```  
    -- Returns only two of the records in the table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
        WHERE ProductID < 60  
    GO  
  
    ```  
  
5.  Можно работать со значениями столбцов, по мере того как столбцы возвращаются. В следующем примере выполняется математическая операция над столбцом `Price` . Столбцы, изменяемые подобным образом, не имеют имени, если только имя не указывается с использованием ключевого слова `AS` .  
  
    ```  
    -- Returns ProductName and the Price including a 7% tax  
    -- Provides the name CustomerPays for the calculated column  
    SELECT ProductName, Price * 1.07 AS CustomerPays  
        FROM dbo.Products  
    GO  
    ```  
  
## <a name="functions-that-are-useful-in-a-select-statement"></a>Функции, используемые в инструкции SELECT  
Сведения о работе с функциями, которые используются в инструкциях SELECT, см. в следующих разделах:  
  
|||  
|-|-|  
|[Строковые функции (Transact-SQL)](../t-sql/functions/string-functions-transact-sql.md)|[Типы данных и функции даты и времени (Transact-SQL)](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[Математические функции (Transact-SQL)](../t-sql/functions/mathematical-functions-transact-sql.md)|[Функции для работы с типами данных text и image (Transact-SQL)](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
[Сводка. Создание объектов базы данных](../t-sql/lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>См. также:  
[SELECT (Transact-SQL)](../t-sql/queries/select-transact-sql.md)  
  
  
  
