---
title: Пакетная элемент (XMLA) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Batch Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Batch
- microsoft.xml.analysis.batch
- http://schemas.microsoft.com/analysisservices/2003/engine#Batch
helpviewer_keywords:
- Batch command
ms.assetid: 818f3212-9605-4e34-8623-1154d9fae1f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d402c1f6c35370a506ed57c43b8fbc05d0b6bef7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178144"
---
# <a name="batch-element-xmla"></a>Элемент Batch (XML для аналитики)
  Выполняет один или несколько XML для аналитики (XMLA) команды пакетной операции, последовательно или параллельно на экземпляр [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Command>  
   <Batch Transaction="Boolean" ProcessAffectedObjects="Boolean">  
      <Bindings>...</Bindings>  
      <DataSource>...</DataSource>  
      <DataSourceView>...</DataSourceView>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <Parallel>...</Parallel>  
      <!-- One or more XMLA commands -->  
   </Batch>  
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
|Дочерние элементы|[Привязки](../xml-elements-properties/bindings-element-xmla.md), [DataSource](../xml-elements-properties/source-element-xmla.md), [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../../scripting/objects/errorconfiguration-element-assl.md), [параллельных](../xml-elements-properties/parallel-element-xmla.md)<br /><br /> Один или несколько из следующих команд XML для Аналитики: [Alter](alter-element-xmla.md), [резервного копирования](backup-element-xmla.md), [BeginTransaction](begintransaction-element-xmla.md), [ClearCache](clearcache-element-xmla.md), [ CommitTransaction](committransaction-element-xmla.md), [создать](create-element-xmla.md), [удалить](delete-element-xmla.md), [DesignAggregations](designaggregations-element-xmla.md), [Drop](drop-element-xmla.md), [Вставить](insert-element-xmla.md), [блокировки](lock-element-xmla.md), [MergePartitions](mergepartitions-element-xmla.md), [NotifyTableChange](notifytablechange-element-xmla.md), [процесс](process-element-xmla.md), [Восстановить](restore-element-xmla.md), [RollbackTransaction](rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [инструкции](statement-element-xmla.md), [подписаться](subscribe-element-xmla.md), [Синхронизировать](synchronize-element-xmla.md), [разблокировать](unlock-element-xmla.md), [обновление](update-element-xmla.md), [UpdateCells](drop-element-xmla.md)|  
  
## <a name="attributes"></a>Атрибуты  
  
|attribute|Описание|  
|---------------|-----------------|  
|ProcessAffectedObjects|(Необязательный атрибут `Boolean`) Показывает, будут ли обработаны все объекты, которые нуждаются в повторной обработке.<br /><br /> Если установлено значение true, то экземпляр служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] будет обрабатывать все объекты, необходимость обработки которых была вызвана обработкой объекта, включенного в команду `Batch`.<br /><br /> Если установлено значение `false`, то экземпляр служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] будет обрабатывать только те объекты, которые были включены в команду `Batch`.|  
|Transaction|(Необязательный атрибут `Boolean`) Показывает, будут ли команды, включенные в команду `Batch`, обрабатываться в одной транзакции или они будут обрабатываться как индивидуальные транзакции.<br /><br /> Если установлено значение true, то все команды, которые были включены в команду `Batch`, считаются одной транзакцией. Если любая из команд завершается неуспешно, то происходит откат команд, выполненных до появления ошибки, а выполнение команды `Batch` останавливается без выполнения дальнейших команд.<br /><br /> Если установлено значение `false`, то команда `Batch` пытается выполнить каждую команду; результаты каждой успешно выполненной команды фиксируются.|  
  
## <a name="remarks"></a>Примечания  
  
> [!WARNING]  
>  Команда, выполнение или инструкция в настоящее время не поддерживается в пакетной операции.  
  
 Дополнительные сведения о выполнении пакетных операций в XML для Аналитики см. в разделе [выполнение пакетных операций &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="see-also"></a>См. также  
 [Команды &#40;XML для Аналитики&#41;](xml-elements-commands.md)  
  
  
