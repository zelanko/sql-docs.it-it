---
title: 'Procedura: Inviare e recuperare dati ASCII in Linux e macOS (SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, ASCII data
- sending data
- linux
- macOS
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: 9edd73f5ef01d1d3f22db78400cc3c204efe1379
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68251898"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>Procedura: Inviare e recuperare dati ASCII in Linux e macOS 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Questo articolo presuppone che le impostazioni locali ASCII (non UTF-8) siano state generate o installate nei sistemi Linux o macOS. 

Per inviare o recuperare i set di caratteri ASCII al server:  

1.  Se le impostazioni locali desiderate non sono quelle predefinite nell'ambiente di sistema, assicurarsi di richiamare `setlocale(LC_ALL, $locale)` prima di eseguire la prima connessione. La funzione PHP setlocale () modifica le impostazioni locali solo per lo script corrente e, se richiamata dopo aver eseguito la prima connessione, può essere ignorata.
 
2.  Quando si usa il driver SQLSRV, è possibile specificare `'CharacterSet' => SQLSRV_ENC_CHAR` come opzione di connessione. Questo passaggio è tuttavia facoltativo perché si tratta della codifica predefinita.

3.  Quando si usa il driver PDO_SQLSRV, esistono due modi. In primo luogo, quando si esegue la connessione, impostare `PDO::SQLSRV_ATTR_ENCODING` su `PDO::SQLSRV_ENCODING_SYSTEM`. Per un esempio di impostazione di un'opzione di connessione, vedere [PDO::__construct](../../connect/php/pdo-construct.md). In alternativa, dopo aver eseguito la connessione, aggiungere questa riga `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
Quando si specifica la codifica di una risorsa di connessione (in SQLSRV) o di un oggetto connessione (PDO_SQLSRV), il driver presuppone che le altre stringhe delle opzioni di connessione usino la stessa codifica. Si presuppone, inoltre, che anche le stringhe di query e nome del server usino tale set di caratteri.  
  
La codifica predefinita per il driver PDO_SQLSRV è UTF-8 (PDO::SQLSRV_ENCODING_UTF8), a differenza del driver SQLSRV. Per altre informazioni su queste costanti, vedere [Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). 
  
## <a name="example"></a>Esempio  
Gli esempi seguenti illustrano come inviare e recuperare i dati ASCII usando i driver PHP per SQL Server, specificando determinate impostazioni locali prima di eseguire la connessione. Le impostazioni locali in varie piattaforme Linux possono essere denominate in modo diverso rispetto alle stesse impostazioni locali in macOS. Ad esempio le impostazioni locali US ISO-8859-1 (Latin 1) sono `en_US.ISO-8859-1` in Linux, mentre in macOS il nome è `en_US.ISO8859-1`.
  
Negli esempi si presuppone che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia installato in un server. Quando gli esempi vengono eseguiti dal browser, tutto l'output viene scritto nel browser.  
  
```  
<?php  
  
// SQLSRV Example
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';
$connectionInfo = array('Database'=>'Test', 'UID'=>$uid, 'PWD'=>$pwd);
$conn = sqlsrv_connect($serverName, $connectionInfo);
  
if ($conn === false) {
    echo "Could not connect.<br>";  
    die(print_r(sqlsrv_errors(), true));
}  
  
// Set up the Transact-SQL query to create a test table
//   
$stmt = sqlsrv_query($conn, "CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");

// Insert data using a parameter array 
//
$tsql = "INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (?, ?)";
  
// Execute the query, $value being some ASCII string
//   
$stmt = sqlsrv_query($conn, $tsql, array(1, array($value, SQLSRV_PARAM_IN, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR))));
  
if ($stmt === false) {
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
else {  
    echo "The insertion was successfully executed.<br>";  
}  
  
// Retrieve the newly inserted data
//   
$stmt = sqlsrv_query($conn, "SELECT * FROM Table1");
$outValue = null;  
if ($stmt === false) {  
    echo "Error in statement execution.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data
//   
if (sqlsrv_fetch($stmt)) {  
    $outValue = sqlsrv_get_field($stmt, 1, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    echo "Value: " . $outValue . "<br>";
    if ($value !== $outValue) {
        echo "Data retrieved, \'$outValue\', is unexpected!<br>";
    }
}  
else {  
    echo "Error in fetching data.<br>";  
    die(print_r(sqlsrv_errors(), true));  
}  

// Free statement and connection resources
//   
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
```
<?php  
  
// PDO_SQLSRV Example:
//
// Setting locale for the script is only necessary if Latin 1 is not the default 
// in the environment
$locale = strtoupper(PHP_OS) === 'LINUX' ? 'en_US.ISO-8859-1' : 'en_US.ISO8859-1';
setlocale(LC_ALL, $locale);
        
$serverName = 'MyServer';
$database = 'Test';

try {
    $conn = new PDO("sqlsrv:Server=$serverName;Database=$database;", $uid, $pwd);
    $conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);
    
    // Set up the Transact-SQL query to create a test table
    //   
    $stmt = $conn->query("CREATE TABLE [Table1] ([c1_int] int, [c2_varchar] varchar(512))");
    
    // Insert data using parameters, $value being some ASCII string
    //
    $stmt = $conn->prepare("INSERT INTO [Table1] (c1_int, c2_varchar) VALUES (:var1, :var2)");
    $stmt->bindValue(1, 1);
    $stmt->bindParam(2, $value);
    $stmt->execute();
    
    // Retrieve and display the data
    //
    $stmt = $conn->query("SELECT * FROM [Table1]");
    $outValue = null;
    if ($row = $stmt->fetch()) {
        $outValue = $row[1];
        echo "Value: " . $outValue . "<br>";
        if ($value !== $outValue) {
            echo "Data retrieved, \'$outValue\', is unexpected!<br>";
        }
    }
} catch (PDOException $e) {
    echo $e->getMessage() . "<br>";
} finally {
    // Free statement and connection resources
    //
    unset($stmt);
    unset($conn);
}

?>  
```  

## <a name="see-also"></a>Vedere anche  
[Recupero di dati](../../connect/php/retrieving-data.md)  
[Uso dei dati UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[Aggiornamento dei dati &#40;Driver Microsoft per PHP per SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Applicazione di esempio &#40;Driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
