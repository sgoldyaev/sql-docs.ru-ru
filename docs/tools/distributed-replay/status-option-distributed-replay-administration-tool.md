---
title: Параметр состояния (средство администрирования распределенного воспроизведения) | Документы Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22abb1619002a20255778d901c2194795830384f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781325"
---
# <a name="status-option-distributed-replay-administration-tool"></a>Параметр состояния (средство администрирования распределенного воспроизведения)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Средство администрирования программы распределенного воспроизведения [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( **DReplay.exe**) представляет собой программу командной строки, которая служит для взаимодействия с контроллером распределенного воспроизведения. В этой статье описан параметр командной строки **status** и соответствующий синтаксис.  
  
 Параметр **status** опрашивает контроллер и отображает его текущее состояние.  
  
 ![Topic link icon](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") Дополнительные сведения о синтаксических обозначениях, используемых в синтаксисе средства администрирования, см. в разделе [Синтаксические обозначения в Transact-SQL (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### <a name="parameters"></a>Параметры  
 **-m** *controller*  
 Задает имя компьютера для контроллера. Локальный компьютер можно указать как «`localhost`» или «`.`».  
  
 Если параметр **-m** не задан, то используется локальный компьютер.  
  
 **-f** *status_interval*  
 Указывает частоту (в секундах) отображения состояния.  
  
 Если параметр **-f** не задан, то интервал по умолчанию составляет 30 секунд.  
  
## <a name="examples"></a>Примеры  
 В следующем примере текущий статус отображается каждые 60 секунд. Значение `localhost` указывает, что служба контроллера запущена на том же компьютере, что и средство администрирования.  
  
```  
dreplay status –m localhost -f 60  
```  
  
## <a name="permissions"></a>Разрешения  
 Средство администрирования должно запускаться как интерактивный пользователь, с учетной записью локального пользователя или пользователя домена. Для использования учетной записи локального пользователя средство администрирования и контроллер должны быть запущены на одном компьютере.  
  
 Дополнительные сведения см. в статье [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>См. также:  
 [Распределенное воспроизведение SQL Server](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Отладчик Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
