---
title: 'Procedura: Disabilitare più set di risultati attivi (MARS) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c5edf63a654b21d080e48f93c71553b8909ce8fd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993564"
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
  
## <a name="example"></a>Esempio  
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
  
## <a name="example"></a>Esempio  
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
  
