---
title: Детализация структур интеллектуального анализа данных | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f8d1e4f8b036a21becde793f2d4fdde89913e7b3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48146034"
---
# <a name="drillthrough-on-mining-structures"></a>Детализация структур интеллектуального анализа данных
  *Детализация* — это возможность выполнять запросы к модели или структуре интеллектуального анализа данных и получать подробные данные, не представленные в модели.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] обеспечивает два различных варианта для детализации данных вариантов. Можно детализировать данные, которые были использованы для построения модели интеллектуального анализа данных, или исходные данные в структуре интеллектуального анализа данных.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Детализация вариантов модели и детализация структуры  
 С помощью детализации **вариантов модели** удобно находить дополнительные сведения о закономерностях, шаблонах или кластерах в модели.  
  
 Однако **Детализация структуры** используется, если данные должны давать доступ к сведениям, которые не были доступны в модели. Например, при наличии соответствующих разрешений можно попробовать выяснить, какие строки данных использовались для обучения модели, а какие для проверки.  
  
 Кроме того, можно просматривать атрибуты данных, которые не использовались в анализе, при условии, что они включены в определение структуры. Например, часто структуры интеллектуального анализа данных поддерживают много различных типов моделей, а некоторые столбцы структур могут быть исключены из модели из-за несовместимости типа данных или их бесполезности для анализа. Например, в модели нет смысла использовать контактные сведения клиентов, даже если данные включены в структуру, однако включение детализации обеспечивает доступ к этим сведениям без запуска отдельных запросов к источнику данных.  
  
## <a name="enabling-drillthrough-to-structure-data"></a>Включение детализации для данных структуры  
 Чтобы использовать детализацию для структуры интеллектуального анализа данных, должны выполняться следующие условия.  
  
-   Должна быть также включена детализация для модели. По умолчанию детализация обоих типов отключена. Чтобы включить детализацию в мастере интеллектуального анализа данных, выберите включение детализации для вариантов моделей на последней странице мастера. Вы можно также добавить возможность детализации существующей модели позже, изменив `AllowDrillthrough` свойство.  
  
-   При создании структуры интеллектуального анализа данных с помощью расширения интеллектуального анализа данных следует использовать предложение WITH DRILLTHROUGH. Дополнительные сведения см. в статье [CREATE MINING STRUCTURE (DMX)](/sql/dmx/create-mining-structure-dmx).  
  
-   Детализация работает посредством получения информации об обучающих вариантах структуры интеллектуального анализа данных. Эта информация была кэширована при обработке структуры. Таким образом Если произвести удаление всех кэшированных данных структуры, изменив <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> свойства `ClearAfterProcessing`, детализация работать не будет. Чтобы разрешить детализацию до столбцов структуры, необходимо изменить <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> свойства `KeepTrainingCases` и затем выполнить повторную обработку структуры.  
  
-   Убедитесь, что структура интеллектуального анализа данных и модели интеллектуального анализа данных имеют [AllowDrillThrough](../scripting/properties/allowdrillthrough-element-assl.md) свойство значение `True`. Более того, необходимо быть членом роли, обладающей разрешением на детализацию как в структуре, так и в модели.  
  
## <a name="security-issues-for-drillthrough"></a>Вопросы безопасности, связанные с детализацией  
 Разрешения на детализацию устанавливаются отдельно для структуры и для модели. Разрешение на детализацию модели позволяет проводить детализацию на основе модели, даже если у пользователя нет разрешения на детализацию структуры. Разрешения на детализацию структуры предоставляют дополнительную возможность включать столбцы структуры в запросы детализации с помощью функции [StructureColumn (DMX)](/sql/dmx/structurecolumn-dmx).  
  
 Дополнительные сведения о создании ролей и назначении разрешений в службах Analysis Services см. в разделе [Конструктор ролей (службы Analysis Services — многомерные данные)](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx).  
  
> [!NOTE]  
>  Если включить детализацию как структуры, так и модели интеллектуального анализа данных, то любой пользователь, являющийся членом роли с разрешениями детализации в модели, также видит столбцы в структуре, даже если эти столбцы не входят в модель интеллектуального анализа данных. Поэтому, чтобы защитить конфиденциальные данные, необходимо настроить в представлении источника данных маскирование персональных данных и разрешать доступ к детализации структуры интеллектуального анализа данных только при необходимости.  
  
## <a name="related-tasks"></a>Связанные задачи  
 Дополнительные сведения см. в следующих разделах по использованию детализации с моделями интеллектуального анализа данных.  
  
|||  
|-|-|  
|Использование детализации для структуры из средств просмотра моделей интеллектуального анализа данных|[Использование детализации из средств просмотра моделей](use-drillthrough-from-the-model-viewers.md)|  
|См. примеры запросов детализации для конкретных типов моделей.|[Запросы интеллектуального анализа данных](data-mining-queries.md)|  
|Получите сведения о разрешениях, относящихся к конкретным структурам и моделям интеллектуального анализа данных.|[Предоставление разрешений на структур интеллектуального анализа данных и моделей &#40;служб Analysis Services&#41;](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>См. также  
 [Детализация моделей интеллектуального анализа данных](drillthrough-on-mining-models.md)  
  
  
