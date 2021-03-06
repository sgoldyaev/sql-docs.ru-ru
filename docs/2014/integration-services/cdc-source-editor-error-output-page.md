---
title: Редактор источника «CDC» (страница "Вывод ошибок") | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 8a4c2cb8-fd2f-4c45-824f-b93473a8981e
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a43085040e3bc1fde5f01b9ccb769695ea877341
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129844"
---
# <a name="cdc-source-editor-error-output-page"></a>Редактор источника «CDC» (страница «Вывод ошибок»)
  Страница **Вывод ошибок** диалогового окна **Редактор источника CDC** используется для выбора параметров обработки ошибок.  
  
 Дополнительные сведения об источнике CDC см. в разделе [CDC Source](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Список задач  
 **Открытие страницы «Вывод ошибок» редактора источника CDC**  
  
1.  В среде [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]откройте пакет служб [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] , содержащий источник CDC.  
  
2.  На вкладке **Поток данных** дважды щелкните источник CDC.  
  
3.  В окне **Редактор источника CDC**нажмите кнопку **Вывод ошибок**.  
  
## <a name="options"></a>Параметры  
 **Ввод-вывод**  
 Просмотр имени источника данных.  
  
 **Столбец**  
 Просмотрите внешние (исходные) столбцы, выбранные на странице **Диспетчер соединений** диалогового окна **Редактор источника CDC** .  
  
 **Ошибка**  
 Выберите порядок обработки ошибок в потоке источником CDC: пропустить ошибку, перенаправить строку или вызвать сбой компонента.  
  
 **Усечение**  
 Выберите порядок обработки усечений в потоке источником CDC: пропустить ошибку, перенаправить строку или вызвать сбой компонента.  
  
 **Описание**  
 Не используется.  
  
 **Присвоить указанное значение выбранным ячейкам**  
 Выберите, как источник CDC обрабатывает все выбранные ячейки при возникновении ошибки или усечения: пропустить ошибку, перенаправить строку или вызвать сбой компонента.  
  
 **Применить**  
 Примените параметры обработки ошибок к выбранным ячейкам.  
  
## <a name="error-handling-options"></a>Параметры обработки ошибок  
 Следующие параметры позволяют настроить обработку ошибок и усечений источником CDC.  
  
 **Компонент, завершившийся сбоем**  
 Задача потока данных заканчивается сбоем, если возникли ошибка или усечение. Это поведение по умолчанию.  
  
 **Пропуск неудачи**  
 Ошибка или усечение пропускается, и строка данных направляется на выход источника CDC.  
  
 **Перенаправление потока**  
 Ошибка или строка данных усечения направляется на выход ошибок источника CDC. В этом случае используется обработка ошибок источника CDC. Дополнительные сведения см. в статье [CDC Source](data-flow/cdc-source.md).  
  
## <a name="see-also"></a>См. также  
 [Редактор источника CDC &#40;страницы диспетчера соединений&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [Редактор источника CDC &#40;страница "столбцы"&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)  
  
  
