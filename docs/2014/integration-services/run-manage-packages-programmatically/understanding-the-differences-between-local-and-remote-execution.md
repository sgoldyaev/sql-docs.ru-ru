---
title: Основные сведения об отличиях между локальным и удаленным выполнением | Документы Майкрософт
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: af56b93fc4b14e542a5a9f6423e9064c848417be
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158694"
---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>Основные сведения об отличиях между локальным и удаленным выполнением
  Разработчики пакетов и администраторы должны знать, в чем состоят ограничения, связанные с местом выполнения пакета служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Пакет выполняется на том же компьютере, что и запустившая его программа**. Даже если программа загружает пакет, который хранится удаленно на другом сервере, пакет выполняется на локальном компьютере.  
  
-   **Вне среды разработки пакет может выполняться только на том компьютере, на котором установлены службы Integration Services**. Невозможно выполнять пакеты вне среды [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] на клиентском компьютере, если не установлены службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Условия вашей лицензии на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] могут не допускать установку служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] на дополнительных компьютерах. Службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] являются серверным компонентом и не могут устанавливаться на клиентских компьютерах. Чтобы выполнить пакеты с клиентского компьютера, необходимо запускать их таким способом, который позволяет гарантировать выполнение пакетов на сервере.  
  
 Дополнительные сведения о загрузке и выполнении сохраненного пакета см. в разделах:  
  
-   [Программная загрузка и запуск локального пакета](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [Программная загрузка и запуск удаленного пакета](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 Дополнительные сведения о выполнении пакета и загрузке его выхода в пользовательскую программу см. в разделах:  
  
-   [Загрузка выхода локального пакета](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
![Значок служб Integration Services (маленький)](../media/dts-16.gif "значок служб Integration Services (маленький)")**оставаться до даты со службами Integration Services** <br /> Чтобы загрузить новейшую документацию, статьи, образцы и видеоматериалы корпорации Майкрософт, а также лучшие решения участников сообщества, посетите страницу служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] на сайте MSDN:<br /><br /> [Посетите страницу служб Integration Services на сайте MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Чтобы получать автоматические уведомления об этих обновлениях, подпишитесь на RSS-каналы, предлагаемые на этой странице.  
  
## <a name="see-also"></a>См. также  
 [Программная загрузка и запуск локального пакета](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Программная загрузка и запуск удаленного пакета](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Загрузка выхода локального пакета](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
