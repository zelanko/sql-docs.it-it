---
title: 'Procedura: inviare e recuperare dati ASCII in Linux e macOS (SQL) | Microsoft Docs'
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
manager: mbarwin
ms.openlocfilehash: 2fe78cc80cd7ca77f09465fb7d3e92482da7d008
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181152"
---
# <a name="how-to-send-and-retrieve-ascii-data-in-linux-and-macos"></a>Procedura: Inviare e recuperare dati ASCII in Linux e macOS 
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Questo articolo si presuppone che le impostazioni locali ASCII (non-UTF-8) sono state generate o installate nei sistemi Linux o macOS. 

Per inviare o recuperare set di caratteri ASCII per il server:  

1.  Se le impostazioni locali desiderata non sono il valore predefinito del sistema nell'ambiente in uso, assicurarsi che si richiama `setlocale(LC_ALL, $locale)` prima di effettuare la prima connessione. La funzione setlocale PHP modifica le impostazioni locali solo per lo script corrente e se richiamata dopo aver apportato la prima connessione, può essere ignorato.
 
2.  Quando si usa il driver SQLSRV, è possibile specificare `'CharacterSet' => SQLSRV_ENC_CHAR` come connessione opzione, ma in questo passaggio è facoltativo perché è il valore predefinito di codifica.

3.  Quando si usa il driver PDO_SQLSRV, esistono due modi. Innanzitutto, quando si effettua la connessione, impostare `PDO::SQLSRV_ATTR_ENCODING` al `PDO::SQLSRV_ENCODING_SYSTEM` (per un esempio di impostazione di un'opzione di connessione, vedere [PDO::__construct](../../connect/php/pdo-construct.md)). In alternativa, dopo aver connesso, aggiungere questa riga `$conn->setAttribute(PDO::SQLSRV_ATTR_ENCODING, PDO::SQLSRV_ENCODING_SYSTEM);` 
  
Quando si specifica la codifica di una risorsa di connessione (in SQLSRV) o un oggetto di connessione (PDO_SQLSRV), il driver presuppone che le altre stringhe di opzione di connessione usano la stessa codifica. Si presuppone, inoltre, che anche le stringhe di query e nome del server usino tale set di caratteri.  
  
La codifica per il driver PDO_SQLSRV predefinita è UTF-8 (PDO::SQLSRV_ENCODING_UTF8), a differenza del driver SQLSRV. Per altre informazioni su queste costanti, vedere [Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). 
  
## <a name="example"></a>Esempio  
Gli esempi seguenti illustrano come inviare e recuperare dati ASCII usando il driver PHP per SQL Server specificando determinate impostazioni locali prima di effettuare la connessione. Le impostazioni locali in varie piattaforme di Linux potrebbero essere denominate in modo diverso dalle stesse impostazioni locali in macOS. Ad esempio, le impostazioni locali US ISO-8859-1 (Latin 1) sono `en_US.ISO-8859-1` in Linux, mentre in macOS è il nome `en_US.ISO8859-1`.
  
Gli esempi presuppongono che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene installato in un server. Quando gli esempi vengono eseguiti dal browser, tutto l'output viene scritto nel browser.  
  
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
[Utilizzo dei dati UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)
[l'aggiornamento dei dati &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)  
[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Applicazione di esempio &#40;Driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
