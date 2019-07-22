---
title: 'DOP:: query | Microsoft Docs'
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb7131e96277ea05b43f30923dcc64c5be602696
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936205"
---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esegue una query SQL e restituisce un set di risultati come oggetto PDOStatement.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>Parametri  
*$statement*: istruzione SQL da eseguire.  
  
*$fetch_style*: istruzioni facoltative sull'esecuzione della query. Per altre informazioni, vedere le sezione Osservazioni. $*fetch_style* in PDO::query può essere sostituito da $*fetch_style* in PDO::fetch.  
  
## <a name="return-value"></a>Valore restituito  
Se la chiamata ha esito positivo, PDO::query restituisce un oggetto PDOStatement. Se la chiamata non riesce, PDO::query genera un oggetto PDOException oppure restituisce false, a seconda dell'impostazione di PDO::ATTR_ERRMODE.  
  
## <a name="exceptions"></a>Eccezioni  
PDOException.  
  
## <a name="remarks"></a>Remarks  
Una query eseguita con PDO::query può effettuare l'esecuzione diretta o preparata di un'istruzione, a seconda dell'impostazione di PDO::SQLSRV_ATTR_DIRECT_QUERY. Per altre informazioni, vedere [Esecuzione di istruzioni diretta e preparata nel driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  
  
PDO::SQLSRV_ATTR_QUERY_TIMEOUT influisce anche sul comportamento di PDO::exec. Per altre informazioni, vedere [PDO::setAttribute](../../connect/php/pdo-setattribute.md).  
  
È possibile specificare le opzioni seguenti per $*fetch_style*.  
  
|style|Descrizione|  
|---------|---------------|  
|PDO::FETCH_COLUMN, *num*|Richiede i dati della colonna specificata. La prima colonna della tabella è la colonna 0.|  
|PDO::FETCH_CLASS, '*classname*', array( *arglist* )|Crea un'istanza di una classe e assegna i nomi di colonna alle proprietà della classe. Se il costruttore della classe accetta uno o più parametri, è anche possibile passare *arglist*.|  
|PDO::FETCH_CLASS, '*classname*'|Assegna i nomi delle colonne alle proprietà di una classe esistente.|  
  
Eseguire una chiamata a PDOStatement::closeCursor per rilasciare le risorse di database associate all'oggetto PDOStatement prima di eseguire una nuova chiamata a PDO::query.  
  
È possibile chiudere un oggetto PDOStatement impostandolo su null.  
  
Se non vengono recuperati tutti i dati di un set di risultati, la chiamata successiva a PDO::query avrà esito positivo.  
  
Nella versione 2.0 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]è stato aggiunto il supporto per PDO.  
  
## <a name="example"></a>Esempio  
Questo esempio mostra diverse query.  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```

## <a name="example"></a>Esempio
Questo esempio illustra come creare una tabella di tipi [sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql) e recuperare i dati inseriti.

```
<?php
$server = 'serverName';
$dbName = 'databaseName';
$uid = 'yourUserName';
$pwd = 'yourPassword';

$conn = new PDO("sqlsrv:server=$server; database = $dbName", $uid, $pwd);
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  

try {
    $tableName = 'testTable';
    $query = "CREATE TABLE $tableName ([c1_int] sql_variant, [c2_varchar] sql_variant)";

    $stmt = $conn->query($query);
    unset($stmt);

    $query = "INSERT INTO [$tableName] (c1_int, c2_varchar) VALUES (1, 'test_data')";
    $stmt = $conn->query($query);
    unset($stmt);

    $query = "SELECT * FROM $tableName";
    $stmt = $conn->query($query);

    $result = $stmt->fetch(PDO::FETCH_ASSOC);
    print_r($result);
    
    unset($stmt);
    unset($conn);
} catch (Exception $e) {
    echo $e->getMessage();
}
?>
```

L'output previsto è il seguente:

```
Array
(
    [c1_int] => 1
    [c2_varchar] => test_data
)
```

## <a name="see-also"></a>Vedere anche  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
