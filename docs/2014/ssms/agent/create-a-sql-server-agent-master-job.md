---
title: Creare un processo master di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], master jobs
- jobs [SQL Server Agent], creating
- master SQL Server Agent job [SQL Server]
ms.assetid: c12ab23f-d7ee-43a5-8cd2-0a9121292bcd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e80d5790f78c83a8a1ff3059e12e0946e206c060
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211457"
---
# <a name="create-a-sql-server-agent-master-job"></a>Creazione di un processo master di SQL Server Agent
  In questo argomento viene descritto come creare un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo di agente [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Master in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tramite [!INCLUDE[tsql](../../includes/tsql-md.md)]o.  
  
 
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Le modifiche apportate ai processi master di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent devono essere propagate a tutti i server di destinazione interessati. Poiché i server di destinazione non scaricano il processo finché le destinazioni non vengono specificate, [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di completare tutti i passaggi e le pianificazioni di un particolare processo prima di specificare i server di destinazione. In caso contrario, è necessario richiedere manualmente che i server di destinazione scarichino nuovamente il processo modificato, eseguendo la stored procedure **sp_post_msx_operation** o modificando il processo con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per ulteriori informazioni, vedere [sp_post_msx_operation &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql) o [modificare un processo](modify-a-job.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 I processi distribuiti con passaggi associati a un proxy vengono eseguiti nel contesto dell'account proxy nel server di destinazione. Verificare che siano soddisfatte le condizioni seguenti, per assicurare che i passaggi di processo associati a un proxy vengano scaricati dal server master a quello di destinazione:  
  
-   La sottochiave del registro di sistema **\ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Microsoft SQL Server\\<*instance_name*> \SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) è impostata su 1 (true). Per impostazione predefinita, questa sottochiave è impostata su 0 (False).  
  
-   Nel server di destinazione deve esistere un account proxy con lo stesso nome dell'account proxy del server master utilizzato per l'esecuzione del passaggio del processo.  
  
 Se si verificano errori nel download dei passaggi dei processi che usano account proxy dal server master a quello di destinazione, è possibile controllare se nella colonna **error_message** della tabella **sysdownloadlist** nel database **msdb** sono presenti i messaggi di errore seguenti:  
  
-   "Per questo passaggio del processo è necessario un account proxy, ma l'individuazione dei proxy è disabilitata nel server di destinazione." Per risolvere il problema, impostare la sottochiave del Registro di sistema **AllowDownloadedJobsToMatchProxyName** su 1.  
  
-   "Impossibile trovare il proxy." Per risolvere il problema, verificare che nel server di destinazione sia disponibile un account proxy con lo stesso nome dell'account proxy del server master utilizzato per l'esecuzione del passaggio di processo.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>Per creare un processo master di SQL Server Agent  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui si desidera creare un processo di SQL Server Agent.  
  
2.  Fare clic sul segno più per espandere **SQL Server Agent**.  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **processi** e scegliere **nuovo processo.**...  
  
4.  Nella pagina **Generale** della finestra di dialogo **Nuove processo** modificare le proprietà generali del processo. Per ulteriori informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo e nuovo processo &#40;pagina generale&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
5.  Nella pagina **Passaggi** , organizzare i passaggi del processo. Per ulteriori informazioni sulle opzioni disponibili in questa pagina, vedere la [pagina Proprietà processo: nuovo processo &#40;passaggi&#41;](job-properties-new-job-steps-page.md)  
  
6.  Nella pagina **Pianificazioni** , organizzare le pianificazioni per il processo. Per ulteriori informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo: pagina Pianificazioni nuovo processo &#40;&#41;](job-properties-new-job-schedules-page.md)  
  
7.  Nella pagina **Avvisi** , organizzare gli avvisi per il processo. Per ulteriori informazioni sulle opzioni disponibili in questa pagina, vedere la [pagina Proprietà processo: nuovo processo &#40;avvisi&#41;](job-properties-new-job-alerts-page.md)  
  
8.  Nella pagina **Notifiche** impostare le azioni che [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve eseguire al completamento del processo. Per ulteriori informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo: nuova pagina notifiche &#40;processo&#41;](job-properties-new-job-notifications-page.md).  
  
9. Nella pagina **Destinazioni** , gestire i server di destinazione per il processo. Per ulteriori informazioni sulle opzioni disponibili in questa pagina, vedere [Proprietà processo: nuova pagina &#40;di destinazione processo&#41;](job-properties-new-job-targets-page.md).  
  
10. Al termine, fare clic su **OK**.  
  

  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>Per creare un processo master di SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
-   [sp_add_job &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_add_jobserver &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  

  
  
