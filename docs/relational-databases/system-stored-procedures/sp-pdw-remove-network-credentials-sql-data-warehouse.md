---
title: "sp_pdw_remove_network_credentials (хранилище данных SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30f35803c804b6e895bf5287cb864c9cc979f013
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="sppdwremovenetworkcredentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials (хранилище данных SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Эта функция удаляет сетевые учетные данные, хранящиеся в [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] для доступа к общей сетевой папке. Например, использовать эту хранимую процедуру для удаления разрешений для [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] для архивации и восстановления операции на сервере, который находится в пределах своей сети.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "значок ссылки на раздел") [синтаксические обозначения Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>Аргументы  
 "*имя_сервера_назначения*"  
 Указывает имя целевого сервера узла или IP-адрес. Учетные данные для доступа к серверу будут удалены из [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Это не измените или удалите разрешения на фактический целевой сервер, который находится под управлением вашей группе.  
  
 *имя_сервера_назначения* определяется как nvarchar(337).  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="permissions"></a>Permissions  
 Требуется **ALTER SERVER STATE** разрешение.  
  
## <a name="error-handling"></a>Обработка ошибок  
 Если удаление учетных данных не работает на узле управления, а все вычислительные узлы, возникает ошибка.  
  
## <a name="general-remarks"></a>Общие замечания  
 Эта хранимая процедура удаляет сетевые учетные данные из учетной записи NetworkService для [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Учетной записи NetworkService выполняется каждый экземпляр SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на узел элемента управления и вычислительных узлов. Например при выполнении операции резервного копирования, узел элемента управления и каждый вычислительный узел будет использовать учетные данные учетной записи NetworkService для доступа к целевой сервер.  
  
## <a name="metadata"></a>Метаданные  
 Чтобы проверить учетные данные будут удалены и список всех учетных данных, используйте [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
 Чтобы добавить учетные данные, используйте [sp_pdw_add_network_credentials &#40; Хранилище данных SQL &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Примеры: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. Удаление учетных данных для выполнения резервной копии базы данных  
 Следующий пример удаляет учетные данные имя и пароль пользователя для доступа на сервер, который имеет IP-адрес 10.192.147.63.  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  
