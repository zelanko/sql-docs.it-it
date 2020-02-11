---
title: Creare un processo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: b35af2b6-6594-40d1-9861-4d5dd906048c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7126b01fcaee1a0ab3f7776cc54e6eb0dbe2774d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72798314"
---
# <a name="create-a-job"></a>Creare un processo
  In questo argomento viene descritto come creare un processo di SQL Server Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects (SMO).  
  
 Per aggiungere al processo passaggi, pianificazioni, avvisi e notifiche da inviare agli operatori, vedere i collegamenti agli argomenti nella sezione Vedere anche.  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un processo usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure),  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SQL Server Management Objects](#SMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Per creare un processo, è necessario che l'utente sia membro di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o del ruolo predefinito del server **sysadmin** . Un processo può essere modificato solo dal proprietario o dai membri del ruolo **sysadmin** . Per altre informazioni sui ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vedere [Ruoli di database predefiniti di SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
-   L'assegnazione di un processo a un altro account di accesso non garantisce che il nuovo proprietario disponga di autorizzazioni sufficienti per eseguire correttamente il processo.  
  
-   I processi locali vengono memorizzati nella cache dall'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Eventuali modifiche, pertanto, forzano in modo implicito una nuova memorizzazione nella cache da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Poiché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non memorizza nella cache il processo fino alla chiamata di **sp_add_jobserver** , è consigliabile chiamare la store procedure **sp_add_jobserver** per ultima.  
  
###  <a name="Security"></a> Sicurezza  
  
-   Solo un amministratore di sistema può cambiare il proprietario di un processo.  
  
-   Per motivi di sicurezza, solo il proprietario del processo o un membro del ruolo **sysadmin** può modificare la definizione del processo. Solo i membri del ruolo predefinito del server **sysadmin** possono assegnare la proprietà di un processo ad altri utenti ed eseguire qualsiasi processo, indipendentemente dal proprietario.  
  
    > [!NOTE]  
    >  Se si assegna la proprietà di un processo a un utente che non è membro del ruolo predefinito del server **sysadmin** e il processo sta eseguendo operazioni per le quali sono necessari account proxy, ad esempio l'esecuzione del pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)] , verificare che l'utente possa accedere all'account proxy. In caso contrario, verrà generato un errore.  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-job"></a>Per creare un processo di SQL Server Agent  
  
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
  
#### <a name="to-create-a-sql-server-agent-job"></a>Per creare un processo di SQL Server Agent  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backup';  
    GO  
    ```  
  
 Per altre informazioni, vedere:  
  
-   [sp_add_job &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_add_jobserver &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
##  <a name="SMOProcedure"></a>Utilizzo di SQL Server Management Objects  
 **Per creare un processo di SQL Server Agent**  
  
 Chiamare il metodo `Create` della classe `Job` usando un linguaggio di programmazione come Visual Basic, Visual C# o PowerShell. Per un esempio di codice, vedere [Pianificazione delle attività amministrative automatiche in SQL Server Agent](sql-server-agent.md).  
  
##  <a name="SSMSProc2"></a>  
