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
manager: v-mabarw
ms.openlocfilehash: 3edba0cde94d8661eed053319142ce7f84a70613
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265173"
---
# <a name="idle-connection-resiliency"></a>Resilienza delle connessioni inattive
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

La resilienza della [connessione](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) è il principio che è possibile ristabilire una connessione inattiva interruppe, entro determinati vincoli. Se una connessione a Microsoft SQL Server ha esito negativo, la resilienza della connessione consente al client di provare automaticamente a ristabilire la connessione. La resilienza della connessione è una proprietà dell'origine dati. solo SQL Server 2014 e versioni successive e il database SQL di Azure supportano la resilienza della connessione.

La resilienza della connessione viene implementata con due parole chiave di connessione che è possibile aggiungere alle stringhe di connessione: **ConnectRetryCount** e **ConnectRetryInterval**.

|Parola chiave|Valori|Default|Descrizione|
|-|-|-|-|
|**ConnectRetryCount**| Numero intero compreso tra 0 e 255 inclusi|1|Numero massimo di tentativi di ristabilire una connessione interruppe prima di rinunciare. Per impostazione predefinita, viene eseguito un singolo tentativo di ristabilire una connessione in caso di interruzione. Il valore 0 indica che non verrà tentata alcuna riconnessione.|
|**ConnectRetryInterval**| Numero intero compreso tra 1 e 60 inclusi|1| Tempo, in secondi, tra i tentativi di ristabilire una connessione. L'applicazione tenterà di riconnettersi immediatamente al rilevamento di una connessione interruppe e attenderà **ConnectRetryInterval** secondi prima di riprovare. Questa parola chiave viene ignorata se **ConnectRetryCount** è uguale a 0.

Se il prodotto di **ConnectRetryCount** moltiplicato per **ConnectRetryInterval** è maggiore di **LoginTimeout**, il client smette di tentare di connettersi una volta raggiunto **LoginTimeout** ; in caso contrario, continuerà a tentare di riconnettersi fino a quando non viene raggiunto **ConnectRetryCount** .

#### <a name="remarks"></a>Remarks

La resilienza della connessione si applica quando la connessione è inattiva. Gli errori che si verificano durante l'esecuzione di una transazione, ad esempio, non attiverà i tentativi di riconnessione. questi avranno esito negativo come previsto altrimenti. Nelle situazioni seguenti, note come stati di sessione non ripristinabili, i tentativi di riconnessione non vengono attivati:

* Tabelle temporanee
* Cursori globali e locali
* Blocchi delle transazioni a livello di sessione e di contesto di transazione
* Blocchi a livello di applicazione
* Esegui come/Ripristina contesto di sicurezza
* Handle di automazione OLE
* Handle XML preparati
* Flag di traccia

## <a name="example"></a>Esempio

Il codice seguente consente di connettersi a un database ed eseguire una query. La connessione viene interrotta terminando la sessione e viene tentata una nuova query utilizzando la connessione interrotta. Questo esempio usa il database di esempio [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx).

In questo esempio viene specificato un cursore memorizzato nel buffer prima di suddividere la connessione. Se non si specifica un cursore memorizzato nel buffer, la connessione non verrà ristabilita perché è presente un cursore sul lato server attivo e pertanto la connessione non sarà inattiva quando viene interrotta. In tal caso, tuttavia, è possibile chiamare sqlsrv_free_stmt () prima di suddividere la connessione per liberare il cursore e la connessione viene ristabilita correttamente.

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
