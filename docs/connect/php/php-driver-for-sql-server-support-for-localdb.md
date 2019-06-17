---
title: Supporto per LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 48c9955733672699e16cb4a00e28fa2f59717b80
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797090"
---
# <a name="support-for-localdb"></a>Supporto per LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB è una versione lightweight della [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cui è stato reso disponibile dal [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. In questo argomento viene discussa la modalità di connessione a un database in un'istanza del database locale.

## <a name="remarks"></a>Remarks

Per altre informazioni su LocalDB, incluse le procedure per installarlo e configurare l'istanza di Local DB, vedere la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] argomento della documentazione Online su [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB.

In breve, database locale consente di:

-   Uso **sqllocaldb.exe ho** per individuare il nome dell'istanza predefinita.

-   Usare la parola chiave della stringa di connessione **AttachDBFilename** per specificare a quale file di database si deve collegare il server. Quando si usa **AttachDBFilename**, se non viene specificato il nome del database con la parola chiave della stringa di connessione **Database**, il database sarà rimosso dall'istanza di Local DB quando l'applicazione viene chiusa.

-   Specificare un'istanza di Local DB nella stringa di connessione. Ad esempio, ecco un esempio di stringa di connessione SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    Successivamente è una stringa di connessione di esempio PDO_SQLSRV:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Se necessario, è possibile creare un'istanza del database locale con sqllocaldb.exe. È possibile utilizzare anche sqlcmd.exe per aggiungere e modificare i database in un'istanza del database locale. Ad esempio, `sqlcmd -S (localdb)\v11.0`. (Quando si esegue IIS, è necessario per l'esecuzione con l'account corretto per ottenere gli stessi risultati quando si esegue la riga di comando, vedere [utilizzo di LocalDB con IIS completo, parte 2: la proprietà dell'istanza](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) per altre informazioni.)

Di seguito sono esempio le stringhe di connessione usando il driver SQLSRV che si connettono a un database in un database locale di istanza denominata myInstance denominato:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Di seguito sono stringhe di connessione esempio Usa il driver PDO_SQLSRV che si connettono a un database in un database locale di istanza denominata myInstance denominato:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Per istruzioni sull'installazione di LocalDB, vedere la [documentazione di Local DB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Se si usa sqlcmd.exe per modificare i dati nell'istanza di LocalDB, sarà necessario il [utilità sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Vedere anche

[Connessione al server](../../connect/php/connecting-to-the-server.md)
