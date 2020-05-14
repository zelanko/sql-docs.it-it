---
title: Supporto del driver PHP per LocalDB
description: Informazioni su come i driver Microsoft per PHP per SQL Server supportano le connessioni alle istanze del database LocalDB.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d618706cd05796079904c971cdf7b0c32485c1d4
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886288"
---
# <a name="support-for-localdb"></a>Supporto per LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Local DB è una versione leggera di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibile a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. In questo argomento viene discussa la modalità di connessione a un database in un'istanza del database locale.

## <a name="remarks"></a>Osservazioni

Per altre informazioni su Local DB, inclusa la procedura per l'installazione di Local DB e la configurazione dell'istanza di Local DB, vedere la documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB.

In breve, Local DB consente di:

-   Usare **sqllocaldb.exe** per individuare il nome dell'istanza predefinita.

-   Usare la parola chiave della stringa di connessione **AttachDBFilename** per specificare a quale file di database si deve collegare il server. Quando si usa **AttachDBFilename**, se non viene specificato il nome del database con la parola chiave della stringa di connessione **Database**, il database sarà rimosso dall'istanza di Local DB quando l'applicazione viene chiusa.

-   Specificare un'istanza di Local DB nella stringa di connessione. Di seguito è riportata una stringa di connessione SQLSRV di esempio:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    Di seguito è riportata una stringa di connessione PDO_SQLSRV di esempio:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Se necessario, è possibile creare un'istanza del database locale con sqllocaldb.exe. È possibile utilizzare anche sqlcmd.exe per aggiungere e modificare i database in un'istanza del database locale. Ad esempio: `sqlcmd -S (localdb)\v11.0`. Durante l'esecuzione in IIS, è necessario usare l'account corretto per ottenere gli stessi risultati dell'esecuzione dalla riga di comando. Per altre informazioni, vedere [Using LocalDB with Full IIS, Part 2: Instance Ownership](/archive/blogs/sqlexpress/using-localdb-with-full-iis-part-2-instance-ownership).

Di seguito sono riportate le stringhe di connessione di esempio che usano il driver SQLSRV che si connettono a un database in un'istanza denominata di Local DB denominata myInstance:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Di seguito sono riportate le stringhe di connessione di esempio che usano il driver PDO_SQLSRV che si connettono a un database in un'istanza denominata di Local DB denominata myInstance:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Per istruzioni sull'installazione di Local DB, vedere la [documentazione di Local DB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Se si usa sqlcmd.exe per modificare i dati nell'istanza di Local DB, è necessaria l'[utilità sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Vedere anche

[Connessione al server](../../connect/php/connecting-to-the-server.md)
