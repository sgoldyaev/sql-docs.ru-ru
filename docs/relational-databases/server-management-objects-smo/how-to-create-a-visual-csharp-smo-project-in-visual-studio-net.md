---
title: "Создание проекта Visual C# SMO в Visual Studio .NET | Документы Microsoft"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 231e49bce1350370917871c131d3558b02b82d8d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>Создание проекта Visual C# SMO в Visual Studio .NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]В этом разделе описывается создание простого консольного приложения SMO.  
  
 В этом примере импортируются пространства имен, что позволяет программе ссылаться на типы объектов SMO. Импорт **агента** пространства имен является необязательным. Его следует выполнить при написании программы, в которой используется агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Общие** пространства имен, необходимые для безопасного подключения к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **SqlClient** пространства имен используется для обработки ошибки исключения SQL.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Создание проекта SMO на языке Visual C# в среде Visual Studio.NET  
  
1. Запустите Visual Studio
  
2. На **файл** меню, нажмите кнопку **New** и затем **проекта**.  Откроется диалоговое окно **Создание проекта** .   
  
3. В [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **установленные** панели перейдите к **шаблоны**\\**Visual C#**\\**Windows** и выберите **консольное приложение**.  
  
4. (Необязательно) В **имя** текста введите имя нового приложения.  

5. Нажмите кнопку **ОК** загрузить шаблон консольного приложения.  

6. Следуйте инструкциям на [Установка SMO](installing-smo.md) установить пакет для проекта для ссылки.
  
7. В меню **Вид** выберите пункт **Код**.
    
8. Введите следующую команду в коде перед инструкцией пространства имен **с помощью** инструкции для определения типов в пространстве имен объектов SMO:
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. В SMO имеются различные пространства имен в узле Microsoft.SqlServer.Management.Smo, такие как Microsoft.SqlServer.Management.Smo.Agent. Добавьте эти пространства имен при необходимости.  
  
16. Теперь можно добавить свой код SMO.  
  
  