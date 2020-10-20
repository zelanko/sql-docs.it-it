---
title: 'Procedura: Inviare e recuperare dati UTF-8 con il supporto incorporato di UTF-8'
description: Informazioni su come inviare e recuperare dati con codifica UTF-8 usando il supporto per UTF-8 integrato nei driver per PHP.
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, UTF-8 encoded data
- converting data types
- updating data
ms.assetid: 366c57cf-352f-4202-8074-6ddce44880d1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7c914306258394bde91d64e5cb84665d62ab2b4
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081400"
---
# <a name="how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support"></a>Procedura: Inviare e recuperare dati UTF-8 con il supporto incorporato di UTF-8
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Se si usa il driver PDO_SQLSRV, è possibile specificare la codifica tramite l'attributo PDO::SQLSRV_ATTR_ENCODING. Per altre informazioni, vedere [Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
Nella parte restante di questo argomento viene illustrata la codifica con il driver SQLSRV.  
  
Per inviare dati con codifica UTF-8 al server o per recuperarli:  
  
1.  Assicurarsi che la colonna di origine o di destinazione sia di tipo **nchar** o **nvarchar**.  
  
2.  Specificare il tipo di PHP `SQLSRV_PHPTYPE_STRING('UTF-8')` nella matrice di parametri. In alternativa, specificare `"CharacterSet" => "UTF-8"` come opzione di connessione.  
  
    Quando si specifica un set di caratteri come parte delle opzioni di connessione, il driver presuppone che le altre stringhe delle opzioni di connessione usino lo stesso set di caratteri. Si presuppone, inoltre, che anche le stringhe di query e nome del server usino tale set di caratteri.  
  
È possibile passare UTF-8 o SQLSRV_ENC_CHAR a **CharacterSet**, ma non è possibile passare SQLSRV_ENC_BINARY. La codifica predefinita è SQLSRV_ENC_CHAR.  
  
## <a name="connection-example"></a>Esempio di connessione  
Nell'esempio seguente viene illustrato come inviare e recuperare dati con codificata UTF-8 specificando il set di caratteri UTF-8 quando si effettua la connessione. Nell'esempio viene aggiornata la colonna Comments della tabella Production.ProductReview per un ID revisione specificato. Nell'esempio vengono inoltre recuperati e visualizzati i dati appena aggiornati. Si noti che la colonna Comments è di tipo **nvarchar(3850)** . Si noti inoltre che, prima che vengano inviati al server, i dati vengono convertiti nella codifica UTF-8 usando la funzione PHP **utf8_encode**. Questa operazione viene eseguita solo per scopi dimostrativi. In uno scenario di applicazione reale, si inizierebbe già con dati con codifica UTF-8.  
  
Nell'esempio si presuppone che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando l'esempio viene eseguito dal browser, tutto l'output viene scritto nel browser.  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", "CharacterSet" => "UTF-8");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing 1, 2, 3, 4.  Testing.");  
$params1 = array(  
                  array( $comments, null ),  
                  array( $reviewID, null )  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field( $stmt2, 0 );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
Per informazioni sull'archiviazione di dati Unicode, vedere [Working with Unicode Data](/previous-versions/sql/sql-server-2008-r2/ms175180(v=sql.105)) (Uso di dati Unicode).  
  
## <a name="column-example"></a>Esempio di colonna  
L'esempio seguente è simile al primo, ma anziché specificare il set di caratteri UTF-8 nella connessione, in questo caso si illustra come specificare il set di caratteri UTF-8 nella colonna.  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing");  
$params1 = array(  
                  array($comments,  
                        SQLSRV_PARAM_IN,  
                        SQLSRV_PHPTYPE_STRING('UTF-8')  
                  ),  
                  array($reviewID)  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field($stmt2,   
                            0,   
                            SQLSRV_PHPTYPE_STRING('UTF-8')  
                           );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Recupero di dati](../../connect/php/retrieving-data.md)

[Utilizzo di dati ASCII in un ambiente non Windows](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)

[Aggiornamento dei dati &#40;Driver Microsoft per PHP per SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Applicazione di esempio &#40;Driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
