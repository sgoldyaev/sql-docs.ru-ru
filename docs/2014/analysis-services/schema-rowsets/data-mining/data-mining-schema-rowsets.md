---
title: Наборы строк схемы интеллектуального анализа данных | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- schema rowsets [Analysis Services]
- rowsets [Analysis Services], data mining
- data mining [Analysis Services], schema rowsets
ms.assetid: bd7d5df5-500b-4159-8467-880e141bc043
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9da58e5966c47a18562b87c20696be28b4cbcee5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147814"
---
# <a name="data-mining-schema-rowsets"></a>Data Mining Schema Rowsets
  Сервер, на котором выполняется [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] поддерживает следующие наборы строк схемы интеллектуального анализа данных. Чтобы проверить, поддерживает ли определенный поставщик XML/A определенного набора строк, используйте [DISCOVER_ENUMERATORS](../xml/discover-enumerators-rowset.md) набор строк с помощью [Discover](../../xmla/xml-elements-methods-discover.md) метод.  
  
 В [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] к наборам строк схемы интеллектуального анализа данных доступ предоставляется так же, как к таблицам на языке Transact-SQL, в схеме $SYSTEM. Например, следующий запрос применительно к экземпляру служб Analysis Services возвращает список схем, доступных в текущем экземпляре.  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>в этом разделе  
  
|Набор строк схемы|Описание|  
|-------------------|-----------------|  
|[Набор строк DMSCHEMA_MINING_COLUMNS](dmschema-mining-columns-rowset.md)|Описывает отдельные столбцы всех определенных моделей интеллектуального анализа данных, которые развернуты на сервере.|  
|[Набор строк DMSCHEMA_MINING_FUNCTIONS](dmschema-mining-functions-rowset.md)|Описывает прогнозирующие функции и функции интеллектуального анализа данных, которые могут использоваться с каждым алгоритмом интеллектуального анализа данных, установленным на сервере.|  
|[Набор строк DMSCHEMA_MINING_MODEL_CONTENT](dmschema-mining-model-content-rowset.md)|Обеспечивает возможность просматривать в клиентском приложении содержимое модели интеллектуального анализа данных, полученной в результате обучения.|  
|[Набор строк DMSCHEMA_MINING_MODEL_CONTENT_PMML](dmschema-mining-model-content-pmml-rowset.md)|Возвращает XML-представление (PMML 2.1) содержимого модели интеллектуального анализа данных.|  
|[Набор строк DMSCHEMA_MINING_MODEL_XML](dmschema-mining-model-xml-rowset.md)|Возвращает структуру XML (PMML 2.1) модели интеллектуального анализа данных. Это — та же схема, что и DMSCHEMA_MINING_MODEL_PMML, сохраняемая для обеспечения обратной совместимости.|  
|[Набор строк DMSCHEMA_MINING_MODELS](dmschema-mining-models-rowset.md)|Перечисляет модели интеллектуального анализа данных, которые развернуты на сервере.|  
|[Набор строк DMSCHEMA_MINING_SERVICE_PARAMETERS](dmschema-mining-service-parameters-rowset.md)|Предоставляет список параметров, которые могут использоваться для настройки поведения каждого алгоритма интеллектуального анализа данных, установленного на сервере.|  
|[Набор строк DMSCHEMA_MINING_SERVICES](dmschema-mining-services-rowset.md)|Предоставляет описание каждого алгоритма интеллектуального анализа данных, который доступен на сервере.|  
|[Набор строк DMSCHEMA_MINING_STRUCTURE_COLUMNS](dmschema-mining-structure-columns-rowset.md)|Описывает отдельные столбцы всех структур интеллектуального анализа данных, которые развернуты на сервере.|  
|[Набор строк DMSCHEMA_MINING_STRUCTURES](dmschema-mining-structures-rowset.md)|Перечисляет сведения о структурах интеллектуального анализа данных.|  
  
 Все наборы строк схемы, перечисленные здесь поддерживаются сервером, на котором выполняется [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>См. также  
 [Наборы строк схемы служб аналитики](../../schema-rowsets/analysis-services-schema-rowsets.md)   
 [Запросив системный каталог SQL Server](https://technet.microsoft.com/en-us/library/ms189082\(v=sql.110\).aspx)   
 [Запрос данных, наборы строк схемы интеллектуального анализа &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](../../data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
