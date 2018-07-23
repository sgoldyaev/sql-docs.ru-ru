---
title: Свойства объектов (столбцов) с табличными значениями (визуальные инструменты для баз данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.designers.properties.QueryViewColumn
ms.assetid: 212d9bcd-aded-4313-a6b9-d7e2270e5954
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b26eb1ebcc3beec799ec56ee0e5eb895ec01ae1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303084"
---
# <a name="table-valued-object-column-properties-visual-database-tools"></a>Свойства объектов (столбцов) с табличными значениями (визуальные инструменты для баз данных)
  Эти свойства отображаются при выборе столбца в табличном объекте на панели **Диаграмма** конструктора запросов и представлений.  
  
> [!NOTE]  
>  Свойства в данном разделе сгруппированы по категориям, а не по алфавиту.  
  
> [!NOTE]  
>  В зависимости от установок или выпуска сервера доступные диалоговые окна и команды меню могут отличаться от описанных в справке. Чтобы изменить параметры, выберите **Импорт и экспорт параметров** в меню **Сервис** .  
  
 **Категория «Идентификатор»**  
 Разверните для отображения свойства **Имя** .  
  
 **Название**  
 Отображает имя выбранного столбца.  
  
 **Категория конструктора запросов**  
 Разворачивается и отображает свойства **Разрешить значения NULL**, **Параметры сортировки**, **Тип данных**, **Длина**, **Точность**, **Масштаб**и **Размер**.  
  
 **Разрешить значения NULL**  
 Указывает, разрешены ли в столбце данного типа значения NULL.  
  
 **Параметры сортировки**  
 Отображает установку параметров сортировки для выбранного столбца. Параметры сортировки могут быть заданы во вкладке «Свойства столбца» в конструкторе таблиц.  
  
 **Тип данных**  
 Отображает тип данных выбранного столбца.  
  
 **Длина**  
 Показывает число символов или цифр, допустимых выбранным типом данных этого столбца. Данное свойство доступно только для символьных типов данных.  
  
> [!NOTE]  
>  Размер в байтах см. в свойстве **Размер** ниже.  
  
 **Точность**  
 Указывает максимальное число разрядов, допустимых для числовых типов данных. Для нечисловых типов данных в этом свойстве отображается **0** .  
  
 **Масштаб**  
 Указывает максимальное количество цифр справа от запятой в числовых типах данных. Это значение должно быть меньше или равно указанной точности. Для нечисловых типов данных в этом свойстве отображается **0** .  
  
 **Размер**  
 Показывает размер в байтах, допустимых типом данных этого столбца. Например, тип данных nchar может иметь длину 10 (количество символов), однако для работы с кодировкой Юникод его длина будет равняться 20.  
  
  