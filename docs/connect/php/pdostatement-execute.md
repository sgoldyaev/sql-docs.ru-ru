---
title: PDOStatement::execute | Документация Майкрософт
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75f6b34d722fc5624270162e7f3e31231946685e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773162"
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Выполняет инструкцию.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>Параметры  
*$input*: ассоциативный массив, содержащий значения для маркеров параметров (необязательно).  
  
## <a name="return-value"></a>Возвращаемое значение  
Значение true в случае успеха, в противном случае — значение false.  
  
## <a name="remarks"></a>Remarks  
Инструкции, выполняемые с помощью PDOStatement::execute, необходимо сначала подготовить с помощью [PDO::prepare](../../connect/php/pdo-prepare.md). Статья [Выполнение прямых и подготовленных инструкций в драйвере PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) содержит сведения о том, как указать выполнение прямой или подготовленной инструкции.  
  
Все значения массива входных параметров обрабатываются как значения PDO::PARAM_STR.  
  
Если подготовленная инструкция содержит маркеры параметров, необходимо вызвать PDOStatement::bindParam, чтобы осуществить привязку переменных PHP к маркерам параметров или передать массив значений параметров, используемых только в качестве входных.  
  
Поддержка PDO была добавлена в версии 2.0 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Пример  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
$stmt->execute();  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
  
echo "\n";  
$param = "Owner";  
$query = "select * from Person.ContactType where name = ?";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
?>  
```  
  
> [!NOTE]
> Рекомендуется использовать строки в качестве входных данных при привязке значения [столбца decimal или numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) чтобы обеспечить точность и правильность, как PHP имеет ограниченную точность для [чисел с плавающей запятой](http://php.net/manual/en/language.types.float.php). То же применимо к столбцами bigint, особенно в том случае, если значения вне диапазона [целое число](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).

## <a name="see-also"></a>См. также:  
[Класс PDOStatement](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
