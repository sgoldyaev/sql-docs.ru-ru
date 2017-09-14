---
title: "Роли безопасности (службы Analysis Services — многомерные данные) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], roles
- Analysis Services objects, roles
- security [Analysis Services], roles
- roles [Analysis Services], about roles
- server roles [Analysis Services]
- database roles [Analysis Services]
- roles [Analysis Services]
- storing data [Analysis Services], roles
- access rights [Analysis Services], roles
ms.assetid: 5b7e9cef-ff68-4d8e-99bc-e0094ced1baa
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ee88f607ae1370746db12ea4b9f9f6acc98c4c09
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="security-roles--analysis-services---multidimensional-data"></a>Роли безопасности (службы Analysis Services — многомерные данные)
  Роли используются в [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] для управления безопасностью [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] объектов и данных. По сути роли связывают идентификаторы безопасности (SID) для Microsoft Windows пользователей и групп, имеющих определенные права доступа и разрешения, определенные для объектов, управляемых с помощью экземпляра [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Два типа ролей приведены в [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:  
  
-   Роль сервера — фиксированная роль, предоставляющая права администратора для доступа к экземпляру служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   Роли базы данных — роли, определенные администраторами для контроля доступа к объектам и данным пользователям, которые не являются администраторами.  
  
 Безопасность в [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] обеспечивается с использованием ролей и разрешений. Роли — это группы пользователей. Пользователи, называемые также членами, могут быть добавлены или удалены из состава ролей. Разрешения для объектов регламентируются с помощью ролей, и все члены, относящиеся к некоторой роли, могут использовать объекты, на которые в этой роли имеются разрешения. Все члены одной и той же роли имеют одинаковые разрешения на объекты. Разрешения связаны с конкретными объектами. Для каждого объекта предусмотрена коллекция разрешений, в которой указаны предоставленные разрешения на этот объект, причем на каждый объект могут быть предоставлены разные наборы разрешений. Для каждого разрешения из коллекции разрешений объекта назначена отдельная роль.  
  
## <a name="role-and-role-member-objects"></a>Объекты ролей и членов ролей  
 Роль — это объект, который предназначен для использования в качестве контейнера для коллекции пользователей (членов). Определение роли регламентируется членство пользователей в [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Таким образом, разрешения присваиваются с учетом роли, поэтому пользователь должен стать членом роли, прежде чем получить доступ к какому-либо объекту.  
  
 Объект <xref:Microsoft.AnalysisServices.Role> состоит из значений параметров Name, Id и Members. Значение Members — это коллекция строк. Каждый член роли содержит имя пользователя в форме «домен\имя_пользователя». Значение Name — это строка, которая содержит имя роли. Значение ID — это строка, которая содержит уникальный идентификатор роли.  
  
### <a name="server-role"></a>Роль сервера  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Роли сервера определяет административный доступ пользователей и групп Windows к экземпляру компонента [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Члены этой роли имеют доступ ко всем [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] баз данных и объектов в экземпляре [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]и могут выполнять следующие задачи:  
  
-   Выполнение административных функций на уровне сервера в среде SQL Server Management Studio или [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], включая создание баз данных и настройку свойств на уровне сервера.  
  
-   Выполнение административных функций программным методом с помощью объектов AMO.  
  
-   Обслуживание ролей базы данных служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   Запуск трассировок (отличных от обработки событий, которые могут выполняться ролью базы данных с правом доступа Process).  
  
 Каждый экземпляр служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] имеет роль сервера, которая определяет пользователей с функциями администрирования этого экземпляра. Имя и идентификатор этой роли — «Администраторы»; в отличие от ролей базы данных, роль сервера удалить нельзя, в нее также нельзя добавлять разрешения или удалять их. Другими словами, пользователь является или не является администратором экземпляра [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]в зависимости от того, включены ли пользователь в роли сервера для этого экземпляра [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
### <a name="database-roles"></a>Роли базы данных  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Роль базы данных определяет доступ пользователей к объектам и данным в [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] базы данных. Роль базы данных создается как отдельный объект в базе данных служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] и применяется только к той базе данных, в которой эта роль создана. Пользователи и группы Windows включаются в эту роль администратором. Он же определяет разрешения этой роли.  
  
 Разрешения роли, помимо доступа к объектам и данным в базе данных, позволяют членам роли получить доступ и права администрирования базы данных. Каждое разрешение имеет одно или несколько связанных прав доступа, которые, в свою очередь, позволяют точно контролировать доступ к отдельным объектам в базе данных.  
  
## <a name="permission-objects"></a>Объекты разрешений  
 Разрешения связаны с объектом (куб, измерение и др.) для конкретной роли. Разрешения указывают на то, какие операции может выполнять над этим объектом член этой роли.  
  
 Класс <xref:Microsoft.AnalysisServices.Permission> представляет собой абстрактный класс. Поэтому необходимо использовать производные классы для определения разрешений на соответствующие объекты. Для каждого объекта определяется производный класс разрешения.  
  
|Объект|Class|  
|------------|-----------|  
|<xref:Microsoft.AnalysisServices.Database>|<xref:Microsoft.AnalysisServices.DatabasePermission>|  
|<xref:Microsoft.AnalysisServices.DataSource>|<xref:Microsoft.AnalysisServices.DataSourcePermission>|  
|<xref:Microsoft.AnalysisServices.Dimension>|<xref:Microsoft.AnalysisServices.DimensionPermission>|  
|<xref:Microsoft.AnalysisServices.Cube>|<xref:Microsoft.AnalysisServices.CubePermission>|  
|<xref:Microsoft.AnalysisServices.MiningStructure>|<xref:Microsoft.AnalysisServices.MiningStructurePermission>|  
|<xref:Microsoft.AnalysisServices.MiningModel>|<xref:Microsoft.AnalysisServices.MiningModelPermission>|  
  
 Возможные действия, допускаемые в соответствии с разрешениями, показаны в следующем списке.  
  
|Действие|Значения|Объяснение|  
|------------|------------|-----------------|  
|Процесс|{**true**, **false**}<br /><br /> Default=**false**|Если дано значение **true**, то члены роли могут обрабатывать и сам объект, и любые содержащиеся в нем объекты.<br /><br /> Разрешения на обработку не применяются к моделям интеллектуального анализа данных. <xref:Microsoft.AnalysisServices.MiningModel>всегда наследуются разрешения <xref:Microsoft.AnalysisServices.MiningStructure>.|  
|ReadDefinition|{**None**, **Basic**, **Allowed**}<br /><br /> Default=**None**|Определяет, могут ли члены читать определение данных (в коде ASSL), связанное с объектом.<br /><br /> Если дано значение **Allowed**, то члены могут читать код ASSL, связанный с объектом.<br /><br /> Разрешения**Basic** и **Allowed** наследуются объектами, которые содержатся в данном объекте. **Allowed** переопределяет **Basic** и **None**.<br /><br /> Разрешение**Allowed** необходимо для выполнения операции DISCOVER_XML_METADATA над объектом. Разрешение**Basic** необходимо для создания связанных объектов и локальных кубов.|  
|Чтение|{**None**, **Allowed**}<br /><br /> Default=**None** (за исключением DimensionPermission, где default=**Allowed**)|Указывает, имеют ли члены доступ для чтения к наборам строк схемы и содержимому данных.<br /><br /> Значение**Allowed** предоставляет доступ для чтения в базе данных, что позволяет изучать состав объектов базы данных.<br /><br /> **Допускается** применительно к кубу предоставляет доступ на чтение к наборам строк схемы и доступ к содержимому куба (если не ограничивается <xref:Microsoft.AnalysisServices.CellPermission> и <xref:Microsoft.AnalysisServices.CubeDimensionPermission>).<br /><br /> **Допускается** применительно к измерению предоставляет разрешение на все атрибуты в измерении чтение (если не ограничивается <xref:Microsoft.AnalysisServices.CubeDimensionPermission>). Разрешение на чтение используется для статического наследования только для <xref:Microsoft.AnalysisServices.CubeDimensionPermission>. **None** применительно к измерению скрывает это измерение и предоставляет доступ к члену по умолчанию только для статистически обрабатываемых атрибутов. Если измерение содержит статистически необрабатываемый атрибут, возникает ошибка.<br /><br /> **Допускается** на <xref:Microsoft.AnalysisServices.MiningModelPermission> предоставляет разрешения для просмотра объектов в наборах строк схемы и выполнения прогнозирования соединения.<br /><br /> **NoteAllowed** требуется для чтения или записи любого объекта в базе данных.|  
|запись|{**None**, **Allowed**}<br /><br /> Default=**None**|Указывает, имеют ли члены доступ для записи к данным родительского объекта.<br /><br /> Права доступа относятся к подклассам <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube> и <xref:Microsoft.AnalysisServices.MiningModel>. Не применяется к базе данных <xref:Microsoft.AnalysisServices.MiningStructure> подклассов, которые формирует ошибку проверки.<br /><br /> **Допускается** на <xref:Microsoft.AnalysisServices.Dimension> предоставляет разрешение на запись на все атрибуты в измерении.<br /><br /> **Допускается** на <xref:Microsoft.AnalysisServices.Cube> предоставляет разрешение на ячейки куба для секции, определенные как тип запись = обратной записи.<br /><br /> **Допускается** на <xref:Microsoft.AnalysisServices.MiningModel> предоставляет разрешение на изменение содержимого модели.<br /><br /> **Допускается** на <xref:Microsoft.AnalysisServices.MiningStructure> не имеет конкретного смысла [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Примечание: Записи не может быть присвоено **разрешено** чтения также равным **разрешено**|  
|Administer<br /><br /> Примечание: Только в разрешениях базы данных|{**true**, **false**}<br /><br /> Default=**false**|Указывает, могут ли члены выполнять административные функции по отношению к базе данных.<br /><br /> Значение**true** предоставляет членам роли разрешение для доступа ко всем объектам в базе данных.<br /><br /> Член роли может иметь разрешение на администрирование применительно к какой-то конкретной базе данных, но не к другим.|  
  
## <a name="see-also"></a>См. также:  
 [Разрешения и права доступа &#40; Analysis Services — многомерные данные &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Авторизацию доступа к объектам и операции &#40; Службы Analysis Services &#41;](../../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
  