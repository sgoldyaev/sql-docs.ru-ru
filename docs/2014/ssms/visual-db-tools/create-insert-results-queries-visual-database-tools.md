---
title: Создание запросов на вставку результатов (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 34e1fb7b3744cd07f58f47dd68b8055908bdeb3c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216494"
---
# <a name="create-insert-results-queries-visual-database-tools"></a>Создание запросов на вставку результатов (визуальные инструменты для баз данных)
  Запрос вставки результатов позволяет копировать строки внутри таблицы или из одной таблицы в другую. Например, с помощью запроса вставки результатов можно скопировать сведения о названиях книг некоторого издателя из таблицы `titles` в другую таблицу, которая будет ему доступна. Запрос вставки результатов похож на запрос создания таблицы, но копирует строки в уже существующую таблицу.  
  
> [!TIP]  
>  Строки можно скопировать из одной таблицы в другую методом вырезания и вставки. Создайте запрос для каждой таблицы и запустите их. Скопируйте нужные строки из одной сетки результатов в другую.  
  
 При создании запроса вставки результатов необходимо указать следующее.  
  
-   Таблицу базы данных, куда нужно скопировать строки (целевую таблицу).  
  
-   Таблицу или таблицы, из которых копируются строки (исходную таблицу). Исходная таблица или таблицы становятся частью вложенного запроса. При копировании данных внутри таблицы целевая таблица совпадает с исходной.  
  
-   Столбцы в исходной таблице, содержимое которых нужно скопировать.  
  
-   Столбцы в целевой таблице, в которые нужно скопировать данные.  
  
-   Условия поиска для выборки строк, которые нужно скопировать.  
  
-   Порядок сортировки, когда нужно скопировать строки в определенном порядке.  
  
-   Параметры группировки для случаев, когда нужно скопировать только сводные данные.  
  
 Например, следующий запрос копирует сведения о названиях книг из таблицы `titles` в архивную таблицу `archivetitles`. Запрос копирует содержимое четырех столбцов для всех названий, принадлежащих указанному издателю:  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
>  Чтобы вставить значения в новую строку, используйте запрос вставки значений.  
  
 Можно скопировать содержимое всех или только выбранных столбцов в строке таблицы. В любом случае, копируемые данные должны быть совместимы со столбцами целевой таблицы. Например, при копировании содержимого столбца `price`столбец, куда копируются данные, должен допускать числовые данные с десятичным разделителем. При копировании всей строки физическое положение совместимых столбцов целевой и исходной таблицы должно совпадать.  
  
 При создании запроса вставки результатов внешний вид панели критериев меняется, отражая параметры, доступные для копирования данных. Добавляется столбец «Добавить» позволяющий указать столбцы, в которые необходимо скопировать данные.  
  
> [!CAUTION]  
>  Результат выполнения запроса вставки результатов отменить нельзя. В целях предосторожности создайте резервную копию данных перед выполнением запроса.  
  
### <a name="to-create-an-insert-results-query"></a>Создание запроса вставки результатов  
  
1.  Создайте новый запрос и добавьте таблицу, из которой нужно скопировать строки (исходную таблицу). При копировании строк внутри таблицы в качестве целевой таблицы нужно указать исходную.  
  
2.  В меню **Конструктор запросов** выберите пункт **Тип изменения**, а затем пункт **Вставить результаты**.  
  
3.  В диалоговом окне [Выбор целевой таблицы для инструкции Insert Results](visual-database-tools.md)выберите таблицу, в которую нужно скопировать строки (целевую таблицу).  
  
    > [!NOTE]  
    >  Конструктор запросов и представлений не может заранее определить, какие таблицы и представления можно обновить. Поэтому список **Имя таблицы** в диалоговом окне **Выбор целевой таблицы для вставки результатов** содержит все доступные таблицы и представления в запрашиваемом подключении к данным (даже те, в которые нельзя скопировать строки).  
  
4.  В прямоугольнике, представляющем таблицу или возвращающий табличное значение объект, выберите имена столбцов, содержимое которых нужно скопировать. Чтобы скопировать строки целиком, выберите  **\* (все столбцы)**.  
  
     Конструктор запросов и представлений добавляет выбранные столбцы к столбцу **Столбец** панели критериев.  
  
5.  В столбце **Добавить** на панели критериев выберите столбец в целевой таблице для каждого копируемого столбца исходной таблицы. Выберите *tablename.\**  при копировании всей строки. Столбцы в исходной и целевой таблице должны иметь одинаковые или совместимые типы данных.  
  
6.  Чтобы скопировать строки в определенном порядке, укажите порядок сортировки. Дополнительные сведения см. в разделе [Результаты запросов сортировки и группирования (визуальные инструменты для баз данных)](sort-and-group-query-results-visual-database-tools.md).  
  
7.  Укажите копируемые строки путем ввода условий поиска в столбце **Фильтр**. Дополнительные сведения см. в разделе [Определение критериев поиска (визуальные инструменты для баз данных)](specify-search-criteria-visual-database-tools.md).  
  
     Если условия поиска не заданы, в целевую таблицу будут скопированы все строки исходной таблицы.  
  
    > [!NOTE]  
    >  При добавления столбца для поиска на панели критериев конструктор запросов и представлений также включит его в список столбцов, подлежащих копированию. Если столбец нужно использовать только для поиска, но не для копирования, снимите флажок рядом с именем столбца в прямоугольнике, который представляет таблицу или возвращающий табличное значение объект.  
  
8.  Чтобы скопировать сводные данные, укажите параметры Group By. Дополнительные сведения см. в разделе [Резюмирование результатов запросов (визуальные инструменты для баз данных)](summarize-query-results-visual-database-tools.md).  
  
 При выполнении запроса "вставка результатов" панель [Результаты](results-pane-visual-database-tools.md) не отображает никаких сообщений. Вместо этого появляется сообщение о количестве скопированных строк.  
  
## <a name="see-also"></a>См. также  
 [Типы запросов &#40;визуальных инструментах баз данных&#41;](types-of-queries-visual-database-tools.md)   
 [Разделы по конструированию запросов и представлений (визуальные инструменты для баз данных)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  