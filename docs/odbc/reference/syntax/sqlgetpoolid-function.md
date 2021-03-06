---
title: Функция SQLGetPoolID | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39b3d3d1ecdc21acee8b238f56cede0a59146bd2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740062"
---
# <a name="sqlgetpoolid-function"></a>Функция SQLGetPoolID
**Соответствие стандартам**  
 Версия была введена: ODBC 3,81 соответствие стандартам: ODBC  
  
 **Сводка**  
 **SQLGetPoolID** извлекает идентификатор пула.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>Аргументы  
 *hDbcInfoToken*  
 [Вход] Дескриптор токена, содержащий все сведения о соединении.  
  
 *pPoolID*  
 [Выход] Идентификатор пула, который используется для идентификации набора соединений, которые могут использоваться как взаимозаменяемые (возможно, требуется дополнительный сброса).  
  
## <a name="returns"></a>Возвращает  
 Значение SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, значение SQL_ERROR или SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Диагностика  
 Когда **SQLGetPoolID** возвращает значение SQL_ERROR или SQL_SUCCESS_WITH_INFO, диспетчер драйверов будут использовать **HandleType** из SQL_HANDLE_DBC_INFO_TOKEN и **обрабатывать** из *hDbcInfoToken*.  
  
## <a name="remarks"></a>Примечания  
 **SQLGetPoolID** позволяет получить идентификатор пула, исходя из набора сведений о соединении (из **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**, и  **SQLSetConnectInfo**). Этот пул, идентификатор используется для идентификации набора подключений, которые могут использоваться как взаимозаменяемые (возможно, требуется дополнительный сброса). Идентификатор пула будет использоваться для идентификации пула подключений для этой группы подключений.  
  
 Каждый раз, когда драйвер возвращает значение SQL_ERROR или SQL_INVALID_HANDLE, диспетчер драйверов возвращает ошибку в приложение (в [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) или [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Каждый раз, когда драйвер возвращает значение SQL_SUCCESS_WITH_INFO, диспетчер драйверов будет получить диагностическую информацию от *hDbcInfoToken*и возвращают значение SQL_SUCCESS_WITH_INFO для приложения в [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)и [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Приложения не эту функцию следует вызывать напрямую. Драйвер ODBC, который поддерживает пулы соединений с учетом драйвера необходимо реализовать эту функцию.  
  
 Включить sqlspi.h для разработки драйвера ODBC.  
  
## <a name="see-also"></a>См. также  
 [Разработка драйвера ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Организация пулов соединений с учетом драйвера](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Разработка драйвера ODBC с поддержкой пула подключений](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
