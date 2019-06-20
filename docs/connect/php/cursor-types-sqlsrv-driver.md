---
title: Tipi di cursore (driver SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6452fc506814cdfdeee4f61085ec9a1ee0cededa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801486"
---
# <a name="cursor-types-sqlsrv-driver"></a>Tipi di cursore (driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Il driver SQLSRV consente di creare un set di risultati con righe a cui si può accedere in qualsiasi ordine, a seconda del tipo di cursore.  Questo argomento vengono illustrati (memorizzato nel buffer) sul lato client e lato server (senza buffer) dei cursori.  
  
## <a name="cursor-types"></a>Tipi di cursore  
Quando si crea un set di risultati con [sqlsrv_query](../../connect/php/sqlsrv-query.md) o con [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md), è possibile specificare il tipo di cursore. Per impostazione predefinita, viene utilizzato un cursore forward-only, che consente di spostare una riga alla volta a partire dalla prima riga del gruppo di risultati fino a quando non si raggiunge la fine del set di risultati.  
  
È possibile creare un set di risultati con cursori scorrevoli, che consente di accedere a qualsiasi riga nel set di risultati, in qualsiasi ordine. Nella tabella seguente sono elencati i valori che possono essere passati per il **Scrollable** opzione sqlsrv_query o sqlsrv_prepare.  
  
|Opzione|Descrizione|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|Consente di spostare una riga alla volta a partire dalla prima riga del gruppo di risultati fino a quando non si raggiunge la fine del set di risultati.<br /><br />Questo è il tipo di cursore predefinito.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) restituisce un errore per set di risultati creati con questo tipo di cursore.<br /><br />**inoltrare** è la forma abbreviata di SQLSRV_CURSOR_FORWARD.|  
|SQLSRV_CURSOR_STATIC|Consente di accedere alle righe in qualsiasi ordine, ma non rifletterà le modifiche nel database.<br /><br />**statico** è la forma abbreviata di SQLSRV_CURSOR_STATIC.|  
|SQLSRV_CURSOR_DYNAMIC|Consente accedere alle righe in qualsiasi ordine e rifletterà le modifiche nel database.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) restituisce un errore per set di risultati creati con questo tipo di cursore.<br /><br />**dinamica** è la forma abbreviata di SQLSRV_CURSOR_DYNAMIC.|  
|SQLSRV_CURSOR_KEYSET|Consente accedere alle righe in qualsiasi ordine. Tuttavia un cursore keyset non aggiorna il conteggio delle righe se dalla tabella viene eliminata una riga (una riga eliminata viene restituita senza alcun valore).<br /><br />**keyset** è la forma abbreviata di SQLSRV_CURSOR_KEYSET.|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|Consente accedere alle righe in qualsiasi ordine. Crea una query di cursore lato client.<br /><br />**memorizzati nel buffer** è la forma abbreviata di SQLSRV_CURSOR_CLIENT_BUFFERED.|  
  
Se una query genera più set di risultati, il **Scrollable** opzione si applica a tutti i set di risultati.  
  
## <a name="selecting-rows-in-a-result-set"></a>La selezione di righe in un Set di risultati  
Dopo aver creato un set di risultati, è possibile usare [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md), [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md), o [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) per specificare una riga.  
  
Nella tabella seguente vengono descritti i valori in cui è possibile specificare il *riga* parametro.  
  
|Parametro|Descrizione|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|Specifica la riga successiva. Questo è il valore predefinito, se non si specifica la *riga* parametro per un set di risultati scorrevoli.|  
|SQLSRV_SCROLL_PRIOR|Specifica la riga precedente alla riga corrente.|  
|SQLSRV_SCROLL_FIRST|Specifica la prima riga del set di risultati.|  
|SQLSRV_SCROLL_LAST|Specifica l'ultima riga del set di risultati.|  
|SQLSRV_SCROLL_ABSOLUTE|Specifica la riga specificata con il *offset* parametro.|  
|SQLSRV_SCROLL_RELATIVE|Specifica la riga specificata con il *offset* parametro dalla riga corrente.|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>I cursori sul lato server e il Driver SQLSRV  
Nell'esempio seguente mostra l'effetto dei cursori del diversi. Nella riga 33 dell'esempio, noterete che la prima delle tre istruzioni di query che specificano cursori diversi.  Due delle istruzioni query impostare come commento. Ogni volta che si esegue il programma, usare un tipo di cursore diverso per visualizzare l'effetto dell'aggiornamento del database nella riga 47.  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>I cursori sul lato client e il Driver SQLSRV  
I cursori sul lato client sono una funzionalità aggiunta nella versione 3.0 del [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] che consente di memorizzare nella cache un intero set di risultati in memoria. Conteggio delle righe è disponibile dopo l'esecuzione della query quando si usa un cursore lato client.  
  
È consigliabile usare i cursori lato client per set di risultati di piccole e medie dimensioni. Utilizzare cursori sul lato server per i set di risultati di grandi dimensioni.  
  
Una query restituirà false se il buffer non è sufficientemente grande da contenere l'intero set di risultati. Si possono aumentare le dimensioni del buffer fino al limite di memoria di PHP.  
  
Usa il driver SQLSRV, è possibile configurare le dimensioni del buffer che contiene il set di risultati con l'impostazione ClientBufferMaxKBSize [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) restituisce il valore di ClientBufferMaxKBSize. È anche possibile impostare la dimensione massima del buffer nel file PHP. ini con sqlsrv. ClientBufferMaxKBSize (ad esempio sqlsrv. ClientBufferMaxKBSize = 1024).  
  
L'esempio seguente mostra:  
  
-   Conteggio delle righe è sempre disponibile con un cursore lato client.  
  
-   Utilizzo di cursori sul lato client e le istruzioni batch.  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
L'esempio seguente illustra un cursore lato client tramite [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) e una dimensione del buffer client diversi.
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable" => SQLSRV_CURSOR_CLIENT_BUFFERED, "ClientBufferMaxKBSize" => 51200));
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Specifica di un tipo di cursore e selezione di righe](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
