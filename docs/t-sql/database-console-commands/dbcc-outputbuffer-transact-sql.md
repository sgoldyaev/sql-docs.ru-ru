---
title: "Инструкция DBCC OUTPUTBUFFER (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC OUTPUTBUFFER
- OUTPUTBUFFER_TSQL
- OUTPUTBUFFER
- DBCC_OUTPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC OUTPUTBUFFER statement
- output buffers
- current output buffer
ms.assetid: e912a06d-9fde-4e26-b057-801255d79504
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: de51ee1a87f37e8fcdf97e23be0d2fb9701e9433
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-outputbuffer-transact-sql"></a>DBCC OUTPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Возвращает текущий буфер вывода в шестнадцатеричном формате и формате ASCII для указанного *session_id*.
  
![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Синтаксис  
```sql
DBCC OUTPUTBUFFER ( session_id [ , request_id ])  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Аргументы  
 *session_id*  
 Идентификатор сеанса, связанный с каждым активным первичным соединением.  
  
 *идентификатор_запроса*  
 Строгий (пакетный) запрос для поиска в текущем сеансе.  
 Следующий запрос возвращает *request_id*:  
  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
  
 на  
 Позволяет указывать параметры.  
  
 NO_INFOMSGS  
 Подавляет все информационные сообщения со степенями серьезности от 0 до 10.  
  
## <a name="remarks"></a>Замечания  
DBCC OUTPUTBUFFER выводит результаты, отправленные для указанного клиента (*session_id*). Для процессов, не содержащих выходных потоков, возвращается сообщение об ошибке.
  
Для вывода выполненной инструкции, которая возвратила результаты, отображаемые инструкцией DBCC OUTPUTBUFFER, выполните инструкцию DBCC INPUTBUFFER.
  
## <a name="result-sets"></a>Результирующие наборы  
Инструкция DBCC OUTPUTBUFFER возвращает следующее (значения могут меняться):
  
```sql
Output Buffer                                                              
------------------------------------------------------------------------   
01fb8028:  04 00 01 5f 00 00 00 00 e3 1b 00 01 06 6d 00 61  ..._.........m.a  
01fb8038:  00 73 00 74 00 65 00 72 00 06 6d 00 61 00 73 00  .s.t.e.r..m.a.s.  
'...'  
01fb8218:  04 17 00 00 00 00 00 d1 04 18 00 00 00 00 00 d1  ................  
01fb8228:   .  
  
(33 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
Необходимо членство в предопределенной роли сервера **sysadmin** .
  
## <a name="examples"></a>Примеры  
В следующем примере сведения о текущем буфере вывода возвращаются для вымышленного идентификатора сеанса `52`.
  
```sql
DBCC OUTPUTBUFFER (52);  
```  
  
## <a name="see-also"></a>См. также:  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[Флаги трассировки (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
