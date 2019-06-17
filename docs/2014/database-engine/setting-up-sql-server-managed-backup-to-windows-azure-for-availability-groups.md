---
title: Configurazione di SQL Server Managed Backup to Windows Azure per i gruppi di disponibilità | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 0c4553cd-d8e4-4691-963a-4e414cc0f1ba
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6a67b2331959dbc3087f6282be05de90b42443c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843567"
---
# <a name="setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups"></a>Configurazione del backup gestito di SQL Server in Windows Azure per i gruppi di disponibilità
  In questo argomento viene fornita un'esercitazione sulla configurazione del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per i database che partecipano ai gruppi di disponibilità AlwaysOn.  
  
## <a name="availability-group-configurations"></a>Configurazioni del gruppo di disponibilità  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è supportato per database del gruppo di disponibilità se le repliche sono tutte configurate in locale o interamente in Windows Azure oppure per un'implementazione ibrida tra un'istanza in locale e in una o più macchine virtuali di Windows Azure. Tuttavia potrebbe essere necessario prendere in considerazione quanto riportato di seguito per una o più implementazioni.  
  
-   Frequenza Backup del log: La frequenza del backup del log è la crescita di termini di tempo e di log. Ad esempio, il backup del log viene eseguito una volta ogni 2 ore, a meno che lo spazio del log utilizzato entro questo periodo di tempo non sia di almeno 5 MB. Questo aspetto riguarda tutte le implementazioni, in locale, nel cloud o in una soluzione ibrida.  
  
-   Larghezza di banda di rete: Questo vale per le implementazioni in cui le repliche si trovano in posizioni fisiche diverse, ad esempio in un cloud ibrido o in diverse aree di Azure in una configurazione solo cloud. La larghezza di banda di rete può influire sulla latenza delle repliche secondarie e l'eventuale impostazione di queste ultime sulla replica sincrona può determinare un aumento delle dimensioni del log nella replica primaria. Se le repliche secondarie sono impostate sulla replica sincrona, potrebbero non rimanere sincronizzate a causa della latenza di rete che può comportare la perdita di dati in caso di failover sulla replica secondaria.  
  
### <a name="configuring-includesssmartbackupincludesss-smartbackup-mdmd-for-availability-databases"></a>Configurazione del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per i database di disponibilità  
 **Autorizzazioni:**  
  
-   Richiede l'appartenenza al **db_backupoperator** ruolo del database con **ALTER ANY CREDENTIAL** autorizzazioni, e `EXECUTE` le autorizzazioni per **sp_delete_backuphistory**stored procedure.  
  
-   È necessario **selezionate** le autorizzazioni per il **smart_admin.fn_get_current_xevent_settings**(funzione).  
  
-   È necessario `EXECUTE` le autorizzazioni per il **smart_admin.sp_get_backup_diagnostics** stored procedure. È inoltre richiesta l'autorizzazione `VIEW SERVER STATE` poiché vengono chiamati internamente altri oggetti di sistema che richiedono tale autorizzazione.  
  
-   È necessario `EXECUTE` le autorizzazioni per il `smart_admin.sp_set_instance_backup` e `smart_admin.sp_backup_master_switch` stored procedure.  
  
 Di seguito sono riportati i passaggi da eseguire per la configurazione di un gruppo di disponibilità AlwaysOn con il [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Un'esercitazione dettagliata viene descritta più avanti in questo argomento.  
  
1.  Una volta creato il gruppo di disponibilità, configurare la replica di backup preferita. Questa impostazione per il gruppo di disponibilità viene inoltre usata dal [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per determinare la replica da usare per il backup. Per istruzioni dettagliate su come configurare le preferenze di backup, vedere [configurare Backup sulle repliche di disponibilità &#40;SQL Server&#41;](availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  Se si sta creando un nuovo gruppo di disponibilità AlwaysOn, vedere [Introduzione ai gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md).  
  
2.  Configurare l'accesso per la connessione in sola lettura alle repliche secondarie. Per istruzioni dettagliate su come configurare accesso in sola lettura, vedere [configurare l'accesso in sola lettura in una Replica di disponibilità &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
3.  Specificare la replica di backup. L'impostazione della replica di backup preferita viene utilizzata dal [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per determinare il database da utilizzare per la pianificazione dei backup.  Per determinare se la replica corrente è la replica di backup preferita, usare il [Sys. fn_hadr_backup_is_preferred_replica &#40;Transact-SQL&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) (funzione).  
  
4.  In ogni replica eseguire [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurazione del database utilizzando il **smart admin.sp_set_db_backup** stored procedure.  
  
     **[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] comportamento dopo un failover:** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] continueranno a funzionare e manterrà le copie di backup e la recuperabilità dopo un evento di failover. Non è richiesta alcuna azione specifica dopo un failover.  
  
#### <a name="considerations-and-requirements"></a>Considerazioni e requisiti:  
 Per la configurazione del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per database che fanno parte del gruppo di disponibilità AlwaysOn sono necessari determinati requisiti e considerazioni. Di seguito è riportato un elenco delle considerazioni e dei requisiti:  
  
-   Le impostazioni di configurazione del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] devono essere identiche per tutti i database in tutti i nodi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che fanno parte dello stesso gruppo di disponibilità. È possibile soddisfare questa esigenza impostando le stesse configurazioni del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per la replica primaria e per tutte le repliche a livello di database oppure impostando le stesse impostazioni predefinite del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] in tutti i nodi che fanno parte dei gruppi di disponibilità. Si consiglia di impostare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] a livello di database perché questa configurazione di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] consente di isolare le impostazioni nei database e le modifiche alle impostazioni predefinite interessano tutti gli altri database nell'istanza.  
  
-   Specificare la replica di backup. L'impostazione della replica di backup preferita viene usata dal [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per pianificare i backup. Per determinare se la replica corrente è la replica di backup preferita, usare il [Sys. fn_hadr_backup_is_preferred_replica &#40;Transact-SQL&#41; ](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) (funzione).  
  
-   Se la replica secondaria è configurata come replica preferita, deve essere configurata in modo da avere almeno l'accesso per la connessione in sola lettura. I gruppi di disponibilità privi di accesso per la connessione ai database secondari non sono supportati.  Per altre informazioni, vedere [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
-   Se si configura il [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] dopo aver configurato il gruppo di disponibilità, tramite il [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] si tenterà di copiare tutti i backup esistenti nel contenitore di archiviazione.  Se tramite il [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non sarà possibile trovare i backup esistenti o accedere a questi ultimi, verrà pianificato un backup completo del database. Questa operazione viene eseguita in modo particolare per ottimizzare le operazioni di backup per i database del gruppo di disponibilità.  
  
-   È possibile provare a disabilitare le impostazioni a livello di istanza se si sta creando un nuovo database di disponibilità e non si prevede di applicare le impostazioni a livello di istanza nel database  
  
-   Quando si usa la crittografia, usare lo stesso certificato in tutte le repliche. In questo modo vengono facilitate le operazioni di backup continue e ininterrotte in caso di failover su una replica diversa o di ripristini in quest'ultima.  
  
#### <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-for-an-availability-database"></a>Abilitare e configurare il [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per un database di disponibilità  
 In questa esercitazione vengono descritti i passaggi per abilitare e configurare il [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per un database (AGTestDB) nei computer Node1 e Node2, nonché i passaggi per abilitare il monitoraggio dello stato di integrità del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
1.  **Creare un account di archiviazione di Azure:** I backup vengono archiviati nel servizio di archiviazione Blob di Windows Azure. È necessario innanzitutto creare un account di archiviazione Windows Azure, nel caso non ne sia già disponibile uno. Per altre informazioni, vedere [creazione di un Account di archiviazione Windows Azure](http://www.windowsazure.com/manage/services/storage/how-to-create-a-storage-account/). Prendere nota del nome dell'account di archiviazione, delle chiavi di accesso e dell'URL dell'account di archiviazione. Le informazioni sul nome dell'account di archiviazione e sulla chiave di accesso vengono utilizzate per creare le credenziali SQL. Queste credenziali vengono utilizzate dal [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] durante le operazioni di backup per l'autenticazione nell'account di archiviazione.  
  
2.  **Creare credenziali SQL:** Creare credenziali SQL usando il nome dell'account di archiviazione come identità e la chiave di accesso di archiviazione come password.  
  
3.  **Assicurarsi che il servizio SQL Server Agent sia avviato e in esecuzione:** se non è in esecuzione, avviare SQL Server Agent. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è necessaria l'esecuzione di SQL Server Agent nell'istanza per poter eseguire le operazioni di backup.  Per assicurarsi che le operazioni in questione vengano eseguite regolarmente, è possibile impostare l'esecuzione automatica di SQL Agent.  
  
4.  **Determinare il periodo di conservazione:** Determinare il periodo di memorizzazione desiderato per i file di backup. Il periodo di memorizzazione viene specificato in giorni in un intervallo compreso tra 1 e 30. Il periodo di memorizzazione determina l'intervallo di tempo di recuperabilità del database.  
  
5.  **Creare una certificato o chiave asimmetrica da usare per la crittografia durante il backup:** Creare il certificato nel primo nodo, Node1 e quindi esportarlo in un file usando [certificato di BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)... Nel nodo 2 creare un certificato utilizzando il file esportato dal nodo 1. Per altre informazioni sulla creazione di un certificato da un file, vedere l'esempio nella [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql).  
  
6.  **Abilitare e configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per AGTestDB in Node1:** Avviare SQL Server Management Studio e connettersi all'istanza in Node1 in cui è installato il database di disponibilità. Nella finestra Query eseguire l'istruzione riportata di seguito dopo aver modificato i valori per il nome del database, l'URL di archiviazione, le credenziali SQL e il periodo di memorizzazione in base alle esigenze:  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     Per altre informazioni sulla creazione di un certificato per la crittografia, vedere la **creare un certificato di Backup** passaggio [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md).  
  
7.  **Abilitare e configurare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per AGTestDB in Node2:** Avviare SQL Server Management Studio e connettersi all'istanza in Node2 in cui è installato il database di disponibilità. Nella finestra Query eseguire l'istruzione riportata di seguito dopo aver modificato i valori per il nome del database, l'URL di archiviazione, le credenziali SQL e il periodo di memorizzazione in base alle esigenze:  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ora è abilitato nel database specificato. L'inizio delle operazioni di backup nel database può richiedere fino a 15 minuti. Il backup verrà eseguito nella replica di backup preferita.  
  
8.  **Esaminare la configurazione predefinita degli eventi estesi:**  Esaminare la configurazione degli eventi estesi eseguendo l'istruzione transact-SQL seguente nella replica [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per la pianificazione dei backup. Si tratta in genere dell'impostazione della replica di backup preferita per il gruppo di disponibilità a cui appartiene il database.  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     Verificare che gli eventi dei canali amministrativo, operativo e analitico siano abilitati per impostazione predefinita e che non possano essere disabilitati. Questa verifica dovrebbe essere sufficiente per monitorare gli eventi per i quali è richiesto un intervento manuale.  È possibile abilitare gli eventi di debug, ma in questi canali sono inclusi eventi informativi e di debug usati dal [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per rilevare eventuali problemi e risolverli. Per altre informazioni, vedere [monitoraggio di SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
9. **Abilitare e configurare notifiche per lo stato di integrità** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] contiene una stored procedure che consente di creare un processo dell'agente per inviare notifiche tramite posta elettronica di errori o avvisi che potrebbero richiedere attenzione.  Per ricevere notifiche di questo tipo, è necessario eseguire la stored procedure per creare un processo di SQL Server Agent. Nei passaggi seguenti viene illustrato il processo per abilitare e configurare le notifiche tramite posta elettronica:  
  
    1.  Configurare Posta elettronica database se non è già abilitato nell'istanza. Per altre informazioni, vedere [Configurare Posta elettronica database](../relational-databases/database-mail/configure-database-mail.md).  
  
    2.  Configurare la notifica di SQL Server Agent per l'uso di Posta elettronica database. Per altre informazioni, vedere [Configure SQL Server Agent Mail to Use Database Mail](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Abilitare le notifiche di posta elettronica per ricevere avvisi ed errori di backup:** Nella finestra query, eseguire le istruzioni Transact-SQL seguenti:  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email>'  
  
        ```  
  
         Per altre informazioni e uno script di esempio completo, vedere [monitoraggio di SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
10. **Visualizza i file di backup nell'Account di archiviazione Windows Azure:** Connettersi all'account di archiviazione da SQL Server Management Studio o il portale di gestione di Azure. Verrà visualizzato un contenitore per l'istanza di SQL Server in cui viene ospitato il database configurato per utilizzare il [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. È inoltre possibile visualizzare un database e un backup del log entro 15 minuti dall'abilitazione del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per il database.  
  
11. **Monitorare lo stato di integrità:**  è possibile eseguire il monitoraggio attraverso notifiche tramite posta elettronica configurate in precedenza o monitorare attivamente gli eventi registrati. Di seguito sono riportate alcune istruzioni Transact-SQL di esempio utilizzate per visualizzare gli eventi:  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event varchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 I passaggi descritti in questa sezione riguardano in modo specifico la configurazione del [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per la prima volta nel database. È possibile modificare le configurazioni esistenti usando la stessa stored procedure di sistema **sp_set_db_backup** e fornire i nuovi valori. Per altre informazioni, vedere [SQL Server Managed Backup to Windows Azure - impostazioni di archiviazione e memorizzazione](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md).  
  
### <a name="considerations-when-removing-a-database-from-alwayson-availability-group-configuration"></a>Considerazioni in caso di rimozione di un database dalla configurazione del gruppo di disponibilità AlwaysOn  
 Se un database viene rimosso dalla configurazione del gruppo di disponibilità AlwaysOn ed è ora un database autonomo, è consigliabile eseguire il backup usando [smart_admin.sp_backup_on_demand &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql). Quando si crea un backup del database in questo modo, si stabilisce una nuova catena di backup e il file verrà inserito nel contenitore specifico dell'istanza anziché nel contenitore Disponibilità in cui sono stati archiviati i backup quando il database faceva parte del gruppo di disponibilità.  
  
> [!WARNING]  
>  La recuperabilità del database in questo scenario dai backup precedenti alla modifica dello stato del gruppo di disponibilità non è garantita.  
  
  
