---
title: "Подготовка и выполнение инструкции (ODBC) | Документы Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- statement execution
- statement preparation
ms.assetid: 0adecc63-4da5-486c-bc48-09a004a2fae6
caps.latest.revision: "21"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea42cfdc65bec4580a08856b349e4f11437f60c2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="prepare-and-execute-a-statement-odbc"></a>Подготовка и выполнение инструкцию (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-prepare-a-statement-once-and-then-execute-it-multiple-times"></a>Однократная подготовка инструкции и многократное ее выполнение  
  
1.  Вызовите функцию [SQLPrepare](http://go.microsoft.com/fwlink/?LinkId=59360) , чтобы подготовить инструкцию.  
  
2.  Можно также вызвать метод [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) , чтобы определить количество параметров в подготовленной инструкции.  
  
3.  Выполните следующие действия для каждого параметра подготовленной инструкции (не обязательно).  
  
    -   Вызовите [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) для получения сведений о параметре.  
  
    -   Привяжите каждый параметр к переменной программы с помощью [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md). Присвойте значения всем параметрам времени выполнения.  
  
4.  Перед каждым выполнением подготовленной инструкции.  
  
    -   Если в инструкции имеются маркеры параметров, поместите значения данных в буфер связанного параметра.  
  
    -   Вызовите функцию [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) , чтобы выполнить подготовленную инструкцию.  
  
    -   При использовании входных параметров времени выполнения функция [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) возвращает SQL_NEED_DATA. Данные передаются фрагментами при помощи методов [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=58405) и [SQLPutData](../../../relational-databases/native-client-odbc-api/sqlputdata.md).  
  
### <a name="to-prepare-a-statement-with-column-wise-parameter-binding"></a>Подготовка инструкции с привязкой параметра на уровне столбца  
  
1.  Вызовите функцию [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) , чтобы задать следующие атрибуты.  
  
    -   Атрибуту SQL_ATTR_PARAMSET_SIZE задайте число наборов параметров (S).  
  
    -   Атрибуту SQL_ATTR_PARAM_BIND_TYPE задайте значение SQL_PARAMETER_BIND_BY_COLUMN.  
  
    -   Атрибут SQL_ATTR_PARAMS_PROCESSED_PTR должен указывать на переменную SQLUINTEGER, в которую помещается число обработанных параметров.  
  
    -   Задайте значение SQL_ATTR_PARAMS_STATUS_PTR, которое указывает на массив [S] переменных SQLUSSMALLINT, предназначенный для сохранения признаков состояния параметра.  
  
2.  Вызов SQLPrepare, чтобы подготовить инструкцию.  
  
3.  Можно также вызвать метод [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) , чтобы определить количество параметров в подготовленной инструкции.  
  
4.  При необходимости для каждого параметра подготовленной инструкции вызовите функцию SQLDescribeParam, чтобы получить сведения о параметрах.  
  
5.  Для каждого маркера параметра выполните следующее.  
  
    -   Выделите массив из S буферов параметра для сохранения значений данных.  
  
    -   Выделите массив из S буферов параметра для сохранения длин данных.  
  
    -   Вызов SQLBindParameter для привязки параметра значение и массивы длин данных с параметром инструкции.  
  
    -   Если параметр использует данные времени выполнения типов text или image, присвойте ему значение.  
  
    -   Если используются параметры с данными времени выполнения, присвойте им значения.  
  
6.  Перед каждым выполнением подготовленной инструкции.  
  
    -   Поместите значения и длины S-данных в массивы связанных параметров.  
  
    -   Вызовите SQLExecute, чтобы выполнить подготовленную инструкцию.  
  
    -   Если используются входные параметры данных времени выполнения, SQLExecute возвращает SQL_NEED_DATA. Отправляет данные в виде фрагментов с помощью методов SQLParamData и SQLPutData.  
  
### <a name="to-prepare-a-statement-with-row-wise-bound-parameters"></a>Подготовка инструкции с привязкой параметра на уровне строки  
  
1.  Выделите массив структур [S], где S — число наборов параметров. Структура имеет по одному элементу для каждого параметра, а каждый элемент состоит из двух частей.  
  
    -   Первая часть — переменная соответствующего типа данных, в которую помещаются данные параметра.  
  
    -   Вторая часть — переменная SQLINTEGER, в которую помещается признак состояния.  
  
2.  Вызовите функцию [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) , чтобы задать следующие атрибуты.  
  
    -   Атрибуту SQL_ATTR_PARAMSET_SIZE задайте число наборов параметров (S).  
  
    -   Атрибуту SQL_ATTR_PARAM_BIND_TYPE задайте размер структуры, выделенной в шаге 1.  
  
    -   Атрибут SQL_ATTR_PARAMS_PROCESSED_PTR должен указывать на переменную SQLUINTEGER, в которую помещается число обработанных параметров.  
  
    -   Задайте значение SQL_ATTR_PARAMS_STATUS_PTR, которое указывает на массив [S] переменных SQLUSSMALLINT, предназначенный для сохранения признаков состояния параметра.  
  
3.  Вызов SQLPrepare, чтобы подготовить инструкцию.  
  
4.  Для каждого маркера параметра вызовите SQLBindParameter для указания параметра значение и указатель на длину данных с соответствующими им переменными в первом элементе массива структур, выделенных на шаге 1. Если параметр использует данные времени выполнения, присвойте ему значение.  
  
5.  Перед каждым выполнением подготовленной инструкции.  
  
    -   Заполните массив буфера привязанного параметра значениями данных.  
  
    -   Вызовите SQLExecute, чтобы выполнить подготовленную инструкцию. Драйвер эффективно выполнит инструкцию SQL S раз, по одному разу для каждого набора параметров.  
  
    -   Если используются входные параметры данных времени выполнения, SQLExecute возвращает SQL_NEED_DATA. Отправляет данные в виде фрагментов с помощью методов SQLParamData и SQLPutData.  
  
## <a name="see-also"></a>См. также:  
 [Выполнение инструкции запросов &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  