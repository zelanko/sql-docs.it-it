---
title: 'Procedura: eseguire transazioni | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transaction support
ms.assetid: f4643b85-f929-4919-8951-23394bc5bfa7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26ca7fbe56a17e1bf2a7c69b9e8c2dcd63073f87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936431"
---
# <a name="how-to-perform-transactions"></a>Procedura: Eseguire le transazioni
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Il driver SQLSRV dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] fornisce tre funzioni per l'esecuzione di transazioni:  
  
-   [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)  
  
-   [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)  
  
-   [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)  
  
Il driver PDO_SQLSRV fornisce tre metodi per l'esecuzione di transazioni:  
  
-   [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
-   [PDO::commit](../../connect/php/pdo-commit.md)  
  
-   [PDO::rollback](../../connect/php/pdo-rollback.md)  
  
Per un esempio, vedere [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) .  
  
Di seguito in questo argomento viene descritto come usare il driver SQLSRV per eseguire le transazioni.  
  
## <a name="remarks"></a>Remarks  
I passaggi principali per l'esecuzione di una transazione sono i seguenti:  
  
1.  Avviare la transazione con **sqlsrv_begin_transaction**.  
  
2.  Verificare l'esito positivo o negativo di ogni query inclusa nella transazione.  
  
3.  Se appropriato, eseguire il commit della transazione con **sqlsrv_commit**. In caso contrario, eseguire il rollback della transazione con **sqlsrv_rollback**. Dopo la chiamata a **sqlsrv_commit** o **sqlsrv_rollback** viene ripristinata la modalità autocommit per il driver.  
  
    I [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] sono in modalità autocommit per impostazione predefinita. Ciò significa che viene eseguito automaticamente il commit di tutte le query al completamento dell'operazione a meno che non siano state programmate come parte di una transazione esplicita usando **sqlsrv_begin_transaction**.  
  
    Se non viene eseguito il commit di una transazione esplicita tramite **sqlsrv_commit**, viene eseguito il rollback alla chiusura della connessione o al termine dello script.  
  
    Non usare Transact-SQL incorporato per l'esecuzione delle transazioni. Ad esempio, non eseguire un'istruzione con "BEGIN TRANSACTION" come query Transact-SQL per iniziare una transazione. Il comportamento transazionale previsto non può essere garantito quando si usa Transact-SQL incorporato per l'esecuzione delle transazioni.  
  
    Usare le funzioni **sqlsrv** elencate in precedenza per eseguire le transazioni.  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
L'esempio seguente esegue diverse query come parte di una transazione. Se tutte le query hanno esito positivo, viene eseguito il commit della transazione. Se una delle query ha esito negativo, viene eseguito il rollback della transazione.  
  
L'esempio tenta di eliminare un ordine di vendita dalla tabella *Sales.SalesOrderDetail* e di correggere i livelli di inventario del prodotto nella tabella *Product.ProductInventory* per ogni prodotto dell'ordine di vendita. Queste query vengono incluse in una transazione perché tutte le query devono essere completate correttamente per riflettere accuratamente lo stato degli ordini e la disponibilità del prodotto.  
  
La prima query dell'esempio recupera gli ID prodotto e le quantità per l'ID ordine di vendita specificato. Questa query non è inclusa nella transazione. Lo script viene tuttavia interrotto se la query ha esito negativo perché ID prodotto e quantità sono necessari per completare le query della transazione successiva.  
  
Le query che seguono (eliminazione dell'ordine di vendita e aggiornamento delle quantità di inventario del prodotto) sono parte della transazione.  
  
Nell'esempio si presuppone che SQL Server e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando si esegue l'esempio dalla riga di comando, tutto l'output viene scritto nel browser.  
  
### <a name="code"></a>codice  
  
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
  
/* Begin transaction. */  
if( sqlsrv_begin_transaction($conn) === false )   
{   
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set the Order ID.  */  
$orderId = 43667;  
  
/* Execute operations that are part of the transaction. Commit on  
success, roll back on failure. */  
if (perform_trans_ops($conn, $orderId))  
{  
     //If commit fails, roll back the transaction.  
     if(sqlsrv_commit($conn))  
     {  
         echo "Transaction committed.\n";  
     }  
     else  
     {  
         echo "Commit failed - rolling back.\n";  
         sqlsrv_rollback($conn);  
     }  
}  
else  
{  
     "Error in transaction operation - rolling back.\n";  
     sqlsrv_rollback($conn);  
}  
  
/*Free connection resources*/  
sqlsrv_close( $conn);  
  
/*----------------  FUNCTION: perform_trans_ops  -----------------*/  
function perform_trans_ops($conn, $orderId)  
{  
    /* Define query to update inventory based on sales order info. */  
    $tsql1 = "UPDATE Production.ProductInventory   
              SET Quantity = Quantity + s.OrderQty   
              FROM Production.ProductInventory p   
              JOIN Sales.SalesOrderDetail s   
              ON s.ProductID = p.ProductID   
              WHERE s.SalesOrderID = ?";  
  
    /* Define the parameters array. */  
    $params = array($orderId);  
  
    /* Execute the UPDATE statement. Return false on failure. */  
    if( sqlsrv_query( $conn, $tsql1, $params) === false ) return false;  
  
    /* Delete the sales order. Return false on failure */  
    $tsql2 = "DELETE FROM Sales.SalesOrderDetail   
              WHERE SalesOrderID = ?";  
    if(sqlsrv_query( $conn, $tsql2, $params) === false ) return false;  
  
    /* Return true because all operations were successful. */  
    return true;  
}  
?>  
```  
  
### <a name="comments"></a>Commenti  
Per porre l'attenzione sul comportamento delle transazioni, una parte della gestione degli errori consigliata non è inclusa nell'esempio. Per un'applicazione di produzione, è consigliabile controllare qualsiasi chiamata a una funzione **sqlsrv** per individuare eventuali errori e gestirli di conseguenza.
  
## <a name="see-also"></a>Vedere anche  
[Aggiornamento dei dati &#40;Driver Microsoft per PHP per SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Transazioni (Motore di database)](https://msdn.microsoft.com/library/ms190612.aspx)

[Informazioni sugli esempi di codice nella documentazione](../../connect/php/about-code-examples-in-the-documentation.md)  
  
