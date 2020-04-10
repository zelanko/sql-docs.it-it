---
title: 'Procedura: Gestire errori e avvisi usando il driver SQLSRV | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- errors and warnings
ms.assetid: fa231d60-4c06-4137-89e8-097c28638c5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0605fc5a0fc27abfbcd15c22d5553587eecb0349
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80916265"
---
# <a name="how-to-handle-errors-and-warnings-using-the-sqlsrv-driver"></a>Procedura: Gestire errori e avvisi usando il driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Per impostazione predefinita, il driver SQLSRV considera gli avvisi come errori. Una chiamata a una funzione **sqlsrv** che genera un errore o un avviso restituisce **false**. In questo argomento viene illustrato come disattivare questo comportamento predefinito e come gestire gli avvisi separatamente dagli errori.  
  
> [!NOTE]  
> Esistono alcune eccezioni al comportamento predefinito di gestione degli avvisi come errori. Gli avvisi che corrispondono ai valori SQLSTATE 01000, 01001, 01003 e 01S02 non vengono mai considerati come errori.  
  
## <a name="example"></a>Esempio  
L'esempio di codice seguente usa due funzioni definite dall'utente, **DisplayErrors** e **DisplayWarnings**, per la gestione degli errori e degli avvisi. L'esempio illustra la gestione separata di avvisi ed errori tramite le operazioni seguenti:  
  
1.  Disattiva il comportamento predefinito di gestione degli avvisi come errori.  
  
2.  Crea una stored procedure che aggiorna le ore di ferie del dipendente e restituisce le ore di ferie rimanenti come parametro di output. Quando le ore di ferie disponibili di un dipendente sono minori di zero, la stored procedure stampa un avviso.  
  
3.  Aggiorna le ore di ferie per più dipendenti effettuando una chiamata alla stored procedure per ogni dipendente e visualizza i messaggi che corrispondono a eventuali avvisi ed errori che si verificano.  
  
4.  Visualizza le ore di ferie rimanenti per ogni dipendente.  
  
Nella prima chiamata a una funzione **sqlsrv** ([sqlsrv_configure](../../connect/php/sqlsrv-configure.md)), gli avvisi vengono considerati come errori. Poiché gli avvisi vengono aggiunti alla raccolta degli errori, non è necessario controllare gli avvisi separatamente dagli errori. Nelle chiamate successive alle funzioni **sqlsrv** , tuttavia, gli avvisi non verranno considerati come errori e sarà pertanto necessario controllare in modo esplicito gli avvisi e gli errori.  
  
Si noti inoltre che il codice di esempio ricerca gli errori dopo ogni chiamata a una funzione **sqlsrv** . Questa è la procedura consigliata.  
  
L'esempio presuppone che SQL Server e il database [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) siano installati nel computer locale. Quando si esegue l'esempio dalla riga di comando, tutto l'output viene scritto nel browser. Quando l'esempio viene eseguito in una nuova installazione del database AdventureWorks, produce tre avvisi e i due errori. I primi due avvisi sono avvisi standard che vengono rilasciati quando ci si connette a un database. Il terzo avviso si verifica perché le ore di ferie disponibili di un dipendente vengono aggiornate a un valore minore di zero. Gli errori si verificano perché le ore di ferie disponibili di un dipendente vengono aggiornate a un valore inferiore a -40 ore violando un vincolo nella tabella.  
  
```  
<?php  
/* Turn off the default behavior of treating errors as warnings.  
Note: Turning off the default behavior is done here for demonstration  
purposes only. If setting the configuration fails, display errors and  
exit the script. */  
if( sqlsrv_configure("WarningsReturnAsErrors", 0) === false)  
{  
     DisplayErrors();  
     die;  
}  
  
/* Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
/* If the connection fails, display errors and exit the script. */  
if( $conn === false )  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Drop the stored procedure if it already exists. */  
$tsql1 = "IF OBJECT_ID('SubtractVacationHours', 'P') IS NOT NULL  
                DROP PROCEDURE SubtractVacationHours";  
$stmt1 = sqlsrv_query($conn, $tsql1);  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt1 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt1 );  
  
/* Create the stored procedure. */  
$tsql2 = "CREATE PROCEDURE SubtractVacationHours  
                  @EmployeeID int,  
                  @VacationHours smallint OUTPUT  
              AS  
                  UPDATE HumanResources.Employee  
                  SET VacationHours = VacationHours - @VacationHours  
                  WHERE EmployeeID = @EmployeeID;  
                  SET @VacationHours = (SELECT VacationHours    
                                       FROM HumanResources.Employee  
                                       WHERE EmployeeID = @EmployeeID);  
              IF @VacationHours < 0   
              BEGIN  
                PRINT 'WARNING: Vacation hours are now less than zero.'  
              END;";  
$stmt2 = sqlsrv_query( $conn, $tsql2 );  
  
/* If the query fails, display errors and exit the script. */  
if( $stmt2 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Free the statement resources. */  
sqlsrv_free_stmt( $stmt2 );  
  
/* Set up the array that maps employee ID to used vacation hours. */  
$emp_hrs = array (7=>4, 8=>5, 9=>8, 11=>50);  
  
/* Initialize variables that will be used as parameters. */  
$employeeId = 0;  
$vacationHrs = 0;  
  
/* Set up the parameter array. */  
$params = array(  
                 array(&$employeeId, SQLSRV_PARAM_IN),  
                 array(&$vacationHrs, SQLSRV_PARAM_INOUT)  
                );  
  
/* Define and prepare the query to subtract used vacation hours. */  
$tsql3 = "{call SubtractVacationHours(?, ?)}";  
$stmt3 = sqlsrv_prepare($conn, $tsql3, $params);  
  
/* If the statement preparation fails, display errors and exit the script. */  
if( $stmt3 === false)  
{  
     DisplayErrors();  
     die;  
}  
/* Display any warnings. */  
DisplayWarnings();  
  
/* Loop through the employee=>vacation hours array. Update parameter  
 values before statement execution. */  
foreach(array_keys($emp_hrs) as $employeeId)  
{  
     $vacationHrs = $emp_hrs[$employeeId];  
     /* Execute the query.  If it fails, display the errors. */  
     if( sqlsrv_execute($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /*Move to the next result returned by the stored procedure. */  
     if( sqlsrv_next_result($stmt3) === false)  
     {  
          DisplayErrors();  
          die;  
     }  
     /* Display any warnings. */  
     DisplayWarnings();  
  
     /* Display updated vacation hours. */  
     echo "EmployeeID $employeeId has $vacationHrs ";  
     echo "remaining vacation hours.\n";  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt3 );  
sqlsrv_close( $conn );  
  
/* ------------- Error Handling Functions --------------*/  
function DisplayErrors()  
{  
     $errors = sqlsrv_errors(SQLSRV_ERR_ERRORS);  
     foreach( $errors as $error )  
     {  
          echo "Error: ".$error['message']."\n";  
     }  
}  
  
function DisplayWarnings()  
{  
     $warnings = sqlsrv_errors(SQLSRV_ERR_WARNINGS);  
     if(!is_null($warnings))  
     {  
          foreach( $warnings as $warning )  
          {  
               echo "Warning: ".$warning['message']."\n";  
          }  
     }  
}  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Procedura: Configurare la gestione degli errori e degli avvisi usando il driver SQLSRV](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)

[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
