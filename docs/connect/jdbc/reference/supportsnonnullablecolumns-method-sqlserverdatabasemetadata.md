---
title: Метод supportsNonNullableColumns (SQLServerDatabaseMetaData) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsNonNullableColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c32ea64-460e-4636-8a3b-07c8abeed687
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb7686346f89439faf658371efc7dbbdb7fd52f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689922"
---
# <a name="supportsnonnullablecolumns-method-sqlserverdatabasemetadata"></a>Метод supportsNonNullableColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Возвращает значение, определяющее, могут ли столбцы в этой базе данных быть определены как не допускающие значения NULL.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public boolean supportsNonNullableColumns()  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 **значение true,** Если поддерживается. В противном случае — **false**.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Этот метод supportsNonNullableColumns указывается с помощью метода supportsNonNullableColumns в интерфейсе java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>См. также:  
 [Методы SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Элементы SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Класс SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
