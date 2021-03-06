---
title: sp_copymergesnapshot (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_copymergesnapshot
- sp_copymergesnapshot_TSQL
helpviewer_keywords:
- sp_copymergesnapshot
ms.assetid: eaecd6e0-8486-4e5d-ace7-8ae75768c0a8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b4cc5310a96376957110e3baf11da606ba91c296
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822032"
---
# <a name="spcopymergesnapshot-transact-sql"></a>sp_copymergesnapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Копирует папку моментальных снимков указанной публикации в папку, указанную в **@destination_folde*** r*. Эта хранимая процедура выполняется на издателе в базе данных публикации.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_copymergesnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder'  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@publication=**] **"***публикации***"**  
 Имя публикации, из моментального снимка которой копируется содержимое. *Публикация* — **sysname**, не имеет значения по умолчанию.  
  
 [  **@destination_folder=**] **"***папка_назначения***"**  
 Имя папки, куда будет скопировано содержимое моментального снимка публикации. *папка_назначения*— **nvarchar(255)**, не имеет значения по умолчанию. *Папка_назначения* может быть альтернативное расположение, например, на другом сервере, на сетевом диске или на съемном носителе (например, компакт-диски или съемные диски).  
  
## <a name="return-code-values"></a>Значения кода возврата  
 **0** (успешное завершение) или **1** (неуспешное завершение)  
  
## <a name="remarks"></a>Примечания  
 **sp_copymergesnapshot** используется в репликации слиянием. Подписчики, использующие [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] версии 7.0 и более ранних версий не могут использовать альтернативное расположение моментальных снимков.  
  
## <a name="permissions"></a>Разрешения  
 Только члены **sysadmin** предопределенной роли сервера или **db_owner** предопределенной роли базы данных могут выполнять процедуру **sp_copymergesnapshot**.  
  
## <a name="see-also"></a>См. также  
 [Альтернативные расположения папки моментальных снимков](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
