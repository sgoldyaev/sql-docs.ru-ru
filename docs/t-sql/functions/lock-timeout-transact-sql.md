---
title: "@@LOCK_TIMEOUT (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15ee9c5789ea6f1c7bbad6fc8caeabab14f3df4f
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="locktimeout-transact-sql"></a>@@LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Возвращает значение времени ожидания блокировки в миллисекундах для текущего сеанса.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 **integer**  
  
## <a name="remarks"></a>Замечания  
 Инструкция SET LOCK_TIMEOUT позволяет установить в приложении максимальное время ожидания заблокированного ресурса. Если ожидание длится дольше значения LOCK_TIMEOUT, инструкция автоматически отменяется, а приложению возвращается сообщение об ошибке.  
  
 @@LOCK_TIMEOUT возвращает значение -1, если SET LOCK_TIMEOUT не была выполнена в текущем сеансе.  
  
## <a name="examples"></a>Примеры  
 Данный пример иллюстрирует содержимое результирующего набора в случае не установленного заранее значения LOCK_TIMEOUT.  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 Результирующий набор:  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 В этом примере значение LOCK_TIMEOUT устанавливается равным 1 800 миллисекундам, а затем вызывает@LOCK_TIMEOUT.  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 Результирующий набор:  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>См. также:  
 [Функции настройки (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Значение LOCK_TIMEOUT &#40; Transact-SQL &#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  