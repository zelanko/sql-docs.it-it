---
title: Monitorare SQL Server backup gestito in Azure | Microsoft Docs
description: Questo articolo descrive gli strumenti che è possibile usare per determinare l'integrità complessiva dei backup usando SQL Server backup gestito in Azure e identificare gli errori.
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: cfb9e431-7d4c-457c-b090-6f2528b2f315
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: baec99e63c70befde0cfce76e42dd6202ebc0bad
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930642"
---
# <a name="monitor-sql-server-managed-backup-to-azure"></a>Monitorare il backup gestito di SQL Server in Azure
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] dispone di misure predefinite per identificare problemi ed errori durante i processi di backup e risolverli con un'azione correttiva, se possibile.  Tuttavia, vi sono alcune situazioni in cui è richiesto l'intervento dell'utente. In questo argomento vengono descritti gli strumenti che è possibile utilizzare per determinare lo stato di integrità complessivo dei backup e vengono identificati tutti gli errori che devono essere risolti.  
  
## <a name="overview-of-ss_smartbackup-built-in-debugging"></a>Panoramica del debug predefinito di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 Tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] vengono esaminati periodicamente i backup pianificati e viene tentata una ripianificazione di tutti i backup non completati. Viene eseguito periodicamente il polling dell'account di archiviazione per identificare eventuali interruzioni nelle catene di log che interessano la recuperabilità del database e, di conseguenza, vengono pianificati nuovi backup. Vengono inoltre prese in considerazione i criteri di limitazione di Azure e sono presenti meccanismi per la gestione di più backup di database. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] utilizza gli eventi estesi per tenere traccia di tutte le attività. Tra i canali di eventi estesi utilizzati da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] Agent sono inclusi quello amministrativo, operativo, analitico e di debug. Gli eventi che rientrano nella categoria amministrativa sono in genere correlati a errori, richiedono l'intervento dell'utente e sono abilitati per impostazione predefinita. Anche gli eventi analitici sono abilitati per impostazione predefinita, ma in genere non sono correlati a errori per cui è richiesto l'intervento dell'utente. Gli eventi operativi sono in genere informativi. Ad esempio, gli eventi operativi includono la pianificazione di un backup, il corretto completamento del backup e così via. Il debug è il più dettagliato e viene usato internamente da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per determinare i problemi e correggerli, se necessario.  
  
### <a name="configure-monitoring-parameters-for-ss_smartbackup"></a>Configurare parametri di monitoraggio per [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 Il stored procedure di sistema **smart_admin. sp_set_parameter** consente di specificare le impostazioni di monitoraggio. Nelle sezioni seguenti vengono descritti il processo di abilitazione degli eventi estesi e l'abilitazione della notifica tramite posta elettronica per errori e avvisi.  
  
 La funzione **smart_admin. fn_get_parameter** può essere utilizzata per ottenere l'impostazione corrente per un parametro specifico o per tutti i parametri configurati. Se i parametri non sono mai stati configurati, non viene restituito alcun valore.  
  
1.  Connettersi al [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Verranno restituite la configurazione corrente degli eventi estesi e le notifiche di posta elettronica.  
  
```sql
Use msdb  
Go  
SELECT * FROM smart_admin.fn_get_parameter (NULL)  
GO  
```  
  
 Per ulteriori informazioni, vedere [smart_admin. fn_get_parameter &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)  
  
### <a name="extended-events-for-monitoring"></a>Eventi estesi per il monitoraggio  
 Per impostazione predefinita, gli eventi amministrativi, operativi e analitici sono abilitati. Gli eventi amministrativi sono più importanti e utili quando si identificano errori per i quali è richiesto l'intervento manuale per la risoluzione. È possibile che sia necessario abilitare gli eventi operativi e di debug, tuttavia si consideri che questi eventi sono dettagliati e possono richiedere l'applicazione di un filtro. Nelle procedure seguenti viene descritto come monitorare gli eventi registrati tramite gli eventi estesi.  
  
> [!IMPORTANT]  
>  A differenza degli eventi estesi per il motore SQL, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non supporta concetti relativi alla sessione eventi estesi. Per interagire con gli eventi estesi vengono utilizzate le funzioni e le stored procedure di sistema. Inoltre, è possibile visualizzare il registro eventi estesi dalla directory log.  
  
##### <a name="to-configure-and-view-extended-events"></a>Per configurare e visualizzare gli eventi estesi  
  
1.  Per visualizzare i canali di eventi estesi disponibili e il relativo stato corrente, eseguire la query riportata di seguito:  
  
    ```sql
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     Nell'output della query vengono visualizzati l'oggetto event_name, l'eventuale configurabilità e se attualmente abilitato.  Per ulteriori informazioni, vedere [smart_admin. fn_get_current_xevent_settings &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql).  
  
2.  Per abilitare gli eventi di debug, eseguire la query seguente:  
  
    ```sql
    --  to enable debug events  
    Use msdb;  
    GO 
    EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
     Per ulteriori informazioni sulla stored procedure, vedere [smart_admin. sp_set_parameter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql).  
  
3.  Per visualizzare gli eventi registrati, eseguire la query riportata di seguito:  
  
    ```sql
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;
    ```  
  
    ```sql
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'
    ```  
  
### <a name="aggregated-error-countshealth-status"></a>Conteggi errori aggregati/stato di integrità  
 La funzione **smart_admin. fn_get_health_status** restituisce una tabella di conteggi di errori aggregati per ogni categoria che può essere utilizzata per monitorare lo stato di integrità di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] . Questa stessa funzione viene utilizzata anche dal meccanismo di notifica tramite posta elettronica configurato dal sistema descritto più avanti in questo argomento.   
Questi conteggi aggregati possono essere utilizzati per monitorare l'integrità del sistema. Ad esempio, se la colonna number_ of_retention_loops è 0 in 30 minuti, è possibile che la gestione della memorizzazione richieda del tempo o che addirittura non funzioni correttamente. Le colonne di errori diverse da zero possono indicare problemi e, per individuarli, è necessario verificare i registri eventi estesi. In alternativa, chiamare **smart_admin. sp_get_backup_diagnostics** stored procedure per trovare i dettagli dell'errore.  
  
### <a name="using-agent-notification-for-assessing-backup-status-and-health"></a>Utilizzo della notifica dell'agente per valutare l'integrità e lo stato di backup  
 In [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è incluso un meccanismo di notifica basato sui criteri di gestione basata su criteri di SQL Server.  
  
 **Prerequisiti:**  
  
-   Per utilizzare questa funzionalità, è necessario Posta elettronica database. Per ulteriori informazioni su come abilitare posta elettronica database per l'istanza di SQL Server, vedere [Configure posta elettronica database](../relational-databases/database-mail/configure-database-mail.md).  
  
-   Per utilizzare Posta elettronica database devono essere impostate le proprietà di Sistema avvisi di SQL Server Agent.  
  
 **Architettura della notifica:**  
  
-   **Gestione basata su criteri:** Sono impostati due criteri per monitorare l'integrità del backup: **criteri di integrità del sistema di amministrazione intelligente**e i **criteri di integrità dell'azione utente per Smart admin**. Tramite i criteri di integrità del sistema di amministrazione intelligente vengono valutati errori critici come la mancanza di credenziali SQL o credenziali SQL non valide, errori di connettività e viene segnalata l'integrità del sistema. Per questi errori è in genere richiesta un'azione manuale per correggere il problema sottostante. Tramite i criteri di integrità dell'azione utente di amministrazione intelligente vengono valutati gli avvisi, ad esempio backup danneggiati e simili.  Per questi non sono richieste azioni, si tratta solo dell'avviso di un evento. È previsto che problemi di questo tipo vengano risolti automaticamente da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] Agent.  
  
-   **SQL Server Agent** Processo: la notifica viene eseguita usando un processo di SQL Server Agent con tre passaggi di processo. Nel primo passaggio di processo viene verificato se [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è configurato per un database o un'istanza. Se viene rilevato [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] abilitato e configurato, viene eseguito il secondo passaggio: viene eseguito un cmdlet di PowerShell tramite cui viene valutato lo stato di integrità in base ai criteri di gestione basata su criteri di SQL Server. Se viene rilevato un errore o avviso, l'operazione non viene completata attivando il terzo passo, che prevede l'invio di una notifica tramite posta elettronica con il report dell'errore o dell'avviso.  Tuttavia il processo di SQL Server Agent non è abilitato per impostazione predefinita. Per abilitare il processo di notifica tramite posta elettronica, utilizzare il stored procedure di sistema **smart_admin. sp_set_backup_parameter** .  Nella procedura seguente vengono descritti i passaggi in modo più dettagliato:  
  
##### <a name="enabling-email-notification"></a>Abilitazione della notifica tramite posta elettronica  
  
1.  Se Posta elettronica database non è già configurato, attenersi alla procedura descritta in [configurare posta elettronica database](../relational-databases/database-mail/configure-database-mail.md).  
  
2.  Impostare il database come sistema di posta elettronica per SQL Server sistema di avvisi: fare clic con il pulsante destro del mouse su **SQL Server Agent**, selezionare **sistema avvisi**, selezionare la casella di controllo **Abilita profilo di posta** , selezionare **posta elettronica database** come **sistema di posta**e selezionare un profilo di posta creato in precedenza.  
  
3.  Eseguire la query riportata di seguito in una finestra Query e immettere l'indirizzo di posta elettronica a cui si desidera inviare la notifica:  
  
    ```sql
    Use msdb  
    Go  
    EXEC smart_admin.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'
    ```  
  
     Verrà creato un processo di SQL Server Agent utilizzato per raccogliere lo stato di integrità e inviare notifiche quando si verifica un errore o un problema relativo ai backup.  
  
 Di seguito è riportato uno script di esempio per abilitare Posta elettronica database e configurare la notifica di posta elettronica tramite un processo di SQL Server Agent  
  
```sql
-- Prereq: Make sure that SQL Server service runs in a service account that has  
--  access to SMTP Server   
-- set SQL Server service account as domain account   
  
EXEC sp_configure 'show advanced', 1  
RECONFIGURE  
GO  
  
-- Enable DBMail  
EXEC sp_configure 'Database Mail XPs',1  
GO  
RECONFIGURE  
GO  
  
-- Configure DBMail  
DECLARE @emailid NVARCHAR(255)  
-- Note: change this email to your own email id  
SET @emailid = N'emailalias@mycompany.com'  
  
DECLARE @smtpserver NVARCHAR(255)  
SET @smtpserver = N'smtphost.domainname.com'  
  
DECLARE @mailprofile NVARCHAR(255)  
SET @mailprofile = N'my_profile'  
  
EXEC msdb.dbo.sysmail_add_account_sp @account_name=N'myaccount',  
                @email_address = @emailid,  
                @replyto_address = @emailid,  
                @mailserver_name = @smtpserver,  
                @use_default_credentials = 1  
  
EXEC msdb.dbo.sysmail_add_profile_sp @profile_name=@mailprofile  
EXEC msdb.dbo.sysmail_add_profileaccount_sp @profile_name=@mailprofile, @account_name=N'myaccount', @sequence_number=1  
  
-- Set SQL Agent to use DBMail profile  
EXEC msdb.dbo.sp_set_sqlagent_properties @databasemail_profile = @mailprofile  
  
-- Configure Notifications   
EXEC msdb.smart_admin.sp_set_parameter  
@parameter_name = 'SSMBackup2WANotificationEmailIds',  
@parameter_value = @emailid  
  
-- To test is you are receiving notifications  
-- delete few backup files from your storage container, Wait for 15 minutes & see if you get any email notification
```  
  
### <a name="using-powershell-to-setup-custom-health-monitoring"></a>Utilizzo di PowerShell per configurare il monitoraggio dello stato di integrità personalizzato  
 Il cmdlet **test-SqlSmartAdmin** può essere usato per creare un monitoraggio dello stato personalizzato. Ad esempio, l'opzione di notifica descritta nella sezione precedente può essere configurata a livello di istanza.  Se si dispone di più istanze di SQL Server configurate per l'utilizzo di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], il cmdlet di PowerShell può essere utilizzato per creare script per raccogliere lo stato e l'integrità dei backup per tutte le istanze.  
  
 Il cmdlet **test-SqlSmartAdmin** valuta gli errori e gli avvisi restituiti dal SQL Server criteri di gestione basata su criteri e segnala uno stato di rollup.  Per impostazione predefinita, tramite questo cmdlet vengono utilizzati i criteri di sistema. Per includere tutti i criteri personalizzati, utilizzare il parametro `-AllowUserPolicies`.  
  
 Di seguito è riportato un esempio di script di PowerShell tramite cui viene restituito un report di errori e avvisi basato sui criteri di sistema e su tutti i criteri utente creati:  
  
```powershell
$policyResults = Get-SqlSmartAdmin | Test-SqlSmartAdmin -AllowUserPolicies  
$policyResults.PolicyEvaluationDetails | Select Name, Category, Expression, Result, Exception | fl
```  
  
 Lo script seguente restituisce un report dettagliato degli errori e degli avvisi per l'istanza predefinita ( `\SQL\COMPUTER\DEFAULT` ):  
  
```powershell
(Get-SqlSmartAdmin ).EnumHealthStatus()  
```  
  
### <a name="objects-in-msdb-database"></a>Oggetti in un database MSDB  
 Sono disponibili degli oggetti che vengono installati per implementare le funzionalità. Questi oggetti sono riservati per l'utilizzo interno. Tuttavia, è disponibile una tabella di sistema che può essere utile per monitorare lo stato di backup: smart_backup_files. La maggior parte delle informazioni archiviate in questa tabella pertinente per il monitoraggio, ad esempio il tipo di backup, il nome del database, il primo e l'ultimo LSN, le date di scadenza del backup vengono esposte tramite la funzione di sistema [smart_admin. fn_available_backups &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql). Tuttavia la colonna stato nella tabella smart_backup_files in cui viene indicato lo stato del file di backup non è disponibile tramite la funzione. Di seguito è riportata una query di esempio utilizzabile per recuperare alcune informazioni, tra cui lo stato della tabella di sistema:  
  
```sql
USE msdb  
GO  
SELECT  
 database_name AS [Database Name] ,backup_path AS [Backup Destination and File]  
,[Backup Type] =  
CASE backup_type  
WHEN 1 THEN 'FULL'  
WHEN 2 THEN 'LOG'  
END  
,[Backup Status] =  
CASE [status]  
WHEN 'A' THEN 'Available'  
WHEN 'B' THEN 'Copy In Progress'  
WHEN 'C' THEN 'Corrupted'  
WHEN 'D' THEN 'Deleted'  
WHEN 'F' THEN 'Copy Failed'  
WHEN 'U' THEN 'Unknown'  
END  
,first_lsn AS [First LSN]  
,last_lsn AS [Last LSN]  
,backup_start_date AS [Backup Start Time]  
,backup_finish_date AS [Backup Completion Time]  
,expiration_date AS [Backup Expiry Date/Time]  
FROM  
smart_backup_files;
```  
  
 Di seguito è riportata una spiegazione dettagliata del diverso stato restituito:  
  
-   **Disponibile-A:** Si tratta di un normale file di backup. Il backup è stato completato e anche verificato che sia disponibile nell'archiviazione di Azure.  
  
-   **Copia in corso-B:** Questo stato è specifico per i database del gruppo di disponibilità. Se tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] viene rilevata un'interruzione nella catena dei log di backup, tentare innanzitutto di identificare il backup da cui potrebbe essere stata causata l'interruzione della catena di backup. Quando si trova il file di backup, tenta di copiare il file in archiviazione di Azure. Quando il processo di copia è in corso verrà visualizzato questo stato.  
  
-   **Copia non riuscita-F:** Analogamente alla copia in corso, si tratta di database del gruppo di disponibilità t specifici. Se il processo di copia non viene completato, lo stato è contrassegnato come F.  
  
-   **Danneggiato-C:** Se [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non è in grado di verificare il file di backup nell'archiviazione eseguendo un comando restore HEADER_ONLY anche dopo più tentativi, questo file viene contrassegnato come danneggiato. Tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] verrà pianificato un backup per garantire che dal file danneggiato non venga generata un'interruzione della catena di backup.  
  
-   **Eliminato-D:** Il file corrispondente non è stato trovato nell'archiviazione di Azure. Tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] verrà pianificato un backup se viene generata un'interruzione della catena di backup da parte del file eliminato.  
  
-   **Sconosciuto-U:** Questo stato indica che [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non è ancora stato possibile verificare l'esistenza del file e le relative proprietà nell'archiviazione di Azure. Alla successiva esecuzione del processo, vale a dire circa ogni 15 minuti, questo stato verrà aggiornato.  
