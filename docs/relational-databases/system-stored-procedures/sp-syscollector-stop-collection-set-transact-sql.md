---
title: "sp_syscollector_stop_collection_set (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_stop_collection_set_TSQL
- sp_syscollector_stop_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_stop_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 4668cfb7-462f-40d0-948c-8f740a792a4d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 828d097a749fd1c0db89d24d2079fed5a5fd2ce9
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="spsyscollectorstopcollectionset-transact-sql"></a>sp_syscollector_stop_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Останавливает набор элементов сбора.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_syscollector_stop_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @stop_collection_job = ] stop_collection_job ]  
```  
  
## <a name="arguments"></a>Аргументы  
 [ @collection_set_id = ] *collection_set_id*  
 Уникальный локальный идентификатор набора элементов сбора. *collection_set_id, чтобы выделить* — **int** со значением по умолчанию NULL. *collection_set_id, чтобы выделить* должно иметь значение, если *имя* имеет значение NULL.  
  
 [ @name =] '*имя*"  
 Имя набора элементов сбора. *имя* — **sysname** со значением по умолчанию NULL. *имя* должно иметь значение, если *collection_set_id, чтобы выделить* имеет значение NULL.  
  
 [ @stop_collection_job = ] *stop_collection_job*  
 Указывает, что задание сбора для набора элементов сбора должно быть остановлено, если оно выполняется. *stop_collection_job* — **бит** значение по умолчанию 1.  
  
 *stop_collection_job* применяется только к наборам элементов сбора с установлен кэшированный режим сбора. Дополнительные сведения см. в разделе [sp_syscollector_create_collection_set &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="remarks"></a>Remarks  
 Функция sp_syscollector_create_collection_set должна выполняться в контексте системной базы данных msdb.  
  
## <a name="permissions"></a>Разрешения  
 Для выполнения этой процедуры требуется членство в предопределенной роли базы данных dc_operator (с разрешением EXECUTE).  
  
## <a name="examples"></a>Примеры  
 В следующем примере набор сбора останавливается с помощью его идентификатора.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>См. также  
 [Сбор данных](../../relational-databases/data-collection/data-collection.md)   
 [Хранимые процедуры сборщика данных (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  