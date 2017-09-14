---
title: "COMMIT TRANSACTION (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 09/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- user-defined transactions [SQL Server]
- committed transactions
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- implicit transactions
- distributed transactions [SQL Server], committed
- transactions [SQL Server], committed
- COMMIT TRANSACTION statement
- rolling back transactions, COMMIT TRANSACTION
ms.assetid: f8fe26a9-7911-497e-b348-4e69c7435dc1
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 84ca8221700d3eabd443b84d97dea4f698e9f945
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Отмечает успешное завершение явной или неявной транзакции. Если @@TRANCOUNT -1, инструкция COMMIT TRANSACTION делает все изменения данных выполняется с момента начала транзакции постоянной частью базы данных, освобождает ресурсы, удерживаемые транзакцией и уменьшает значение @@TRANCOUNT значение 0. Если @@TRANCOUNT больше 1, инструкция COMMIT TRANSACTION уменьшает @@TRANCOUNT только на 1 и транзакция остается активной.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Applies to SQL Server (starting with 2008) and Azure SQL Database
  
COMMIT [ { TRAN | TRANSACTION }  [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
[ ; ]  
```  
 
```  
-- Applies to Azure SQL Data Warehouse and Parallel Data Warehouse Database
  
COMMIT [ TRAN | TRANSACTION ] 
[ ; ]  
``` 
 
  
## <a name="arguments"></a>Аргументы  
 *transaction_name*  
 **ПРИМЕНЯЕТСЯ к:** SQL Server и база данных Azure SQL
 
 Не учитывается компонентом [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. *transaction_name* указывает имя транзакции, присвоенное предыдущей BEGIN TRANSACTION. *transaction_name*должны соответствовать правилам для идентификаторов, но не может превышать 32 символов. *transaction_name* может использоваться как подсказка, показывающая программистам, с какими вложенными инструкциями BEGIN TRANSACTION связана инструкция COMMIT TRANSACTION, с.  
  
 *@tran_name_variable*  
 **ПРИМЕНЯЕТСЯ к:** SQL Server и база данных Azure SQL  
 
Имя определенной пользователем переменной, содержащей допустимое имя транзакции. Переменная должна быть объявлена с типом данных char, varchar, nchar или nvarchar. Если переменной присваивается значение длиной более 32 символов, используются только первые 32, остальные усекаются.  
  
 DELAYED_DURABILITY  
 **ПРИМЕНЯЕТСЯ к:** SQL Server и база данных Azure SQL   

 Параметр, который запрашивает фиксацию этой транзакции с задержанной устойчивостью. Этот запрос пропускается, если база данных была изменена с использованием `DELAYED_DURABILITY = DISABLED` или `DELAYED_DURABILITY = FORCED`. См. в разделе [управление устойчивостью транзакций](../../relational-databases/logs/control-transaction-durability.md) для получения дополнительной информации.  
  
## <a name="remarks"></a>Замечания  
 Обязанностью программиста на языке [!INCLUDE[tsql](../../includes/tsql-md.md)] является вызов инструкции COMMIT TRANSACTION только в том случае, когда все данные, относящиеся к транзакции, логически верны.  
  
 Если зафиксированная транзакция является распределенной транзакцией [!INCLUDE[tsql](../../includes/tsql-md.md)], инструкция COMMIT TRANSACTION вызывает координатор MS DTC для использования двухфазного протокола фиксации на всех серверах, участвующих в транзакции. Если локальная транзакция охватывает две или более базы данных одного и того же экземпляра компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)], то экземпляр использует встроенный двухэтапный алгоритм для фиксирования всех баз данных, вызванных в транзакции.  
  
 При использовании вложенных транзакций фиксация внутренних транзакций не освобождает ресурсы и не делает их изменения постоянными. Изменения данных становятся постоянными и ресурсы освобождаются только при фиксации внешней транзакции. Выданный каждой инструкции COMMIT TRANSACTION, когда @@TRANCOUNT больше, чем 1 просто уменьшает значение @@TRANCOUNT на 1. Если @@TRANCOUNT — уменьшится до нуля, вся внешняя транзакция зафиксирована. Поскольку *transaction_name* игнорируется [!INCLUDE[ssDE](../../includes/ssde-md.md)], выдачи COMMIT TRANSACTION, ссылаясь на имя внешней транзакции, если существуют необработанные внутренние транзакции только уменьшает значение @@TRANCOUNT на 1.  
  
 Вызов инструкции COMMIT TRANSACTION при @@TRANCOUNT 0 приводит к возникновению ошибки; нет соответствующей инструкции BEGIN TRANSACTION.  
  
 Нельзя произвести откат транзакции после вызова инструкции COMMIT TRANSACTION, так как измененные данные уже стали частью базы данных.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] увеличивает счетчик транзакций внутри выражения, только когда счетчик транзакций равен нулю при запуске инструкции.  
  
## <a name="permissions"></a>Permissions  
 Необходимо быть членом роли **public** .  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-committing-a-transaction"></a>A. Фиксация транзакции  
**ПРИМЕНЯЕТСЯ к:** SQL Server, база данных Azure SQL, хранилище данных Azure SQL и параллельные хранилища данных   

В следующем примере удаляется кандидат на вакансию. Она использует AdventureWorks. 
  
```   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>Б. Фиксация вложенной транзакции  
**ПРИМЕНЯЕТСЯ к:** SQL Server и база данных Azure SQL    

В следующем примере создается таблица и формируется три уровня вложенных транзакций, которые затем фиксируются. Несмотря на то что каждый `COMMIT TRANSACTION` инструкция имеет *transaction_name* параметра, не задано отношение между `COMMIT TRANSACTION` и `BEGIN TRANSACTION` инструкции. *Transaction_name* параметры являются просто для понимания и помогают программисту удостовериться в том, что закодировано верное количество фиксированных транзакций, для уменьшения `@@TRANCOUNT` 0 и таким образом зафиксировать внешнюю транзакцию. 
  
```   
IF OBJECT_ID(N'TestTran',N'U') IS NOT NULL  
    DROP TABLE TestTran;  
GO  
CREATE TABLE TestTran (Cola int PRIMARY KEY, Colb char(3));  
GO  
-- This statement sets @@TRANCOUNT to 1.  
BEGIN TRANSACTION OuterTran;  
  
PRINT N'Transaction count after BEGIN OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
INSERT INTO TestTran VALUES (1, 'aaa');  
 
-- This statement sets @@TRANCOUNT to 2.  
BEGIN TRANSACTION Inner1;  
 
PRINT N'Transaction count after BEGIN Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (2, 'bbb');  
  
-- This statement sets @@TRANCOUNT to 3.  
BEGIN TRANSACTION Inner2;  
  
PRINT N'Transaction count after BEGIN Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (3, 'ccc');  
  
-- This statement decrements @@TRANCOUNT to 2.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner2;  
 
PRINT N'Transaction count after COMMIT Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
-- This statement decrements @@TRANCOUNT to 1.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner1;  
 
PRINT N'Transaction count after COMMIT Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
-- This statement decrements @@TRANCOUNT to 0 and  
-- commits outer transaction OuterTran.  
COMMIT TRANSACTION OuterTran;  
  
PRINT N'Transaction count after COMMIT OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
```  
  
## <a name="see-also"></a>См. также:  
 [BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [ФИКСАЦИЯ РАБОЧЕГО &#40; Transact-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40; Transact-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION (Transact-SQL)](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
