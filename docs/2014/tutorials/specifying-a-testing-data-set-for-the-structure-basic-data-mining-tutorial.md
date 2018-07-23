---
title: Задание набора проверочных данных для структуры (учебник интеллектуального анализа данных) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 75cd508f-b126-418b-848d-3c4c3e6c303f
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 09822e47f6fb8e1a4b91832a2b47492ae1d8c2b6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198374"
---
# <a name="specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial"></a>Задание набора проверочных данных для структуры (учебник по интеллектуальному анализу данных — начальный уровень)
  На нескольких последних экранах мастера интеллектуального анализа данных данные разбиваются на обучающий и проверочный наборы. Затем структура именуется и включается детализация на модели.  
  
## <a name="specifying-a-testing-set"></a>Задание проверочного набора  
 Благодаря разделению данных на обучающий и проверочный наборы при создании структуры интеллектуального анализа стало значительно проще оценить точность моделей интеллектуального анализа данных, создаваемых в дальнейшем. Дополнительные сведения о проверочных наборах см. в разделе [обучающие и проверочные наборы данных](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md).  
  
#### <a name="to-specify-the-testing-set"></a>Задание проверочного набора  
  
1.  На **создание проверочного набора** странице для **процент проверочных данных**, оставьте значение по умолчанию `30`.  
  
2.  Для **максимальное количество вариантов в наборе проверочных данных**, тип `1000`.  
  
3.  Нажмите кнопку **Далее**.  
  
## <a name="specifying-drillthrough"></a>Задание детализации  
 Детализация может быть включена для моделей и структур. Флажок в этом диалоговом окне включает детализацию для именованной модели. После обработки модели можно извлекать подробные сведения из обучающих данных, которые использовались при создании модели.  
  
 Если детализация также разрешена для базовой структуры интеллектуального анализа данных, то можно получать сведения из вариантов модели и структуры интеллектуального анализа данных, включая столбцы, отсутствующие в модели интеллектуального анализа данных. Дополнительные сведения см. в разделе [Drillthrough Queries &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-name-the-model-and-structure-and-specify-drillthrough"></a>Именование модели и структуры и задание детализации  
  
1.  На **завершение работы мастера** странице **имя структуры интеллектуального анализа данных**, тип `Targeted Mailing`.  
  
2.  В **имя модели интеллектуального анализа данных**, тип `TM_Decision_Tree`.  
  
3.  Выберите **разрешить детализацию** "флажок".  
  
4.  Просмотрите **предварительной версии** области. Обратите внимание, что только столбцы, выбранные как **ключ**, **ввода** или **прогнозируемый** отображаются. Остальные выбранные столбцы (например, AddressLine1) не используются для построения модели, но будут доступны в базовой структуре, и к ним можно выполнять запросы после обработки и развертывания модели.  
  
5.  Нажмите кнопку **Готово**.  
  
## <a name="previous-task-in-lesson"></a>Предыдущая задача занятия  
 [Указание типа данных и типа содержимого &#40;учебник интеллектуального анализа данных&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Следующее занятие  
 [Урок 3. Добавление и обработка моделей](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="see-also"></a>См. также  
 [Включение детализации для модели интеллектуального анализа данных](../../2014/analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)   
 [Запросы детализации &#40;интеллектуального анализа данных&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Определение обучающих данных &#40;мастер интеллектуального анализа данных&#41;](../../2014/analysis-services/specify-the-training-data-data-mining-wizard.md)  
  
  