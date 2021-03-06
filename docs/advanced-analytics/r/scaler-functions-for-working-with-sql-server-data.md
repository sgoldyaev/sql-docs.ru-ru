---
title: Функции RevoScaleR для работы с данными SQL Server | Документы Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d97a75cdc7da6a05847373b259ef562353d578ca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203496"
---
# <a name="revoscaler-functions-for-working-with-sql-server-data"></a>Функции RevoScaleR для работы с данными SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Здесь представлен обзор основных функций, предоставляемых в RevoScaleR для работы с данными SQL Server.

Полный список функций ScaleR и способ их использования см. в разделе [Microsoft R Server](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) ссылки.

## <a name="create-sql-server-data-sources"></a>Создание источников данных SQL Server

Здесь приведены функции, которые позволяют определить [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Объект источника данных представляет собой контейнер, который указывает строку подключения с необходимым набором данных и определяется как таблица, представление или запрос. Вызовы хранимых процедур не поддерживаются.

+ [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) -определение [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] объекта источника данных.

+ [RxOdbcData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxodbcdata) -создать объекты данных для других баз данных ODBC. 

## <a name="perform-ddl-statements"></a>Выполнение инструкции DDL

Из R, может выполнять инструкции DDL, если у вас есть необходимые разрешения для экземпляра и базы данных. Следующие функции использовать вызовы ODBC на выполнение инструкций DDL или получить схему базы данных.

+ `rxSqlServerTableExists` и [rxSqlServerDropTable](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdroptable) -удалить [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] таблицу или проверить существование таблицы базы данных или объекта

+ [rxExecuteSQLDDL](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexecutesqlddl) -выполнения команды языка определения данных (DDL), определяет или обрабатывает объекты базы данных. Эта функция не может возвращать данные и используется только для извлечения или изменения схемы объекта или метаданных.

## <a name="define-or-manage-compute-contexts"></a>Определять или управлять контекстов вычислений

Здесь приведены функции, которые позволяют определять новый или текущий контекст вычислений, а также выполнять их переключение.

+ [RxComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxcomputecontext) — создает контекст вычислений.

+ [rxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) — создает контекст вычислений SQL Server, который позволяет функциям **ScaleR** выполняться в службах R SQL Server. Этот контекст вычислений в настоящее время поддерживается только для экземпляров SQL Server под управлением Windows.

+ `rxGetComputeContext` и [rxSetComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetcomputecontext) — получить или задать активный контекст.

## <a name="move-data-and-transform-data"></a>Перемещение данных и преобразования данных

После создания объекта источника данных, можно использовать объект загрузка данных, преобразовывать данные или записать новые данные в указанное назначение. В зависимости от размера данных в источнике вы также можете определить размер пакета как часть источника данных и переместить данные фрагментами.

+ [методы rxOpen](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxopen-methods) — проверьте, является ли источник данных доступен, откройте или закрыть источника данных, чтение данных из источника, записи данных в целевой объект и закрыть источника данных

+ [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) -перемещения данных из источника данных в хранилище файлов или кадров данных.

+ [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) -преобразования данных во время перемещения между источниками данных.

Следующие функции могут использоваться для создания локальное хранилище данных в формате XDF. Этот файл может оказаться полезным при работе с объемом данных, превышающим объем передаваемых данных из базы данных в одном пакете, или же превышающим допустимый объем данных в памяти.

Например если вы регулярно перемещали больших объемов данных из базы данных в локальной рабочей станции, вместо того чтобы запрос базы данных несколько раз для каждой операции R может служить XDF-файла вида кэша сохранить данные локально и затем работать с ними в рабочую область R.

+ [RxXdfData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxxdfdata) -создать объект данных XDF.

+ [rxReadXdf](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxreadxdf) -считывает данные из XDF-файла в кадре данных.

Дополнительные сведения о работе с этими функциями, включая использование данных источников, отличные от [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], в разделе [Howto служит для анализа данных в Microsoft R](https://docs.microsoft.com/r-server/r/how-to-introduction).
