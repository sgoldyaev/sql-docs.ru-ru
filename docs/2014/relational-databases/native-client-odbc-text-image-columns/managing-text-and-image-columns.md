---
title: Управление столбцами Text и Image | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a161b009239db3c17acb64f8d8eeaaa61321cd9f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052047"
---
# <a name="managing-text-and-image-columns"></a>Управление столбцами text и image
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **текст**, **ntext**, и **изображение** данных (также называется данные большой длины), символ или типы двоичных строк данных, которые могут содержать значения данных слишком велик для обработки в **char**, **varchar**, **двоичных**, или **varbinary** столбцов. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Текст** тип данных сопоставляется с типом данных ODBC SQL_LONGVARCHAR; **ntext** с типом SQL_WLONGVARCHAR; а **изображение** с типом SQL_LONGVARBINARY. Некоторые объекты данных (например, длинные документы или большие битовые карты) слишком велики для их размещения в памяти. Для получения данных большой длины из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] последовательными частями [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] драйвер ODBC для собственного клиента позволяет приложению вызывать [SQLGetData](../native-client-odbc-api/sqlgetdata.md). Для отправления объемных данных частям, приложение может вызвать [SQLPutData](../native-client-odbc-api/sqlputdata.md). Параметры, для которых данные посылаются во время выполнения, называются параметрами c данными времени выполнения.  
  
 Приложение может фактически записи или получения любого типа данных (не только большой) с **SQLPutData** или **SQLGetData**, хотя только **символ** и  **двоичный** данных можно посылать и отправлять по частям. Тем не менее, если данные помещаются в один буфер, нет смысла использовать **SQLPutData** или **SQLGetData**. Гораздо проще привязать единичный буфер к параметру или столбцу.  
  
## <a name="in-this-section"></a>в этом разделе  
  
-   [Привязанные и непривязанные столбцы text и image](bound-vs-unbound-text-and-image-columns.md)  
  
-   [Изменения с ведением журнала и без ведения журнала](logged-vs-unlogged-modifications.md)  
  
-   [Данные времени выполнения и столбцы text, ntext или image](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>См. также  
 [SQL Server Native Client (ODBC)](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
