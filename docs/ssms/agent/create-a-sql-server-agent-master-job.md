---
title: Creare un processo master di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], master jobs
- jobs [SQL Server Agent], creating
- master SQL Server Agent job [SQL Server]
ms.assetid: c12ab23f-d7ee-43a5-8cd2-0a9121292bcd
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: aa5231a668873627c12d33dffff77416d5ac3e1f
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553120"
---
# <a name="create-a-sql-server-agent-master-job"></a>Creazione di un processo master di SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come creare un processo master di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Restrictions"></a>Limitazioni e restrizioni  
Le modifiche apportate ai processi master di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent devono essere propagate a tutti i server di destinazione interessati. Poiché i server di destinazione non scaricano il processo finché le destinazioni non vengono specificate, [!INCLUDE[msCoName](../../includes/msconame_md.md)] consiglia di completare tutti i passaggi e le pianificazioni di un particolare processo prima di specificare i server di destinazione. In caso contrario, è necessario richiedere manualmente che i server di destinazione scarichino nuovamente il processo modificato, eseguendo la stored procedure **sp_post_msx_operation** o modificando il processo con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [sp_post_msx_operation (Transact-SQL)](https://msdn.microsoft.com/085deef8-2709-4da9-bb97-9ab32effdacf) o [Modificare un processo](../../ssms/agent/modify-a-job.md).  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
I processi distribuiti con passaggi associati a un proxy vengono eseguiti nel contesto dell'account proxy nel server di destinazione. Verificare che siano soddisfatte le condizioni seguenti, per assicurare che i passaggi di processo associati a un proxy vengano scaricati dal server master a quello di destinazione:  
  
-   La sottochiave del Registro di sistema **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;nome_istanza&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) è impostata su 1 (true). Per impostazione predefinita, questa sottochiave è impostata su 0 (False).  
  
-   Nel server di destinazione deve esistere un account proxy con lo stesso nome dell'account proxy del server master utilizzato per l'esecuzione del passaggio del processo.  
  
Se si verificano errori nel download dei passaggi dei processi che usano account proxy dal server master a quello di destinazione, è possibile controllare se nella colonna **error_message** della tabella **sysdownloadlist** nel database **msdb** sono presenti i messaggi di errore seguenti:  
  
-   "Per questo passaggio del processo è necessario un account proxy, ma l'individuazione dei proxy è disabilitata nel server di destinazione." Per risolvere il problema, impostare la sottochiave del Registro di sistema **AllowDownloadedJobsToMatchProxyName** su 1.  
  
-   "Impossibile trovare il proxy." Per risolvere il problema, verificare che nel server di destinazione sia disponibile un account proxy con lo stesso nome dell'account proxy del server master utilizzato per l'esecuzione del passaggio di processo.  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>Per creare un processo master di SQL Server Agent  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera creare un processo di SQL Server Agent.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Processi** e quindi selezionare **Nuovo processo**.  
  
4.  Nella pagina **Generale** della finestra di dialogo **Nuove processo** modificare le proprietà generali del processo. Per altre informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo - nuovo processo &#40;pagina Generale&#41;](../../ssms/agent/job-properties-new-job-general-page.md)  
  
5.  Nella pagina **Passaggi** , organizzare i passaggi del processo. Per altre informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo - nuovo processo &#40;pagina Passaggi&#41;](../../ssms/agent/job-properties-new-job-steps-page.md)  
  
6.  Nella pagina **Pianificazioni** , organizzare le pianificazioni per il processo. Per altre informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo - Nuovo processo &#40;pagina Pianificazioni&#41;](../../ssms/agent/job-properties-new-job-schedules-page.md)  
  
7.  Nella pagina **Avvisi** , organizzare gli avvisi per il processo. Per altre informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo - nuovo processo &#40;pagina Avvisi&#41;](../../ssms/agent/job-properties-new-job-alerts-page.md)  
  
8.  Nella pagina **Notifiche** impostare le azioni che [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve eseguire al completamento del processo. Per altre informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo - nuovo processo &#40;pagina Notifiche&#41;](../../ssms/agent/job-properties-new-job-notifications-page.md).  
  
9. Nella pagina **Destinazioni** , gestire i server di destinazione per il processo. Per altre informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo - nuovo processo &#40;pagina Destinazioni&#41;](../../ssms/agent/job-properties-new-job-targets-page.md).  
  
10. Al termine, fare clic su **OK**.  
  
## <a name="TsqlProcedure"></a>Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>Per creare un processo master di SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE msdb ;  
    GO  
    -- Adds a new job executed by the SQLServerAgent service called 'Weekly Sales Data Backup'  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    -- Adds a step (operation) to the 'Weekly Sales Data Backup' job.  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    -- Creates a schedule called RunOnce  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    -- Sets the 'RunOnce' schedule to the "Weekly Sales Data Backup' Job  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2  
    -- assumes that SEATTLE2 is registered as a target server for the current instance.  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
Per altre informazioni, vedere:  
  
-   [sp_add_job (Transact-SQL)](https://msdn.microsoft.com/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
  
-   [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_add_schedule (Transact-SQL)](https://msdn.microsoft.com/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7)  
  
-   [sp_attach_schedule (Transact-SQL)](https://msdn.microsoft.com/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)  
  
-   [sp_add_jobserver (Transact-SQL)](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
