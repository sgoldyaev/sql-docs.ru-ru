---
title: "ПРЕДСТАВЛЕНИЯ (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VIEWS_TSQL
- VIEWS
dev_langs: TSQL
helpviewer_keywords:
- VIEWS view
- INFORMATION_SCHEMA.VIEWS view
ms.assetid: 6119bc94-0b22-45d4-a34b-967afd810a9d
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fdfae119d9ed1c214c745de30f019588f47e1a2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Возвращает одну строку для представлений, доступ к которым имеет текущий пользователь в текущей базе данных.  
  
 Чтобы получить сведения из этих представлений, укажите полное имя **INFORMATION_SCHEMA.** *view_name*.  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|**ЗНАЧЕНИЯМ TABLE_CATALOG**|**nvarchar (**128**)**|Квалификатор представления.|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|Имя схемы, содержащей представление.<br /><br /> **\*\*Важные \* \***  не используйте представления INFORMATION_SCHEMA, чтобы определить схему объекта. Единственный надежный способ найти схему объекта — направить запрос к представлению каталога sys.objects.|  
|**ИМЯ_ТАБЛИЦЫ**|**nvarchar (**128**)**|Имя представления.|  
|**VIEW_DEFINITION**|**nvarchar (**4000**)**|Если длина или определение больше, чем **nvarchar (**4000**)**, этот столбец равен NULL. В противном случае этот столбец является текстом определения представления.|  
|**CHECK_OPTION**|**varchar (**7**)**|Тип инструкции WITH CHECK OPTION. CASCADE, если первоначальное представление было создано с помощью инструкции WITH CHECK OPTION. Иначе возвращается значение NONE.|  
|**IS_UPDATABLE**|**varchar (**2**)**|Указывает, можно ли обновлять это представление. Всегда возвращает NO.|  
  
## <a name="see-also"></a>См. также:  
 [Системные представления &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Представления информационной схемы &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views (Transact-SQL)](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  