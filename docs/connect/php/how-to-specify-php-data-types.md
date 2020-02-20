---
title: 'Procedura: Specificare i tipi di dati PHP | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: fee6e6b8-aad9-496b-84a2-18d2950470a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae00c01e962da05015a5132608915fc9d70258f4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67936391"
---
# <a name="how-to-specify-php-data-types"></a>Procedura: Specificare i tipi di dati PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Quando si usa il driver PDO_SQLSRV, è possibile specificare il tipo di dati PHP durante il recupero di dati dal server con PDOStatement::bindColumn e PDOStatement::bindParam. Per ulteriori informazioni, vedere [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) e [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md) .  
  
Di seguito sono elencati i passaggi principali per la specifica dei tipi di dati PHP durante il recupero dei dati dal server usando il driver SQLSRV:  
  
1.  Configurare ed eseguire una query Transact-SQL con [sqlsrv_query](../../connect/php/sqlsrv-query.md) o la combinazione di [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
2.  Rendere una riga di dati disponibile per la lettura con [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md).  
  
3.  Recuperare i dati di campo da una riga restituita usando [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) con il tipo di dati PHP desiderato specificato come terzo parametro facoltativo. Se il terzo parametro facoltativo viene omesso, i dati vengono restituiti in base ai tipi PHP predefiniti. Per informazioni sui tipi PHP restituiti predefiniti, vedere [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
    Per informazioni sulle costanti usate per specificare il tipo di dati PHP, vedere la sezione PHPTYPE in [Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
## <a name="example"></a>Esempio  
L'esempio seguente recupera le righe dalla tabella *Production.ProductReview* del database AdventureWorks. In ogni riga restituita il campo *ReviewDate* viene recuperato come stringa e il campo *Comments* viene recuperato come flusso. I dati del flusso vengono visualizzati usando la funzione [fpassthru](https://php.net/manual/en/function.fpassthru.php) PHP.  
  
Nell'esempio si presuppone che SQL Server e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando si esegue l'esempio dalla riga di comando, tutto l'output viene scritto nel browser.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. */  
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
                ReviewDate,  
                Rating,   
                Comments   
         FROM Production.ProductReview   
         WHERE ProductID = ?   
         ORDER BY ReviewDate DESC";  
  
/* Set the parameter value. */  
$productID = 709;  
$params = array( $productID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data. The first and third fields are  
retrieved according to their default types, strings. The second field  
is retrieved as a string with 8-bit character encoding. The fourth  
field is retrieved as a stream with 8-bit character encoding.*/  
while ( sqlsrv_fetch( $stmt))  
{  
   echo "Name: ".sqlsrv_get_field( $stmt, 0 )."\n";  
   echo "Date: ".sqlsrv_get_field( $stmt, 1,   
                       SQLSRV_PHPTYPE_STRING( SQLSRV_ENC_CHAR))."\n";  
   echo "Rating: ".sqlsrv_get_field( $stmt, 2 )."\n";  
   echo "Comments: ";  
   $comments = sqlsrv_get_field( $stmt, 3,   
                            SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));  
   fpassthru( $comments);  
   echo "\n";   
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Nell'esempio, il recupero del secondo campo (*ReviewDate*) come stringa mantiene la precisione ai millisecondi del tipo di dati DATETIME di SQL Server. Per impostazione predefinita, il tipo di dati DATETIME di SQL Server viene recuperato come oggetto DateTime PHP in cui viene persa la precisione ai millisecondi.  
  
Il recupero del quarto campo (*Comments*) come flusso è a scopo dimostrativo. Per impostazione predefinita, il tipo di dati SQL Server nvarchar(3850) viene recuperato come stringa, comportamento accettabile nella maggior parte dei casi.  
  
> [!NOTE]  
> La funzione [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) offre un modo per ottenere informazioni sui campi, incluse informazioni sul tipo, prima di eseguire una query.  
  
## <a name="see-also"></a>Vedere anche  
[Recupero di dati](../../connect/php/retrieving-data.md)

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)

[Procedura: Recuperare i parametri di output mediante il driver SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[Procedura: Recuperare i parametri di input e output usando il driver SQLSRV](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
