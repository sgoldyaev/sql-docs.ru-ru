---
title: Поддержка высокого уровня доступности | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 2e0f6d3f-0536-46d9-8630-835e199515bf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2d98e061fc71bfa5b9e5b076004934e74cabd35c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112734"
---
# <a name="high-availability-support"></a>Поддержка высокого уровня доступности
  Служба CDC для Oracle разработана с учетом требований высокого уровня доступности. Следующие функции составляют часть функций поддержки высокого уровня доступности:  
  
-   Служба CDC для Oracle не использует никаких файлов ресурсов (локальных или сетевых). Все состояние сохраняется в целевом экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Это позволяет без труда запустить службу на другом компьютере, использующем тот же экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , если в компьютере, на котором запущена служба, произойдет сбой. Чтобы сократить время восстановления, длительные транзакции Oracle хранятся в промежуточной таблице целевого экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], благодаря чему устраняется необходимость повторного сканирования множества журналов транзакций сразу после сбоя (или перезапуска службы).  
  
-   Служба CDC для Oracle может использовать кластеризованные экземпляры [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для восстановления после сбоя экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и последующей отработки отказа на другом узле кластера. Администратору компьютера, на котором запущена служба Oracle CDC, при создании службы Oracle CDC Service необходимо лишь указать сведения о подключении к кластеризованному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Служба CDC для Oracle может использовать [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] **AlwaysOn** функцию зеркального отображения базы данных. Поддержка этой функции требует, чтобы MSXDBCDC и все остальные базы данных CDC находились в одной группе доступности. Он также требуется администратор компьютера службы Oracle CDC, указав соответствующее **AlwaysOn** сведения о подключении к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] группы доступности (например, свойства соединения `Failover_Partner and Network=dbmssocn`). Это позволяет службе CDC автоматически возобновить обработку на вторичной реплике баз данных после отработки отказа.  
  
-   Службу CDC для Oracle можно настроить как ресурс общей службы, расположенный на отказоустойчивом кластере Windows (совместно или отдельно от [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), что упрощает отработку отказа, и повторить обработку CDC при помощи ресурсов кластера. Чтобы настроить службу CDC для Oracle в качестве ресурса отказоустойчивого кластера, системному администратору необходимо настроить службу CDC для Oracle в качестве ресурса общей службы — для каждого узла отказоустойчивого кластера.  
  
-   Служба CDC для Oracle поддерживает Oracle RAC, благодаря чему возможен обмен данными между ней и базой данных Oracle, а также обработка журналов вызова, даже если один из узлов Oracle RAC отключен.  
  
  
