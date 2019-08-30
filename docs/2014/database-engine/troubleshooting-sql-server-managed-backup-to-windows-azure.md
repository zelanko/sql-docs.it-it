---
title: Risoluzione dei problemi di SQL Server backup gestito in Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: a34d35b0-48eb-4ed1-9f19-ea14754650da
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cbdf7f9b9e8a428ed3d3bf6bfcfe14dbd7da68fc
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153935"
---
# <a name="troubleshooting-sql-server-managed--backup-to-azure"></a>Risoluzione dei problemi di SQL Server backup gestito in Azure
  In questo argomento vengono descritti gli strumenti e le attività utilizzabili per la risoluzione dei problemi relativi agli errori che si possono verificare durante le operazioni di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
## <a name="overview"></a>Panoramica  
 In [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] sono inclusi controlli predefiniti e risoluzione dei problemi, pertanto in molti casi gli errori interni vengono risolti dal processo di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] stesso.  
  
 Un esempio di questo caso è l'eliminazione di un file di backup, causando un'interruzioni della catena di log che interessano la recuperabilità [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] . identificherà l'interruzioni nella catena di log e pianifica un backup immediatamente. Tuttavia si consiglia di monitorare lo stato e di risolvere tutti gli errori per cui è richiesto l'intervento manuale.  
  
 Tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] vengono registrati eventi e errori tramite stored procedure di sistema, viste di sistema ed eventi estesi. Tramite le stored procedure e le viste di sistema vengono fornite le informazioni di configurazione di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], lo stato dei backup pianificati, nonché gli errori acquisiti dagli eventi estesi. In [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] vengono utilizzati gli eventi estesi per acquisire gli errori da utilizzare per la risoluzione dei problemi. Oltre alla registrazione di eventi, tramite i criteri di amministrazione intelligente di SQL Server viene specificato lo stato di integrità utilizzato da un processo di notifica tramite posta elettronica per fornire la notifica o errori e problemi. Per altre informazioni, vedere [monitorare SQL Server backup gestito in Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]USA anche la stessa registrazione usata quando si esegue manualmente il backup in archiviazione di Azure (SQL Server backup nell'URL). Per ulteriori informazioni sui problemi relativi al backup in URL, vedere la sezione risoluzione dei problemi in [SQL Server procedure consigliate e risoluzione dei](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) problemi di backup in URL  
  
### <a name="general-troubleshooting-steps"></a>Procedura generale per la risoluzione dei problemi  
  
1.  Abilitare la notifica tramite posta elettronica per iniziare a ricevere messaggi di posta elettronica per errori e avvisi.  
  
     In alternativa, è anche possibile eseguire periodicamente `smart_admin.fn_get_health_status` per controllare gli errori e i conteggi aggregati. Ad esempio, `number_of_invalid_credential_errors` rappresenta il numero di volte in cui il backup intelligente ha tentato di eseguire un backup ma è stato restituito un errore di credenziali non valide. `Number_of_backup_loops` e `number_of_retention_loops` non sono errori; ma indicano il numero di volte in cui il thread di backup e il thread di memorizzazione hanno analizzato l'elenco di database. In genere, @begin_time quando @end_time e non vengono specificati, la funzione Visualizza le informazioni degli ultimi 30 minuti, quindi in genere è necessario visualizzare i valori diversi da zero per queste due colonne. Se vengono visualizzati valori pari a zero, significa che si è verificato un overload del sistema o che il sistema non risponde. Per ulteriori informazioni, vedere la sezione **risoluzione dei problemi di sistema** più avanti in questo argomento.  
  
2.  Esaminare i registri eventi estesi per ulteriori dettagli sugli errori e altri eventi associati.  
  
3.  Utilizzare le informazioni nei registri per risolvere il problema.  In caso di un problema o di un errore del sistema, potrebbe essere necessario riavviare il servizio o SQL Server Agent.  
  
### <a name="common-causes-of-errors"></a>Cause comuni degli errori  
 Di seguito è riportato l'elenco delle cause comuni che provocano gli errori:  
  
1.  **Modifiche alle credenziali SQL:** Se il nome della credenziale utilizzata da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] viene modificato o se viene eliminato, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non sarà in grado di eseguire i backup. La modifica deve essere applicata alle impostazioni di configurazione di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
2.  **Modifiche ai valori della chiave di accesso all'archiviazione:** Se i valori della chiave di archiviazione vengono modificati per l'account Azure, ma le credenziali SQL non vengono aggiornate con i [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] nuovi valori, avrà esito negativo quando si esegue l'autenticazione nella risorsa di archiviazione e non è possibile eseguire il backup dei database configurati per l'uso di questo account.  
  
3.  **Modifiche all'account di archiviazione di Azure:** L'eliminazione o la ridenominazione dell'account di archiviazione senza modifiche corrispondenti alle credenziali [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] SQL causerà un errore e non verrà eseguito alcun backup. Se si elimina un account di archiviazione, verificare che i database vengano riconfigurati con informazioni sull'account di archiviazione valide. Se un account di archiviazione viene ridenominato oppure i valori della chiave vengono modificati, verificare che queste modifiche vengano riflesse nelle credenziali SQL utilizzate da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
4.  **Modifiche alle proprietà del database:** Le modifiche ai modelli di recupero o la modifica del nome possono causare errori di backup.  
  
5.  **Modifiche al modello di recupero:** Se il modello di recupero del database viene modificato in semplice da completo o con registrazione minima delle operazioni bulk, i backup verranno arrestati e i database verranno ignorati da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Per altre informazioni, vedere [SQL Server backup gestito in Azure: Interoperabilità e coesistenza](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>Messaggi di errori più comuni e soluzioni  
  
1.  **Errori durante l'abilitazione [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]o la configurazione di:**  
  
     Errore: " Non è stato possibile accedere all'URL di archiviazione... Specificare una credenziale SQL valida... ": È possibile che si verifichi questo e altri errori simili che fanno riferimento a credenziali SQL.  In questi casi, esaminare il nome delle credenziali SQL fornite, nonché le informazioni archiviate nelle credenziali SQL, ovvero il nome dell'account di archiviazione e la chiave di accesso alle archiviazioni e verificare che siano correnti e valide.  
  
     Errore: "... Impossibile configurare il database... Poiché si tratta di un database di sistema: Questo errore verrà visualizzato se si tenta di abilitare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per un database di sistema.  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non supporta i backup per i database di sistema.  Per configurare il backup di un database di sistema, utilizzare altre tecnologie di backup di SQL Server, ad esempio i piani di manutenzione.  
  
     Errore: "... Specificare un periodo di conservazione... ": È possibile che vengano visualizzati errori relativi al periodo di conservazione se non è stato specificato un periodo di conservazione per il database o l'istanza quando si configurano questi valori per la prima volta. È inoltre possibile visualizzare un errore se si immette un valore diverso da un numero compreso tra 1 e 30. Il valore consentito per il periodo di memorizzazione è un numero compreso tra 1 e 30.  
  
2.  **Errori di notifica tramite posta elettronica:**  
  
     Errore: "Posta elettronica database non è abilitato...". questo errore verrà visualizzato se si abilitano le notifiche tramite posta elettronica, ma Posta elettronica database non è configurato nell'istanza. È necessario configurare Posta elettronica database nell'istanza per poter ricevere la notifica dello stato di integrità di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Per informazioni su come abilitare posta elettronica database, vedere [Configure posta elettronica database](../relational-databases/database-mail/configure-database-mail.md). È inoltre necessario abilitare SQL Server Agent per l'utilizzo di Posta elettronica database per le notifiche. Per ulteriori informazioni, vedere [prima di iniziare](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin).  
  
     Di seguito è riportato un elenco di numeri di errore che potrebbero essere visualizzati, associati alle notifiche tramite posta elettronica:  
  
    -   Numero errore 45209  
  
    -   Numero errore 45210  
  
    -   Numero errore 45211  
  
3.  **Errori di connettività:**  
  
    -   **Errori relativi alla connettività SQL:** Questi errori si verificano quando si verificano problemi di connessione a SQL Server istanza. Negli eventi estesi questi tipi di errori vengono esposti tramite il canale di amministrazione. Di seguito sono riportati i due eventi estesi per cui è possibile visualizzare gli errori relativi a questo tipo di problemi di connettività:  
  
         FileRetentionAdminXEvent con event_type = SqlError. Per i dettagli su questo errore, esaminare error_code, error_message e stack_trace dell'evento in questione. Error_code è il numero di errore di SqlException.  
  
         SmartBackupAdminXevent con i messaggi/prefissi di messaggio seguenti:  
  
         *"Si è verificato un errore interno durante la configurazione di SQL Server backup gestito in impostazioni predefinite di Azure per l'istanza. L'errore potrebbe essere temporaneo ".*  
  
         *"È probabile che si verifichino problemi di connettività con SQL Server. Il database verrà ignorato nell'iterazione corrente ".*  
  
         *"Query sulle informazioni sull'utilizzo del log non riuscita. L'errore potrebbe essere temporaneo. Il database verrà ignorato nell'iterazione corrente ".*  
  
         *"Eccezione SQL rilevata durante il caricamento dei metadati dell'agente SSMBackup2WA. L'errore potrebbe essere temporaneo. Verrà eseguito un nuovo tentativo di esecuzione dell'operazione.*  
  
         *"SSMBackup2WA ha rilevato un'eccezione SQL... "*  
  
    -   **Errori di connessione all'account di archiviazione:**  
  
         Le eccezioni di archiviazione vengono segnalate in FileRetentionAdminXEvent con event_type = XstoreError. Per i dettagli sull'errore, esaminare error_message e stack_trace dell'evento in questione.  
  
         Dal momento che da parte di Backup gestito di SQL Server viene utilizzata la tecnologia sottostante Backup nell'URL, gli errori relativi alla connettività di archiviazione vengono applicati a entrambe le funzionalità. Per ulteriori informazioni sulle procedure per la risoluzione dei problemi, vedere la sezione relativa alla **risoluzione dei problemi** dell'articolo sulle procedure consigliate e sulla risoluzione dei problemi di [SQL Server backup su URL](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) .  
  
### <a name="troubleshooting-system-issues"></a>Risoluzione dei problemi relativi al sistema  
 Di seguito vengono illustrati alcuni scenari quando si verifica un problema con il sistema (SQL Server, SQL Server Agent) e i relativi effetti su [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:  
  
-   **Sqlservr. exe smette di rispondere o smette di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] funzionare quando è in esecuzione:** Se SQL Server smette di funzionare, SQL Agent si arresta normalmente, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] si interrompe e gli eventi vengono registrati nel file SQL Agent. out.  
  
     Se SQL Server non risponde, gli eventi vengono registrati nel canale di amministrazione.  Un esempio del registro eventi:  
  
     *Errore SQL (il motore non risponde o ottiene sqlException: SqlException*   
     *il codice di errore, il messaggio e l'StackTrace verranno visualizzati in un canale di amministrazione XEvent, insieme ad alcune informazioni aggiuntive, ad esempio:*    
    *"È probabile che si verifichino problemi di connettività con SQL Server. Il database verrà ignorato nell'iterazione corrente "*  
  
-   **SQL Agent smette di rispondere o smette di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] funzionare quando è in esecuzione:**  
  
     Se SQL Agent si blocca, viene arrestato anche [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] e gli eventi vengono registrati nel canale di amministrazione. È simile agli scenari in cui SQL Server non risponde.  
  
     Se SQL Agent non risponde, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non sarà in grado di continuare con le operazioni di backup e gli eventi vengono registrati nel canale di amministrazione. Un esempio del registro eventi:  
  
     *Il processo si blocca: vedere il canale di amministrazione XEvent*   
    *"Un aggiornamento dello stato di avanzamento non è stato ricevuto da SQL Server più di" + costanti. DBBackupInfoMsgMaxWaitTime + "ore per il backup del database.   Il backup cloud SSM continuerà ad attendere ".*  
  
 Se è stata abilitata la notifica tramite posta elettronica, si riceverà una notifica che include il **numero di cicli di backup** e il **numero di cicli di conservazione**. Se il valore restituito nella notifica per una o entrambe queste due colonne è zero, potrebbe significare che il sistema non risponde.  
  
> [!WARNING]  
>  Nei processi interni che generano i risultati per il report si presuppone che i log di diagnostica del motore si trovino nello stesso percorso del log degli errori di SQL Agent che, per impostazione predefinita, si trova nella stessa cartella dei log degli errori dell'istanza di SQL Server. Se i log di diagnostica del motore vengono spostati in un percorso diverso da quello del log degli errori di SQL Agent, il sistema non sarà in grado di trovare i log di diagnostica di backup intelligenti e, di conseguenza, il report nella notifica tramite posta elettronica potrebbe non essere corretto. Ad esempio, è possibile che venga visualizzato un valore pari a **0** in tutti i campi segnalati, inclusi il numero di cicli di backup e il numero di cicli di memorizzazione. Nel caso dove i log di diagnostica vengono spostati in un percorso diverso, non vuol dire che il sistema non risponde, bensì non è in grado di trovare i log. Assicurarsi innanzitutto che il percorso dei log di diagnostica e quello dei log degli errori di SQL Agent sia lo stesso. Per verificare il percorso corrente dei log di diagnostica, è possibile usare [sys. dm _os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations). La `path` colonna restituisce il percorso corrente dei log di diagnostica del motore.  Deve trovarsi nella stessa cartella dei log degli errori di SQL Agent. È possibile che si ottenga il percorso dei log degli errori di SQL Agent utilizzando la stored procedure `dbo.sp_get_sqlagent_properties`.  
  
 Controllare i registri eventi estesi per visualizzare i dettagli degli errori. Correggere gli errori o riavviare SQL Server Agent per risolvere la situazione.  
  
  
