---
title: Pool di connessioni (driver Microsoft per PHP per SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 714a3436cc79f3568e14c5e2609e16fd408f288e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80900987"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>Pool di connessioni (Driver Microsoft per PHP per SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Di seguito vengono segnalati aspetti importanti da tenere presenti circa il pool di connessioni nei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]:  
  
-   I [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] usano i pool di connessioni ODBC.  
  
-   Per impostazione predefinita, i pool di connessioni sono abilitati in Windows. In Linux e macOS le connessioni vengono messe in pool solo se il pool di connessioni è abilitato per ODBC (vedere [Abilitazione e disabilitazione del pool di connessioni](#enablingdisabling-connection-pooling)). Quando il pool di connessioni è abilitato e ci si connette a un server, il driver tenta di usare una connessione in pool prima di crearne una nuova. Se nel pool non viene trovata una connessione equivalente, una nuova connessione viene creata e aggiunta al pool. Il driver determina se le connessioni sono equivalenti confrontando le stringhe di connessione.  
  
-   Quando si usa una connessione del pool, lo stato della connessione viene ripristinato.  
  
-   Quando si chiude la connessione, questa viene riportata al pool.  
  
Per altre informazioni sui pool di connessioni, vedere [Pool di connessioni di Gestione driver](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="enablingdisabling-connection-pooling"></a>Abilitazione e disabilitazione del pool di connessioni
### <a name="windows"></a>Windows
È possibile forzare il driver a creare una nuova connessione, anziché cercarne una equivalente nel pool di connessioni, impostando il valore dell'attributo *ConnectionPooling* nella stringa di connessione su **false** o 0.  
  
Se l'attributo *ConnectionPooling* viene omesso dalla stringa di connessione o se è impostato su **true** o 1, il driver crea una nuova connessione solo se non esiste una connessione equivalente nel pool di connessioni.  
  
Per informazioni sugli altri attributi di connessione, vedere [Connection Options](../../connect/php/connection-options.md).  
### <a name="linux-and-macos"></a>Linux e macOS
Non è possibile usare l'attributo *ConnectionPooling* per abilitare o disabilitare il pool di connessioni. 

È possibile abilitare o disabilitare il pool di connessioni modificando il file di configurazione odbcinst.ini. Per rendere effettive le modifiche, è necessario ricaricare il driver.

Impostando `Pooling` su `Yes` e un valore positivo `CPTimeout` nel file odbcinst.ini il pool di connessioni viene abilitato. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
Come minimo, il file odbcinst.ini deve avere un aspetto simile a quello riportato nell'esempio:

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

L'impostazione di `Pooling` su `No` nel file odbcinst.ini impone al driver di creare una nuova connessione.
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>Osservazioni
- In Linux o macOS tutte le connessioni verranno aggiunte al pool se il pool è abilitato nel file odbcinst.ini. Ciò significa che l'opzione di connessione ConnectionPooling non ha alcun effetto. Per disabilitare il pool, impostare Pooling=No nel file odbcinst.ini e ricaricare i driver.
  - unixODBC < = 2.3.4 (Linux e macOS) potrebbe non restituire informazioni di diagnostica appropriate, ad esempio messaggi di errore, avvisi e messaggi informativi
  - per questo motivo, i driver SQLSRV e PDO_SQLSRV potrebbero non essere in grado di recuperare correttamente i dati Long (ad esempio XML, binari) come stringhe. I dati Long possono essere recuperati come flussi come soluzione alternativa. Vedere l'esempio seguente per SQLSRV.

```
<?php
$connectionInfo = array("Database"=>"test", "UID"=>"username", "PWD"=>"password");

$conn1 = sqlsrv_connect("servername", $connectionInfo);

$longSample = str_repeat("a", 8500);
$xml1 = 
'<ParentXMLTag>
  <ChildTag01>'.$longSample.'</ChildTag01>
</ParentXMLTag>';

// Create table and insert xml string into it
sqlsrv_query($conn1, "CREATE TABLE xml_table (field xml)");
sqlsrv_query($conn1, "INSERT into xml_table values ('$xml1')");

// retrieve the inserted xml
$column1 = getColumn($conn1);

// return the connection to the pool
sqlsrv_close($conn1);

// This connection is from the pool
$conn2 = sqlsrv_connect("servername", $connectionInfo);
$column2 = getColumn($conn2);

sqlsrv_query($conn2, "DROP TABLE xml_table");
sqlsrv_close($conn2);

function getColumn($conn)
{
    $tsql = "SELECT * from xml_table";
    $stmt = sqlsrv_query($conn, $tsql);
    sqlsrv_fetch($stmt);
    // This might fail in Linux and macOS
    // $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    // The workaround is to fetch it as a stream
    $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));
    sqlsrv_free_stmt($stmt);
    return ($column);
}
?>
```


## <a name="see-also"></a>Vedere anche  
[Procedura: Connessione con l'autenticazione di Windows](../../connect/php/how-to-connect-using-windows-authentication.md)

[Procedura: Connessione con l'autenticazione di SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
