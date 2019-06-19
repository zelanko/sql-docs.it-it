---
title: Eseguire il backup e ripristino dei database di SQL Server in Linux | Microsoft Docs
description: Informazioni su come eseguire il backup e ripristino dei database di SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: f07885aaef22da63d1c94e669db17e7536ccc933
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713342"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Backup e ripristino di database di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

È possibile eseguire i backup dei database di SQL Server 2017 in Linux con gli stessi strumenti come altre piattaforme. In un server Linux, è possibile usare **sqlcmd** per connettersi a SQL Server ed eseguire i backup. Da Windows, è possibile connettersi a SQL Server in Linux e vengono eseguiti backup con l'interfaccia utente. La funzionalità di backup è lo stesso più piattaforme. Ad esempio, è possibile eseguire il backup database in locale, in unità remote o a [servizio di archiviazione Blob di Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-to-url.md).

## <a name="backup-a-database"></a>Effettuare il backup di un database

Nell'esempio seguente **sqlcmd** si connette all'istanza di SQL Server locale e richiede una procedura completa di backup di un database utente denominato `demodb`.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

Quando si esegue il comando, SQL Server verrà richiesto di immettere una password. Dopo avere immesso la password, la shell verrà restituiti i risultati dello stato di avanzamento backup. Ad esempio:

```
Password:
10 percent processed.
21 percent processed.
32 percent processed.
40 percent processed.
51 percent processed.
61 percent processed.
72 percent processed.
80 percent processed.
91 percent processed.
Processed 296 pages for database 'demodb', file 'demodb' on file 1.
100 percent processed.
Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.
BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).
```

### <a name="backup-the-transaction-log"></a>Eseguire il backup del log delle transazioni

Se il database nel modello di recupero con registrazione completa, è possibile inoltre rendere i backup del log delle transazioni per le opzioni di ripristino più granulare. Nell'esempio riportato di seguito **sqlcmd** si connette all'istanza di SQL Server locale ed esegue il backup un log delle transazioni.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>Ripristinare un database

Nell'esempio seguente **sqlcmd** si connette all'istanza locale di SQL Server e ripristina il database demodb. Si noti che il `NORECOVERY` opzione viene usata per consentire altri ripristini di file di backup del log. Se non si prevede di ripristinare i file di log aggiuntivi, rimuovere il `NORECOVERY` opzione.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> Se accidentalmente, utilizzare l'opzione NORECOVERY ma non dispongono di backup di file di log aggiuntivi, eseguire il comando `RESTORE DATABASE demodb` senza parametri aggiuntivi. Questo termine del ripristino e lascia il database operativo.

### <a name="restore-the-transaction-log"></a>Ripristinare il log delle transazioni

Il comando seguente ripristina il backup del log delle transazioni precedenti.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Backup e ripristino con SQL Server Management Studio (SSMS)

È possibile utilizzare SQL Server Management Studio da un computer Windows per connettersi a un database di Linux ed eseguire un backup tramite l'interfaccia utente.

>[!NOTE] 
> Usare la versione più recente di SSMS per connettersi a SQL Server. Per scaricare e installare la versione più recente, vedere [scaricare SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Per altre informazioni su come usare SQL Server Management Studio, vedere [usare SSMS per gestire SQL Server in Linux](sql-server-linux-manage-ssms.md).

La procedura seguente illustra un backup con SQL Server Management Studio. 

1. Avviare SSMS e connettersi al server in SQL Server 2017 in Linux.

1. In Esplora oggetti fare doppio clic sul database, fare clic su **attività**, quindi fare clic su **eseguire il backup...** .

1. Nel **Backup di Database** finestra di dialogo, verificare i parametri e opzioni, quindi scegliere **OK**.
 
SQL Server viene completato il backup del database.

### <a name="restore-with-sql-server-management-studio-ssms"></a>Ripristino con SQL Server Management Studio (SSMS) 

I passaggi seguenti consentono di eseguire il ripristino di un database con SSMS.

1. In SSMS fare clic sul **database** e fare clic su **ripristino di database...** . 

1. Sotto **origine** fare clic su **dispositivo:** e quindi fare clic sui puntini di sospensione (...).

1. Individuare il file di backup di database e fare clic su **OK**. 

1. Sotto **piano di ripristino**, verificare le impostazioni e file di backup. Fare clic su **OK**. 

1. SQL Server Ripristina il database. 

## <a name="see-also"></a>Vedere anche

* [Creare un Backup completo del Database (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [Eseguire il backup di un Log delle transazioni (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [Backup di SQL Server nell'URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
