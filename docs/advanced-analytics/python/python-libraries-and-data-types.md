---
title: "Библиотеки Python | Документы Microsoft"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ec0e006a71bb8634b77b83551c9ad82bdb41b246
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="python-libraries-and-data-types"></a>Библиотеки Python и типы данных

В этом разделе описываются библиотеки Python, которые входят в состав следующих продуктов:

+ Изучение служб (в базе данных) машины SQL Server
+ Microsoft машинного обучения Server (изолированный)

В этом разделе также перечислены неподдерживаемые типы данных и списки тип данных преобразования, которые может выполнять неявно при передаче данных между Python и SQL Server.

## <a name="python-version"></a>Версия Python

2017 г CTP-версия SQL Server 2.0 включает часть дистрибутив Anaconda и Python 3.6.

Часть возможностей RevoScaleR (rxLinMod rxLogit, rxPredict, rxDTrees, rxBTrees, может быть несколько других) с помощью API-Интерфейсы Python, с помощью нового пакета Python **RevoScalePy**. Для работы с данными, с помощью Pandas кадров данных, можно использовать эти пакеты. XDF-файлов или запросов анализа данных SQL.

Дополнительные сведения см. в разделе [возможности revoscalepy?](what-is-revoscalepy.md).

## <a name="python-and-sql-data-types"></a>Python и типы данных SQL

Python поддерживает ограниченное число типов данных по сравнению с SQL Server.

В результате при использовании данных из [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в скриптах Python, данные могут неявно преобразовываться в совместимый тип данных. Тем не менее часто точное преобразование не может выполняться автоматически, и возвращается сообщение об ошибке.

В этой таблице перечислены неявные преобразования, которые предоставляются. Другие типы данных не поддерживаются.

|SQLtype|Тип Python|
|-|-|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|



