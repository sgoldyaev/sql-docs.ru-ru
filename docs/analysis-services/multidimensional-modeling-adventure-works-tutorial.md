---
title: Многомерное моделирование (учебник Adventure Works) | Документы Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: def2d0f3b09fd7f78b499ed64b83661e6e51f690
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023761"
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>Многомерное моделирование (учебник по Adventure Works)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Добро пожаловать в [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. В этом учебнике рассматривается, как использовать среду [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] при разработке и развертывании проекта служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] на примере вымышленной компании [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] .  
  
## <a name="what-you-learn"></a>Полученные знания  
В этом учебнике рассматриваются следующие темы:  
  
-   Определение источников данных, представлений источников данных, измерений, атрибутов, связей атрибутов, иерархий и кубов в проекте служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] с помощью среды [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Просмотр данных куба и измерения посредством развертывания проекта служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] на экземпляре служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]и последующее заполнение развернутых объектов данными из базового источника данных.  
  
-   Изменение мер, измерений, иерархий, атрибутов и групп мер в проекте служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] и последующее развертывание добавочных изменений в развернутый куб на сервере разработки.  
  
-   Определение в кубе вычислений, ключевых показателей эффективности, действий, перспектив, переводов и ролей безопасности.  
  
В этом учебнике приводится описание сценария работы, что позволит лучше понять контекст для этих занятий. Дополнительные сведения см. в разделе [Analysis Services Tutorial Scenario](../analysis-services/analysis-services-tutorial-scenario.md).  
  
## <a name="prerequisites"></a>Предварительные требования  
Для выполнения всех занятий этого учебника потребуются образцы данных, файлов проекта и программное обеспечение. Инструкции по поиску и установке необходимых компонентов для этого учебника см. в разделе [Установка образцов данных и проектов для учебника по многомерному моделированию в службах Analysis Services](../analysis-services/install-sample-data-and-projects.md).  
  
Кроме того, для успешного завершения этого учебника необходимо иметь следующие разрешения.  
  
-   Необходимо быть членом локальной группы «Администраторы» на компьютере с установленными службами [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] или членом административной роли сервера в экземпляре [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   Вы должны иметь право на чтение **AdventureWorksDW** образца базы данных. Этот образец базы данных является допустимым для выпуска [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] .  
  
## <a name="lessons"></a>Занятия  
Этот учебник включает следующие занятия.  
  
|Занятие|Предположительное время выполнения|  
|----------|------------------------------|  
|[Урок 1: Определение представления источника данных в рамках служб Analysis Services проекта](../analysis-services/lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15 минут|  
|[Занятие 2: Определение и развертывание куба](../analysis-services/lesson-2-defining-and-deploying-a-cube.md)|30 минут|  
|[Урок 3: Изменение мер, атрибутов и иерархий](../analysis-services/lesson-3-modifying-measures-attributes-and-hierarchies.md)|45 минут|  
|[Урок 4: Определение расширенных атрибутов и свойств измерений](../analysis-services/lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120 минут|  
|[Занятие 5: Определение связей между измерениями и группами мер](../analysis-services/lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45 минут|  
|[Урок 6: Создание вычислений коэффициента](../analysis-services/lesson-6-defining-calculations.md)|45 минут|  
|[Занятие 7: Определение ключевых показателей эффективности & #40; Ключевые показатели эффективности & #41;](../analysis-services/lesson-7-defining-key-performance-indicators-kpis.md)|30 минут|  
|[Занятие 8: Определение действий](../analysis-services/lesson-8-defining-actions.md)|30 минут|  
|[Занятие 9: Определение перспектив и переводов](../analysis-services/lesson-9-defining-perspectives-and-translations.md)|30 минут|  
|[Занятие 10: Определение ролей администрирования](../analysis-services/lesson-10-defining-administrative-roles.md)|15 минут|  
  
> [!NOTE]  
> База данных куба, который будет создан в этом учебнике — это упрощенная версия [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] проекта многомерной модели, который является частью Adventure Works образцы баз данных доступны для загрузки на сайте GitHub. Учебная версия многомерной базы данных Adventure Works была упрощена с целью обеспечить ускоренное овладение рядом основных навыков. После завершения работы с учебником попробуйте поработать с проектом многомерной модели самостоятельно, чтобы более детально ознакомиться с многомерным моделированием в службах [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="next-step"></a>Следующий шаг  
Чтобы приступить к изучению этого учебника, перейдите к первому занятию: [Занятие 1. Определение представления источников данных в проекте служб Analysis Services](../analysis-services/lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md).  
  
  
  
