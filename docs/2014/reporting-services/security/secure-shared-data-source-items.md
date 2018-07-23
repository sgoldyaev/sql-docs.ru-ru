---
title: Защита элементов общего источника данных | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 71fc9ae4563515bdfebf79af4a41e9379502d872
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256216"
---
# <a name="secure-shared-data-source-items"></a>Защита совместно используемых элементов источника данных
  Можно задать параметры безопасности для общего элемента источника данных, чтобы разрешить или запретить доступ к нему.  
  
 Пользователь с минимальным доступом к общему источнику данных (например, такой доступ предоставляется ролью **Браузер** ) может просматривать список отчетов, использующих данный элемент, при условии, что ему также разрешено просматривать сами отчеты.  
  
 Пользователь с более широким набором прав доступа (например, предоставляемым ролью **Диспетчер содержимого** ) может просматривать и задавать свойства для общего источника данных.  
  
 Для настройки безопасности нужно создать назначение роли, указывающей, какой пользователь или группа имеет доступ к данному общему источнику данных. Пользователи, которым разрешен доступ к общему элементу источника данных, могут изменять его имя, описание, строку соединения и учетные данные.  
  
## <a name="tasks-and-access-to-items"></a>Задачи и доступ к элементам  
 При создании назначений ролей используйте роль, у которой есть такие задачи для назначения необходимых разрешений пользователям и группам.  
  
|Выберите эту задачу|Предоставить пользователям следующие разрешения.|  
|----------------------|---------------------------------|  
|Просмотр источников данных|Просмотр общего элемента источника данных в иерархии папок. Без этой задачи элемент будет невидим для пользователей, и они не будут знать, что этот источник данных доступен.|  
|Управление источниками данных|Просмотр свойств, задающих имя, описание и сведения о соединении. Эта задача используется также для отображения общего элемента источника данных в иерархии папок. Если эта задача выбрана, можно опустить задачу «Просмотр источников данных».|  
|Установка безопасности элементов|Создание и изменение назначений ролей, управляющих доступом к общему источнику данных. Эта задача должна использоваться совместно с задачей «Просмотр источников данных» или «Управление источниками данных». В противном случае она не будет действовать, поскольку пользователь не сможет выбрать источник.|  
  
## <a name="see-also"></a>См. также  
 [Управление источниками данных отчета](../report-data/manage-report-data-sources.md)   
 [Защита папок](secure-folders.md)   
 [Защищенные отчеты и ресурсы](secure-reports-and-resources.md)   
 [Предоставление разрешений на сервер отчетов в собственном режиме](granting-permissions-on-a-native-mode-report-server.md)   
 [Сохраненные учетные данные в источнике данных Reporting Services](../report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  