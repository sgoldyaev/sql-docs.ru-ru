---
title: Предоставление разрешений для служб Integration Services | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0c2caa68-7834-4ea0-bd77-4f3a7c86d634
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4785dbeb300838a5a765798cd7a4330d09bdaf3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200654"
---
# <a name="grant-permissions-to-integration-services-service"></a>Предоставление разрешений службам Integration Services
  В предыдущих версиях [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]по умолчанию при установке [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] все пользователи в группе пользователей имели доступ к службе [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . При установке текущего выпуска [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]пользователи не имеют доступа к службе [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . По умолчанию эта служба является защищенной. После завершения установки [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] администратор должен предоставить доступ к службе.  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>Предоставление доступа к службе Integration Services  
  
1.  Запустите файл Dcomcnfg.exe. Программа Dcomcnfg.exe предоставляет пользовательский интерфейс для изменения определенных параметров в реестре.  
  
2.  В диалоговом окне **Службы и компоненты** последовательно разверните "Службы и компоненты" > "Компьютеры" > "Мой компьютер" > "Настройка DCOM".  
  
3.  Щелкните правой кнопкой мыши **Microsoft SQL Server Integration Services 12.0**, а затем нажмите кнопку **свойства**.  
  
4.  На вкладке **Безопасность** нажмите кнопку **Правка** в области **Разрешение на запуск и активацию** .  
  
5.  Добавьте пользователей и назначьте им соответствующие разрешения, а затем нажмите кнопку «ОК».  
  
6.  Повторите шаги 4 - 5 для назначения разрешений на доступ.  
  
7.  Перезапустите среду SQL Server Management Studio.  
  
8.  Перезапустите службу [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
  
