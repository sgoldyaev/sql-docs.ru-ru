---
title: Элемент CommitTransaction (XML для Аналитики) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CommitTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CommitTransaction
- urn:schemas-microsoft-com:xml-analysis#CommitTransaction
- microsoft.xml.analysis.committransaction
helpviewer_keywords:
- CommitTransaction command
ms.assetid: 1cd814dc-a0be-4305-b44d-faf15e843f7d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eff18a85bc33dfc47377f0613f0696811ff1389a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203204"
---
# <a name="committransaction-element-xmla"></a>Элемент CommitTransaction (XML для аналитики)
  Фиксирует транзакцию в текущем сеансе работы с [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] экземпляра.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Command>  
   <CommitTransaction />  
</Command>  
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
|Родительские элементы|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Дочерние элементы|None|  
  
## <a name="remarks"></a>Примечания  
 Команда `CommitTransaction` фиксирует активную транзакцию, явно определенную с использованием элемента `BeginTransaction` в текущем сеансе. Если еще не существует активной транзакции, возникает ошибка. Если активная транзакция уже существует, то в экземпляре служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] уменьшается количество ссылок на транзакции для текущего сеанса. Если количество ссылок на явно определенные активные транзакции достигает нуля, в экземпляре служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] фиксируется соответствующая транзакция.  
  
## <a name="see-also"></a>См. также  
 [Элемент BeginTransaction &#40;XML для Аналитики&#41;](begintransaction-element-xmla.md)   
 [Элемент Cancel &#40;XML для Аналитики&#41;](cancel-element-xmla.md)   
 [Элемент RollbackTransaction &#40;XML для Аналитики&#41;](rollbacktransaction-element-xmla.md)   
 [Команды &#40;XML для Аналитики&#41;](xml-elements-commands.md)  
  
  
