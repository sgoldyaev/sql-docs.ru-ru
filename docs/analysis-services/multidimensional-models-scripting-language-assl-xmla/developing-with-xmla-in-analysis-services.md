---
title: Разработка с использованием XML для Аналитики в службах Analysis Services | Документы Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a7af006d5d52002480844b8776d8262fa8ae202
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024651"
---
# <a name="developing-with-xmla-in-analysis-services"></a>Разработка с использованием XMLA в службах Analysis Services
  XML для аналитики (XMLA) — это XML-протокол, основанный на протоколе SOAP и специально предназначенный для обеспечения унифицированного доступа к данным в любом стандартном многомерном источнике данных, доступном через HTTP-соединение. В службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XMLA является единственным протоколом для связи с клиентскими приложениями. Все клиентские библиотеки, поддерживаемые службами Analysis Services, в конечном итоге формируют запросы и ответы по протоколу XMLA.  
  
 С помощью XMLA разработчик может интегрировать клиентское приложение со службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], не создавая зависимости от платформы .NET Framework и COM-интерфейсов. Требования приложений, в том числе касающиеся размещения на широком диапазоне платформ, можно выполнить с помощью XMLA и HTTP-соединения со службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] полностью соответствуют спецификации XMLA 1.1 и расширяют ее для поддержки описания данных, обработки данных и управления данными. Расширения служб Analysis Services называются языком ASSL. Совместное использование XMLA и ASSL расширяет набор возможностей XMLA. Дополнительные сведения о ASSL см. в разделе [разработки в язык сценариев служб Analysis Services &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
## <a name="in-this-section"></a>В этом разделе  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Управление соединениями и сеансами &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)|Описывает соединение с экземпляром служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и управление сеансами и поддержкой состояния в XML для аналитики.|  
|[Обработка ошибок и предупреждений &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/handling-errors-and-warnings-xmla.md)|Описывает, каким образом службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] возвращают сведения об ошибках и предупреждениях для методов и команд XML для аналитики.|  
|[Определение и идентификация объектов &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)|Описывает идентификаторы и ссылки объектов, а также их использование в командах XML для аналитики.|  
|[Управление транзакциями &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-transactions-xmla.md)|Дополнительные сведения об использовании [BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), и [RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md) команд для явного определения и управления транзакциями в текущий XML для Аналитики сеанс.|  
|[Отмена команд &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|Описывает использование [отменить](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)команды для отмены команд, сеансов и соединений в XML для Аналитики.|  
|[Выполнение пакетных операций &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)|Описывает использование [пакета](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) для запуска нескольких XMLA команд, последовательно или параллельно, либо в той же транзакции, либо как отдельные транзакции, при помощи только одного [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) метод.|  
|[Создание и изменение объектов &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md)|Описывает использование [создать](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), и [удалить](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md) команд, а также элементы языка сценариев служб Analysis Services (ASSL) для определения, изменения или удаления объекты из [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] экземпляра.|  
|[Блокировка и снятие блокировки баз данных &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/locking-and-unlocking-databases-xmla.md)|Дополнительные сведения об использовании [блокировки](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) и [Unlock](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) команд для блокирования и разблокирования [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] базы данных.|  
|[Обработка объектов & #40; XML для Аналитики & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)|Описывает использование [процесс](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) для обработки [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] объекта.|  
|[Слияние секций &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)|Описывает использование [MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) для слияния секций на [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] экземпляра.|  
|[Проектирование агрегатов &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)|Описывает использование [DesignAggregations](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md) команды, в последовательном или пакетном режиме для проектирования агрегатов для статистических схем в [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Резервное копирование, восстановление и синхронизация баз данных & #40; XML для Аналитики & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)|Описывает использование [резервного копирования](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) и [восстановить](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) команды, чтобы резервное копирование и восстановление [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] базы данных из файла резервной копии.<br /><br /> Также описывается использование [Synchronize](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) команда синхронизации [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] базы данных с существующей базы данных на том же экземпляре или на другом экземпляре.|  
|[Вставка, обновление и удаление элементов &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)|Описывает использование [вставить](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [обновление](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), и [Drop](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) команды, чтобы добавить, изменить или удалить элементы из измерения, доступные для записи.|  
|[Обновление ячеек &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)|Описывает использование [UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md) команду, чтобы изменить значения ячеек в секции, доступной для записи.|  
|[Управление кэшами &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-caches-xmla.md)|Дополнительные сведения об использовании [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) команду, чтобы очистить кэш [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] объектов.|  
|[Наблюдение за трассировками &#40;XML для Аналитики&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/monitoring-traces-xmla.md)|Описывает использование [Subscribe](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md) команду, чтобы подписаться на и наблюдения за существующей трассировки с [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] экземпляра.|  
  
## <a name="data-mining-with-xmla"></a>Интеллектуальный анализ данных в XML для аналитики  
 Протокол XML для аналитики полностью поддерживает наборы строк схемы интеллектуального анализа данных. Эти наборы строк содержат сведения для выполнения запросов к модели интеллектуального анализа данных с помощью [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) метод. Дополнительные сведения о наборах строк схемы интеллектуального анализа данных см. в разделе [наборы строк схемы интеллектуального анализа данных](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 Дополнительные сведения о расширениях интеллектуального анализа данных см. в разделе [расширений интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; ссылки](../../dmx/data-mining-extensions-dmx-reference.md).  
  
## <a name="namespace-and-schema"></a>Пространство имен и схема  
  
### <a name="namespace"></a>Пространство имен  
 Пространство имен XML используется со схемой, определенной в данной спецификации `http://schemas.microsoft.com/AnalysisServices/2003/Engine` и стандартное сокращение «DDL».  
  
### <a name="schema"></a>Схема  
 В основе определения схемы XSD для языка определения объектов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] лежат определение элементов схемы и иерархии, приведенное в этом разделе.  
  
## <a name="extensibility"></a>Расширяемость  
 Расширяемость схемы языка определения объектов обеспечивается с помощью параметра **заметки** элемент, который включается во все объекты. Этот элемент может содержать любой допустимый код XML из любого пространства имен XML (отличного от целевого пространства имен, определяющего DDL) с соблюдением следующих правил.  
  
-   В XML-коде могут содержаться только элементы.  
  
-   Каждый элемент должен иметь уникальное имя. Рекомендуется значение **имя** ссылаются на целевое пространство имен.  
  
 Эти правила применяются, чтобы содержимое **заметки** тег могут представляться как набор пар имя-значение до принятия решений поддержки объектов DSO 9.0.  
  
 Комментарии и пробелы в **заметки** тег, который не заключаются дочерний элемент не будет сохранен. Кроме того, все элементы должны быть доступными для чтения и записи; элементы, доступные только для чтения, пропускаются.  
  
 Схема языка определения объектов является закрытой; под этим подразумевается то, что сервер не позволяет производить замену производных типов для элементов, определенных в схеме. Поэтому сервер принимает только набор элементов, определенных в схеме, и не принимает другие элементы или атрибуты. Обнаружение неизвестного элемента вынуждает ядро служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] активизировать ошибку.  
  
## <a name="see-also"></a>См. также  
 [Развертывание с помощью функций анализа служб языка сценариев &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Основные сведения об архитектуре Microsoft OLAP](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
