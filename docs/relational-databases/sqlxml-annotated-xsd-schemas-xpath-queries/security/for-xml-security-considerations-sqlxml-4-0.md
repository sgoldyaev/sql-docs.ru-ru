---
title: "Вопросы безопасности FOR XML (SQLXML 4.0) | Документы Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 532c84e44afde1b01f780024e248ee69c93f6074
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>Вопросы безопасности FOR XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Режим FOR XML AUTO создает иерархию XML, в которой имена элементов сопоставляются имена таблиц и имена сопоставление атрибута к именам столбцов. Он предоставляет сведения о таблицах и столбцах базы данных. При использовании режима AUTO (форматирование на стороне сервера) сведения о базе данных можно скрыть, указав в запросе псевдонимы таблиц и столбцов. Эти псевдонимы возвращаются в результирующем XML-документе в виде имен элементов и атрибутов.  
  
 Например, следующий запрос указывает режим AUTO. Таким образом, на сервере выполняется форматирование XML-кода.  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 В результирующем XML-документе псевдонимы используются для имен элементов и атрибутов:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 При использовании режима NESTED (форматирование на стороне клиента) псевдонимы возвращаются только для атрибутов в результирующем XML-документе. Имена базовых таблиц всегда возвращаются в виде имен элементов. Например, следующий запрос указывает режим NESTED.  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 В результирующем XML-документе имена базовых таблиц, возвращаемые в виде имен элементов и псевдонимов таблиц, не используются:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  