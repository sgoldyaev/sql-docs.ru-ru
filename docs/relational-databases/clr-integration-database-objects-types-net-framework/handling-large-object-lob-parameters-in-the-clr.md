---
title: "Обработка параметров больших объектов (LOB) в среде CLR | Документы Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2fa2bb9022d5bc53ecf8424211b1a9bb6a8fe00
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Обработка параметров больших объектов в среде CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Используйте **SqlBytes** и **SqlChars** для передачи больших объектов (LOB) двоичного типа (**varbinary(max)**) и символьного типа (**nvarchar(max)**) параметров, соответственно. Эти типы позволяют передавать значения LOB в потоке из базы данных в процедуры среды CLR, не копируя все значение в управляемое пространство. **SqlBinary** и **SqlString** следует использовать только для небольших двоичных и строковых значений.  
  
## <a name="see-also"></a>См. также:  
 [Типы данных SQL Server в платформе .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  