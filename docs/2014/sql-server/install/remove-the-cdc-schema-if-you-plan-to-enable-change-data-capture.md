---
title: Удалите схему cdc, если вы планируете включить сбор данных изменений | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5d162635a9162871e51fe0664198302804aa487
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180784"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>Удаление схемы cdc, если планируется ввести в действие систему отслеживания измененных данных
  База данных уже содержит схему cdc. Если планируется разрешить использование системы отслеживания измененных данных после обновления, необходимо вначале удалить эту схему cdc. Если в базе данных включено применение системы отслеживания измененных данных, то в [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] создается новая схема с именем cdc.  
  
  
