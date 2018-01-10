---
title: "SQLParamData | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 93ee1e1bd50cbbf34933cdd085fb51a608dd6080
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  При возврате SQLParamData *ValuePtrPtr* , связанный с табличное значение параметра, приложение должно вызывать SQLPutData с *StrLen_Or_Ind*. Если *StrLen_Or_Ind* имеет значение больше 0, это означает, что приложение будет готово для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] собственного клиента для сбора данных параметров для следующей строки возвращающих табличные значения параметра. Если *StrLen_Or_Ind* имеет значение 0, значит отсутствуют дополнительные строки данных для возвращающих табличные значения параметра. Дополнительные сведения см. в разделе [привязки и Data Transfer of Table-Valued параметры и значения столбцов](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Дополнительные сведения о возвращающих табличные значения параметров см. в разделе [табличное значение параметры &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>См. также:  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [Подробные сведения о реализации API-интерфейсов ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  