---
title: База данных служб Master Data Services | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], about the database
- database [Master Data Services]
ms.assetid: 5f590cc1-6ec2-4b8c-a598-03de0f6051a0
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a6d7b54e6df133c4362ba5d9cb998a61fea3202f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115111"
---
# <a name="master-data-services-database"></a>База данных служб Master Data Services
  База данных содержит все сведения, необходимые для системы [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Она является основой для развертывания [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . База данных [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
-   В ней хранятся параметры, объекты базы данных и данные, необходимые системе [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
-   Содержит промежуточные таблицы, используемые для обработки данных из исходных систем.  
  
-   Предоставляет схему и объекты базы данных для хранения основных данных из исходных систем.  
  
-   Поддерживает управление версиями, в том числе проверку бизнес-правил и уведомления по электронной почте.  
  
-   Предоставляет представления для систем-подписчиков, которым надо извлекать данные из базы данных.  
  
## <a name="in-this-section"></a>в этом разделе  
  
-   [Промежуточная таблица конечных элементов &#40;службы Master Data Services&#41;](leaf-member-staging-table-master-data-services.md)  
  
-   [Промежуточная таблица консолидированных элементов &#40;службы Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)  
  
-   [Промежуточная таблица связей &#40;службы Master Data Services&#41;](../../2014/master-data-services/relationship-staging-table-master-data-services.md)  
  
-   [Ошибки промежуточного процесса &#40;службы Master Data Services&#41;](../../2014/master-data-services/staging-process-errors-master-data-services.md)  
  
## <a name="see-also"></a>См. также  
 [Создание базы данных служб Master Data Services](install-windows/create-a-master-data-services-database.md)   
 [Защита объектов базы данных (службы Master Data Services)](../../2014/master-data-services/database-object-security-master-data-services.md)   
 [Имена входа, пользователи и роли базы данных (службы Master Data Services)](../../2014/master-data-services/database-logins-users-and-roles-master-data-services.md)  
  
  
