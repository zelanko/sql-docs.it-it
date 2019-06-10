---
title: 'Procedura: Recuperare dati binari come flusso usando il driver SQLSRV | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, as a binary stream
- streaming data
ms.assetid: cd8d6382-abe6-48ee-9d10-4e6c52c0cb9a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e4bf2ae4330a98d810d0d3291f0045834b8927d3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799333"
---
# <a name="how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver"></a>Procedura: Recuperare dati binari come flusso usando il driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Il recupero di dati come flusso è disponibile solo nel driver SQLSRV dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] e non è disponibile nel driver PDO_SQLSRV.  
  
I [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] sfruttano i flussi PHP per recuperare grandi quantità di dati binari dal server. In questo argomento viene illustrato come recuperare i dati binari come flusso.  
  
L'uso dei flussi per il recupero dei dati binari, ad esempio di immagini, consente di evitare l'uso di grandi quantità di memoria di script recuperando blocchi di dati anziché caricando l'intero oggetto nella memoria di script.  
  
## <a name="example"></a>Esempio  
Nell'esempio seguente vengono recuperati dati binari, in questo caso un'immagine, dalla tabella *Production.ProductPhoto* del database AdventureWorks. L'immagine viene recuperata come flusso e visualizzata nel browser.  
  
Il recupero dei dati dell'immagine come flusso viene eseguito usando [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) e [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) specificando flusso binario come tipo restituito. Il tipo restituito viene specificato usando la costante **SQLSRV_PHPTYPE_STREAM**. Per informazioni sulle costanti **sqlsrv**, vedere [Costanti &#40;driver Microsoft per PHP per SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
Nell'esempio si presuppone che SQL Server e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando l'esempio viene eseguito dal browser, tutto l'output viene scritto nel browser.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
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
$tsql = "SELECT LargePhoto   
         FROM Production.ProductPhoto   
         WHERE ProductPhotoID = ?";  
  
/* Set the parameter values and put them in an array. */  
$productPhotoID = 70;  
$params = array( $productPhotoID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data.  
The return data is retrieved as a binary stream. */  
if ( sqlsrv_fetch( $stmt ) )  
{  
   $image = sqlsrv_get_field( $stmt, 0,   
                      SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_BINARY));  
   header("Content-Type: image/jpg");  
   fpassthru($image);  
}  
else  
{  
     echo "Error in retrieving data.</br>";  
     die(print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
La specifica del tipo restituito nell'esempio mostra come specificare il tipo restituito PHP come flusso binario. Tecnicamente non è necessario nell'esempio perché il campo *LargePhoto* è del tipo SQL Server varbinary(max), che viene restituito come flusso binario per impostazione predefinita. Per informazioni sui tipi di dati PHP predefiniti, vedere [Default PHP Data Types](../../connect/php/default-php-data-types.md). Per informazioni su come specificare i tipi restituiti PHP, vedere [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="see-also"></a>Vedere anche  
[Recupero di dati](../../connect/php/retrieving-data.md)

[Recupero di dati come flusso usando il driver SQLSRV](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)  
  
