---
title: Resilienza delle connessioni inattive
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: a2361c8a2e8cbc709d50a9139678a08e2e850e2d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62522028"
---
# <a name="idle-connection-resiliency"></a>Resilienza delle connessioni inattive
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Resilienza della connessione](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) è il principio che può essere ristabilita una connessione inattiva interrotta, entro determinati vincoli. Se una connessione a Microsoft SQL Server non riesce, la resilienza di connessione consente al client tentano automaticamente di ristabilire la connessione. Resilienza della connessione è una proprietà dell'origine dati. solo SQL Server 2014 e versioni successive e Database SQL di Azure supporta la resilienza di connessione.

Resilienza della connessione viene implementata con due parole chiave di connessione che possono essere aggiunto a stringhe di connessione: **ConnectRetryCount** e **ConnectRetryInterval**.

|Parola chiave|Valori|Default|Descrizione|
|-|-|-|-|
|**ConnectRetryCount**| Numero intero compreso tra 0 e 255 inclusi|1|Il numero massimo di tentativi per ristabilire una connessione interrotta prima di rinunciare. Per impostazione predefinita, un singolo tenta di ristabilire una connessione quando vengono interrotti. Un valore pari a 0 indica che non verrà tentata alcun riconnessione.|
|**ConnectRetryInterval**| Numero intero compreso tra 1 e 60 inclusi|1| Il tempo, espresso in secondi, tra i tentativi per ristabilire una connessione. L'applicazione tenterà di riconnettersi immediatamente dopo aver rilevato una connessione interrotta e quindi rimarrà in attesa **ConnectRetryInterval** secondi prima di riprovare. Questa parola chiave viene ignorata se **ConnectRetryCount** è uguale a 0.

Se il prodotto dei **ConnectRetryCount** moltiplicato **ConnectRetryInterval** maggiore **LoginTimeout**, quindi il client non sarà più provando a connettersi una volta  **LoginTimeout** viene raggiunto; in caso contrario, continuerà a tentare di riconnettersi finché **ConnectRetryCount** viene raggiunto.

#### <a name="remarks"></a>Remarks

Resilienza della connessione si applica quando la connessione rimane inattiva. Gli errori che si verificano durante l'esecuzione di una transazione, ad esempio, non attiveranno tentativi di riconnessione - genereranno errori perché in caso contrario, potrebbe essere previsto. Le situazioni seguenti, note come gli stati di sessione non recuperabili, non attiva i tentativi di riconnessione:

* Tabelle temporanee
* Cursori globali e locali
* Contesto di transazione e la sessione di livello i blocchi delle transazioni
* Blocchi a livello di applicazione
* EXECUTE AS o ripristinare il contesto di sicurezza
* Handle di automazione OLE
* Degli handle preparati XML
* Flag di traccia

## <a name="example"></a>Esempio

Il codice seguente si connette a un database ed esegue una query. Per terminare la sessione viene interrotta la connessione e viene tentata una nuova query utilizzando la connessione interrotta. Questo esempio usa il database di esempio [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx).

In questo esempio, specifichiamo un cursore memorizzato nel buffer prima dell'interruzione della connessione. Se non si specifica un cursore memorizzato nel buffer, viene ristabilita la connessione non perché non vi sarà un cursore lato server attivi e in questo modo la connessione non sarebbe inattiva se interrotto. Tuttavia, in tal caso, utilizzeremmo sqlsrv_free_stmt() prima dell'interruzione della connessione per liberare il cursore e potrebbe essere ristabilita la connessione.

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
Output previsto:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>Vedere anche
[Resilienza di connessione nel driver ODBC di Windows](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
