---
title: Метод getSearchStringEscape (SQLServerDatabaseMetaData) | Документы Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSearchStringEscape
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea0f95d0-0238-4dc8-9f26-7ff9b65f30c3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0eb3fd98c42615dba674e31ed2007fbcfc22f4ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838109"
---
# <a name="getsearchstringescape-method-sqlserverdatabasemetadata"></a>Метод getSearchStringEscape (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Извлекает **строка** , может использоваться для экранирования символов-шаблонов.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public java.lang.String getSearchStringEscape()  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 Объект **строка** , содержащий шаблон escape-символ строки.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Замечания  
 Этот метод getSearchStringEscape указывается с помощью метода getSearchStringEscape в интерфейсе java.sql.DatabaseMetaData.  
  
 Этот метод используется только для поиска по шаблону в метаданных. Возвращает «\\». Объект **строка** шаблона поиска можно экранировать символы-шаблоны («%» и «_») и предоставить их как литералы, добавляя в начало обратной косой черты. Это означает "\\%» в «[%]» и «\\\_» для» [\_]».  
  
## <a name="see-also"></a>См. также  
 [Методы SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Элементы SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Класс SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
