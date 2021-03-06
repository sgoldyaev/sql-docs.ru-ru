---
title: Обработчики событий в службах Integration Services (SSIS) | Документы Майкрософт
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- run-time [Integration Services]
- SQL Server Integration Services packages, events
- event handlers [Integration Services], about event handlers
- events [Integration Services]
- packages [Integration Services], events
- event handlers [Integration Services]
- SSIS packages, events
- containers [Integration Services], events
- events [Integration Services], about events
ms.assetid: 6f60cf93-35dc-431c-908d-2049c4ab66ba
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 41762bb046e5b118d7802555c2b676378e81df7b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48122844"
---
# <a name="integration-services-ssis-event-handlers"></a>Обработчики событий в службах Integration Services (SSIS)
  Во время выполнения исполняемых объектов (пакетов, контейнеров «цикл по каждому элементу», «цикл по элементам», последовательности и узлы задач) возникают события. Например, в случае ошибки возникает событие OnError. Можно создать пользовательские обработчики событий для этих событий, чтобы расширить функциональность пакетов и упростить управление пакетами во время их выполнения. Обработчики событий могут выполнять следующие задачи:  
  
-   Очистка временного хранилища данных, когда пакет или задача прекращает выполнение.  
  
-   Получение сведений о системе для слежения за доступностью ресурса перед запуском пакета.  
  
-   Обновление данных в таблице, когда уточняющий запрос в ссылочной таблице закончился неудачей.  
  
-   Отправка сообщения по электронной почте при возникновении ошибки или предупреждения или при неудачном завершении задачи.  
  
 Если у события нет обработчика, событие передается контейнеру выше по иерархии контейнеров пакета. Если у этого контейнера есть обработчик, он выполняется в ответ на событие. Если нет, то событие передается контейнеру выше в иерархии контейнеров.  
  
 Следующая диаграмма приводит простой пакет, имеющий контейнер «цикл по элементам», который, в свою очередь, содержит задачу «Выполнение SQL».  
  
 ![Пакет, контейнер "Цикл по элементам", сервер задач, задача "Выполнение SQL"](media/mw-dts-eventhandlerpkg.gif "Пакет, контейнер \"Цикл по элементам\", сервер задач, задача \"Выполнение SQL\"")  
  
 Только у пакета имеется обработчик для события `OnError`. Если произошла ошибка при выполнении задачи «Выполнение SQL», `OnError` запускает обработчик событий для пакета. На следующей схеме показана последовательность вызовов, вследствие `OnError` обработчик событий для выполнения пакета.  
  
 ![Поток обработчиков событий](media/mw-dts-eventhandlers.gif "Поток обработчиков событий")  
  
 Обработчики событий являются элементами коллекции обработчиков событий, и эта коллекция включена во все контейнеры. Если пакет создается при помощи конструктора служб [!INCLUDE[ssIS](../includes/ssis-md.md)] , то можно видеть элементы коллекции обработчиков событий в папке **Обработчики событий** на вкладке **Обозреватель пакетов** конструктора служб [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 Можно настроить контейнер обработчика событий следующим образом:  
  
-   Укажите имя и описание для обработчика событий.  
  
-   Укажите, следует ли запускать обработчик событий, следует ли считать выполнение пакета неудачным в случае неудачи выполнения обработчика событий, а также укажите максимальное число ошибок, после которого обработчик считается неудачно завершенным.  
  
-   Укажите результат выполнения, который будет возвращен вместо действительного результата, возвращаемого обработчиком событий во время выполнения.  
  
-   Укажите параметр преобразования обработчика события.  
  
-   Укажите режим создания журнала, используемого обработчиком событий.  
  
## <a name="event-handler-content"></a>Содержимое обработчика событий  
 Создание обработчика событий сходно с построением пакета: у обработчика есть задачи и контейнеры, которые по порядку включаются в поток управления, и обработчик также может включать в себя потоки данных. Конструктор служб [!INCLUDE[ssIS](../includes/ssis-md.md)] содержит вкладку **Обработчики событий** для создания пользовательских обработчиков событий. Дополнительные сведения см. в разделе [обработчики событий пакетов служб SSIS](integration-services-ssis-event-handlers.md).  
  
 Обработчики событий также могут быть созданы программно. Дополнительные сведения см. в статье [Программная обработка событий](building-packages-programmatically/handling-events-programmatically.md).  
  
## <a name="run-time-events"></a>События времени выполнения  
 В следующей таблице перечисляются обработчики событий, предоставляемые службами [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , и описываются события времени выполнения, в случае которых обработчик запускается.  
  
|Обработчик событий|Событие|  
|-------------------|-----------|  
|`OnError`|Обработчик событий для `OnError` событий. Событие вызывается исполняемым объектом при возникновении ошибки.|  
|**OnExecStatusChanged**|Обработчик события **OnExecStatusChanged** . Событие вызывается исполняемым объектом при изменении его состояния выполнения.|  
|**OnInformation**|Обработчик события **OnInformation** . Это событие вызывается во время проверки и выполнения исполняемого объекта для передачи данных. Событие передает только данные; ошибки и предупреждения не передаются.|  
|**OnPostExecute**|Обработчик события **OnPostExecute** . Событие вызывается исполняемым объектом сразу после выполнения.|  
|**OnPostValidate**|Обработчик события **OnPostValidate** . Событие вызывается исполняемым объектом после завершения проверки.|  
|**OnPreExecute**|Обработчик события **OnPreExecute** . Событие вызывается исполняемым объектом непосредственно перед его запуском.|  
|**OnPreValidate**|Обработчик события **OnPreValidate** . Событие вызывается исполняемым объектом в начале проверки.|  
|**OnProgress**|Обработчик события **OnProgress** . Событие вызывается исполняемым объектом в процессе выполнения.|  
|**OnQueryCancel**|Обработчик события **OnQueryCancel** . Событие вызывается исполняемым объектом, чтобы установить, следует ли ему прекратить выполнение.|  
|**OnTaskFailed**|Обработчик события **OnTaskFailed** . Событие вызывается неудачно завершившейся задачей.|  
|**OnVariableValueChanged**|Обработчик события **OnVariableValueChanged** . Событие вызывается исполняемым объектом при изменении значения переменной. Событие вызывается исполняемым объектом, в котором определена переменная. Это событие не происходит, если **RaiseChangeEvent** свойства переменной для `False`. Дополнительные сведения см. в разделе [Integration Services &#40;SSIS&#41; Variables](integration-services-ssis-variables.md).|  
|**OnWarning**|Обработчик события **OnWarning** . Событие вызывается исполняемым объектом при возникновении предупреждения.|  
  
## <a name="configuration-of-an-event-handler"></a>Настройка обработчика событий  
 Задать свойства можно в окне **Свойства** среды [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] или программными средствами.  
  
 Дополнительные сведения о настройке свойств этих свойств в [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] см. в разделе [Задание свойств задач или контейнеров](../../2014/integration-services/set-the-properties-of-a-task-or-container.md).  
  
 Дополнительные сведения о настройке этих свойств программными средствами см. в разделе <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>.  
  
## <a name="related-tasks"></a>Связанные задачи  
 Сведения о том, как добавить обработчик событий в пакет, см. в разделе [Добавление к пакету обработчик событий](../../2014/integration-services/add-an-event-handler-to-a-package.md).  
  
  
