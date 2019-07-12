---
title: Creare ed eseguire i processi di SQL Server in Linux
description: Questa esercitazione illustra come eseguire il processo di SQL Server Agent in Linux.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: 436d7af77557863c647b172062149d26a01ae326
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834763"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Creare ed eseguire i processi di SQL Server Agent in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Processi di SQL Server vengono usati per eseguire regolarmente la stessa sequenza di comandi nel database di SQL Server. Questa esercitazione offre un esempio di come creare un processo di SQL Server Agent in Linux tramite Transact-SQL e SQL Server Management Studio (SSMS).

> [!div class="checklist"]
> * Installare SQL Server Agent in Linux
> * Creare un nuovo processo per eseguire i backup giornalieri di database
> * Pianificare ed eseguire il processo
> * Eseguire gli stessi passaggi in SQL Server Management Studio (facoltativo)

Per problemi noti relativi a SQL Server Agent in Linux, vedere la [note sulla versione](sql-server-linux-release-notes.md).

## <a name="prerequisites"></a>Prerequisiti

Per completare questa esercitazione sono necessari i prerequisiti seguenti:

* Computer Linux con i seguenti prerequisiti:
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), o [Ubuntu](quickstart-install-connect-ubuntu.md)) con gli strumenti da riga di comando.

I prerequisiti seguenti sono facoltativi:

* Computer Windows con SQL Server Management Studio:
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) per passaggi facoltativi di SQL Server Management Studio.

## <a name="enable-sql-server-agent"></a>Abilitare SQL Server Agent

Per usare SQL Server Agent in Linux, è innanzitutto necessario abilitare SQL Server Agent in un computer che dispone già di SQL Server installata.

1. Per abilitare SQL Server Agent, attenersi alla procedura seguente.
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. Riavviare SQL Server con il comando seguente:
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> A partire da SQL Server 2017 CU4, SQL Server Agent è incluso con il **mssql-server** pacchetto ed è disabilitata per impostazione predefinita. Per configurare l'agente prima della visita, CU4 [installare SQL Server Agent in Linux](sql-server-linux-setup-sql-agent.md).

## <a name="create-a-sample-database"></a>Creare un database di esempio

Usare la procedura seguente per creare un database di esempio denominato **SampleDB**. Questo database viene utilizzato per il processo di backup giornaliero.

1. Nel computer Linux, aprire una finestra del terminale bash.

1. Uso **sqlcmd** per eseguire t-SQL **CREATE DATABASE** comando.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. Verificare che il database viene creato elencando i database nel server.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>Creare un processo con Transact-SQL

La procedura seguente crea un processo di SQL Server Agent in Linux con i comandi Transact-SQL. Il processo viene eseguito un backup del database di esempio, giornaliero **SampleDB**.

> [!TIP]
> È possibile utilizzare qualsiasi client di T-SQL per eseguire questi comandi. In Linux, ad esempio, è possibile usare [sqlcmd](sql-server-linux-setup-tools.md) oppure [Visual Studio Code](sql-server-linux-develop-use-vscode.md). Da un Server remoto di Windows, è anche possibile eseguire query in SQL Server Management Studio (SSMS) o usare l'interfaccia dell'interfaccia utente per la gestione dei processi, che è descritti nella sezione successiva.

1. Uso [sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md) per creare un processo denominato `Daily SampleDB Backup`.

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. Chiamare [sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md) per creare un passaggio di processo che crea un backup del `SampleDB` database.

   ```sql
   -- Adds a step (operation) to the job
   EXEC sp_add_jobstep
      @job_name = N'Daily SampleDB Backup',
      @step_name = N'Backup database',
      @subsystem = N'TSQL',
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
         N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
         NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',
      @retry_attempts = 5,
      @retry_interval = 5 ;
   GO
   ```

1. Quindi creare una pianificazione giornaliera per il processo con [sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md).

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. Collegare la pianificazione del processo al processo con [sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md).

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. Uso [sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md) per assegnare il processo a un server di destinazione. In questo esempio, la destinazione è il server locale.

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. Avviare il processo con [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>Creare un processo con SQL Server Management Studio

È anche possibile creare e gestire i processi in remoto con SQL Server Management Studio (SSMS) in Windows.

1. Avviare SQL Server Management Studio in Windows e connettersi all'istanza di Linux di SQL Server. Per altre informazioni, vedere [gestire SQL Server in Linux con SQL Server Management Studio](sql-server-linux-manage-ssms.md).

1. Verificare che è stato creato un database di esempio denominato **SampleDB**.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. Verificare che SQL Agent sia stata [installato](sql-server-linux-setup-sql-agent.md) e configurato correttamente. Cercare il segno più accanto a SQL Server Agent in Esplora oggetti. Se SQL Server Agent non è abilitata, provare a riavviare la **mssql-server** service in Linux.

   ![Verificare che sia stato installato SQL Server Agent](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. Creare un nuovo processo.

   ![Creare un nuovo processo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. Assegnare un nome di processo e crea il passaggio di processo.

   ![Creare un passaggio di processo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. Specificare quale sottosistema da usare e ciò che dovrebbe eseguire il passaggio del processo.

   ![Sottosistema di processo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![Azione del passaggio processo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. Creare una nuova pianificazione processo.

   ![Pianificazioni processo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![Pianificazioni processo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. Avviare il processo.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Installare SQL Server Agent in Linux
> * Uso di Transact-SQL e di sistema stored procedure per creare i processi
> * Creare un processo che esegue i backup giornalieri di database
> * Usare SSMS UI per creare e gestire i processi

Successivamente, esplorare altre funzionalità per la creazione e la gestione dei processi:

> [!div class="nextstepaction"]
>[Documentazione di SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
