---
title: Supporto per local DB | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6da7f1aed956c8b2f5c71496c9c121f6006eabb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935953"
---
# <a name="support-for-localdb"></a>Supporto per LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Il database locale è una versione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] leggera di, disponibile a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]partire da. In questo argomento viene discussa la modalità di connessione a un database in un'istanza del database locale.

## <a name="remarks"></a>Remarks

Per ulteriori informazioni sul database locale, inclusa la modalità di installazione del database locale e la configurazione dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza del database locale [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , vedere l'argomento della documentazione online su Express local DB.

In breve, il database locale consente di:

-   Utilizzare **SqlLocalDB. exe** i per individuare il nome dell'istanza predefinita.

-   Usare la parola chiave della stringa di connessione **AttachDBFilename** per specificare a quale file di database si deve collegare il server. Quando si usa **AttachDBFilename**, se non viene specificato il nome del database con la parola chiave della stringa di connessione **Database**, il database sarà rimosso dall'istanza di Local DB quando l'applicazione viene chiusa.

-   Specificare un'istanza di Local DB nella stringa di connessione. Ad esempio, di seguito è riportato un esempio di stringa di connessione SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    Di seguito è illustrata una stringa di connessione PDO_SQLSRV di esempio:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Se necessario, è possibile creare un'istanza del database locale con sqllocaldb.exe. È possibile utilizzare anche sqlcmd.exe per aggiungere e modificare i database in un'istanza del database locale. Ad esempio, `sqlcmd -S (localdb)\v11.0`. Quando è in esecuzione in IIS, è necessario eseguire con l'account corretto per ottenere gli stessi risultati di quando si esegue dalla riga di comando. per ulteriori informazioni [, vedere Utilizzo del database locale con IIS completo, parte 2: proprietà dell'istanza](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) .

Di seguito sono riportate le stringhe di connessione di esempio che utilizzano il driver SQLSRV che si connettono a un database in un'istanza denominata di locale denominata istanza:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Di seguito sono riportate le stringhe di connessione di esempio che utilizzano il driver PDO_SQLSRV che si connettono a un database in un'istanza denominata di locale denominata istanza:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Per istruzioni sull'installazione del database locale, vedere la [documentazione del database locale](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Se si utilizza sqlcmd. exe per modificare i dati nell'istanza del database locale, sarà necessaria l' [utilità sqlcmd](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Vedere anche

[Connessione al server](../../connect/php/connecting-to-the-server.md)
