---
title: Переводы (службы Analysis Services) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e8454d379bcce879ed444a98bf5938e0736ea30e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153065"
---
# <a name="translations-analysis-services"></a>Переводы (службы Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  Только многомерные  
  
 В многомерной модели данных [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] можно внедрять несколько переводов заголовка для предоставления строк, связанных с определенным языковым стандартом, в зависимости от кода языка. Можно добавлять переводы для имени базы данных, объектов куба и объектов измерений базы данных.  
  
 При определении перевода метаданные и переведенный заголовок создаются внутри модели, но для отображения локализованных строк в клиентском приложении следует либо задать свойство `Language` для объекта, либо передать параметр `Locale Identifier` в строке подключения (например, установив `LocaleIdentifier=1036` для возврата строк на французском). Используйте `Locale Identifier`, если требуется поддерживать несколько одновременных переводов одного объекта на разных языках. Параметр `Language` свойство работает, но оно также влияет на обработку и запросы, что может привести к непредвиденным последствиям. Параметр `Locale Identifier` является лучшим выбором, поскольку он используется только для получения переведенных строк.  
  
 Перевод содержит код языка (LCID), переведенный заголовок объекта (например, измерение или имя атрибута), а также, при необходимости, привязку к столбцу, предоставляющему значения данных на целевом языке. Может быть несколько переводов, но для любого соединения можно использовать только один. Нет теоретического ограничения для количества переводов, которые можно внедрить в модель, но каждый перевод усложняет тестирование, а все переводы должны совместно использовать одинаковые параметры сортировки, поэтому при разработке решения учитывайте эти естественные ограничения.  
  
> [!TIP]  
>  Вы можете использовать клиентские приложения, например Excel, Management Studio и [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] , для возврата переведенных строк. Дополнительные сведения см. в разделе [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .  
  
## <a name="setting-up-a-model-to-support-translated-members"></a>Настройка модели для поддержки переведенный членов  
 Модели данных, используемой в многоязычном решении, нужны не только переведенные метки (имена полей и описания). Также модели необходимо предоставить значения данных, которые выводятся в различных скриптах. Для создания многоязычного решения необходимо иметь отдельные атрибуты, привязанные к столбцам во внешней базе данных, возвращающим данные.  
  
 Образцы баз данных Adventure Works (многомерное и реляционное хранилище данных) демонстрируют функцию перевода. Образец модели включает переведенные заголовки и описания. Образец реляционного хранилища данных содержит столбцы переведенных значений, предоставляющих локализованные элементы атрибутов в модели.  
  
 Для просмотра переведенных значений данных, доступных для модели выполните следующее.  
  
1.  Откройте многомерную модель Adventure Works в конструкторе.  
  
2.  В обозревателе решений откройте представления источников данных и дважды щелкните файл Adventure Works DW\<версия > .dsv.  
  
3.  Найдите dimDate, dimProduct, dimProductCategory или dimProductSubcateogry. Все эти измерения содержат атрибуты для преобразованных элементов месяца, дня недели, названия продукта, имени категории и т. д.  
  
4.  Щелкните правой кнопкой мыши любое поле и выберите **Просмотр данных**. Вы увидите английский, испанский и французский переводы для каждого элемента.  
  
 Форматы даты, времени и валюты не преобразуются с помощью переводов. Для динамического предоставления определенных форматов на основе языкового стандарта клиента используйте мастер преобразования валюты и свойство `FormatString`. Дополнительные сведения см. в разделах [Конвертация валюты (службы Analysis Services)](currency-conversions-analysis-services.md) и [Элемент FormatString (ASSL)](scripting/properties/formatstring-element-assl.md).  
  
 В разделе[Lesson 9: Defining Perspectives and Translations](lesson-9-defining-perspectives-and-translations.md) в учебнике по службам Analysis Services описывается создание и тестирование переводов.  
  
## <a name="defining-translations"></a>Определение переводов  
 При определении перевода создается объект `Translation` в качестве дочернего элемента базы данных [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], измерения или объекта куба. Используйте [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] , чтобы открыть решение и определить переводы.  
  
### <a name="add-translations-to-a-cube"></a>Добавление переводов в куб  
 Можно добавлять переводы для куба, мер, групп мер, измерения куба, перспектив, КПИ, действий, именованных наборов и вычисляемых элементов.  
  
1.  В обозревателе решений дважды щелкните имя куба, чтобы открыть конструктор кубов.  
  
2.  Перейдите на вкладку **Переводы** . На этой странице перечислены все объекты, которые поддерживают переводы.  
  
3.  Для каждого объекта укажите целевой язык (автоматически преобразуется в код языка), переведенный заголовок и переведенное описание. Список языков в службах Analysis Services согласован как для языка сервера в Management Studio, так и при добавлении переопределения перевода для одного атрибута.  
  
     Помните, что невозможно изменить параметры сортировки. Куб фактически использует один набор параметров сортировки, даже если вы поддерживаете несколько языков с помощью перевода заголовков (для атрибутов измерений есть исключение, описанное ниже). Если окажется, что в языках при общих параметрах сортировки сортировка работает неправильно, потребуется сделать копии куба, чтобы разместить требования к параметрам сортировки.  
  
4.  Постройте и разверните проект.  
  
5.  Подключитесь к базе данных с помощью клиентского приложения, например Excel, добавив в строку подключения код языка. Дополнительные сведения см. в разделе [Советы и рекомендации по глобализации (службы Analysis Services)](globalization-tips-and-best-practices-analysis-services.md).  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>Добавление переводов в измерение и атрибуты  
 Переводы можно добавить в измерения базы данных, атрибуты, иерархии и уровни в иерархии.  
  
 Переведенные заголовки добавляются к модели вручную с помощью клавиатуры или копирования и вставки, но для элементов атрибута измерения переведенные значения можно получить из внешней базы данных. В частности `CaptionColumn` свойство атрибута может быть привязано к столбцу в представлении источника данных.  
  
 На уровне атрибута можно переопределить параметры сортировки, например может потребоваться учитывать ширину или использовать двоичную сортировку для конкретного атрибута. В [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]параметры сортировки предоставляется там, где определены привязки данных. Поскольку вы привязываете перевод атрибута измерения к другому исходному столбцу в другом исходном столбце в DSV, доступны параметры сортировки, с помощью которых можно настроить сортировку, используемую исходным столбцом. Подробные сведения о параметрах сортировки столбца в реляционной базе данных см. в разделе [Set or Change the Column Collation](../relational-databases/collations/set-or-change-the-column-collation.md) .  
  
1.  В обозревателе решений дважды щелкните имя измерения, чтобы открыть конструктор измерений.  
  
2.  Перейдите на вкладку **Переводы** . На этой странице перечислены все объекты измерений, которые поддерживают переводы.  
  
     Для каждого объекта укажите целевой язык (автоматически преобразуется в код языка), переведенный заголовок и переведенное описание. Список языков в службах Analysis Services согласован как для языка сервера в Management Studio, так и при добавлении переопределения перевода для одного атрибута.  
  
3.  Привязка атрибута к столбцу, который предоставляет переведенные значения  
  
    1.  В конструкторе измерений в области **Переводы**добавьте новый перевод. Выберите язык. На странице появится новый столбец, чтобы принять переведенные значения.  
  
    2.  Поместите курсор в пустую ячейку рядом с одним из атрибутов. Атрибут не может быть ключом, но все остальные атрибуты допустимы. Вы увидите маленькую кнопку с точкой. Нажмите ее, чтобы открыть диалоговое окно **Перевод данных атрибута**.  
  
    3.  Введите перевод заголовка. Он используется как метка данных на целевом языке, например как имя поля в списке полей сводной таблицы.  
  
    4.  Выберите исходный столбец, который предоставляет переведенные значения элементов атрибута. Доступны только существующие столбцы в таблице или запросе, связанные с измерением. Если столбец не существует, необходимо изменить представление источника данных, измерение и куб, чтобы выбрать столбец.  
  
    5.  Выберите параметры и порядок сортировки, если применимо.  
  
4.  Постройте и разверните проект.  
  
5.  Подключитесь к базе данных с помощью клиентского приложения, например Excel, добавив в строку подключения код языка. Дополнительные сведения см. в разделе [Советы и рекомендации по глобализации (службы Analysis Services)](globalization-tips-and-best-practices-analysis-services.md).  
  
### <a name="add-a-translation-of-the-database-name"></a>Добавление перевода имени базы данных  
 На уровне базы данных можно добавлять переводы имени и описания. Переведенное имя базы данных может быть видимо для клиентских подключений, которые указывают код языка, но это зависит от используемого средства. Например, при просмотре базы данных в Management Studio переведенное имя не будет показано, даже если в соединении указан код языкового стандарта. API, который используется Management Studio для подключения к службам Analysis Services, не читает свойство `Language`.  
  
1.  В обозревателе решений щелкните правой кнопкой мыши имя проекта и выберите **Изменить базу данных** , чтобы открыть конструктор баз данных.  
  
2.  В области "Перевод" укажите целевой язык (автоматически преобразуется в код языка), переведенный заголовок и переведенное описание. Список языков однороден в пределах Analysis Services и при настройке языка сервера в Management Studio, и при добавлении переопределения перевода для одного атрибута.  
  
3.  На странице свойств базы данных, задайте `Language` код языка, указанный для перевода. При необходимости задайте `Collation` также в том случае, если значение по умолчанию больше не имеет смысл.  
  
4.  Соберите и разверните базу данных.  
  
## <a name="resolving-translations"></a>Разрешение переводов  
 Если клиентское приложение запрашивает код языка, экземпляр [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] пытается разрешить данные и метаданные для объектов [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] в ближайший соответствующий код языка. Если клиентское приложение не задает язык по умолчанию или задает нейтральный код локали (0) или идентификатор языка процесса по умолчанию (1024), то службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] используют язык по умолчанию для экземпляра, чтобы вернуть данные и метаданные для объектов служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>См. также  
 [Сценарии глобализации для многомерных служб Analysis Services](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Языки и параметры сортировки &#40;служб Analysis Services&#41;](languages-and-collations-analysis-services.md)   
 [Задание или изменение параметров сортировки столбца](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Глобализация, советы и рекомендации по &#40;служб Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)  
  
  
