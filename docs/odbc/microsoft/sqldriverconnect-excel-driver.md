---
title: SQLDriverConnect (драйвер для Excel) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2d7e879c35e7cbf2f2b261d94eff22936f7880b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775352"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (драйвер для Excel)
> [!NOTE]  
>  В этом разделе сведения конкретного драйвера Excel. Общие сведения об этой функции см. в соответствующем разделе [Справочник по API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** позволяет подключиться к драйверу без создания источника данных (DSN).  
  
 В строке подключения для всех драйверов поддерживаются следующие ключевые слова: **DSN**, **DBQ**, и **FIL**.  
  
 В следующей таблице показаны минимальные необходимые для подключения к драйверу ключевые слова и пример пар "ключевое слово значение", используемый с **SQLDriverConnect**. Полный список значений DRIVERID, см. в разделе [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Если DBQ или его значения не указан для Microsoft Excel 3.0 или 4.0 драйвера, драйвер будет использоваться текущий каталог.  
  
|Драйвер|Необходимые ключевые слова|Примеры|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 или 4.0|Драйвер, DriverID|Driver = {драйвер Microsoft Excel (*.xls)}; DBQ = c:\temp; DriverID = 278|  
|Microsoft Excel 5.0/7.0|Драйвер, DriverID, DBQ|Driver = {драйвер Microsoft Excel (*.xls)}; DBQ=c:\temp\sample.xls; DriverID = 22|  
|Microsoft Excel 97 и более поздние версии|Драйвер, DriverID, DBQ|Driver = {драйвер Microsoft Excel (*.xls)}; DBQ=c:\temp\sample.xls; DriverID = 790|
