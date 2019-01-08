---
title: Risoluzione dei problemi relativi a SQL Server Managed Backup in Windows Azure | Microsoft Docs
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
ms.openlocfilehash: fd68f6f8bcb83bfbc980be0809e12141403e4012
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52522530"
---
# <a name="troubleshooting-sql-server-managed--backup-to-windows-azure"></a>Risoluzione dei problemi relativi al backup gestito di SQL Server in Windows Azure
  In questo argomento vengono descritti gli strumenti e le attività utilizzabili per la risoluzione dei problemi relativi agli errori che si possono verificare durante le operazioni di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
## <a name="overview"></a>Panoramica  
 In [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] sono inclusi controlli predefiniti e risoluzione dei problemi, pertanto in molti casi gli errori interni vengono risolti dal processo di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] stesso.  
  
 Esempio di uno di questi casi è un'eliminazione di un file di backup conseguente interruzione del log concatenare che interessa la recuperabilità - [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] identificherà l'interruzione nella catena di log e pianifica un backup da intraprendere immediatamente. Tuttavia si consiglia di monitorare lo stato e di risolvere tutti gli errori per cui è richiesto l'intervento manuale.  
  
 Tramite [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] vengono registrati eventi e errori tramite stored procedure di sistema, viste di sistema ed eventi estesi. Tramite le stored procedure e le viste di sistema vengono fornite le informazioni di configurazione di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], lo stato dei backup pianificati, nonché gli errori acquisiti dagli eventi estesi. In [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] vengono utilizzati gli eventi estesi per acquisire gli errori da utilizzare per la risoluzione dei problemi. Oltre alla registrazione di eventi, tramite i criteri di amministrazione intelligente di SQL Server viene specificato lo stato di integrità utilizzato da un processo di notifica tramite posta elettronica per fornire la notifica o errori e problemi. Per altre informazioni, vedere [monitoraggio di SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] utilizza inoltre la stessa registrazione utilizzata per l'esecuzione manuale del backup nel servizio di archiviazione Windows Azure (backup di SQL Server nell'URL). Per altre informazioni sul Backup nell'URL i problemi correlati, vedere la sezione sulla risoluzione dei problemi in [Backup SQL Server in URL le procedure consigliate e risoluzione dei problemi](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
### <a name="general-troubleshooting-steps"></a>Procedura generale per la risoluzione dei problemi  
  
1.  Abilitare la notifica tramite posta elettronica per iniziare a ricevere messaggi di posta elettronica per errori e avvisi.  
  
     In alternativa, è anche possibile eseguire periodicamente `smart_admin.fn_get_health_status` per controllare gli errori e i conteggi aggregati. Ad esempio, `number_of_invalid_credential_errors` rappresenta il numero di volte in cui il backup intelligente ha tentato di eseguire un backup ma è stato restituito un errore di credenziali non valide. `Number_of_backup_loops` e `number_of_retention_loops` non sono errori; ma indicano il numero di volte in cui il thread di backup e il thread di memorizzazione hanno analizzato l'elenco di database. In genere, quando @begin_time e @end_time vengono omessi, la funzione Mostra le informazioni degli ultimi 30 minuti, quindi dovrebbe essere visualizzato in genere valori diversi da zero per queste due colonne. Se vengono visualizzati valori pari a zero, significa che si è verificato un overload del sistema o che il sistema non risponde. Per altre informazioni, vedere **risoluzione dei problemi di sistema** sezione più avanti in questo argomento.  
  
2.  Esaminare i registri eventi estesi per ulteriori dettagli sugli errori e altri eventi associati.  
  
3.  Utilizzare le informazioni nei registri per risolvere il problema.  In caso di un problema o di un errore del sistema, potrebbe essere necessario riavviare il servizio o SQL Server Agent.  
  
### <a name="common-causes-of-errors"></a>Cause comuni degli errori  
 Di seguito è riportato l'elenco delle cause comuni che provocano gli errori:  
  
1.  **Modifiche alle credenziali SQL:** Se il nome delle credenziali utilizzato da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] viene modificato o se viene eliminato, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non sarà in grado di eseguire i backup. La modifica deve essere applicata alle impostazioni di configurazione di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
2.  **Modifiche ai valori chiave di accesso archiviazione:** Se vengono modificati i valori di chiave di archiviazione per l'account di Windows Azure, ma le credenziali SQL non viene aggiornata con i nuovi valori, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] avrà esito negativo durante l'autenticazione alla risorsa di archiviazione e non riesce a eseguire backup di database configurato per usare questo account.  
  
3.  **Modifiche apportate all'Account di archiviazione di Azure di Windows:** L'eliminazione o ridenominazione dell'account di archiviazione senza le modifiche corrispondenti alle credenziali SQL causerà [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] esito negativo e non verranno eseguiti alcun backup. Se si elimina un account di archiviazione, verificare che i database vengano riconfigurati con informazioni sull'account di archiviazione valide. Se un account di archiviazione viene ridenominato oppure i valori della chiave vengono modificati, verificare che queste modifiche vengano riflesse nelle credenziali SQL utilizzate da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
4.  **Modifiche alle proprietà del Database:** Le modifiche ai modelli di recupero o la modifica del nome può causare mancata esecuzione dei backup.  
  
5.  **Modifiche al modello di recupero:** Se il modello di recupero del database viene modificato su simple completa o con registrazione minima delle operazioni bulk, i backup verranno arrestati e i database verranno ignorati da [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Per altre informazioni, vedere [SQL Server Managed Backup to Windows Azure: Interoperabilità e coesistenza](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>Messaggi di errori più comuni e soluzioni  
  
1.  **Errori durante l'abilitazione o la configurazione [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:**  
  
     Errore: " Non è riuscito ad accedere all'URL di archiviazione... Specificare una credenziale SQL valida...": È possibile riscontrare questo e altri errori simili che fa riferimento alle credenziali SQL.  In questi casi, verificare il nome delle credenziali SQL fornite, nonché le informazioni archiviate nelle credenziali SQL - nome account di archiviazione e la chiave di accesso di archiviazione e assicurarsi che siano correnti e valide.  
  
     Errore: "... non è possibile configurare il database... perché si tratta di un database di sistema": Verrà visualizzato questo errore se si prova ad abilitare [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] per un database di sistema.  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non supporta i backup per i database di sistema.  Per configurare il backup di un database di sistema, utilizzare altre tecnologie di backup di SQL Server, ad esempio i piani di manutenzione.  
  
     Errore: "... Specificare un periodo di conservazione...": Se uno non è stato specificato un periodo di conservazione per il database o istanza durante la configurazione di questi valori per la prima volta, è possibile riscontrare errori riguardanti il periodo di conservazione. È inoltre possibile visualizzare un errore se si immette un valore diverso da un numero compreso tra 1 e 30. Il valore consentito per il periodo di memorizzazione è un numero compreso tra 1 e 30.  
  
2.  **Errori di notifica di posta elettronica:**  
  
     Errore: "Posta elettronica database non è abilitata...", verrà visualizzato questo errore se si abilitano le notifiche di posta elettronica, ma posta elettronica Database non è configurato nell'istanza. È necessario configurare Posta elettronica database nell'istanza per poter ricevere la notifica dello stato di integrità di [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Per informazioni su come abilitare posta elettronica database, vedere [Configura posta elettronica Database](../relational-databases/database-mail/configure-database-mail.md). È inoltre necessario abilitare SQL Server Agent per l'utilizzo di Posta elettronica database per le notifiche. Per altre informazioni, vedere [prima di iniziare](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin).  
  
     Di seguito è riportato un elenco di numeri di errore che potrebbero essere visualizzati, associati alle notifiche tramite posta elettronica:  
  
    -   Numero errore: 45209  
  
    -   Numero errore: 45210  
  
    -   Numero errore: 45211  
  
3.  **Errori di connettività:**  
  
    -   **Errori relativi alla connettività SQL:** Questi errori si verificano quando sono presenti problemi di connessione all'istanza di SQL Server. Negli eventi estesi questi tipi di errori vengono esposti tramite il canale di amministrazione. Di seguito sono riportati i due eventi estesi per cui è possibile visualizzare gli errori relativi a questo tipo di problemi di connettività:  
  
         FileRetentionAdminXEvent con event_type = SqlError. Per i dettagli su questo errore, esaminare error_code, error_message e stack_trace dell'evento in questione. Error_code è il numero di errore di SqlException.  
  
         SmartBackupAdminXevent con i messaggi/prefissi di messaggio seguenti:  
  
         *"Si è verificato un errore interno durante la configurazione del Backup gestito di SQL Server per le impostazioni predefinite di Windows Azure, ad esempio. Errore potrebbe essere temporaneo."*  
  
         *"Probabilmente riscontra problemi di connettività di SQL Server. Il database verrà ignorato nell'iterazione corrente."*  
  
         *"Query sulle informazioni del log non è riuscita. L'errore potrebbe essere temporaneo. Il database verrà ignorato nell'iterazione corrente."*  
  
         *"Eccezione SQL rilevata durante il caricamento dei metadati dell'agente SSMBackup2WA. L'errore potrebbe essere temporaneo. Operazione verrà rieseguita."*  
  
         *"SSMBackup2WA eccezione SQL rilevata durante... "*  
  
    -   **Errori di connessione all'account di archiviazione:**  
  
         Le eccezioni di archiviazione vengono segnalate in FileRetentionAdminXEvent con event_type = XstoreError. Per i dettagli sull'errore, esaminare error_message e stack_trace dell'evento in questione.  
  
         Dal momento che da parte di Backup gestito di SQL Server viene utilizzata la tecnologia sottostante Backup nell'URL, gli errori relativi alla connettività di archiviazione vengono applicati a entrambe le funzionalità. Per ulteriori informazioni sulla risoluzione dei problemi, vedere **risoluzione dei problemi di sezione** delle [SQL Server Backup in URL Best Practices and Troubleshooting](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) articolo.  
  
### <a name="troubleshooting-system-issues"></a>Risoluzione dei problemi relativi al sistema  
 Di seguito vengono illustrati alcuni scenari quando si verifica un problema con il sistema (SQL Server, SQL Server Agent) e i relativi effetti su [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:  
  
-   **Sqlservr.exe non risponde o si blocca quando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è in esecuzione:** Se SQL Server smette di funzionare, SQL Agent verrà chiuso normalmente, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] anche si interrompe e gli eventi vengono registrati nel file di SQL Agent.  
  
     Se SQL Server non risponde, gli eventi vengono registrati nel canale di amministrazione.  Un esempio del registro eventi:  
  
     *Errore di SQL (motore non risponde o restituito sqlException: SqlException:*   
     *analisi dello stack, messaggio e codice di errore verrà visualizzati in un canale di amministrazione xevent, insieme a alcune informazioni aggiuntive, ad esempio:*   
    *"Probabilmente riscontra problemi di connettività di SQL Server. Database verrà ignorato nell'iterazione corrente"*  
  
-   **SQL Agent non risponde o si blocca quando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] è in esecuzione:**  
  
     Se SQL Agent si blocca, viene arrestato anche [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] e gli eventi vengono registrati nel canale di amministrazione. È simile agli scenari in cui SQL Server non risponde.  
  
     Se SQL Agent non risponde, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] non sarà in grado di continuare con le operazioni di backup e gli eventi vengono registrati nel canale di amministrazione. Un esempio del registro eventi:  
  
     *Blocco del processo: vedere canale di amministrazione xevents*   
    *"Non è stato ricevuto un aggiornamento dello stato da SQL Server in più di" + dbbackupinfomsgmaxwaittime + "ore per il backup del database.   Backup Cloud di SSM rimarrà in attesa. "*  
  
 Se è stata abilitata la notifica di posta elettronica, si riceverà una notifica che include **numero di cicli di Backup** e **numero di cicli di memorizzazione**. Se il valore restituito nella notifica per una o entrambe queste due colonne è zero, potrebbe significare che il sistema non risponde.  
  
> [!WARNING]  
>  Nei processi interni che generano i risultati per il report si presuppone che i log di diagnostica del motore si trovino nello stesso percorso del log degli errori di SQL Agent che, per impostazione predefinita, si trova nella stessa cartella dei log degli errori dell'istanza di SQL Server. Se i log di diagnostica del motore vengono spostati in un percorso diverso da quello del log degli errori di SQL Agent, il sistema non sarà in grado di trovare i log di diagnostica di backup intelligenti e, di conseguenza, il report nella notifica tramite posta elettronica potrebbe non essere corretto. Ad esempio, si potrebbe visualizzare un valore pari **0** tutti i campi segnalati, tra cui il numero di cicli di Backup e il numero di cicli di memorizzazione. Nel caso dove i log di diagnostica vengono spostati in un percorso diverso, non vuol dire che il sistema non risponde, bensì non è in grado di trovare i log. Assicurarsi innanzitutto che il percorso dei log di diagnostica e quello dei log degli errori di SQL Agent sia lo stesso. Per verificare il percorso corrente dei log di diagnostica, è possibile usare [os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations). Il `path` colonna restituisce la posizione corrente del motore di log di diagnostica.  Deve essere nella stessa cartella dei log degli errori di SQL Agent. È possibile che si ottenga il percorso dei log degli errori di SQL Agent utilizzando la stored procedure `dbo.sp_get_sqlagent_properties`.  
  
 Controllare i registri eventi estesi per visualizzare i dettagli degli errori. Correggere gli errori o riavviare SQL Server Agent per risolvere la situazione.  
  
  
