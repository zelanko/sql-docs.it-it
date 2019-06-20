---
title: Eseguire la migrazione di un database di SQL Server da Windows a Linux | Microsoft Docs
description: Questa esercitazione illustra come portare un database di SQL Server backup in Windows e ripristinarlo in un computer Linux che esegue SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 7d31490369b1562db91820d0e47f5935b5b42911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713131"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>Eseguire la migrazione di un database di SQL Server da Windows a Linux tramite backup e restore

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server di backup e ripristino configurazione di funzionalità è il modo consigliato per eseguire la migrazione di un database da SQL Server in Windows per SQL Server in Linux. In questa esercitazione verrà illustrata la procedura per spostare un database in Linux con il backup e ripristino tecniche.

> [!div class="checklist"]
> * Creare un file di backup in Windows con SQL Server Management Studio
> * Installare una shell Bash in Windows
> * Spostare il file di backup per Linux dalla shell di Bash
> * Ripristinare il file di backup in Linux con Transact-SQL
> * Eseguire una query per verificare la migrazione

È anche possibile creare un SQL Server gruppo di disponibilità AlwaysOn per la migrazione di un database di SQL Server da Windows a Linux. Visualizzare [sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md).

## <a name="prerequisites"></a>Prerequisiti

Per completare questa esercitazione sono necessari i prerequisiti seguenti:

* Computer Windows con il codice seguente:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) installato.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) installato.
  * Database di destinazione per eseguire la migrazione.

* Computer Linux con installati i componenti seguenti:
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), o [Ubuntu](quickstart-install-connect-ubuntu.md)) con gli strumenti da riga di comando.

## <a name="create-a-backup-on-windows"></a>Creare un backup in Windows

Esistono diversi modi per creare un file di backup di un database in Windows. La procedura seguente Usa SQL Server Management Studio (SSMS).

1. Avviare **SQL Server Management Studio** nel computer Windows.

1. Nella finestra di dialogo connessione, immettere **localhost**.

1. In Esplora oggetti, espandere **database**.

1. Fare clic su database di destinazione, selezionare **attività**, quindi fare clic su **eseguire il backup...** .

   ![Usare SSMS per creare un file di backup](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. Nel **Backup di Database** finestra di dialogo verificare che **tipo di Backup** viene **completo** e **backup su** è **disco**. Prendere nota del nome e percorso del file. Ad esempio, un database denominato **YourDB** in SQL Server 2016 ha un percorso di backup predefinito di `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`.

1. Fare clic su **OK** per eseguire il backup del database.

> [!NOTE]
> Un'altra opzione consiste nell'eseguire una query Transact-SQL per creare il file di backup. Il comando Transact-SQL seguente esegue le stesse azioni come la procedura precedente per un database denominato **YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>Installare una shell Bash in Windows

Per ripristinare il database, è innanzitutto necessario trasferire il file di backup dal computer Windows per computer Linux di destinazione. In questa esercitazione è spostare il file di Linux da una shell Bash (finestra del terminale) in esecuzione su Windows.

1. Installare una shell Bash nel computer Windows che supporta il **scp** (proteggere copia) e **ssh** comandi (account di accesso remoto). Due esempi:

   * Il [sottosistema Windows per Linux](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * La Shell Git Bash ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. Aprire una sessione Bash in Windows.

## <a id="scp"></a> Copiare il file di backup in Linux

1. Nella sessione di Bash, passare alla directory contenente il file di backup. Ad esempio:

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. Usare la **scp** comando per trasferire il file in computer Linux di destinazione. I trasferimenti di esempio seguenti **YourDB.bak** nella home directory del *user1* nel server Linux con un indirizzo IP *192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![comando SCP](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> Sono disponibili alternative all'uso di scp per il trasferimento di file. Uno consiste nell'usare [Samba](https://help.ubuntu.com/community/Samba) per configurare una condivisione di rete SMB tra Windows e Linux. Per una procedura dettagliata in Ubuntu, vedere [come creare una condivisione di rete tramite Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!). Una volta stabilita, è possibile accedervi come un file di rete condivisione da Windows, ad esempio  **\\ \\machinenameorip\\condividere**.

## <a name="move-the-backup-file-before-restoring"></a>Spostare il file di backup prima del ripristino

A questo punto, il file di backup è nel server Linux nella home directory dell'utente. Prima di ripristinare il database a SQL Server, è necessario inserire il backup in una sottodirectory della **/var/opt/mssql**.

1. Nella stessa sessione di Windows di Bash, connettersi in remoto al computer Linux con destinazione **ssh**. Nell'esempio seguente si connette al computer Linux **192.0.2.9** come utente **user1**.

   ```bash
   ssh user1@192.0.2.9
   ```

   Si stanno eseguendo comandi nel server Linux remoto.

1. Attivare la modalità utente con privilegi avanzati.

   ```bash
   sudo su
   ```

1. Creare una nuova directory di backup. Il parametro -p non esegue alcuna operazione se la directory esiste già.

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. Spostare il file di backup in tale directory. Nell'esempio seguente, il file di backup si trova nella home directory dei *user1*. Modificare il comando per corrispondere al nome file e percorso del file di backup.

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. Esci dalla modalità utente con privilegi avanzati.

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>Ripristinare il database in Linux

Per ripristinare il backup del database, è possibile usare la **RESTORE DATABASE** comando Transact-SQL (TQL).

> [!NOTE]
> La procedura seguente usa il **sqlcmd** dello strumento. Se non è ancora stato installazione gli strumenti di SQL Server, vedere [gli strumenti da riga di comando di installazione di SQL Server in Linux](sql-server-linux-setup-tools.md).

1. Nel stesso terminale, avviare **sqlcmd**. Nell'esempio seguente si connette all'istanza di SQL Server locale con il **SA** utente. Immettere la password quando richiesto oppure specificare la password tramite l'aggiunta di **-P** parametro.

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. Nel `>1` richiesto, immettere quanto segue **Ripristina DATABASE** comando, premere INVIO dopo ogni riga (è possibile copiare e incollare l'intero comando su più righe in una sola volta). Sostituire tutte le occorrenze di `YourDB` con il nome del database.

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   Viene visualizzato un messaggio che è stato ripristinato il database.

   `RESTORE DATABASE` può restituire un errore simile al seguente:

   ```bash
   File 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.
   Msg 5133, Level 16, State 1, Server servername, Line 1
   Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).
   ```
   
   In questo caso, il database contiene file secondari. Se questi file non vengono specificati nel `MOVE` clausola di `RESTORE DATABASE`, la procedura di ripristino tenterà di crearli nello stesso percorso del server originale. 

   È possibile elencare tutti i file inclusi nel backup:
   ```sql
   RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   GO
   ```
   È necessario ottenere un elenco, come quello riportato di seguito (elenco solo le prime due colonne):
   ```sql
   LogicalName         PhysicalName                                                                 ..............
   ----------------------------------------------------------------------------------------------------------------------
   YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............
   YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............
   YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............
   YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............
   ```
   
   È possibile usare questo elenco per creare `MOVE` clausole per i file aggiuntivi. In questo esempio, il `RESTORE DATABASE` è:

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',
   MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```


1. Verificare il ripristino elencando tutti i database nel server. Il database ripristinato deve essere elencato.

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. Eseguire le altre query sul database migrato. Il comando seguente cambia contesto per il **YourDB** seleziona le righe da una delle relative tabelle e database.

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. Dopo aver usando **sqlcmd**, tipo `exit`.

1. Dopo aver lavorare in remoto **ssh** sessione, digitare `exit` nuovamente.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato descritto come eseguire il backup di un database in Windows e spostarlo in un server Linux che esegue SQL Server. Si è appreso come a:
> [!div class="checklist"]
> * Usare SQL Server Management Studio e Transact-SQL per creare un file di backup in Windows
> * Installare una shell Bash in Windows
> * Uso **scp** per spostare i file di backup da Windows a Linux
> * Uso **ssh** per connettersi in remoto al computer Linux
> * Rilocare il file di backup per la preparazione per il ripristino
> * Uso **sqlcmd** per eseguire i comandi Transact-SQL
> * Ripristinare il backup di database con il **RESTORE DATABASE** comando 
> * Eseguire la query per verificare la migrazione

Successivamente, è possibile esplorare altri scenari di migrazione per SQL Server in Linux. 

> [!div class="nextstepaction"]
>[Eseguire la migrazione di database a SQL Server in Linux](sql-server-linux-migrate-overview.md)
