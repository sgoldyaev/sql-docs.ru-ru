---
title: Куб элемент (ASSL) | Документы Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2cce21443b29b3340b5c21ae7f73ba028023e1b2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
---
# <a name="cube-element-assl"></a>Элемент Cube (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Определяет обычный, виртуальный или связанный куб в [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [базы данных](../../../analysis-services/scripting/objects/database-element-assl.md) элемента.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Cubes>  
   <Cube>  
            <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
            <Description>...</Description>  
            <Language>...</Language>  
            <Collation>...</Collation>  
            <Translations>...</Translations>  
      <Dimensions>...</Dimensions>  
            <CubePermissions>...</CubePermissions>  
      <MdxScripts>...</MdxScripts>  
      <Perspectives>...</Perspectives>  
      <State>...</State>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Visible>...</Visible>  
      <MeasureGroups>...</MeasureGroups>  
      <DataSourceView >...</Source>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
      <ProactiveCaching>...</ProactiveCaching>  
            <Kpis>...</Kpis>  
            <ErrorConfiguration>...</ErrorConfiguration>  
            <Actions>...</Actions>  
      <StorageLocation>...</StorageLocation>  
      <EstimatedRows>...</EstimatedRows>  
      <LastProcessed>...</LastProcessed>  
      <Annotations>...</Annotations>  
   </Cube>  
</Cubes>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|None|  
|Значение по умолчанию|None|  
|Количество элементов|от 0 до n: необязательный элемент, который может встречаться несколько раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|[Кубы](../../../analysis-services/scripting/collections/cubes-element-assl.md)|  
|Дочерние элементы|[Действия](../../../analysis-services/scripting/collections/actions-element-assl.md), [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md), [заметки](../../../analysis-services/scripting/collections/annotations-element-assl.md), [сортировки](../../../analysis-services/scripting/properties/collation-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [ CubePermissions](../../../analysis-services/scripting/collections/cubepermissions-element-assl.md), [DefaultMeasure](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md), [описание](../../../analysis-services/scripting/properties/description-element-assl.md), [измерения](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md) , [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md), [идентификатор](../../../analysis-services/scripting/properties/id-element-assl.md), [ключевые показатели эффективности](../../../analysis-services/scripting/collections/kpis-element-assl.md), [язык](../../../analysis-services/scripting/properties/language-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [ LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MdxScripts](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md), [MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md), [имя](../../../analysis-services/scripting/properties/name-element-assl.md), [перспективы](../../../analysis-services/scripting/collections/perspectives-element-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md), [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md), [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md), [ScriptCacheProcessingMode](../../../analysis-services/scripting/properties/scriptcacheprocessingmode-element-assl.md), [состояние ](../../../analysis-services/scripting/properties/state-element-assl.md), [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md), [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md), [переводы](../../../analysis-services/scripting/collections/translations-element-assl.md), [видимыми](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Примечания  
 Соответствующий элемент в объектной модели Analysis Management объекты AMO — это <xref:Microsoft.AnalysisServices.Cube>.  
  
## <a name="see-also"></a>См. также  
 [Объекты & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
