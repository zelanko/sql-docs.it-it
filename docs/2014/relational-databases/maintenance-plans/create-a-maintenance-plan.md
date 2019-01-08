---
title: Creare un piano di manutenzione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- maintenance plans [SQL Server], creating
ms.assetid: a945cb65-ba7a-42f4-bbd9-6ec675745523
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de7ff72e7ce135ab477e3d254eeb26193c8bbc69
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52801543"
---
# <a name="create-a-maintenance-plan"></a>Creare un piano di manutenzione
  In questo argomento viene illustrato come creare un piano di manutenzione a uno o più server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]è possibile creare questi piani di manutenzione in uno di due modi: utilizzando la Creazione guidata piano di manutenzione o l'area di progettazione. La procedura guidata è più appropriata per la creazione di piani di manutenzione di base, mentre con l'area di progettazione sono disponibili funzionalità avanzate per i flussi di lavoro.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un piano di manutenzione utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Per creare un piano di manutenzione multiserver, è necessario configurare un ambiente multiserver composto da un server master e uno o più server di destinazione. I piani di manutenzione multiserver devono essere creati e gestiti nel server master. Questi piani possono essere visualizzati, ma non gestiti, nei server di destinazione.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per creare o gestire piani di manutenzione, è necessario essere membri del ruolo predefinito del server **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-maintenance-plan-using-the-maintenance-plan-wizard"></a>Per creare un piano di manutenzione utilizzando la Creazione guidata piano di manutenzione  
  
1.  In Esplora oggetti fare clic sul segno più per espandere il server in cui si desidera creare un piano di manutenzione.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Piani di manutenzione** e scegliere **Creazione guidata piano di manutenzione**.  
  
4.  Eseguire i passaggi della procedura guidata per creare un piano di manutenzione. Per altre informazioni, vedere [Use the Maintenance Plan Wizard](use-the-maintenance-plan-wizard.md).  
  
#### <a name="to-create-a-maintenance-plan-using-the-design-surface"></a>Per creare un piano di manutenzione utilizzando l'area di progettazione  
  
1.  In Esplora oggetti fare clic sul segno più per espandere il server in cui si desidera creare un piano di manutenzione.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic con il pulsante destro del mouse sulla cartella **Piani di manutenzione** e scegliere **Nuovo piano di manutenzione**.  
  
4.  Creare un piano di manutenzione seguendo i passaggi illustrati in [Creare un piano di manutenzione &#40;area di progettazione del piano di manutenzione&#41;](create-a-maintenance-plan-maintenance-plan-design-surface.md).  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-maintenance-plan"></a>Per creare un piano di manutenzione  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE msdb;  
    GO  
    --  Adds a new job, executed by the SQL Server Agent service, called "HistoryCleanupTask_1".  
    EXEC dbo.sp_add_job  
       @job_name = N'HistoryCleanupTask_1',   
       @enabled = 1,   
       @description = N'Clean up old task history' ;   
    GO  
    -- Adds a job step for reorganizing all of the indexes in the HumanResources.Employee table to the HistoryCleanupTask_1 job.   
    EXEC dbo.sp_add_jobstep  
        @job_name = N'HistoryCleanupTask_1',   
        @step_name = N'Reorganize all indexes on HumanResources.Employee table',   
        @subsystem = N'TSQL',   
        @command = N'USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_LoginID ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_rowguid ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX IX_Employee_OrganizationNode ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX PK_Employee_BusinessEntityID ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    ',   
        @retry_attempts = 5,   
        @retry_interval = 5 ;   
    GO  
    -- Creates a schedule named RunOnce that executes every day when the time on the server is 23:00.   
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',   
        @freq_type = 4,   
        @freq_interval = 1,   
        @active_start_time = 233000 ;   
    GO  
    -- Attaches the RunOnce schedule to the job HistoryCleanupTask_1.   
    EXEC sp_attach_schedule  
       @job_name = N'HistoryCleanupTask_1'  
       @schedule_name = N'RunOnce' ;   
    GO  
  
    ```  
  
 Per altre informazioni, vedere:  
  
-   [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
  
