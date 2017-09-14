---
title: "INSERT (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INSERT_TSQL
- INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- inserting multiple rows
- user-defined types [SQL Server], inserting values
- DML [SQL Server], INSERT statement
- bulk load [SQL Server]
- row additions [SQL Server], INSERT statement
- inserting rows
- table value constructor [SQL Server]
- adding data
- INSERT statement [SQL Server], about INSERT statement
- INSERT statement [SQL Server]
- UDTs [SQL Server], inserting values
- adding rows
- INSERT INTO statement
- data manipulation language [SQL Server], INSERT statement
- inserting data
ms.assetid: 1054c76e-0fd5-4131-8c07-a6c5d024af50
caps.latest.revision: 136
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ef8387c2bbbc109ad7ec325e4faf632a983d96c9
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="insert-transact-sql"></a>Инструкция INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Добавляет одну или несколько строк в таблицу или представление [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Примеры см. в разделе [примеры](#InsertExamples).  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ ( column_list ) ]   
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
  table_or_view_name  
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  
```  
  
```  
-- External tool only syntax  

INSERT   
{  
    [BULK]  
    [ database_name . [ schema_name ] . | schema_name . ]  
    [ table_name | view_name ]  
    ( <column_definition> )  
    [ WITH (  
        [ [ , ] CHECK_CONSTRAINTS ]  
        [ [ , ] FIRE_TRIGGERS ]  
        [ [ , ] KEEP_NULLS ]  
        [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]  
        [ [ , ] ROWS_PER_BATCH = rows_per_batch ]  
        [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]  
        [ [ , ] TABLOCK ]  
    ) ]  
}  
  
[; ] <column_definition> ::=  
 column_name <data_type>  
    [ COLLATE collation_name ]  
    [ NULL | NOT NULL ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

INSERT INTO [ database_name . [ schema_name ] . | schema_name . ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    {   
      VALUES ( { NULL | expression } )  
      | SELECT <select_criteria>  
    }  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
[;]  
```  
  
## <a name="arguments"></a>Аргументы  
 С \<общее_табличное_выражение >  
 Определяет временный именованный результирующий набор, также называемый обобщенным табличным выражением, определенным в области инструкции INSERT. Результирующий набор получается из инструкции SELECT. Дополнительные сведения см. в разделе [с общее_табличное_выражение &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Начало (*выражение*) [%]  
 Задает число или процент вставляемых случайных строк. *expression* может быть либо числом, либо процентом от числа строк. Дополнительные сведения см. в разделе [в начало &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 INTO  
 Необязательное ключевое слово, которое можно использовать между ключевым словом INSERT и целевой таблицей.  
  
 *имя_сервера*  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Имя связанного сервера, на котором расположены таблица или представление. *имя_сервера* может быть указан как [связанного сервера](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) name, или с помощью [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) функции.  
  
 Когда *имя_сервера* указан в качестве связанного сервера, *имя_базы_данных* и *schema_name* являются обязательными. Когда *имя_сервера* , указанном с помощью OPENDATASOURCE, *имя_базы_данных* и *schema_name* могут применяться не ко всем источникам данных, зависит от возможностей OLE DB Поставщик, который обращается к удаленному объекту.  
  
 *database_name*  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Имя базы данных.  
  
 *schema_name*  
 Имя схемы, которой принадлежит таблица или представление.  
  
 *table_or view_name*  
 Имя таблицы или представления, которые принимают данные.  
  
 Объект [таблицы](../../t-sql/data-types/table-transact-sql.md) переменную внутри своей области можно использовать в качестве источника таблицы в инструкции INSERT.  
  
 Представление ссылается *table_or_view_name* должно быть обновляемым и ссылаться ровно одну базовую таблицу в предложении FROM представления. Например, инструкция INSERT в многотабличном представлении должна использовать *column_list* , ссылается только на столбцы из одной базовой таблицы. Дополнительные сведения об обновляемых представлениях см. в разделе [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Либо [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) или [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) функции. Использование этих функций зависит от возможностей поставщика OLE DB, который обращается к удаленному объекту.  
  
 С помощью ( \<table_hint_limited > [... *n* ] )  
 Задает одно или несколько табличных указаний, разрешенных для целевой таблицы. Ключевое слово WITH и круглые скобки обязательны.  
  
 Нельзя использовать подсказки READPAST, NOLOCK, и READUNCOMMITTED. Дополнительные сведения о табличных подсказках см. в разделе [табличные подсказки &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
> [!IMPORTANT]  
>  Возможность указать подсказки HOLDLOCK, SERIALIZABLE, READCOMMITTED, REPEATABLEREAD или UPDLOCK в целевых таблицах инструкций INSERT будет удалена в будущих версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Эти указания не влияют на производительность инструкций INSERT. Избегайте применять их в новых разработках и запланируйте внесение изменений в приложения, использующие их в настоящее время.  
  
 Указание подсказки TABLOCK для целевой таблицы инструкции INSERT приведет к тем же последствиям, что и указание подсказки TABLOCKX. К таблице будет применена монопольная блокировка.  
  
 (*column_list*)  
 Список, состоящий из одного или нескольких столбцов, в которые вставляются данные. *column_list* должен быть заключен в круглые скобки и разделен запятыми.  
  
 Если столбец не находится в *column_list*, [!INCLUDE[ssDE](../../includes/ssde-md.md)] должен быть способен предоставить значение в соответствии с определением столбца; в противном случае строку нельзя будет загрузить. Компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] автоматически задает значение для столбца, если столбец имеет следующие характеристики.  
  
-   Имеется свойство IDENTITY. Используется следующее значение приращения для идентификатора.  
  
-   Имеется стандартное значение. Используется стандартное значение для столбца.  
  
-   Имеет **timestamp** тип данных. В этом случае используется текущее значение отметки времени.  
  
-   Допускает значение NULL. Используется значение NULL.  
  
-   Вычисляемый столбец. Используется вычисленное значение.  
  
*column_list* необходимо использовать, когда в столбец идентификаторов вставляются явно заданные значения, а параметру SET IDENTITY_INSERT необходимо присвоить значение ON для таблицы.  
  
Предложение OUTPUT  
 Возвращает вставленные строки во время операции вставки. Результаты могут возвращаться в обрабатывающее приложение или вставляться в таблицу или табличную переменную для дальнейшей обработки.  
  
 [Предложение OUTPUT](../../t-sql/queries/output-clause-transact-sql.md) не поддерживается в инструкции DML, которые ссылаются на локальные секционированные представления, распределенные секционированные представления и удаленные таблицы или инструкции INSERT, содержащие *execute_statement*. Предложение OUTPUT INTO не поддерживается в инструкциях INSERT, содержащих \<dml_table_source > предложения. 
  
 VALUES  
 Позволяет использовать один или несколько списков вставляемых значений данных. Должно быть одно значение данных для каждого столбца в *column_list*, если указан или в таблице. Список значений должен быть заключен в скобки.  
  
 Если значения в списке значений не находятся в отличном от порядка следования столбцов в таблице или имеют значения для каждого столбца в таблице, *column_list* необходимо использовать для явного указания столбца, в котором хранится каждое входное значение.  
  
 Можно использовать конструктор строк [!INCLUDE[tsql](../../includes/tsql-md.md)] (также называемый конструктором табличных значений), позволяющий указать несколько строк в одной инструкции INSERT. Этот конструктор строк состоит из одного предложения VALUES со списками из нескольких значений, заключенными в круглые скобки и разделенными запятыми. Дополнительные сведения см. в разделе [конструктор табличных значений &#40; Transact-SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 DEFAULT  
 Указывает компоненту [!INCLUDE[ssDE](../../includes/ssde-md.md)] необходимость принудительно загружать значения по умолчанию, определенные для столбца. Если для столбца не задано значение по умолчанию и он может содержать значение NULL, вставляется значение NULL. Для столбца, определенного с **timestamp** тип данных, вставляется следующее значение отметки времени. Значение DEFAULT недопустимо для столбца идентификаторов.  
  
 *expression*  
 Константа, переменная или выражение. Выражение не может содержать инструкцию EXECUTE.  
  
 При ссылке на типы данных символов Юникода **nchar**, **nvarchar**, и **ntext**, "*выражение*" должно начинаться с заглавной буквы 'N'. Если префикс «N» не указан, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполнит преобразование строки в кодовую страницу, соответствующую параметрам сортировки базы данных или столбца, действующим по умолчанию. Любые символы, не входящие в эту кодовую страницу, будут утрачены.  
  
 *derived_table*  
 Любая допустимая инструкция SELECT, возвращающая строки данных, которые загружаются в таблицу. Инструкция SELECT не может содержать обобщенное табличное выражение (CTE).  
  
 *execute_statement*  
 Любая допустимая инструкция EXECUTE, возвращающая данные с помощью инструкций SELECT или READTEXT. Дополнительные сведения см. в разделе [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md).  
  
 Параметры RESULT SETS инструкции EXECUTE нельзя указывать в инструкции INSERT…EXEC.  
  
 Если *execute_statement* используется с инструкцией INSERT, каждый результирующий набор должен быть совместимы со столбцами в таблице или в *column_list*.  
  
 *execute_statement* можно использовать для выполнения хранимых процедур на том же сервере или на удаленном сервере. На удаленном сервере выполняется процедура, результирующий набор возвращается на локальный сервер и загружается в таблицу на локальном сервере. В распределенной транзакции *execute_statement* не может быть выполнена к связанному серверу с замыканием на себя, если при соединении нескольких активных результирующих наборов (MARS) включен.  
  
 Если *execute_statement* возвращает данные с инструкцией READTEXT, каждая инструкция READTEXT может возвращать не более 1 МБ (1024 КБ) данных. *execute_statement* также может использоваться с расширенными процедурами. *execute_statement* вставляет данные, возвращенные основным потоком расширенной процедуры; Однако выходные данные из других потоков не вставляются.  
  
 Возвращающий табличное значение параметр нельзя указывать в качестве объекта инструкции INSERT EXEC, но его можно указать в виде источника в строке INSERT EXEC или в хранимой процедуре. Дополнительные сведения см. в статье [Использование возвращающих табличные значения параметров (компонент Database Engine)](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
 \<dml_table_source >  
 Указывает, что вставленные в целевую таблицу строки были возвращены предложением OUTPUT инструкции INSERT, UPDATE, DELETE или MERGE с возможной фильтрацией предложением WHERE. Если \<dml_table_source > указан, целевой внешняя инструкция INSERT должна удовлетворять следующим ограничениям: 
  
-   Быть базовой таблицей, а не представлением.  
  
-   Не быть удаленной таблицей.  
  
-   Не иметь определенных для нее триггеров.  
  
-   Не участвовать в связях «первичный-внешний ключ».  
  
-   Объект не должен участвовать в репликации слиянием или обновляемых подписках для репликации транзакций.  
  
 Уровень совместимости базы данных должен быть не ниже 100. Дополнительные сведения см. в разделе [предложение OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 \<select_list >  
 Список с разделителями-запятыми, указывающий, какие столбцы возвращены предложением OUTPUT для вставки. Столбцы в \<select_list > должны быть совместимы со столбцами, в которые вставляются значения. \<select_list > не может ссылаться на агрегатные функции или TEXTPTR. 
  
> [!NOTE]  
>  Все переменные, перечисленные в списке ВЫБОРА обратитесь к исходным значениям, независимо от того, любые изменения, внесенные в них в \<dml_statement_with_output_clause >.  
  
 \<dml_statement_with_output_clause >  
 Допустимая инструкция INSERT, UPDATE, DELETE или MERGE, возвращающая изменяемые строки в предложении OUTPUT. Инструкция не может содержать предложение WITH и использовать удаленные таблицы или секционированные представления в качестве целевых. Если указаны UPDATE или DELETE, это не могут быть использующие курсор инструкции UPDATE или DELETE. На исходные строки нельзя ссылаться как на вложенные инструкции DML.  
  
 ГДЕ \<search_condition >  
 Любое предложение WHERE, содержащее допустимое \<search_condition >, фильтры строк, возвращенных \<dml_statement_with_output_clause >. Дополнительные сведения см. в разделе [условие поиска &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md). При использовании в этом контексте \<search_condition > не может содержать вложенные запросы, скалярные определяемые пользователем функции, которые выполняют доступ к данным, агрегатных функций, TEXTPTR или предикатов полнотекстового поиска. 
  
 DEFAULT VALUES  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Заполняет новую строку значениями по умолчанию, определенными для каждого столбца.  
  
 BULK  
**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Используется внешними средствами для передачи потока двоичных данных. Этот параметр не предназначен для использования средств, таких как [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], SQLCMD, OSQL или данных таких как доступ к API-интерфейсов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 FIRE_TRIGGERS  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Указывает, что при передаче потока двоичных данных будут выполняться триггеры INSERT, определенные для целевой таблицы. Дополнительные сведения см. в разделе [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 CHECK_CONSTRAINTS  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Указывает, что при передаче потока двоичных данных будет выполняться проверка всех ограничений целевой таблицы или представления. Дополнительные сведения см. в разделе [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 KEEPNULLS  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Указывает, что пустые столбцы во время передачи потока двоичных данных должны сохранить значение NULL. Дополнительные сведения см. в разделе [Сохранение значений NULL или использование значений по умолчанию при массовом импорте данных (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 KILOBYTES_PER_BATCH = kilobytes_per_batch  
 Указывает приблизительное число килобайт (КБ) данных в пакете как *kilobytes_per_batch*. Дополнительные сведения см. в разделе [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 **Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Указывает приблизительное число строк в потоке двоичных данных. Дополнительные сведения см. в разделе [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
>  [!NOTE]
>  Синтаксическая ошибка возникает в том случае, если не указан список столбцов.  

## <a name="remarks"></a>Замечания  
Сведения о вставке данных в таблицы SQL graph см. в разделе [вставки (SQL граф)](../../t-sql/statements/insert-sql-graph.md). 

## <a name="best-practices"></a>Рекомендации  
 Используйте @@ROWCOUNT функция возвращает количество вставленных строк клиентскому приложению. Дополнительные сведения см. в разделе [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).  
  
### <a name="best-practices-for-bulk-importing-data"></a>Рекомендации по массовому импорту данных  
  
#### <a name="using-insert-intoselect-to-bulk-import-data-with-minimal-logging"></a>Использование инструкции INSERT INTO…SELECT для массового импорта данных с минимальным протоколированием  
 Можно использовать `INSERT INTO <target_table> SELECT <columns> FROM <source_table>` может эффективно перенести большое количество строк из одной таблицы, например промежуточной таблицы в другую таблицу с минимальным протоколированием. Минимальное протоколирование может повысить производительность выполнения инструкции и снизить вероятность того, что во время операции будет заполнен весь журнал транзакций.  
  
 Для минимального протоколирования этой инструкции необходимо выполнение следующих требований.  
  
-   Модель восстановления базы данных настроена на простое или неполное протоколирование.  
  
-   Целевой таблицей является пустая или непустая куча.  
  
-   Целевая таблица не используется в репликации.  
  
-   Для целевой таблицы указана подсказка TABLOCK.  
  
Для строк, которые вставляются в кучу в результате действия вставки в инструкции MERGE, также может применяться минимальное протоколирование.  
  
 В отличие от инструкции BULK INSERT, которая удерживает менее строгую блокировку массового обновления, инструкция INSERT INTO…SELECT с указанием TABLOCK удерживает монопольную блокировку (X) таблицы. Это означает, что отсутствует возможность вставки строк с помощью параллельных операций вставки.  
  
#### <a name="using-openrowset-and-bulk-to-bulk-import-data"></a>Использование предложений OPENROWSET и BULK для массового импорта данных  
 Функция OPENROWSET может принимать следующие табличные подсказки, обеспечивающие оптимизацию массовой загрузки с инструкцией INSERT.  
  
-   Использование подсказки TABLOCK может свести к минимуму число записей в журнале для операции вставки. Для базы данных должна быть установлена простая модель восстановления или модель восстановления с неполным протоколированием. Кроме того, целевая таблица не может использоваться в репликации. Дополнительные сведения см. в разделе [необходимые условия для минимального протоколирования массового импорта](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
-   Проверку ограничений FOREIGN KEY и CHECK можно временно отключить с помощью подсказки IGNORE_CONSTRAINTS.  
  
-   Выполнение триггеров можно временно отключить с помощью подсказки IGNORE_TRIGGERS.  
  
-   Указание KEEPDEFAULTS позволяет вставлять значение по умолчанию столбец таблицы, если таковая имеется, вместо значения NULL при записи данных отсутствует значение для столбца.  
  
-   Подсказка KEEPIDENTITY позволяет использовать значения идентификаторов в файле импортированных данных для столбца идентификаторов в целевой таблице.  
  
Эти оптимизации похожи на оптимизации, доступные для команды BULK INSERT. Дополнительные сведения см. в разделе [Табличные указания (Transact-SQL)](../../t-sql/queries/hints-transact-sql-table.md).  
  
## <a name="data-types"></a>Типы данных  
 При вставке строк необходимо учитывать поведение следующих типов данных:  
  
-   Если значение загружается в столбцы с **char**, **varchar**, или **varbinary** тип данных, добавление или усечение конечных пробелов (пробелы для  **char** и **varchar**, нули для **varbinary**) определяется значением параметра SET ANSI_PADDING, определенная для столбца при создании таблицы. Дополнительные сведения см. в разделе [SET ANSI_PADDING (Transact-SQL)](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
     В следующей таблице показаны операции по умолчанию для параметра SET ANSI_PADDING, установленного в значение OFF.  
  
    |Тип данных|Стандартная операция|  
    |---------------|-----------------------|  
    |**char**|Заполнение значения пробелами до заданной ширины столбца.|  
    |**varchar**|Удаление конечных пробелов до последнего непробельного символа или до одного пробела, если строка состоит только из пробелов.|  
    |**varbinary**|Удаление конечных нулей.|  
  
-   Если это пустая строка ("") загружена в столбец с **varchar** или **текст** тип данных операцией по умолчанию будет загрузка строки нулевой длины.  
  
-   Вставка значения null в **текст** или **изображения** столбца не создает действительный текстовый указатель, и предварительному распределению 8-Килобайтной текстовой страницы.  
  
-   В столбцах с **uniqueidentifier** тип хранилища данных специальное форматирование 16-байтовые двоичные значения. В отличие от столбцов идентификаторов [!INCLUDE[ssDE](../../includes/ssde-md.md)] не создает автоматически значения для столбцов с **uniqueidentifier** тип данных. Во время операции вставки переменные с данным типом **uniqueidentifier** и строковые константы в виде *xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx* (36 символов, включая дефисы, где *x* представляет собой шестнадцатеричную цифру в диапазоне 0-9 или a-f) могут использоваться для **uniqueidentifier** столбцов. Например, 6F9619FF-8B86-D011-B42D-00C04FC964FF является допустимым значением для **uniqueidentifier** переменной или столбца. Используйте [NEWID()](../../t-sql/functions/newid-transact-sql.md) функции, чтобы получить глобальный уникальный идентификатор (GUID).  
  
### <a name="inserting-values-into-user-defined-type-columns"></a>Вставка значений в столбцы определяемого пользователем типа  
 Вставлять значения в столбцы определяемого пользователем типа можно следующими способами.  
  
-   Предоставление значения определяемого пользователем типа.  
  
-   Предоставление значения типа системных данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] происходит, если определяемый пользователем тип поддерживает явное или неявное преобразование из этого типа. В следующем примере показано, как вставить значение в столбце определяемого пользователем типа `Point`, путем явного преобразования из строки.  
  
    ```  
    INSERT INTO Cities (Location)  
    VALUES ( CONVERT(Point, '12.3:46.2') );  
    ```  
  
     Двоичное значение также может предоставляться без выполнения явного преобразования, так как все определяемые пользователем типы могут быть неявно преобразованы из двоичного.  
  
-   Вызов определяемой пользователем функции, которая возвращает значение определяемого пользователем типа. В следующих примерах используется определяемая пользователем функция `CreateNewPoint()` для создания новых значений определяемого пользователем типа `Point` и вставки значения в таблицу `Cities`.  
  
    ```  
    INSERT INTO Cities (Location)  
    VALUES ( dbo.CreateNewPoint(x, y) );  
    ```  
  
## <a name="error-handling"></a>Обработка ошибок  
 Для инструкции INSERT можно реализовать обработку ошибок, указав инструкцию в конструкции TRY…CATCH.  
  
 Если инструкция INSERT нарушает ограничение или правило, либо в ней присутствует значение, несовместимое с типом данных столбца, то при выполнении инструкции происходит сбой и отображается сообщение об ошибке.  
  
 Если инструкция INSERT загружает несколько строк с помощью инструкции SELECT или EXECUTE, то любые нарушения правил или ограничений, возникающие из-за загружаемых значений, приводят к остановке выполнения инструкции, и ни одна из строк не будет загружена.  
  
 Если при выполнении инструкции INSERT возникает арифметическая ошибка (переполнение, деление на ноль или ошибка домена), компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] обрабатывает эти ошибки так же, как если бы параметру SET ARITHABORT было присвоено значение ON. Выполнение пакета прекращается и выводится сообщение об ошибке. Во время оценки выражения, когда параметры SET ARITHABORT и SET ANSI_WARNINGS установлены в значение OFF, если в инструкции INSERT, DELETE или UPDATE происходит арифметическая ошибка переполнения, деления на ноль или ошибка области определения, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вставляет или обновляет значение NULL. Если целевой столбец не пустой, вставка или обновление не осуществляются, и пользователь получает ошибку.  
  
## <a name="interoperability"></a>Совместимость  
 Если триггер INSTEAD OF определен в операциях INSERT для таблицы или представления, то триггер выполняется вместо инструкции INSERT. Дополнительные сведения о триггеры INSTEAD OF см. в разделе [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Ограничения  
 Если во время вставки значений в удаленные таблицы указаны не все значения для всех столбцов, то необходимо указать столбцы, в которые вставляются заданные значения.  
  
 При использовании выражения TOP в инструкции INSERT строки, на которые имеются ссылки, не упорядочиваются, а предложение ORDER BY не может быть прямо указано в этих инструкциях. Если для вставки строк в значимом хронологическом порядке необходимо использовать предложение TOP, вместе с ним в инструкции подзапроса выборки следует использовать предложение ORDER BY. См. подраздел «Примеры» далее в этом разделе.
 
Запросы INSERT, использующие ВЫБЕРИТЕ вместе с ORDER BY для заполнения строк гарантии, как вычисляются значения идентификаторов, но не порядок, в котором строки вставлены.    
  
## <a name="logging-behavior"></a>Режим ведения журнала  
 Инструкция INSERT всегда полностью протоколируются за исключением того, при использовании с ключевым словом BULK функции OPENROWSET или при использовании `INSERT INTO <target_table> SELECT <columns> FROM <source_table>`. Для этих операций возможно минимальное протоколирование. Дополнительные сведения см. в подразделе «Рекомендации по массовой загрузке данных» этого раздела.  
  
## <a name="security"></a>безопасность  
 При соединении со связанным сервером отправляющий сервер указывает имя входа и пароль для подключения к принимающему серверу от его имени. Для работы подключения, необходимо создать сопоставление имен входа между связанными серверами с помощью [sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md).  
  
 При использовании функции OPENROWSET(BULK…) важно понимать, каким образом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] обрабатывает олицетворение. Дополнительные сведения см. в разделе «Вопросы безопасности» в [массовый импорт данных с помощью инструкции BULK INSERT или OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Permissions  
 Требуется разрешение INSERT на целевую таблицу.  
  
 Вставить разрешения по умолчанию предоставляются членам **sysadmin** предопределенной роли сервера **db_owner** и **db_datawriter** фиксированной роли базы данных, а также владельцу таблицы. Члены **sysadmin**, **db_owner**и **db_securityadmin** ролей, а также владелец таблицы могут передавать разрешения другим пользователям.  
  
 Чтобы выполнить инструкцию INSERT с помощью параметра BULK функции OPENROWSET, необходимо быть членом **sysadmin** предопределенной роли сервера или **bulkadmin** предопределенной роли сервера.  
  
##  <a name="InsertExamples"></a> Примеры  
  
|Категория|Используемые элементы синтаксиса|  
|--------------|------------------------------|  
|[Базовый синтаксис](#BasicSyntax)|INSERT • конструктор табличных значений|  
|[Обработка значений столбца](#ColumnValues)|IDENTITY • NEWID • значения по умолчанию • определяемые пользователем типы|  
|[Вставка данных из других таблиц](#OtherTables)|INSERT…SELECT • INSERT…EXECUTE • WITH обобщенное табличное выражение • TOP• OFFSET FETCH|  
|[Указание целевых объектов, отличных от стандартных таблиц](#TargetObjects)|Представления • табличные переменные|  
|[Вставка строк в удаленную таблицу](#RemoteTables)|Связанный сервер • OPENQUERY, функция набора строк • OPENDATASOURCE, функция набора строк|  
|[Массовая загрузка данных из таблиц или файлов данных](#BulkLoad)|INSERT…SELECT • OPENROWSET, функция|  
|[Переопределение поведения по умолчанию оптимизатор запросов с помощью подсказок](#TableHints)|Табличные указания|  
|[Сбор результатов инструкции INSERT](#CaptureResults)|OUTPUT, предложение|  
  
###  <a name="BasicSyntax"></a>Базовый синтаксис  
 В примерах в этом разделе описывается базовая функциональность инструкции INSERT с помощью минимального необходимого синтаксиса.  
  
#### <a name="a-inserting-a-single-row-of-data"></a>A. Вставка одной строки данных  
 В следующем примере показана вставка одной строки в таблицу `Production.UnitMeasure` базы данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. В этой таблице содержатся столбцы `UnitMeasureCode`, `Name` и `ModifiedDate`. Так как значения для всех столбцов предоставлены и перечислены в порядке, соответствующем порядку столбцов таблицы, имена столбцов не указан в списке столбцов*.*  
  
```  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT', N'Feet', '20080414');  
```  
  
#### <a name="b-inserting-multiple-rows-of-data"></a>Б. Вставка нескольких строк данных  
 В следующем примере используется [конструктор табличных значений](../../t-sql/queries/table-value-constructor-transact-sql.md) для вставки трех строк в `Production.UnitMeasure` в таблицу [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] базы данных в одной инструкции INSERT. Так как значения для всех столбцов предоставлены и перечислены в том же порядке, что и столбцы в таблице, то не нужно в параметре указывать имена столбцов.  
  
```  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923')
    , (N'Y3', N'Cubic Yards', '20080923');  
```  
  
#### <a name="c-inserting-data-that-is-not-in-the-same-order-as-the-table-columns"></a>В. Вставка данных в порядке, отличном от порядка столбцов таблицы  
 В следующем примере используется список столбцов для явного указания значений, которые будут вставляться в каждый столбец. Порядок столбцов в `Production.UnitMeasure` в таблицу [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] база данных находится в `UnitMeasureCode`, `Name`, `ModifiedDate`, однако столбцы не указываются в данном порядке в *column_list*.  
  
```  
INSERT INTO Production.UnitMeasure (Name, UnitMeasureCode,  
    ModifiedDate)  
VALUES (N'Square Yards', N'Y2', GETDATE());  
```  
  
###  <a name="ColumnValues"></a>Обработка значений столбца  
 В примерах этого раздела показаны методы вставки значений в столбцы, которые определены со свойством IDENTITY, значение по умолчанию, определенные с типами данных, таких как **uniqueidentifer** или столбцов определяемого пользователем типа.  
  
#### <a name="d-inserting-data-into-a-table-with-columns-that-have-default-values"></a>Г. Вставка данных в таблицу со столбцами, имеющими значение по умолчанию  
 В следующем примере показана вставка строк в таблицу со столбцами, для которых автоматически создается значение или которые имеют значение по умолчанию. `Column_1` — это вычисляемый столбец, который автоматически создает значение, объединяя строку со значением, вставленным в столбец `column_2`. Столбец `Column_2` определен с ограничением по умолчанию. Если для этого столбца не указано значение, используется значение по умолчанию. `Column_3`определено с помощью **rowversion** тип данных, который автоматически формирует уникальное увеличивающееся двоичное число. Столбец `Column_4` не формирует значения автоматически. Если значение для этого столбца отсутствует, то вставляется значение NULL. Инструкция INSERT вставляет строки, которые содержат значения для некоторых столбцов, но не для всех. В последней инструкции INSERT столбцы не указаны, и поэтому вставляются только значения по умолчанию с помощью предложения DEFAULT VALUES.  
  
```  
CREATE TABLE dbo.T1   
(  
    column_1 AS 'Computed column ' + column_2,   
    column_2 varchar(30)   
        CONSTRAINT default_name DEFAULT ('my column default'),  
    column_3 rowversion,  
    column_4 varchar(40) NULL  
);  
GO  
INSERT INTO dbo.T1 (column_4)   
    VALUES ('Explicit value');  
INSERT INTO dbo.T1 (column_2, column_4)   
    VALUES ('Explicit value', 'Explicit value');  
INSERT INTO dbo.T1 (column_2)   
    VALUES ('Explicit value');  
INSERT INTO T1 DEFAULT VALUES;   
GO  
SELECT column_1, column_2, column_3, column_4  
FROM dbo.T1;  
GO  
```  
  
#### <a name="e-inserting-data-into-a-table-with-an-identity-column"></a>Д. Вставка данных в таблицу со столбцом идентификаторов  
 В следующем примере показаны различные методы вставки данных в столбец идентификаторов. Первые две инструкции INSERT позволяют формировать значения идентификаторов для новых строк. Третья инструкция INSERT переопределяет свойство IDENTITY столбца с помощью инструкции SET IDENTITY_INSERT и вставляет явно заданное значение в столбец идентификаторов.  
  
```  
CREATE TABLE dbo.T1 ( column_1 int IDENTITY, column_2 VARCHAR(30));  
GO  
INSERT T1 VALUES ('Row #1');  
INSERT T1 (column_2) VALUES ('Row #2');  
GO  
SET IDENTITY_INSERT T1 ON;  
GO  
INSERT INTO T1 (column_1,column_2)   
    VALUES (-99, 'Explicit identity value');  
GO  
SELECT column_1, column_2  
FROM T1;  
GO  
```  
  
#### <a name="f-inserting-data-into-a-uniqueidentifier-column-by-using-newid"></a>Е. Вставка данных в столбец типа uniqueidentifier с помощью функции NEWID()  
 В следующем примере используется [NEWID](../../t-sql/functions/newid-transact-sql.md)функции (), чтобы получить идентификатор GUID для `column_2`. В отличие от столбцов идентификаторов, [!INCLUDE[ssDE](../../includes/ssde-md.md)] не создает автоматически значения для столбцов с [uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md) типа данных, как показано во второй `INSERT` инструкции.  
  
```  
CREATE TABLE dbo.T1   
(  
    column_1 int IDENTITY,   
    column_2 uniqueidentifier,  
);  
GO  
INSERT INTO dbo.T1 (column_2)   
    VALUES (NEWID());  
INSERT INTO T1 DEFAULT VALUES;   
GO  
SELECT column_1, column_2  
FROM dbo.T1;  
  
```  
  
#### <a name="g-inserting-data-into-user-defined-type-columns"></a>Ж. Вставка данных в столбцы определяемого пользователем типа  
 Следующие инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] вставляют три строки в столбец  `PointValue` таблицы `Points`. В данном столбце используются [определяемого пользователем типа CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) (UDT). Тип данных `Point` состоит из целочисленных значений X и Y, которые представлены как свойства определяемого пользователем типа. Необходимо привести разделяемые запятой значения X и Y к типу `Point` с помощью функции CAST или CONVERT. Первые две инструкции используют функцию CONVERT для преобразования строкового значения `Point` типа, а третья инструкция использует функцию CAST. Дополнительные сведения см. в разделе [управление определяемого пользователем ТИПА данных](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-manipulating-udt-data.md).  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
###  <a name="OtherTables"></a>Вставка данных из других таблиц  
 В примерах этого раздела показаны методы вставки строк из одной таблицы в другую.  
  
#### <a name="h-using-the-select-and-execute-options-to-insert-data-from-other-tables"></a>З. Вставка данных из других таблиц с помощью параметров SELECT и EXECUTE  
 В следующем примере описана вставка данных из одной таблицы в другую с помощью инструкций INSERT…SELECT и INSERT…EXECUTE. Каждый метод основан на многотабличной инструкции SELECT, содержащей выражение и литеральное значение в списке столбцов.  
  
 Первая инструкция INSERT использует инструкцию SELECT для получения данных из исходных таблиц (`Employee`, `SalesPerson`, и `Person`) в [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] базы данных и сохранения результирующего набора `EmployeeSales` таблицы. Вторая инструкция INSERT с помощью предложения EXECUTE вызывает хранимую процедуру, содержащую инструкцию SELECT, а третья инструкция INSERT с помощью предложения EXECUTE ссылается на инструкцию SELECT как на символьную строку.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( DataSource   varchar(20) NOT NULL,  
  BusinessEntityID   varchar(11) NOT NULL,  
  LastName     varchar(40) NOT NULL,  
  SalesDollars money NOT NULL  
);  
GO  
CREATE PROCEDURE dbo.uspGetEmployeeSales   
AS   
    SET NOCOUNT ON;  
    SELECT 'PROCEDURE', sp.BusinessEntityID, c.LastName,   
        sp.SalesYTD   
    FROM Sales.SalesPerson AS sp    
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY sp.BusinessEntityID, c.LastName;  
GO  
--INSERT...SELECT example  
INSERT INTO dbo.EmployeeSales  
    SELECT 'SELECT', sp.BusinessEntityID, c.LastName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY sp.BusinessEntityID, c.LastName;  
GO  
--INSERT...EXECUTE procedure example  
INSERT INTO dbo.EmployeeSales   
EXECUTE dbo.uspGetEmployeeSales;  
GO  
--INSERT...EXECUTE('string') example  
INSERT INTO dbo.EmployeeSales   
EXECUTE   
('  
SELECT ''EXEC STRING'', sp.BusinessEntityID, c.LastName,   
    sp.SalesYTD   
    FROM Sales.SalesPerson AS sp   
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE ''2%''  
    ORDER BY sp.BusinessEntityID, c.LastName  
');  
GO  
--Show results.  
SELECT DataSource,BusinessEntityID,LastName,SalesDollars  
FROM dbo.EmployeeSales;  
```  
  
#### <a name="i-using-with-common-table-expression-to-define-the-data-inserted"></a>И. Использование обобщенного табличного выражения WITH для определения вставляемых данных  
 В следующем примере создается таблица `NewEmployee` в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Обобщенное табличное выражение (`EmployeeTemp`) определяет строки из одной или нескольких таблиц, которые вставляются в таблицу `NewEmployee`. Инструкция INSERT ссылается на столбцы в обобщенном табличном выражении.  
  
```  
CREATE TABLE HumanResources.NewEmployee  
(  
    EmployeeID int NOT NULL,  
    LastName nvarchar(50) NOT NULL,  
    FirstName nvarchar(50) NOT NULL,  
    PhoneNumber Phone NULL,  
    AddressLine1 nvarchar(60) NOT NULL,  
    City nvarchar(30) NOT NULL,  
    State nchar(3) NOT NULL,   
    PostalCode nvarchar(15) NOT NULL,  
    CurrentFlag Flag  
);  
GO  
WITH EmployeeTemp (EmpID, LastName, FirstName, Phone,   
                   Address, City, StateProvince,   
                   PostalCode, CurrentFlag)  
AS (SELECT   
       e.BusinessEntityID, c.LastName, c.FirstName, pp.PhoneNumber,  
       a.AddressLine1, a.City, sp.StateProvinceCode,   
       a.PostalCode, e.CurrentFlag  
    FROM HumanResources.Employee e  
        INNER JOIN Person.BusinessEntityAddress AS bea  
        ON e.BusinessEntityID = bea.BusinessEntityID  
        INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
        INNER JOIN Person.PersonPhone AS pp  
        ON e.BusinessEntityID = pp.BusinessEntityID  
        INNER JOIN Person.StateProvince AS sp  
        ON a.StateProvinceID = sp.StateProvinceID  
        INNER JOIN Person.Person as c  
        ON e.BusinessEntityID = c.BusinessEntityID  
    )  
INSERT INTO HumanResources.NewEmployee   
    SELECT EmpID, LastName, FirstName, Phone,   
           Address, City, StateProvince, PostalCode, CurrentFlag  
    FROM EmployeeTemp;  
GO  
```  
  
#### <a name="j-using-top-to-limit-the-data-inserted-from-the-source-table"></a>К. Использование TOP для ограничения данных, вставляемых из исходной таблицы  
 В следующем примере создается таблица `EmployeeSales` и выполняется вставка данных о продажах за текущий год для пяти первых случайно выбранных сотрудников из таблицы `HumanResources.Employee` в базу данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Инструкция INSERT выбирает любые пять строк из строк, возвращенных инструкцией `SELECT`. Предложение OUTPUT отображает строки, вставляемые в таблицу `EmployeeSales`. Обратите внимание, что предложение ORDER BY в инструкции SELECT не используется для определения 5 наиболее успешных сотрудников.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   nvarchar(11) NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  YearlySales  money NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, 
        inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
```  
  
 Если для вставки строк в значимом хронологическом порядке решено использовать предложение TOP, вместе с ним в инструкции подзапроса выборки следует использовать предложение ORDER BY, как показано в следующем примере. Предложение OUTPUT отображает строки, вставляемые в таблицу `EmployeeSales`. Обратите внимание, что вставка данных 5 наиболее успешных сотрудников выполняется на основе результатов предложения ORDER BY, а не случайных строк.  
  
```  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, 
        inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
```  
  
###  <a name="TargetObjects"></a>Указание целевых объектов, отличных от стандартных таблиц  
 В примерах этого раздела показаны методы вставки строк с указанием представления или табличной переменной.  
  
#### <a name="k-inserting-data-by-specifying-a-view"></a>Л. Вставка данных с указанием представления  
 В следующем примере в качестве целевого объекта указано имя представления; новая строка вставляется в базовую таблицу. Порядок следования значений в инструкции `INSERT` должен совпадать с порядком следования столбцов в представлении. Дополнительные сведения см. в разделе [изменение данных через представление](../../relational-databases/views/modify-data-through-a-view.md).  
  
```  
CREATE TABLE T1 ( column_1 int, column_2 varchar(30));  
GO  
CREATE VIEW V1 AS   
SELECT column_2, column_1   
FROM T1;  
GO  
INSERT INTO V1   
    VALUES ('Row 1',1);  
GO  
SELECT column_1, column_2   
FROM T1;  
GO  
SELECT column_1, column_2  
FROM V1;  
GO  
```  
  
#### <a name="l-inserting-data-into-a-table-variable"></a>М. Вставка данных в табличную переменную  
 В следующем примере задается переменная таблицы в качестве целевого объекта в базе данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    LocationID int NOT NULL,  
    CostRate smallmoney NOT NULL,  
    NewCostRate AS CostRate * 1.5,  
    ModifiedDate datetime);  
  
-- Insert values into the table variable.  
INSERT INTO @MyTableVar (LocationID, CostRate, ModifiedDate)  
    SELECT LocationID, CostRate, GETDATE() 
    FROM Production.Location  
    WHERE CostRate > 0;  
  
-- View the table variable result set.  
SELECT * FROM @MyTableVar;  
GO  
```  
  
###  <a name="RemoteTables"></a>Вставка строк в удаленную таблицу  
 В примерах этого раздела показано, как вставлять строки в удаленную целевую таблицу с помощью [связанного сервера](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) или [функцию набора строк](../../t-sql/functions/rowset-functions-transact-sql.md) для ссылки на удаленную таблицу.  
  
#### <a name="m-inserting-data-into-a-remote-table-by-using-a-linked-server"></a>Н. Вставка данных в удаленную таблицу с использованием связанного сервера  
 В следующем примере в удаленную таблицу вставляются строки. Пример начинается с создания ссылки на удаленный источник данных с помощью [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Имя связанного сервера, `MyLinkServer`, задается в качестве части имени объекта, состоящее из четырех частей в форме *сервер.каталог.схема.объект*.  
  
**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  
```  
  
```  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
INSERT INTO MyLinkServer.AdventureWorks2012.HumanResources.Department (Name, GroupName)  
VALUES (N'Public Relations', N'Executive General and Administration');  
GO  
```  
  
#### <a name="n-inserting-data-into-a-remote-table-by-using-the-openquery-function"></a>О. Вставка данных в удаленную таблицу с помощью функции OPENQUERY  
 Следующий пример вставляет строку в удаленную таблицу, указав [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) функцию набора строк. В этом примере используется имя связанного сервера, созданного в предыдущем примере.  
  
**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
INSERT OPENQUERY (MyLinkServer, 
    'SELECT Name, GroupName 
     FROM AdventureWorks2012.HumanResources.Department')  
VALUES ('Environmental Impact', 'Engineering');  
GO  
```  
  
#### <a name="o-inserting-data-into-a-remote-table-by-using-the-opendatasource-function"></a>П. Вставка данных в удаленную таблицу с помощью функции OPENDATASOURCE  
 Следующий пример вставляет строку в удаленную таблицу, указав [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) функцию набора строк. Укажите допустимое имя сервера для источника данных, используя формат *имя_сервера* или *имя_сервера\имя_экземпляра*.  
  
**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_nameinstance_name.  
  
INSERT INTO OPENDATASOURCE('SQLNCLI',  
    'Data Source= <server_name>; Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department (Name, GroupName)  
    VALUES (N'Standards and Methods', 'Quality Assurance');  
GO  
```  
  
#### <a name="p-inserting-into-an-external-table-created-using-polybase"></a>Т. Вставка в внешней таблицы, созданные с помощью PolyBase  
 Вы можете экспортировать данные из SQL Server в службу хранилища Azure или Hadoop. Для этого сначала необходимо создать внешнюю таблицу, которая указывает на целевой файл или каталог. Затем используйте инструкцию INSERT INTO, чтобы экспортировать данные из локальной таблицы SQL Server во внешний источник данных. При выполнении инструкции INSERT INTO создается целевой файл или каталог (если его не существует), а результаты выполнения инструкции SELECT экспортируются в указанное расположение в заданном формате.  Дополнительные сведения см. в разделе [Приступая к работе с PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
**Область применения**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
-- Create an external table.   
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
        [FirstName] char(25) NOT NULL,   
        [LastName] char(25) NOT NULL,   
        [YearlyIncome] float NULL,   
        [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
        LOCATION='/old_data/2009/customerdata.tbl',  
        DATA_SOURCE = HadoopHDP2,  
        FILE_FORMAT = TextFileFormat,  
        REJECT_TYPE = VALUE,  
        REJECT_VALUE = 0  
);  
  
-- Export data: Move old data to Hadoop while keeping 
-- it query-able via external table.  

INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  
  
###  <a name="BulkLoad"></a>Массовая загрузка данных из таблиц или файлов данных  
 В примерах этого раздела показано два метода для массовой загрузки данных в таблицу с помощью инструкции INSERT.  
  
#### <a name="q-inserting-data-into-a-heap-with-minimal-logging"></a>У. Вставка данных в кучу с минимальным протоколированием  
 В следующем примере создается новая таблица (куча), в которую вставляются данные из другой таблицы с минимальным протоколированием. В примере предполагается, что для базы данных `AdventureWorks2012` выбрана модель восстановления FULL. Чтобы убедиться, что применяется минимальное протоколирование, модель восстановления базы данных `AdventureWorks2012` перед вставкой строк устанавливается в значение BULK_LOGGED, а после выполнения инструкции INSERT INTO… SELECT возвращается в значение FULL. Кроме того, для целевой таблицы `Sales.SalesHistory` указывается подсказка TABLOCK. Это обеспечивает минимальное использование журнала транзакций инструкцией и ее эффективное выполнение.  
  
```  
-- Create the target heap.  
CREATE TABLE Sales.SalesHistory(  
    SalesOrderID int NOT NULL,  
    SalesOrderDetailID int NOT NULL,  
    CarrierTrackingNumber nvarchar(25) NULL,  
    OrderQty smallint NOT NULL,  
    ProductID int NOT NULL,  
    SpecialOfferID int NOT NULL,  
    UnitPrice money NOT NULL,  
    UnitPriceDiscount money NOT NULL,  
    LineTotal money NOT NULL,  
    rowguid uniqueidentifier ROWGUIDCOL  NOT NULL,  
    ModifiedDate datetime NOT NULL );  
GO  
-- Temporarily set the recovery model to BULK_LOGGED.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY BULK_LOGGED;  
GO  
-- Transfer data from Sales.SalesOrderDetail to Sales.SalesHistory  
INSERT INTO Sales.SalesHistory WITH (TABLOCK)  
    (SalesOrderID,   
     SalesOrderDetailID,  
     CarrierTrackingNumber,   
     OrderQty,   
     ProductID,   
     SpecialOfferID,   
     UnitPrice,   
     UnitPriceDiscount,  
     LineTotal,   
     rowguid,   
     ModifiedDate)  
SELECT * FROM Sales.SalesOrderDetail;  
GO  
-- Reset the recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
#### <a name="r-using-the-openrowset-function-with-bulk-to-bulk-load-data-into-a-table"></a>Ф. Использование функции OPENROWSET с параметром BULK для массовой загрузки данных а таблицу  
 В следующем примере выполняется вставка строки в таблицу из файла данных вызовом функции OPENQUERY. Для оптимизации производительности указывается табличная подсказка IGNORE_TRIGGERS. Дополнительные примеры см. в разделе [массовый импорт данных с помощью инструкции BULK INSERT или OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
**Область применения**: начиная с [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
INSERT INTO HumanResources.Department WITH (IGNORE_TRIGGERS) (Name, GroupName)  
SELECT b.Name, b.GroupName   
FROM OPENROWSET (  
    BULK 'C:SQLFilesDepartmentData.txt',  
    FORMATFILE = 'C:SQLFilesBulkloadFormatFile.xml',  
    ROWS_PER_BATCH = 15000)AS b ;  
```  
  
###  <a name="TableHints"></a>Переопределение поведения по умолчанию оптимизатор запросов с помощью подсказок  
 Примеры в этом разделе демонстрируют, как использовать [табличные подсказки](../../t-sql/queries/hints-transact-sql-table.md) для временного переопределения поведения по умолчанию оптимизатор запросов при обработке инструкции INSERT.  
  
> [!CAUTION]  
>  Поскольку оптимизатор запросов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] обычно выбирает наилучший план выполнения запроса, подсказки рекомендуется использовать только опытным разработчикам и администраторам баз данных в качестве последнего средства.  
  
#### <a name="s-using-the-tablock-hint-to-specify-a-locking-method"></a>Х. Использование подсказки TABLOCK для указания метода блокировки  
 В следующем примере показано, как монопольная блокировка (Х) применяется к таблице Production.Location и сохраняется до завершения инструкции UPDATE.  
  
**Применяется к**: [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].  
  
```  
INSERT INTO Production.Location WITH (XLOCK)  
(Name, CostRate, Availability)  
VALUES ( N'Final Inventory', 15.00, 80.00);  
```  
  
###  <a name="CaptureResults"></a>Сбор результатов инструкции INSERT  
 Примеры в этом разделе демонстрируют, как использовать [предложение OUTPUT](../../t-sql/queries/output-clause-transact-sql.md) для возврата сведений или на основе выражений, всех строк, изменившихся с помощью инструкции INSERT. Эти результаты могут быть возвращены приложению, например для вывода подтверждающих сообщений, архивирования и т. п.  
  
#### <a name="t-using-output-with-an-insert-statement"></a>T. Применение предложения OUTPUT с инструкцией INSERT  
 В следующем примере производится вставка строки в таблицу `ScrapReason`, а затем при помощи предложения `OUTPUT` результаты выполнения инструкции возвращаются в табличную переменную `@MyTableVar`. Так как столбец `ScrapReasonID` определен с помощью свойства `IDENTITY`, то значение для этого столбца не указано в инструкции `INSERT`. Однако следует заметить, что значение, созданное компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)] для этого столбца, возвращается в предложении `OUTPUT` в столбец `INSERTED.ScrapReasonID`.  
  
```  
DECLARE @MyTableVar table( NewScrapReasonID smallint,  
                           Name varchar(50),  
                           ModifiedDate datetime);  
INSERT Production.ScrapReason  
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate  
        INTO @MyTableVar  
VALUES (N'Operator error', GETDATE());  
  
--Display the result set of the table variable.  
SELECT NewScrapReasonID, Name, ModifiedDate FROM @MyTableVar;  
--Display the result set of the table.  
SELECT ScrapReasonID, Name, ModifiedDate   
FROM Production.ScrapReason;  
```  
  
#### <a name="u-using-output-with-identity-and-computed-columns"></a>Ф. Применение предложения OUTPUT со столбцами идентификаторов и вычисляемыми столбцами  
 В следующем примере создается таблица `EmployeeSales`, а затем в нее с помощью инструкции INSERT вставляется несколько строк, получаемых инструкцией SELECT из исходных таблиц. Таблица `EmployeeSales` содержит столбец идентификаторов (`EmployeeID`) и вычисляемый столбец (`ProjectedSales`). Поскольку значения создаются компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)] при вставке, ни один из этих столбцов не может быть определен в `@MyTableVar`.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   int IDENTITY (1,5)NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales AS CurrentSales * 1.10   
);  
GO  
DECLARE @MyTableVar table(  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL  
  );  
  
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)  
  OUTPUT INSERTED.LastName,   
         INSERTED.FirstName,   
         INSERTED.CurrentSales  
  INTO @MyTableVar  
    SELECT c.LastName, c.FirstName, sp.SalesYTD  
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY c.LastName, c.FirstName;  
  
SELECT LastName, FirstName, CurrentSales  
FROM @MyTableVar;  
GO  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM dbo.EmployeeSales;  
```  
  
#### <a name="v-inserting-data-returned-from-an-output-clause"></a>Х. Вставка данных, возвращенных предложением OUTPUT  
 В следующем примере производится отслеживание данных, возвращаемых предложением OUTPUT инструкции MERGE, а затем производится вставка этих данных в другую таблицу. В инструкции MERGE ежедневно обновляется столбец `Quantity` таблицы `ProductInventory` на основе заказов, обработанных в таблице `SalesOrderDetail` базы данных [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Инструкция также удаляет строки с продуктами, запас которых сократился до 0. В примере собираются удаленные строки и вставляются в другую таблицу, `ZeroInventory`, в которой ведется учет закончившихся продуктов.  
  
```  
--Create ZeroInventory table.  
CREATE TABLE Production.ZeroInventory (DeletedProductID int, RemovedOnDate DateTime);  
GO  
  
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)  
SELECT ProductID, GETDATE()  
FROM  
(   MERGE Production.ProductInventory AS pi  
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
           JOIN Sales.SalesOrderHeader AS soh  
           ON sod.SalesOrderID = soh.SalesOrderID  
           AND soh.OrderDate = '20070401'  
           GROUP BY ProductID) AS src (ProductID, OrderQty)  
    ON (pi.ProductID = src.ProductID)  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0  
        THEN DELETE  
    WHEN MATCHED  
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)  
WHERE Action = 'DELETE';  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were inserted';  
GO  
SELECT DeletedProductID, RemovedOnDate FROM Production.ZeroInventory;  
```  

#### <a name="w-inserting-data-using-the-select-option"></a>ВТ. Вставка данных с помощью параметра SELECT  
 В следующем примере показано, как вставить несколько строк данных с помощью инструкции INSERT с ВЫБЕРИТЕ параметр. Первый `INSERT` использует оператор `SELECT` инструкции непосредственно для извлечения данных из исходной таблицы, и затем установите для сохранения результатов в `EmployeeTitles` таблицы.  
  
```  
CREATE TABLE EmployeeTitles  
( EmployeeKey   INT NOT NULL,  
  LastName     varchar(40) NOT NULL,  
  Title      varchar(50) NOT NULL  
);  
INSERT INTO EmployeeTitles  
    SELECT EmployeeKey, LastName, Title   
    FROM ssawPDW.dbo.DimEmployee  
    WHERE EndDate IS NULL;  
```  
  
#### <a name="x-specifying-a-label-with-the-insert-statement"></a>X. Указание метки при помощи инструкции INSERT  
 В следующем примере показано использование метки с инструкцией INSERT.  
  
```  
-- Uses AdventureWorks  
  
INSERT INTO DimCurrency   
VALUES (500, N'C1', N'Currency1')  
OPTION ( LABEL = N'label1' );  
```  
  
#### <a name="y-using-a-label-and-a-query-hint-with-the-insert-statement"></a>Y. С помощью метки и подсказки в запросе с помощью инструкции INSERT  
 Этот запрос показан основной синтаксис для использования метки и подсказки в запросе соединения при помощи инструкции INSERT. После отправки запроса к узлу управления [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], на вычислительных узлах, стратегии хэш соединения применяются при формировании [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] плана запроса. Дополнительные сведения о указания соединения и как использовать предложение OPTION. в разделе [параметр (SQL Server PDW)](http://msdn.microsoft.com/en-us/72bbce98-305b-42fa-a19f-d89620621ecc).  
  
```  
-- Uses AdventureWorks  
  
INSERT INTO DimCustomer (CustomerKey, CustomerAlternateKey, 
    FirstName, MiddleName, LastName )   
SELECT ProspectiveBuyerKey, ProspectAlternateKey, 
    FirstName, MiddleName, LastName  
FROM ProspectiveBuyer p JOIN DimGeography g ON p.PostalCode = g.PostalCode  
WHERE g.CountryRegionCode = 'FR'  
OPTION ( LABEL = 'Add French Prospects', HASH JOIN);  
```  
  
## <a name="see-also"></a>См. также:  
 [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [Свойство IDENTITY (Transact-SQL)](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [NEWID &#40; Transact-SQL &#41;](../../t-sql/functions/newid-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [СЛИТЬ &#40; Transact-SQL &#41;](../../t-sql/statements/merge-transact-sql.md)   
 [Предложение OUTPUT &#40; Transact-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [Использование вставленных и удаленных таблиц](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)  
  
  



