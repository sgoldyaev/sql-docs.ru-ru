---
title: Элементы SQLServerParameterMetaData | Документы Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f9ebb203-2013-4feb-94f5-494b7f098f9a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ce99e161c3b825c88c4eee33fa6778b5444db07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverparametermetadata-members"></a>Элементы SQLServerParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  В следующих таблицах перечислены члены, предоставляемые [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) класса.  
  
## <a name="constructors"></a>Конструкторы  
 Нет.  
  
## <a name="fields"></a>Поля  
 Нет.  
  
## <a name="inherited-fields"></a>Наследуемые поля  
  
|Название|Описание|  
|----------|-----------------|  
|java.sql.ParameterMetaData|parameterModeIn, parameterModeInOut, parameterModeOut, parameterModeUnknown, parameterNoNulls, parameterNullable, parameterNullableUnknown|  
  
## <a name="methods"></a>Методы  
  
|Название|Описание|  
|----------|-----------------|  
|[getParameterClassName](../../../connect/jdbc/reference/getparameterclassname-method-sqlserverparametermetadata.md)|Получает полное имя класса Java, экземпляры которого должны быть переданы в [setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) метод [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) класса.|  
|[getParameterCount](../../../connect/jdbc/reference/getparametercount-method-sqlserverparametermetadata.md)|Возвращает число параметров в [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) объекта, для которого данный [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) объект содержит сведения.|  
|[getParameterMode](../../../connect/jdbc/reference/getparametermode-method-sqlserverparametermetadata.md)|Возвращает режим указанного параметра.|  
|[getParameterType](../../../connect/jdbc/reference/getparametertype-method-sqlserverparametermetadata.md)|Возвращает тип SQL указанного параметра.|  
|[getParameterTypeName](../../../connect/jdbc/reference/getparametertypename-method-sqlserverparametermetadata.md)|Возвращает имя определяемого базой данных типа для указанного параметра.|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverparametermetadata.md)|Возвращает число десятичных разрядов для указанного параметра.|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverparametermetadata.md)|Возвращает число цифр справа от десятичной запятой для указанного параметра.|  
|[IsNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverparametermetadata.md)|Возвращает значение, определяющее, допустимы ли значения NULL для указанного параметра.|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverparametermetadata.md)|Возвращает значение, определяющее, могут ли быть значения указанного параметра числами со знаком.|  
  
## <a name="inherited-methods"></a>Наследуемые методы  
  
|Класс, из которого наследуется:|Методы|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>См. также  
 [Класс SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
