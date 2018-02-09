---
title: "PDW и устройством структуры физические компоненты (система платформы аналитики)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7748d3da-0b7c-4ec6-9c22-4897758ba573
caps.latest.revision: "17"
ms.openlocfilehash: 95e80aaa641b04391d96b55f7491e21f1a30b6d1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-and-appliance-fabric-physical-components"></a>Физические компоненты PDW и структуры устройства
Имена и описания для компонентов физической структуры PDW и устройством. Регион PDW содержит все эти компоненты.  
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Схемы компонентов  
Это показывает имена физических компонентов и их расположение в стойку первого устройства 6 вычислительных узлов.  
  
![Имена компонентов региона PDW — HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
Фактическое имя для компонентов PDW — имя региона PDW, а затем дефис, за которым следует имя компонента. Например, если имя региона PDW PDW123, фактические имена являются **PDW123 CTL01**, **PDW123 CMP01**и т. д.  
  
Аналогичным образом фактическое имя для устройства компоненты структуры — домен устройства, а затем дефис, за которым следует имя компонента. Например, если домен устройства FSW123, устройство структуры виртуальные машины — **FSW123 WDS**, **FSW123 AD01**, **FSW123 VMM**и т. д.  
  
Вот обобщенное представление регион PDW с 6 вычислительных узлов.  
  
![Имена компонентов PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Компоненты PDW  
Виртуальные машины PDW являются частью региона PDW.  
  
*PDW_region*-CTL01  
Виртуальная машина, работающая узел элемента управления. Это выполняется на HST01 и могут выполнять переход на HST02.  
  
> [!WARNING]  
> SQL Server PDW не поддерживает создание моментальных снимков виртуальной машины CTL01 с помощью диспетчера Hyper-V. Моментальные снимки зависят от локального хранилища, которая приведет к ошибкам, если виртуальная машина предпринимает попытки перехода на другой ресурс для его резервного копирования. Создание моментального снимка также может вызвать сбои в надежности с других Виртуальных машин, отработка отказа на сервер пассивный.  
  
*PDW_region*-CMP01 через *PDW_Region*-CMP06  
Виртуальная машина, работающая вычислительных узлов. На этой диаграмме 6 вычислительных узлов узлов HSA01 через HSA06 запуска вычислительного узла CMP01 виртуальные машины, через CMP06 соответственно.  
  
## <a name="fabric"></a>Компоненты структуры устройства  
Эти компоненты являются частью структуры устройства.  
  
### <a name="virtual-machines"></a>Виртуальные машины  
*appliance_domain*- WDS  
Это узлов виртуальных машин службы развертывания Windows (WDS), который использует система платформы аналитики развертывания операционных систем Windows по сети устройства. Он также содержит службу DHCP, которая позволяет узлам appliance присоединиться к сети устройство без необходимости предварительно настроенный IP-адрес.  
  
*Appliance_domain*WDS — виртуальная машина работает на HST01 и могут выполнять переход на HST02. Виртуальная машина WDS и виртуальных машин VMM во время установки устройства развертывания Windows на физических узлах. Во время жизненного цикла устройства VMM и WDS операций, таких как замена узла.  
  
*appliance_domain*- VMM  
Virtual Machine Manager (VMM) на виртуальной машине и могут выполнять переход на HST02. System Center для развертывания операционной системы на физических узлах, размещаемых VMM. VMM также предоставляет Windows Server Update Services (WSUS) для применения или удаления обновления Windows для всех узлов и виртуальных машин.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Доменных служб к Active Directory, содержащий доменных имен (DNS), работающая на виртуальной машине HST01 и HST02. Для обеспечения высокой доступности устройства AD01 и AD02 являются контроллерами домена реплицированные, и они этого не отработки отказа. В случае сбоя одного другой уже доступен в правильные данные.  
  
*appliance_domain*-ISCSI01  
Одна виртуальная машина ISCSI выполняется на каждом узле с присоединенного хранилища (HSA01 HSA06). Эта виртуальная машина не не отработки отказа.  
  
### <a name="hosts"></a>Узлы  
*appliance_domain*-HST01 через *appliance_domain*-HST06  
Узлы управления PDW узла и устройством структуры виртуальных машин. HST03 — необязательный пассивный узел.  
  
*appliance_domain*-HSA01 через *appliance_domain*-HSA08  
Узлы с присоединенного хранилища (HSA). Каждый HAS узла выполняется один ВМ вычислительного узла и одной виртуальной Машины ISCSI.  
  
### <a name="cluster-for-pdw"></a>Кластер для PDW  
*appliance_domain*-WFOHST01  
Кластер PDW называется WFOHST01. Он управляет все физические узлы и виртуальные машины, принадлежащих PDW.  
  
### <a name="direct-attached-storage"></a>Непосредственно подключенное хранилище  
*appliance_domain*-DAS01 через *appliance_domain*-DAS03  
Это непосредственно подключенное хранилище, подключенном к вычислительных узлов. HP имеет один DAS для каждые два вычислительных узлов. Dell и такты имеют один DAS для каждые три вычислительных узлов.  
  
## <a name="see-also"></a>См. также:  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Конфигурация устройства &#40; Система платформы аналитики &#41;](appliance-configuration.md)  
[Задачи управления устройством &#40; Система платформы аналитики &#41;](appliance-management-tasks.md)  
  