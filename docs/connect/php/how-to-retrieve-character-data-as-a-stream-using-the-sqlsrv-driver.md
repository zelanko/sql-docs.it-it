---
title: Recuperare di dati di tipo carattere come flusso usando il driver SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, as a character stream
- streaming data
ms.assetid: 3c0dbca4-abfc-4449-b133-66c819681840
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3b4a0fd48809d53cda18f2ceb4eaf1f435210e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936419"
---
# <a name="how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver"></a>Procedura: Recupero di dati di tipo carattere come flusso usando il driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Il recupero di dati come flusso è disponibile solo nel driver SQLSRV dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] e non è disponibile nel driver PDO_SQLSRV.  
  
Il driver SQLSRV sfrutta i flussi PHP per recuperare grandi quantità di dati dal server. Nell'esempio riportato in questo argomento viene illustrato come recuperare i dati di tipo carattere come flusso.  
  
## <a name="example"></a>Esempio  
Nell'esempio seguente viene recuperata una riga dalla tabella *Production.ProductReview* del database AdventureWorks. Il campo *Comments* della riga restituita viene recuperato come flusso e visualizzato tramite la funzione PHP [fpassthru](https://php.net/manual/function.fpassthru.php) .  
  
Il recupero di dati come flusso viene eseguito usando [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) e [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) specificando flusso di caratteri come tipo restituito. Il tipo restituito viene specificato usando la costante **SQLSRV_PHPTYPE_STREAM**. Per informazioni sulle costanti **sqlsrv**, vedere [Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
Nell'esempio si presuppone che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando si esegue l'esempio dalla riga di comando, tutto l'output viene scritto nel browser.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "SELECT ReviewerName,   
               CONVERT(varchar(32), ReviewDate, 107) AS [ReviewDate],  
               Rating,   
               Comments   
         FROM Production.ProductReview   
         WHERE ProductReviewID = ? ";  
  
/* Set the parameter value. */  
$productReviewID = 1;  
$params = array( $productReviewID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first three fields are retrieved  
as strings and the fourth as a stream with character encoding. */  
if(sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
echo "Date: ".sqlsrv_get_field( $stmt, 1 )."\n";  
echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
echo "Comments: ";  
$comments = sqlsrv_get_field( $stmt, 3,   
                             SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
fpassthru($comments);  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Poiché per i primi tre campi non è stato specificato alcun tipo restituito PHP, ogni campo viene restituito in base al proprio tipo PHP predefinito. Per informazioni sui tipi di dati PHP predefiniti, vedere [Default PHP Data Types](../../connect/php/default-php-data-types.md). Per informazioni su come specificare i tipi restituiti PHP, vedere [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="see-also"></a>Vedere anche  
[Recupero di dati](../../connect/php/retrieving-data.md)

[Recupero di dati come flusso usando il driver SQLSRV](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)  
  
