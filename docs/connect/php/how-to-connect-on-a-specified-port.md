---
title: 'Procedura: Connettersi a una porta specificata | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: af055a73904bb8feec92fb2afe93df064a09ab23
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015056"
---
# <a name="how-to-connect-on-a-specified-port"></a>Procedura: Connettersi a una porta specificata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In questo argomento viene descritto come connettersi a SQL Server mediante una porta specifica con i [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
### <a name="to-connect-on-a-specified-port"></a>Per connettersi a una porta specifica  
  
1.  Verificare la porta del server configurata per accettare le connessioni. Per informazioni sulla configurazione di un server in modo che accetti le connessioni su una porta specificata, vedere [Procedura: Configurare un server per l'attesa su una porta TCP specifica (Gestione configurazione SQL Server)](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
2.  Aggiungere la porta desiderata al parametro *$serverName* della funzione [sqlsrv_connect](../../connect/php/sqlsrv-connect.md). Separare il nome del server e la porta con una virgola. Ad esempio, le righe di codice seguente usano il driver SQLSRV per illustrare come connettersi a un server denominato *myServer* sulla porta 1521:  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    Le righe di codice seguente usano il driver PDO_SQLSRV per illustrare come connettersi a un server denominato *myServer* sulla porta 1521:  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>Vedere anche  
[Connessione al server](../../connect/php/connecting-to-the-server.md)

[Guida alla programmazione per i driver Microsoft per PHP per SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Introduzione ai driver Microsoft per PHP per SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Guida di riferimento del driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
