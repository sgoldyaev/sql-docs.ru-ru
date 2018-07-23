---
title: Диалоговое окно «видимость столбцов» | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.columnvisibility.f1
- "10127"
ms.assetid: ca59d1cd-d782-4298-aa61-4f312c32eb50
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8a63473d706fa25f69910a52b4ab352d631bcc11
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268960"
---
# <a name="column-visibility-dialog-box"></a>Диалоговое окно «Видимость столбца»
  Используйте диалоговое окно **Видимость столбца** , чтобы отобразить или скрыть выбранный столбец при первом запуске отчета либо назначить другой элемент отчета для переключения видимости столбца.  
  
## <a name="options"></a>Параметры  
 **При первоначальном запуске отчета**  
 Выберите параметр, определяющий, как элемент отчета отображается в отчете первоначально.  
  
 **Показать**  
 Выберите этот параметр, чтобы отобразить элемент отчета.  
  
 **Скрыть**  
 Выберите этот параметр, чтобы скрыть элемент отчета.  
  
 **Отображать или скрывать в зависимости от выражения**  
 Этот параметр используется для изменения исходной видимости с помощью выражения.  
  
 Введите выражение, результатом которого является `Boolean` значение `True` элемент скрыт, и `False` для отображения элемента. Чтобы изменить выражение, нажмите кнопку "Выражение" (*fx*).  
  
 **Отображение может переключаться этим элементом отчета**  
 Выберите данный параметр для отображения изображения переключателя, который позволяет пользователю отображать или скрывать данный элемент отчета в средстве просмотра HTML-страниц.  
  
 Введите или выберите имя текстового поля отчета для отображения изображения отчета, например, Textbox1. Выбранное текстовое поле должно быть в текущей области или области, содержащей этот элемент отчета. Например, чтобы включить видимость строк, связанных с дочерней группой, выберите текстовое поле в строке, связанной с родительской группой. Чтобы переключить видимость диаграммы, выберите текстовое поле в той же области, где находится эта диаграмма, например, в тексте отчета или в прямоугольнике.  
  
## <a name="see-also"></a>См. также  
 [Примеры выражений (построитель отчетов и службы SSRS)](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Добавление действия "Развернуть" или "Свернуть" к элементу (построитель отчетов и службы SSRS)](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Образы &#40;построитель отчетов и службы SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Справка F1 по использованию конструктора отчетов](tools/report-designer-f1-help.md)  
  
  