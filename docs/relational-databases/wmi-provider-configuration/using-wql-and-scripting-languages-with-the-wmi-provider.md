---
title: "Использование WQL и языков сценариев с поставщиком WMI | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- scripts [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
- WMI Provider for Configuration Management, scripts
ms.assetid: c1e64905-3c2b-4974-88f4-abf17cf7e289
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f86bfa3cb0c8adaf178641bbeadf2c74c48bc65d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>Использование WQL и языков сценариев с поставщиком WMI
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Доступ к управлению приложениями [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] службами и сетевыми настройками с помощью поставщика инструментария управления Windows (WMI) для объектов управления конфигурацией двумя способами:  
  
-   С помощью редактора WQL или средства создания запросов, например WBEMTest.exe, создается запрос к набору объектов на языке WQL (языке запросов к инструментарию управления Windows).  
  
-   С помощью языка для создания сценариев (например, VBScript).  
  
 Другой способ — управлять службами и сетевыми настройками [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] программным образом, используя управляемые объекты WMI в SMO. Дополнительные сведения о программировании WMI управляемые объекты, см. в разделе [управление службами и сетевыми настройками с помощью поставщика WMI](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
 Поставщик WMI для управления конфигурацией может осуществляться с помощью [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager и [!INCLUDE[msCoName](../../includes/msconame-md.md)] консоли управления. Дополнительные сведения о доступе к поставщику WMI с помощью пользовательского интерфейса см. в разделе [разделы руководства по управлению службами &#40; Диспетчер конфигурации SQL Server &#41; ](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6).  
  
## <a name="see-also"></a>См. также:  
 [Поставщик WMI доступа для управления конфигурацией с использованием WQL](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [Изменить SQL Server расширенные свойства службы с помощью VBScript](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  