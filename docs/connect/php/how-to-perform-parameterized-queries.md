---
title: 'Procedura: eseguire query con parametri | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data
- parameterized queries
ms.assetid: dc7d0ede-a9b6-4ce2-977e-4d1e7ec2131c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e406d64bd8c56b467c9b331eb4aef132dc0cc67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993499"
---
# <a name="how-to-perform-parameterized-queries"></a>Procedura: Eseguire query con parametri
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In questo argomento viene descritto come usare i [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] per eseguire una query con parametri.  
  
I passaggi per l'esecuzione di una query con parametri sono fondamentalmente quattro:  
  
1.  Inserire punti interrogativi (?) come segnaposto di parametri nella stringa Transact-SQL che corrisponde alla query da eseguire.  
  
2.  Inizializzare o aggiornare le variabili PHP che corrispondono ai segnaposto della query Transact-SQL.  
  
3.  Usare le variabili PHP del passaggio 2 per creare o aggiornare una matrice di valori di parametri che corrispondono ai segnaposto della stringa di Transact-SQL. I valori dei parametri nella matrice devono essere nello stesso ordine dei segnaposti destinati a rappresentarli.
  
4.  Eseguire la query:  
  
    -   Se si usa il driver SQLSRV, usare [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)/[sqlsrv_execute](../../connect/php/sqlsrv-execute.md).  
  
    -   Se si usa il driver PDO_SQLSRV, eseguire la query con [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md). Gli argomenti relativi a [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md) includono esempi di codice.  
  
Nella parte rimanente di questo argomento sono descritte le query con parametri con il driver SQLSRV.  
  
> [!NOTE]  
> I parametri sono associati in modo implicito tramite **sqlsrv_prepare**. Ciò significa che se una query con parametri viene preparata usando **sqlsrv_prepare** e i valori della matrice di parametri vengono aggiornati, alla successiva esecuzione della query verranno usati i valori aggiornati. Per altre informazioni, vedere il secondo esempio in questo argomento.  
  
## <a name="example"></a>Esempio  
L'esempio seguente aggiorna la quantità di un ID prodotto specificato nella tabella *Production.ProductInventory* del database AdventureWorks. Quantità e ID prodotto sono parametri nella query UPDATE.  
  
L'esempio esegue quindi una query nel database per verificare che la quantità sia stata aggiornata correttamente. ID prodotto è un parametro nella query SELECT.  
  
Nell'esempio si presuppone che SQL Server e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando si esegue l'esempio dalla riga di comando, tutto l'output viene scritto nel browser.  
  
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
  
/* Define the Transact-SQL query.  
Use question marks as parameter placeholders. */  
$tsql1 = "UPDATE Production.ProductInventory   
          SET Quantity = ?   
          WHERE ProductID = ?";  
  
/* Initialize $qty and $productId */  
$qty = 10; $productId = 709;  
  
/* Execute the statement with the specified parameter values. */  
$stmt1 = sqlsrv_query( $conn, $tsql1, array($qty, $productId));  
if( $stmt1 === false )  
{  
     echo "Statement 1 could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement resources. */  
sqlsrv_free_stmt( $stmt1);  
  
/* Now verify the updated quantity.  
Use a question mark as parameter placeholder. */  
$tsql2 = "SELECT Quantity   
          FROM Production.ProductInventory  
          WHERE ProductID = ?";  
  
/* Execute the statement with the specified parameter value.  
Display the returned data if no errors occur. */  
$stmt2 = sqlsrv_query( $conn, $tsql2, array($productId));  
if( $stmt2 === false )  
{  
     echo "Statement 2 could not be executed.\n";  
     die( print_r(sqlsrv_errors(), true));  
}  
else  
{  
     $qty = sqlsrv_fetch_array( $stmt2);  
     echo "There are $qty[0] of product $productId in inventory.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
L'esempio precedente usa la funzione **sqlsrv_query** per eseguire le query. Questa funzione è utile per l'esecuzione di query singole poiché esegue sia la preparazione delle istruzioni che l'esecuzione. Per rieseguire una query con valori di parametri diversi è consigliabile usare una combinazione di **sqlsrv_prepare**/**sqlsrv_execute**. Per un esempio di riesecuzione di una query con valori di parametri diversi, vedere l'esempio successivo.  
  
## <a name="example"></a>Esempio  
L'esempio seguente mostra l'associazione implicita delle variabili durante l'uso della funzione **sqlsrv_prepare** . L'esempio inserisce più ordini di vendita nella tabella *Sales.SalesOrderDetail* . La matrice *$params* viene associata all'istruzione ( *$stmt*) quando viene effettuata la chiamata a **sqlsrv_prepare**. Prima di ogni esecuzione di una query che inserisce un nuovo ordine di vendita nella tabella, la matrice *$params* viene aggiornata con i nuovi valori corrispondenti ai dettagli dell'ordine di vendita. La successiva esecuzione della query usa i nuovi valori di parametri.  
  
Nell'esempio si presuppone che SQL Server e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando si esegue l'esempio dalla riga di comando, tutto l'output viene scritto nel browser.  
  
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
  
$tsql = "INSERT INTO Sales.SalesOrderDetail (SalesOrderID,   
                                             OrderQty,   
                                             ProductID,   
                                             SpecialOfferID,   
                                             UnitPrice)  
         VALUES (?, ?, ?, ?, ?)";  
  
/* Each sub array here will be a parameter array for a query.  
The values in each sub array are, in order, SalesOrderID, OrderQty,  
 ProductID, SpecialOfferID, UnitPrice. */  
$parameters = array( array(43659, 8, 711, 1, 20.19),  
                     array(43660, 6, 762, 1, 419.46),  
                     array(43661, 4, 741, 1, 818.70)  
                    );  
  
/* Initialize parameter values. */  
$orderId = 0;  
$qty = 0;  
$prodId = 0;  
$specialOfferId = 0;  
$price = 0.0;  
  
/* Prepare the statement. $params is implicitly bound to $stmt. */  
$stmt = sqlsrv_prepare( $conn, $tsql, array( &$orderId,  
                                             &$qty,  
                                             &$prodId,  
                                             &$specialOfferId,  
                                             &$price));  
if( $stmt === false )  
{  
     echo "Statement could not be prepared.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute a statement for each set of params in $parameters.  
Because $params is bound to $stmt, as the values are changed, the  
new values are used in the subsequent execution. */  
foreach( $parameters as $params)  
{  
     list($orderId, $qty, $prodId, $specialOfferId, $price) = $params;  
     if( sqlsrv_execute($stmt) === false )  
     {  
          echo "Statement could not be executed.\n";  
          die( print_r( sqlsrv_errors(), true));  
     }  
     else  
     {  
          /* Verify that the row was successfully inserted. */  
          echo "Rows affected: ".sqlsrv_rows_affected( $stmt )."\n";  
     }  
}  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Conversione dei tipi di dati](../../connect/php/converting-data-types.md)

[Considerazioni sulla sicurezza per i driver Microsoft per PHP per SQL Server](../../connect/php/security-considerations-for-php-sql-driver.md)

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)

[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)  
  
