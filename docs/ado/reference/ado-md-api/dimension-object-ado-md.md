---
title: "Измерение объекта (ADO MD) | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad282fee080d57546335029eceff5475fe6aecc1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="dimension-object-ado-md"></a>Объект измерения (ADO MD)
Представляет одно из измерений многомерного куба, содержащего иерархии на один или несколько элементов.  
  
## <a name="remarks"></a>Замечания  
 С коллекциями и свойствами **измерения** объекта, можно сделать следующее:  
  
-   Определить **измерения** с [имя](../../../ado/reference/ado-md-api/name-property-ado-md.md) и [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) свойства.  
  
-   Возвращает осмысленное строку, описывающую **измерения** с [описание](../../../ado/reference/ado-md-api/description-property-ado-md.md) свойство.  
  
-   Вернуть [иерархии](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) объекты, составляющие **измерения** с [иерархий](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) коллекции.  
  
-   Используйте стандартные ADO [свойства](../../../ado/reference/ado-api/properties-collection-ado.md) коллекции для получения дополнительных сведений о **измерения** объекта.  
  
 **Свойства** коллекция содержит указанный поставщик свойства. В следующей таблице перечислены свойства, которые могут быть доступны. Фактическое свойство списка могут различаться в зависимости от реализации поставщика. См. в документации для поставщика более полный список доступных свойств.  
  
|Имя|Description|  
|----------|-----------------|  
|CatalogName|Имя каталога, к которому принадлежит этот куб.|  
|Имя куба|Имя куба.|  
|DefaultHierarchy|Уникальное имя иерархии по умолчанию.|  
|Description|Понятное описание куба.|  
|DimensionCaption|Метка или заголовок, связанный с выбранным измерением.|  
|DimensionCardinality|Количество элементов в измерении.|  
|DimensionGUID|Идентификатор GUID для измерения.|  
|Имя измерения|Имя измерения.|  
|DimensionOrdinal|Порядковый номер среди группы измерений, которые образуют куба измерения.|  
|DimensionType|Тип измерения.|  
|DimensionUniqueName|Однозначная имя измерения.|  
|SchemaName|Имя схемы, которой принадлежит этот куб.|  
  
 Этот раздел содержит следующий раздел.  
  
-   [Свойства, методы и события](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>См. также:  
 [Пример CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Объект CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Коллекции измерений (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Коллекция hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Коллекция свойств (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)