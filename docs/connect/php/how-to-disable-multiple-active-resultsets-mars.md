---
title: 'Procedura: Disabilitare più set di risultati attivi (MARS)'
description: Informazioni su come disabilitare il supporto per più set di risultati attivi quando si usano i driver Microsoft per PHP per SQL Server
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 11ca08618f0b8d7675e8ec74ec259d4225d44aba
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/15/2020
ms.locfileid: "92080620"
---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>Procedura: Disabilitare più set di risultati attivi (MARS)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Se è necessario connettersi a un'origine dati SQL Server che non abilita più set di risultati attivi (MARS, Multiple Active Result Sets), è possibile usare l'opzione di connessione MultipleActiveResultSets per disabilitare o abilitare più set di risultati attivi.  
  
## <a name="procedure"></a>Procedura  
  
#### <a name="to-disable-mars-support"></a>Per disabilitare il supporto MARS  
  
-   Usare l'opzione di connessione seguente:  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    Se l'applicazione tenta di eseguire una query su una connessione con un set di risultati attivo aperto, il secondo tentativo di query restituirà le informazioni di errore seguenti:  
  
    La connessione non può elaborare questa operazione perché è presente un'istruzione con risultati in sospeso.  Per rendere disponibile la connessione per altre query recuperare tutti i risultati, annullare o liberare l'istruzione. Per altre informazioni sull'opzione di connessione MultipleActiveResultSets, vedere [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="sqlsrv-example"></a>Esempio di SQLSRV  
Nell'esempio seguente viene illustrato come disabilitare il supporto MARS usando il driver SQLSRV dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'MultipleActiveResultSets'=> false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="pdo_sqlsrv-example"></a>Esempio di PDO_SQLSRV  
L'esempio seguente illustra come disabilitare il supporto MARS usando il driver PDO_SQLSRV dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
```  
<?php  
// Connect to the local server using Windows Authentication and AdventureWorks database  
$serverName = "(local)";   
$database = "AdventureWorks";  
  
try {  
   $conn = new PDO(" sqlsrv:server=$serverName ; Database=$database ; MultipleActiveResultSets=false ", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
$conn = null;   
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Connessione al server](../../connect/php/connecting-to-the-server.md)  
  
