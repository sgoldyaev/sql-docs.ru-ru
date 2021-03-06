---
title: 'Как: извлечение параметров вывода с помощью драйвера SQLSRV | Документы Microsoft'
ms.custom: ''
ms.date: 04/11/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1157bab7-6ad1-4bdb-a81c-662eea3e7fcd
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81a94f68d7198285125236337a0025e41f1bf8ef
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34563892"
---
# <a name="how-to-retrieve-output-parameters-using-the-sqlsrv-driver"></a>Практическое руководство. Извлечение параметров вывода с помощью драйвера SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Эта статья описывает, как вызвать хранимую процедуру, в которой один параметр определен как параметр вывода. При извлечении параметра ввода вывода, должны быть использованы все результаты, возвращаемые хранимой процедурой перед становится доступно значение возвращаемого параметра.  
  
> [!NOTE]  
> Переменные, которые инициализируются или обновляются с использованием **null**, **DateTime**или типов потоков, нельзя использовать в качестве параметров вывода.  
  
Когда потоковые типы, такие как SQLSRV_SQLTYPE_VARCHAR('max'), используются в качестве параметров вывода, может возникнуть усечение данных. Использование потоковых типов в качестве параметров вывода не поддерживается. Для непотоковых типов усечение данных может произойти, если длина параметра вывода не указана или если указанная длина недостаточна для параметра вывода.  
  
## <a name="example-1"></a>Пример 1
Следующий пример вызывает хранимую процедуру, которая возвращает продажи для определенного сотрудника за период с начала года и до настоящего момента. Переменная *$lastName* PHP является параметром ввода, а *$salesYTD* — параметром вывода.  
  
> [!NOTE]  
> Инициализация *$salesYTD* значением 0.0 задает для возвращаемого PHPTYPE значение **float**. Для обеспечения целостности типа данных параметры вывода должны быть инициализированы перед вызовом хранимой процедуры, либо должен быть указан нужный PHPTYPE. Сведения об указании PHPTYPE см. в статье [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Поскольку хранимая процедура возвращает только один результат, *$salesYTD* содержит возвращаемое значение параметра вывода сразу после выполнения хранимой процедуры.  
  
> [!NOTE]  
> Рекомендуется вызывать хранимые процедуры с использованием канонического синтаксиса. Дополнительные сведения о каноническом синтаксисе см. в разделе [вызов хранимой процедуры](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md).  
  
Предполагается, что SQL Server и [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) базы данных установлены на локальном компьютере. При выполнении примера из командной строки все выходные данные выводятся в консоль.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Drop the stored procedure if it already exists. */  
$tsql_dropSP = "IF OBJECT_ID('GetEmployeeSalesYTD', 'P') IS NOT NULL  
                DROP PROCEDURE GetEmployeeSalesYTD";  
$stmt1 = sqlsrv_query( $conn, $tsql_dropSP);  
if( $stmt1 === false )  
{  
     echo "Error in executing statement 1.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Create the stored procedure. */  
$tsql_createSP = " CREATE PROCEDURE GetEmployeeSalesYTD  
                   @SalesPerson nvarchar(50),  
                   @SalesYTD money OUTPUT  
                   AS  
                   SELECT @SalesYTD = SalesYTD  
                   FROM Sales.SalesPerson AS sp  
                   JOIN HumanResources.vEmployee AS e   
                   ON e.EmployeeID = sp.SalesPersonID  
                   WHERE LastName = @SalesPerson";  
$stmt2 = sqlsrv_query( $conn, $tsql_createSP);  
if( $stmt2 === false )  
{  
     echo "Error in executing statement 2.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*--------- The next few steps call the stored procedure. ---------*/  
  
/* Define the Transact-SQL query. Use question marks (?) in place of  
 the parameters to be passed to the stored procedure */  
$tsql_callSP = "{call GetEmployeeSalesYTD( ?, ? )}";  
  
/* Define the parameter array. By default, the first parameter is an  
INPUT parameter. The second parameter is specified as an OUTPUT  
parameter. Initializing $salesYTD to 0.0 sets the returned PHPTYPE to  
float. To ensure data type integrity, output parameters should be  
initialized before calling the stored procedure, or the desired  
PHPTYPE should be specified in the $params array.*/  
$lastName = "Blythe";  
$salesYTD = 0.0;  
$params = array(   
                 array($lastName, SQLSRV_PARAM_IN),  
                 array(&$salesYTD, SQLSRV_PARAM_OUT)  
               );  
  
/* Execute the query. */  
$stmt3 = sqlsrv_query( $conn, $tsql_callSP, $params);  
if( $stmt3 === false )  
{  
     echo "Error in executing statement 3.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Display the value of the output parameter $salesYTD. */  
echo "YTD sales for ".$lastName." are ". $salesYTD. ".";  
  
/*Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_free_stmt( $stmt3);  
sqlsrv_close( $conn);  
?>  
```  

> [!NOTE]
> При привязке выходной параметр типа bigint, если значение может оказаться за пределами диапазона [целое](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md), необходимо указать его тип SQL в качестве SQLSRV_SQLTYPE_BIGINT. В противном случае это может привести к исключению «значение вне допустимого диапазона».

## <a name="example-2"></a>Пример 2
В этом примере кода демонстрируется привязка значения больших bigint в качестве выходного параметра.  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"testDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Assume the stored procedure spTestProcedure exists, which retrieves a bigint value of some large number
// e.g. 9223372036854
$bigintOut = 0;
$outSql = "{CALL spTestProcedure (?)}";
$stmt = sqlsrv_prepare($conn, $outSql, array(array(&$bigintOut, SQLSRV_PARAM_OUT, null, SQLSRV_SQLTYPE_BIGINT)));
sqlsrv_execute($stmt);
echo "$bigintOut\n";   // Expect 9223372036854

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>См. также  
[Практическое руководство. Указание направления параметров с помощью драйвера SQLSRV](../../connect/php/how-to-specify-parameter-direction-using-the-sqlsrv-driver.md)

[Практическое руководство. Извлечение параметров ввода и вывода с помощью драйвера SQLSRV](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)

[Извлечение данных](../../connect/php/retrieving-data.md)  
  
