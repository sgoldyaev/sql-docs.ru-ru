---
title: "Выгрузка расширенной хранимой процедуры DLL | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31afe06af1285f2537a0712bdd8bd7d14e31e98f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Выгрузка DLL-библиотеки расширенной хранимой процедуры
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Пользуйтесь вместо этого интеграцией со средой CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] загружает библиотеку DLL расширенной хранимой процедуры, как только выполняется вызов одной из функций библиотеки DLL. DLL-библиотека остается загруженной до тех пор, пока не выключается сервер или системный администратор не выгружает ее с помощью инструкции DBCC. Например, следующая команда выгружает **xp_hello.dll**, позволяя системному администратору для копирования более новой версии этого файла в каталоге без выключения сервера:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>См. также:  
 [Имя DLL-библиотеки DBCC &#40; Бесплатные &#41; &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  