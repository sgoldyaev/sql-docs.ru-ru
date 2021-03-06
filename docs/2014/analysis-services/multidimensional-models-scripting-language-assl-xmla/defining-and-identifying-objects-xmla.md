---
title: Определение и идентификация объектов (XMLA) | Документация Майкрософт
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 023ea2580b0cd8322a6c0bb17cfc76d6ddf70f54
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225324"
---
# <a name="defining-and-identifying-objects-xmla"></a>Определение и идентификация объектов (XMLA)
  В командах XML для аналитики (XMLA) объекты указываются при помощи идентификаторов и ссылок на объекты, а определяются при помощи элементов языка ASSL команд XMLA.  
  
## <a name="object-identifiers"></a>Идентификаторы объектов  
 Объект определяется с помощью уникальный идентификатор объекта, как определено в экземпляре [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Идентификаторы объектов могут быть либо указаны явным образом, либо определены экземпляром служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] при создании этого объекта службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Можно использовать [Discover](../xmla/xml-elements-methods-discover.md) метод позволяет получать идентификаторы объектов для последующих `Discover` или [Execute](../xmla/xml-elements-methods-execute.md) вызовы методов.  
  
## <a name="object-references"></a>Ссылки на объекты  
 Несколько команд XML для Аналитики, такие как [удалить](../xmla/xml-elements-commands/delete-element-xmla.md) или [процесс](../xmla/xml-elements-commands/process-element-xmla.md), используйте ссылку на объект для ссылки на объект однозначным образом. Ссылка содержит идентификатор объекта, для которого выполняется команда, а также идентификаторы объектов-предков этого объекта. Например, для секции ссылка на объект содержит идентификатор объекта секции, а также идентификаторы объектов родительских группы мер, куба и базы данных этой секции.  
  
## <a name="object-definitions"></a>Определения объектов  
 [Создать](../xmla/xml-elements-commands/create-element-xmla.md) и [Alter](../xmla/xml-elements-commands/alter-element-xmla.md) XML для Аналитики команды создания или изменения, соответственно, объектов на [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] экземпляра. Определения этих объектов представлены [ObjectDefinition](../xmla/xml-elements-properties/objectdefinition-element-xmla.md) элемент, содержащий элементы из языка ASSL. Идентификаторы объектов могут быть явно указано для всех основных и многих второстепенных объектов с помощью [идентификатор](../xmla/xml-elements-properties/id-element-xmla.md) элемент. Если элемент `ID` не используется, то уникальный идентификатор предоставляется экземпляром служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. При этом используется соглашение об именах, которое зависит от объекта, которому назначается идентификатор. Дополнительные сведения об использовании `Create` и `Alter` команды для определения объектов, см. в разделе [Создание и изменение объектов &#40;XMLA&#41;](../xmla/xml-elements-objects.md).  
  
## <a name="see-also"></a>См. также  
 [Объект элемента &#40;XML для Аналитики&#41;](../xmla/xml-elements-properties/object-element-xmla.md)   
 [Элемент ParentObject &#40;XML для Аналитики&#41;](../xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [Элемент Source &#40;XML для Аналитики&#41;](../xmla/xml-elements-properties/source-element-xmla.md)   
 [Элемент target &#40;XML для Аналитики&#41;](../xmla/xml-elements-properties/target-element-xmla.md)   
 [Разработка с использованием XMLA в службах Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
