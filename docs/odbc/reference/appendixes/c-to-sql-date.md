---
title: "C в SQL: дата | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e5806fe1dcdbabbc27e25c0387f2d06ea25f64ee
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-date"></a>C в SQL: дата
Идентификатор для типа данных ODBC C дата является:  
  
 SQL_C_TYPE_DATE  
  
 Следующая таблица показывает ODBC SQL типы данных, к которым может быть преобразован даты данных C. Объяснение столбцы и условия в таблице см. в разделе [преобразование данных из C в типы данных SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Идентификатор типа SQL|Тест|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Длина столбца в байтах > = 10<br /><br /> Столбец байтов длина < 10<br /><br /> Значение данных не является допустимой датой|н/д<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Длина столбца символ > = 10<br /><br /> Длина < 10 символов столбца<br /><br /> Значение данных не является допустимой датой|н/д<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Значение данных представляет собой допустимую дату<br /><br /> Значение данных не является допустимой датой|н/д<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Значение данных представляет собой допустимую дату []<br /><br /> Значение данных не является допустимой датой|н/д<br /><br /> 22007|  
  
 [] части метку времени, установленным равным нулю.  
  
 Сведения о какие значения являются допустимыми в структуре SQL_C_TYPE_DATE см. в разделе [типы данных C](../../../odbc/reference/appendixes/c-data-types.md)ранее в этом приложении.  
  
 После даты C данные преобразуются в символьные данные SQL, результирующий символьных данных находится в «*гггг*-*мм*-*дд*» формата.  
  
 Драйвер не учитывает значение длины/индикатора при преобразовании данных из типа данных date C и предполагает, что размер типа данных date C размер буфера данных. Переданное значение длины/индикатора *StrLen_or_Ind* аргумент в **SQLPutData** и в указанный буфер с *StrLen_or_IndPtr* аргумент в **SQLBindParameter**. Буфер данных задается с помощью *DataPtr* аргумент в **SQLPutData** и *ParameterValuePtr* аргумент в **SQLBindParameter**.