---
title: Элемент RefreshPolicy (ASSL) | Документы Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d553fc069242c8c9c3ba3348820c81474fd3a668
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="refreshpolicy-element-assl"></a>Элемент RefreshPolicy (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Определяет частоту проверки на наличие изменений в динамической части измерения или группе мер (как определено в элементе [Persistence](../../../analysis-services/scripting/properties/persistence-element-assl.md) ).  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <RefreshPolicy>...</RefreshPolicy>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|String (перечисление)|  
|Значение по умолчанию|См. таблицу ниже.|  
|Количество элементов|0—1: необязательный элемент, который может появляться только один раз.|  
  
|Предок или родитель|Значение по умолчанию|  
|------------------------|-------------------|  
|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|*ByQuery*|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|Нет|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|[DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|Дочерние элементы|None|  
  
## <a name="remarks"></a>Замечания  
 Значением этого элемента может быть только одна из строк в следующей таблице.  
  
|Значение|Description|  
|-----------|-----------------|  
|*ByQuery*|Каждый запрос проверяет, не изменился ли источник данных.|  
|*ByInterval*|Источник данных проверяется на изменения только в интервале, заданном элементом [RefreshInterval](../../../analysis-services/scripting/properties/refreshinterval-element-assl.md).|  
  
 Перечисление, соответствующее разрешенным значениям для **RefreshPolicy** в модели объектов Analysis Management объекты AMO — <xref:Microsoft.AnalysisServices.RefreshPolicy>.  
  
## <a name="see-also"></a>См. также  
 [Элемент Persistence & #40; ASSL & #41;](../../../analysis-services/scripting/properties/persistence-element-assl.md)   
 [Свойства & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
