---
title: Настройте для контейнера цикл | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2adcb3e79e3733b5fb8151bfa7f65e7bebb4d910
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126170"
---
# <a name="configure-a-for-loop-container"></a>Настройка контейнера «цикл по элементам»
  В процедуре описывается, как настроить контейнер «цикл по элементам» с помощью диалогового окна **Редактор циклов по элементам** .  
  
 Пример контейнера цикла «по элементам» см. в статье [Циклы SSIS, не завершающиеся сбоями](http://go.microsoft.com/fwlink/?LinkId=240295) на сайте bimonkey.com.  
  
### <a name="to-configure-the-for-loop-container"></a>Настройка контейнера «цикл по элементам»  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]дважды щелкните контейнер "цикл по элементам", чтобы открыть **Редактор циклов по элементам**.  
  
2.  При необходимости измените имя и описание контейнера «цикл по элементам».  
  
3.  При необходимости введите выражение инициализации в текстовое поле **InitExpression** .  
  
4.  Введите выражение в текстовое поле **EvalExpression** .  
  
    > [!NOTE]  
    >  Выражение должно иметь логическое значение. Если значением этого выражения будет `false`, выполнение цикла останавливается.  
  
5.  При необходимости введите выражение присвоения в текстовое поле **AssignExpression** .  
  
6.  При необходимости щелкните **Выражения** и на странице **Выражения** создайте выражения свойств для свойств контейнера «цикл по элементам». Дополнительные сведения см. в разделе [Добавление или изменение выражение свойства](expressions/add-or-change-a-property-expression.md).  
  
7.  Щелкните **ОК** , чтобы закрыть **Редактор циклов For**.  
  
## <a name="see-also"></a>См. также  
 [Для контейнера цикла](control-flow/for-loop-container.md)   
 [Выражения служб Integration Services (SSIS)](expressions/integration-services-ssis-expressions.md)   
 [Использование выражений свойств в пакетах](expressions/use-property-expressions-in-packages.md)  
  
  
