---
title: "&lt;запрос источника данных&gt; | Документы Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- data sources [DMX]
- predictions [DMX]
- source data query element
- queries [DMX], source data
- external data access [DMX]
- <source data query> element
- training mining models
ms.assetid: 9dce5e37-1354-4d28-87c2-f9c419cb5b09
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 195c2ecd04a28ad830aca2d90df821b76d46e98e
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt"></a>&lt;запрос источника данных&gt;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Для обучения модели интеллектуального анализа данных и создания прогнозов на основе модели интеллектуального анализа данных, имеют доступ к данным, внешних по отношению к [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] базы данных. Вы используете \<запросом источника данных > предложение в расширений интеллектуального анализа (DMX) для определения этих внешних данных. [INSERT INTO &#40; расширений интеллектуального анализа данных &#41;](../dmx/insert-into-dmx.md), [SELECT FROM &#60; модели &#62; ПРОГНОЗИРУЕМОЕ соединение &#40; расширений интеллектуального анализа данных &#41; ](../dmx/select-from-model-prediction-join-dmx.md), и [SELECT FROM NATURAL PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) все инструкции используют  **\<запросом источника данных >**.  
  
## <a name="query-types"></a>Типы запросов  
 Тремя наиболее распространенными способами указания данных источника являются:   
  
 [OPENQUERY &#40; РАСШИРЕНИЙ ИНТЕЛЛЕКТУАЛЬНОГО АНАЛИЗА ДАННЫХ &#41;](../dmx/source-data-query-openquery.md)  
 Эта инструкция запрашивает данные, являющиеся внешними для экземпляра служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], при помощи существующего источника данных.  
  
 Хотя **OPENQUERY** работает аналогично функции **OPENROWSET**, **OPENQUERY** имеет следующие преимущества:  
  
-   DMX-запрос намного легче записать с помощью **OPENQUERY**. Вместо создания новой строки соединения каждый раз при написании запроса, можно воспользоваться существующей строкой соединения в источнике данных. Объект источника данных также может управлять доступом к данным для отдельных пользователей.  
  
-   Администратор имеет больший контроль над доступом к данным на сервере. Например, администратор может управлять загрузкой поставщиков на сервер и доступом к внешним данным.  
  
 [OPENROWSET &#40; РАСШИРЕНИЙ ИНТЕЛЛЕКТУАЛЬНОГО АНАЛИЗА ДАННЫХ &#41;](../dmx/source-data-query-openrowset.md)  
 Эта инструкция запрашивает данные, являющиеся внешними для экземпляра служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], при помощи существующего источника данных.  
  
 [ФИГУРА &#40; РАСШИРЕНИЙ ИНТЕЛЛЕКТУАЛЬНОГО АНАЛИЗА ДАННЫХ &#41;](../dmx/source-data-query-shape.md)  
 Эта инструкция запрашивает несколько источников данных для создания вложенной таблицы. С помощью **ФИГУРЫ**, можно объединить данные из нескольких источников в одну иерархическую таблицу. Это позволит использовать возможность экземпляра служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] вкладывать таблицы друг в друга.  
  
 Для указания источника данных можно также использовать следующие данные:  
  
-   Любую допустимую инструкцию расширений интеллектуального анализа данных.  
  
-   Любую допустимую инструкцию многомерных выражений.  
  
-   Таблицу, возвращающую хранимую процедуру.  
  
-   Набор строк XML для аналитики (XMLA).  
  
-   Параметр набора строк.  
  
## <a name="see-also"></a>См. также:  
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Инструкции управления данными](../dmx/dmx-statements-data-manipulation.md)   
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Справка по инструкции](../dmx/data-mining-extensions-dmx-statements.md)   
 [Вложенные таблицы &#40; Службы Analysis Services — Интеллектуальный анализ данных &#41;](../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  
