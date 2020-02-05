---
title: Backup e ripristino di database SQL Server in Linux
description: Informazioni su come eseguire il backup e il ripristino di database SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: 88ef620a24bc2ce623ea6fb072871dadeffbcf6d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68823110"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>Backup e ripristino di database SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

È possibile eseguire il backup dei database da SQL Server 2017 in Linux con molte opzioni diverse. In un server Linux, per connettersi a SQL Server ed eseguire backup è possibile usare **sqlcmd**. Da Windows è possibile connettersi a SQL Server in Linux ed eseguire backup tramite l'interfaccia utente. La funzionalità di backup è identica in tutte le piattaforme. È ad esempio possibile eseguire il backup di database in locale, in unità remote o nel [servizio di archiviazione BLOB di Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-to-url.md).

## <a name="backup-a-database"></a>Eseguire il backup di un database

Nell'esempio seguente, **sqlcmd** si connette all'istanza di SQL Server locale ed esegue un backup completo di un database utente denominato `demodb`.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

Quando si esegue il comando, SQL Server richiede una password. Dopo l'immissione della password, la shell restituisce i risultati dello stato del backup. Ad esempio:

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

Se il database è nel modello di recupero con registrazione completa, è anche possibile creare backup del log delle transazioni per avere opzioni di ripristino più granulari. Nell'esempio seguente, **sqlcmd** si connette all'istanza di SQL Server locale ed esegue il backup del log delle transazioni.

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>Ripristinare un database

Nell'esempio seguente, **sqlcmd** si connette all'istanza locale di SQL Server e ripristina il database demodb. Si noti che viene usata l'opzione `NORECOVERY` per consentire operazioni di ripristino aggiuntive di backup dei file di log. Se non si prevede di ripristinare altri file di log, rimuovere l'opzione `NORECOVERY`.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> Se si usa accidentalmente NORECOVERY senza avere il backup di altri file di log, eseguire il comando `RESTORE DATABASE demodb` senza parametri aggiuntivi. Questa operazione termina il ripristino e lascia operativo il database.

### <a name="restore-the-transaction-log"></a>Ripristinare il log delle transazioni

Il comando seguente ripristina il backup del log delle transazioni precedente.

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>Backup e ripristino con SQL Server Management Studio (SSMS)

È possibile usare SSMS da un computer Windows per connettersi a un database Linux ed eseguirne il backup tramite l'interfaccia utente.

>[!NOTE] 
> Per connettersi a SQL Server, usare la versione di SSMS più recente. Per scaricare e installare la versione più recente, vedere [Scaricare SSMS](../ssms/download-sql-server-management-studio-ssms.md). Per altre informazioni sull'uso di SSMS, vedere [Usare SSMS per gestire SQL Server in Linux](sql-server-linux-manage-ssms.md).

La procedura seguente illustra in dettaglio l'esecuzione di un backup con SSMS. 

1. Avviare SSMS e connettersi al server in SQL Server 2017 in Linux.

1. In Esplora oggetti, fare clic con il pulsante destro del mouse sul database, fare clic su **Attività** e quindi su **Backup...** .

1. Nella finestra di dialogo **Backup database** verificare i parametri e le opzioni e fare clic su **OK**.
 
SQL Server completerà il backup del database.

### <a name="restore-with-sql-server-management-studio-ssms"></a>Eseguire il ripristino con SQL Server Management Studio (SSMS) 

La procedura seguente illustra in dettaglio il ripristino di un database con SSMS.

1. In SSMS fare clic con il pulsante destro del mouse su **Database** e fare clic su **Ripristina database..** . 

1. In **Origine** fare clic su **Dispositivo:** e quindi fare clic sui puntini (...).

1. Individuare il file di backup del database e fare clic su **OK**. 

1. In **Piano di ripristino** verificare il file e le impostazioni del backup. Fare clic su **OK**. 

1. SQL Server ripristina il database. 

## <a name="see-also"></a>Vedere anche

* [Creare un backup completo del database (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [Backup di un log delle transazioni (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [Backup di SQL Server nell'URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
