---
title: Импорт из реляционного источника данных (табличные службы SSAS) | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44c4f0a5fbdaa64f2145113bf5135dad9acbddbb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167514"
---
# <a name="import-from-a-relational-data-source-ssas-tabular"></a>Импорт из реляционного источника данных (табличные службы SSAS)
  С помощью мастера импорта таблиц можно импортировать данные из разных реляционных баз данных: Этот мастер доступен в меню **Модель** [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Для соединения с источником данных на компьютере должен быть установлен соответствующий поставщик. Дополнительные сведения о поддерживаемых источниках данных и поставщиках см. в разделе [Data Sources Supported &#40;SSAS Tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
 Мастер импорта таблиц поддерживает импорт данных из следующих источников данных:  
  
 **Реляционные базы данных**  
  
-   База данных Microsoft SQL Server  
  
-   Microsoft SQL Azure  
  
-   База данных Microsoft Access  
  
-   Параллельные хранилища данных Microsoft SQL Server  
  
-   Oracle;  
  
-   Teradata  
  
-   Sybase  
  
-   Informix  
  
-   IBM DB2  
  
-   OLE DB/ODBC  
  
 **Многомерные источники**  
  
-   Куб служб Microsoft SQL Server Analysis Services  
  
 Мастер импорта таблиц не поддерживает импорт данных из книги [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] в качестве источника данных.  
  
### <a name="to-import-data-from-a-database"></a>Импорт данных из базы данных  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]выберите пункт **Импорт из источника данных** в меню **Модель**.  
  
2.  На странице **Подключение к источнику данных** выберите тип базы данных для подключения и нажмите кнопку **Далее**.  
  
3.  Выполните шаги мастера импорта таблиц. На последующих страницах можно будет выбрать отдельные таблицы и представления или применить фильтры на странице **Выбор таблиц и представлений** или с помощью создания SQL-запроса на странице **Указание SQL-запроса** .  
  
## <a name="see-also"></a>См. также  
 [Импорт данных &#40;табличные службы SSAS&#41;](import-data-ssas-tabular.md)   
 [Поддерживаемые источники данных &#40;табличные службы SSAS&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
