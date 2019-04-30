---
title: Domande frequenti per gli amministratori di replica | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- administering replication, frequently asked questions
- replication [SQL Server], administering
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce7e9249ec7ba97fdd159a743be30036847882b3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63207052"
---
# <a name="frequently-asked-questions-for-replication-administrators"></a>Domande frequenti per gli amministratori di replica
  Le domande e risposte seguenti offrono indicazioni su una vasta gamma di attività svolte dagli amministratori dei database replicati.  
  
## <a name="configuring-replication"></a>Configurazione della replica  
  
### <a name="does-activity-need-to-be-stopped-on-a-database-when-it-is-published"></a>È necessario arrestare l'attività su un database quando questo viene pubblicato?  
 No. Durante la creazione di una pubblicazione l'attività sul database può proseguire. Tenere presente che la produzione di uno snapshot può impegnare una grande quantità di risorse, per questo conviene generare gli snapshot durante i periodi di minore attività sul database. Per impostazione predefinita, viene generato uno snapshot al termine della Creazione guidata nuova pubblicazione.  
  
### <a name="are-tables-locked-during-snapshot-generation"></a>Durante la generazione dello snapshot le tabelle sono bloccate?  
 La durata dei blocchi dipende dal tipo di replica utilizzata:  
  
-   Per le pubblicazioni di tipo merge, l'agente snapshot non imposta alcun blocco.  
  
-   Per le pubblicazioni transazionali, l'agente snapshot per impostazione predefinita registra i blocchi solo durante la fase iniziale della generazione dello snapshot.  
  
-   Per le pubblicazioni snapshot, l'agente snapshot registra i blocchi durante l'intero processo di generazione dello snapshot.  
  
 Dato tuttavia che il blocco impedisce l'aggiornamento delle tabelle da parte di altri utenti, è consigliabile pianificare l'esecuzione dell'agente snapshot durante gli orari di minore attività del database, specialmente per le pubblicazioni snapshot.  
  
### <a name="when-is-a-subscription-available-when-can-the-subscription-database-be-used"></a>Quando è disponibile una sottoscrizione? Quando è possibile utilizzare il database di sottoscrizione?  
 Una sottoscrizione è disponibile dopo che al database di sottoscrizione è stato applicato lo snapshot. Anche se il database di sottoscrizione è accessibile prima di questo momento, non dovrebbe essere utilizzato prima che sia stato applicato lo snapshot. Utilizzare Monitoraggio replica per verificare lo stato della generazione e dell'applicazione dello snapshot.  
  
-   Lo snapshot viene generato dall'agente snapshot. Visualizzare lo stato della generazione dello snapshot nella scheda **Agenti** per una pubblicazione in Monitoraggio replica. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
-   Lo snapshot viene applicato dall'agente di distribuzione o dall'agente di merge. Visualizzare lo stato dell'applicazione dello snapshot nella pagina **Agente di distribuzione** o **Agente di merge** di Monitoraggio replica. 
  
### <a name="what-happens-if-the-snapshot-agent-has-not-completed-when-the-distribution-or-merge-agent-starts"></a>Cosa accade se l'agente snapshot non ha concluso la propria attività quando viene avviato l'agente di distribuzione o l'agente di merge?  
 L'esecuzione dell'agente di distribuzione o di merge in contemporanea con quella dell'agente snapshot non genera un errore. Tuttavia, è necessario considerare quanto segue:  
  
-   Se l'agente di distribuzione o di merge è configurato per essere eseguito in modo continuato, lo snapshot verrà applicato automaticamente al termine dell'esecuzione dell'agente snapshot.  
  
-   Se l'agente di distribuzione o di merge è configurato per essere eseguito in base a una pianificazione o su richiesta e quando viene eseguito non è disponibile alcuno snapshot, l'agente verrà chiuso e invierà un messaggio indicante che ancora non vi è uno snapshot disponibile. È necessario ripetere l'esecuzione dell'agente per applicare lo snapshot dopo l'esecuzione dell'agente snapshot. Per altre informazioni sull'esecuzione degli agenti, vedere [Sincronizzare una sottoscrizione push](../synchronize-a-push-subscription.md), [Sincronizzare una sottoscrizione pull](../synchronize-a-pull-subscription.md) e [Concetti di base relativi ai file eseguibili dell'agente di replica](../concepts/replication-agent-executables-concepts.md).  
  
### <a name="should-i-script-my-replication-configuration"></a>È necessario creare lo script della configurazione di replica?  
 Sì. La creazione dello script della configurazione di replica è un elemento fondamentale di qualunque piano di ripristino di emergenza per una topologia di replica. Per ulteriori informazioni sulla creazione di script, vedere [Scripting Replication](../scripting-replication.md).  
  
### <a name="what-recovery-model-is-required-on-a-replicated-database"></a>Quale modello di recupero è necessario su un database replicato?  
 Le funzioni di replica che utilizzano correttamente uno dei modelli di recupero: con registrazione minima, con registrazione minima delle operazioni bulk o con registrazione completa. La replica di tipo merge tiene traccia delle modifiche archiviando le informazioni in tabelle di metadati. La replica transazionale tiene traccia delle modifiche contrassegnando il log delle transazioni, ma il modello di recupero non influisce su questo processo di contrassegno.  
  
### <a name="why-does-replication-add-a-column-to-replicated-tables-will-it-be-removed-if-the-table-isnt-published"></a>Perché la replica aggiunge una colonna alle tabelle replicate? Tale colonna viene rimossa se la tabella non viene pubblicata?  
 Per tener traccia delle modifiche, la replica di tipo merge e la replica transazionale con sottoscrizioni ad aggiornamento in coda devono essere in grado di identificare in modo univoco ogni riga di ogni tabella pubblicata. A tale scopo:  
  
-   La replica di tipo merge aggiunge la colonna **rowguid** a ogni tabella, a meno che questa non contenga già una colonna del tipo di dati **uniqueidentifier** con il set di proprietà **ROWGUIDCOL** : in tal caso, viene usata questa colonna. Se la tabella viene rimossa dalla pubblicazione, la colonna **rowguid** viene eliminata; se per il rilevamento è stata utilizzata una colonna esistente, questa non viene eliminata.  
  
-   Se una pubblicazione transazionale supporta le sottoscrizioni ad aggiornamento in coda, la replica aggiunge la colonna **msrepl_tran_version** a ogni tabella. Se la tabella viene rimossa dalla pubblicazione, la colonna **msrepl_tran_version** non viene eliminata.  
  
-   In un filtro non deve essere inclusa la colonna `rowguidcol` utilizzata dalla replica per identificare le righe. Per impostazione predefinita, si tratta della colonna aggiunta al momento dell'impostazione della replica di tipo merge ed è denominata **rowguid**.  
  
### <a name="how-do-i-manage-constraints-on-published-tables"></a>Come si gestiscono i vincoli sulle tabelle pubblicate?  
 Riguardo ai vincoli sulle tabelle pubblicate, è necessario considerare diversi elementi:  
  
-   La replica transazionale richiede un vincolo di chiave primaria in ogni tabella pubblicata. La replica di tipo merge non richiede una chiave primaria ma se ne contiene una è necessario che venga replicata. La replica snapshot non richiede una chiave primaria.  
  
-   Per impostazione predefinita i vincoli di chiave primaria, gli indici e i vincoli CHECK vengono replicati nei Sottoscrittori.  
  
-   Per impostazione predefinita, l'opzione NOT FOR REPLICATION viene specificata per i vincoli di chiave esterna e per i vincoli CHECK; questi vincoli vengono imposti per le operazioni dell'utente ma non per quelle dell'agente.  
  
 Per informazioni sull'impostazione delle opzioni dello schema tramite cui si controlla l'eventuale esecuzione della replica dei vincoli, vedere [Specify Schema Options](../publish/specify-schema-options.md).  
  
### <a name="how-do-i-manage-identity-columns"></a>Come si gestiscono le colonne Identity?  
 La replica offre la gestione automatica dell'intervallo di valori Identity per le topologie di replica che includono aggiornamenti nel Sottoscrittore. Per altre informazioni, vedere [Replicare colonne Identity](../publish/replicate-identity-columns.md).  
  
### <a name="can-the-same-objects-be-published-in-different-publications"></a>È possibile pubblicare gli stessi oggetti in pubblicazioni diverse?  
 Sì, ma con alcune restrizioni. Per altre informazioni, vedere la sezione "Pubblicazione di tabelle in più di una pubblicazione" nell'argomento [Pubblicare dati e oggetti di database](../publish/publish-data-and-database-objects.md).  
  
### <a name="can-multiple-publications-use-the-same-distribution-database"></a>È possibile l'utilizzo dello stesso database di distribuzione da parte di più pubblicazioni?  
 Sì. Non vi sono restrizioni al numero o ai tipi di pubblicazioni che possono utilizzare lo stesso database di distribuzione. Tutte le pubblicazioni di un dato server di pubblicazione devono utilizzare lo stesso server di distribuzione e database di distribuzione.  
  
 Se si dispone di più pubblicazioni, è possibile configurare più database di distribuzione nel server di distribuzione per garantire che il flusso di dati che attraversa ogni database di distribuzione provenga da una sola pubblicazione. Per aggiungere un database di distribuzione, usare la finestra di dialogo **Proprietà database di distribuzione** oppure [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql). Per altre informazioni sull'accesso a questa finestra di dialogo, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="how-do-i-find-information-on-the-distributor-and-publisher-such-as-which-objects-in-a-database-are-published"></a>In che modo è possibile reperire informazioni sul server di distribuzione e sul quello di pubblicazione, ad esempio per sapere quali oggetti di un database vengono pubblicati?  
 Queste informazioni sono disponibili tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e diverse stored procedure di replica. Per altre informazioni, vedere [Distributor and Publisher Information Script](distributor-and-publisher-information-script.md).  
  
### <a name="does-replication-encrypt-data"></a>La replica crittografa i dati?  
 No. La replica non crittografa i dati archiviati nel database o trasferiti nella rete. Per altre informazioni, vedere la sezione "Crittografia" dell'argomento [la sicurezza della replica di SQL Server](../security/view-and-modify-replication-security-settings.md).  
  
### <a name="how-do-i-replicate-data-over-the-internet"></a>Come si replicano i dati su Internet?  
 È possibile replicare i dati su Internet utilizzando:  
  
-   Una rete privata virtuale (VPN). Per altre informazioni, vedere [Pubblicare i dati su Internet tramite VPN](../publish-data-over-the-internet-using-vpn.md).  
  
-   L'opzione di sincronizzazione Web per la replica di tipo merge. Per altre informazioni, vedere [Web Synchronization for Merge Replication](../web-synchronization-for-merge-replication.md).  
  
 Tutti i tipi di replica di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possono replicare i dati in una VPN, ma è consigliabile considerare la sincronizzazione Web se si utilizza la replica di tipo merge.  
  
### <a name="does-replication-resume-if-a-connection-is-dropped"></a>La replica viene ripresa in caso di interruzione della connessione?  
 Sì. L'elaborazione della replica viene ripresa dal punto in cui si era arrestata per interruzione della connessione. Se si utilizza la replica di tipo merge in una rete inaffidabile, è consigliabile considerare l'utilizzo dei record logici, che garantisce che le modifiche correlate vengano elaborate come una unità. Per altre informazioni, vedere [Raggruppare modifiche alle righe correlate con record logici](../merge/group-changes-to-related-rows-with-logical-records.md).  
  
### <a name="does-replication-work-over-low-bandwidth-connections-does-it-use-compression"></a>La replica funziona su connessioni a larghezza di banda ridotta? Utilizza la compressione?  
 Sì, la replica funziona su connessioni a larghezza di banda ridotta. Per le connessioni TCP/IP, utilizza la compressione offerta dal protocollo ma non offre una compressione aggiuntiva. Per le connessioni con sincronizzazione Web in HTTPS, utilizza la compressione offerta dal protocollo e la compressione aggiuntiva dei file XML utilizzati per replicare le modifiche.  
  
## <a name="logins-and-object-ownership"></a>Account di accesso e proprietà degli oggetti  
  
### <a name="are-logins-and-passwords-replicated"></a>Gli account di accesso e le password vengono replicati?  
 No. Per trasferire account di accesso e password da un server di pubblicazione a uno o più Sottoscrittori, si potrebbe creare un pacchetto DTS.  
  
### <a name="what-are-schemas-and-how-are-they-replicated"></a>Cosa sono gli schemi e in che modo vengono replicati?  
 A partire da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], *schema* ha due significati:  
  
-   La definizione di un oggetto, come un'istruzione CREATE TABLE. Per impostazione predefinita, la replica copia le definizioni di tutti gli oggetti replicati nel Sottoscrittore.  
  
-   Lo spazio dei nomi in cui viene creato un oggetto: \<Database>.\<Schema>.\<Oggetto>. Gli schemi vengono definiti utilizzando l'istruzione CREATE SCHEMA.  
  
-   In relazione agli schemi e alla proprietà degli oggetti, la replica ha il seguente comportamento predefinito nella Creazione guidata nuova pubblicazione:  
  
-   Per gli articoli di pubblicazioni di tipo merge con un livello di compatibilità 90 o superiore, per le pubblicazioni snapshot e quelle transazionali: per impostazione predefinita, il proprietario dell'oggetto nel Sottoscrittore è uguale al proprietario dell'oggetto corrispondente nel server di pubblicazione. Se nel Sottoscrittore non esistono gli schemi che possiedono gli oggetti, vengono creati automaticamente.  
  
-   Per articoli contenuti in pubblicazioni di tipo merge con un livello di compatibilità inferiore a 90: per impostazione predefinita, il proprietario viene lasciato vuoto e viene specificato come **dbo** durante la creazione dell'oggetto nel Sottoscrittore.  
  
-   Per articoli contenuti in pubblicazioni Oracle: per impostazione predefinita, viene specificato il proprietario **dbo**.  
  
-   Per articoli di pubblicazioni che usano snapshot in modalità carattere (usati per Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Sottoscrittori [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ): per impostazione predefinita, il proprietario rimane vuoto. Il proprietario viene impostato sul proprietario associato all'account utilizzato dall'agente di distribuzione o dall'agente di merge per la connessione al Sottoscrittore.  
  
 Il proprietario dell'oggetto può essere modificato tramite la finestra di dialogo **Proprietà articolo - \<***Articolo***>** e tramite le stored procedure **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle** e **sp_changemergearticle**. Per altre informazioni, vedere [Visualizzare e modificare le proprietà della pubblicazione](../publish/view-and-modify-publication-properties.md), [Definire un articolo](../publish/define-an-article.md) e [Visualizzare e modificare le proprietà degli articoli](../publish/view-and-modify-article-properties.md).  
  
### <a name="how-can-grants-on-the-subscription-database-be-configured-to-match-grants-on-the-publication-database"></a>In che modo è possibile configurare le concessioni del database di sottoscrizione per ottenere la corrispondenza con quelle del database di pubblicazione?  
 Per impostazione predefinita, la replica non esegue istruzioni GRANT nel database di sottoscrizione. Se si desidera che le autorizzazioni del database di sottoscrizione corrispondano a quelle del database di pubblicazione, utilizzare uno dei seguenti metodi.  
  
-   Eseguire le istruzioni GRANT direttamente nel database di sottoscrizione.  
  
-   Per eseguire le istruzioni, utilizzare uno script post-snapshot. Per altre informazioni, vedere [Eseguire gli script prima e dopo l'applicazione dello snapshot](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  
  
-   Per eseguire le istruzioni, utilizzare la stored procedure [sp_addscriptexec](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql) .  
  
### <a name="what-happens-to-permissions-granted-in-a-subscription-database-if-a-subscription-is-reinitialized"></a>Cosa accade alle autorizzazioni concesse in un database di sottoscrizione se una sottoscrizione viene reinizializzata?  
 Per impostazione predefinita, gli oggetti nel Sottoscrittore vengono eliminati e ricreati quando viene reinizializzata una sottoscrizione, cosa che provoca l'eliminazione di tutte le autorizzazioni concesse per tali oggetti. Questa operazione può essere gestita in due modi:  
  
-   Riapplicare le concessioni dopo la reinizializzazione utilizzando le tecniche descritte nella sezione precedente.  
  
-   Specificare che gli oggetti non devono essere eliminati alla reinizializzazione della sottoscrizione. Prima della reinizializzazione, eseguire una delle seguenti operazioni:  
  
    -   Eseguire [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) o [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Specificare il valore 'pre_creation_cmd' (**sp_changearticle**) o 'pre_creation_command' (**sp_changemergearticle**) per il parametro **@property** e il valore 'none', 'delete' o 'truncate' per il parametro **@value**.  
  
    -   Nella sezione **Oggetto di destinazione\< della finestra di dialogo** Proprietà articolo - **Articolo>** selezionare il valore **Non modificare l'oggetto esistente**, **Elimina i dati. Se all'articolo è associato un filtro di riga, elimina solo i dati che soddisfano i criteri del filtro.** oppure **Tronca tutti i dati nell'oggetto esistente** per l'opzione **Azione se il nome è in uso**. Per altre informazioni sull'accesso a questa finestra di dialogo, vedere [Visualizzare e modificare le proprietà della pubblicazione](../publish/view-and-modify-publication-properties.md).  
  
## <a name="database-maintenance"></a>Manutenzione database  
  
### <a name="why-cant-i-run-truncate-table-on-a-published-table"></a>Per quale motivo non è possibile eseguire TRUNCATE TABLE su una tabella pubblicata?  
 TRUNCATE TABLE è un'operazione non registrata che non attiva i trigger. Non è consentita perché la replica non può tener traccia delle modifiche provocate dall'operazione: la replica transazionale tiene traccia delle modifiche tramite il log delle transazioni, la replica di tipo merge tramite i trigger sulle tabelle pubblicate.  
  
### <a name="what-is-the-effect-of-running-a-bulk-insert-command-on-a-replicated-database"></a>Quale è l'effetto dell'esecuzione di un comando BULK INSERT su un database replicato?  
 Per la replica transazionale, gli inserimenti bulk vengono rilevati e replicati come gli altri inserimenti. Per la replica di tipo merge, è necessario verificare che i metadati di rilevamento delle modifiche vengano aggiornati correttamente.  
  
### <a name="are-there-any-replication-considerations-for-backup-and-restore"></a>Il backup e il ripristino presentano delle considerazioni relativamente alla replica?  
 Sì. I database interessati alla replica richiedono alcune considerazioni speciali per i database. Per altre informazioni, vedere [Eseguire il backup e ripristino di database replicati](back-up-and-restore-replicated-databases.md).  
  
### <a name="does-replication-affect-the-size-of-the-transaction-log"></a>La replica influisce sulla dimensione del log delle transazioni?  
 A differenza della replica di tipo merge e della replica snapshot, la replica transazionale può influire sulla dimensione del log delle transazioni. Se un database include una o più pubblicazioni transazionali, il log non viene troncato finché tutte le transazioni significative per le pubblicazioni non sono state recapitate al database di distribuzione. Se la dimensione del log delle transazioni aumenta in modo eccessivo e l'agente di lettura log viene eseguito in base a una pianificazione, è consigliabile ridurre l'intervallo tra le esecuzioni oppure impostare l'esecuzione in modalità continua. Se l'agente viene impostato per l'esecuzione in modalità continua (impostazione predefinita) verificare che venga eseguito. Per altre informazioni sulla verifica dello stato dell'agente di lettura Log, vedere [visualizzare le informazioni ed eseguire attività con Monitoraggio replica](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Inoltre, se nel database di pubblicazione o in quello di distribuzione è stata impostata l'opzione 'sync with backup', il troncamento del log delle transazioni avviene solo dopo il backup di tutte le transazioni. Se la dimensione del log delle transazioni sta aumentando in modo eccessivo e questa azione è stata impostata, è consigliabile accorciare l'intervallo tra l'esecuzione di operazioni di backup di tale log. Per altre informazioni sul backup e il ripristino dei database coinvolti nella replica transazionale, vedere [Strategie di backup e ripristino della replica snapshot e della replica transazionale](strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### <a name="how-do-i-rebuild-indexes-or-tables-in-replicated-databases"></a>Come si ricompilano gli indici o le tabelle nei database replicati?  
 Per la ricompilazione degli indici esistono diversi meccanismi. Possono essere utilizzati tutti, senza considerazioni speciali per la replica, con la seguente eccezione: le chiavi primarie sono necessarie nelle tabelle delle pubblicazioni transazionali, pertanto non è possibile eliminare e ricreare le chiavi primarie su queste tabelle.  
  
### <a name="how-do-i-add-or-change-indexes-on-publication-and-subscription-databases"></a>Come si aggiungono o si modificano gli indici nei database di pubblicazione e di sottoscrizione?  
 È possibile aggiungere gli indici nel server di pubblicazione o nei Sottoscrittori senza particolari considerazioni per la replica. Ricordare che gli indici possono influire sulle prestazioni. CREATE INDEX e ALTER INDEX non vengono replicati, pertanto se si aggiunge o si modifica un indice, ad esempio, nel server di pubblicazione, è necessario eseguire la stessa aggiunta o modifica nel Sottoscrittore se si desidera che venga riflessa in quest'ultimo.  
  
### <a name="how-do-i-move-or-rename-files-for-databases-involved-in-replication"></a>Come si spostano o si rinominano i file per i database interessati alla replica?  
 Nelle versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]lo spostamento o la ridenominazione dei file di database richiede lo scollegamento e il ricollegamento del database. Poiché un database replicato non può essere scollegato, innanzitutto era necessario rimuovere la replica da questi database. A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], è possibile spostare o rinominare i file senza scollegare e ricollegare il database, senza alcun effetto sulla replica. Per altre informazioni sullo spostamento e la ridenominazione dei file, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
### <a name="how-do-i-drop-a-table-that-is-being-replicated"></a>Come si elimina una tabella in corso di replica?  
 Eliminare in primo luogo l'articolo dalla pubblicazione usando [sp_droparticle](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql), [sp_dropmergearticle](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql) o la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>**, quindi eliminarlo dal database usando `DROP <Object>`. Dopo l'aggiunta di sottoscrizioni non è possibile eliminare articoli dalle pubblicazioni snapshot o transazionali: è necessario eliminare prima le sottoscrizioni. Per altre informazioni, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="how-do-i-add-or-drop-columns-on-a-published-table"></a>Come si aggiungono o si eliminano colonne in una tabella pubblicata?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta una vasta gamma di modifiche dello schema sugli oggetti pubblicati, inclusa l'aggiunta e l'eliminazione di colonne. Ad esempio, se si esegue ALTER TABLE ... DROP COLUMN nel server di pubblicazione, l'istruzione viene replicata ai Sottoscrittori e poi eseguita per eliminare la colonna. I Sottoscrittori che eseguono versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] supportano l'aggiunta e l'eliminazione di colonne tramite le stored procedure [sp_repladdcolumn](/sql/relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql) e [sp_repldropcolumn](/sql/relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql). Per altre informazioni, vedere [Apportare modifiche allo schema nei database di pubblicazione](../publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="replication-maintenance"></a>Manutenzione della replica  
  
### <a name="how-do-i-determine-if-the-data-at-subscribers-is-synchronized-with-data-at-the-publisher"></a>Come si stabilisce se i dati nei Sottoscrittori sono sincronizzati con quelli nel server di pubblicazione?  
 Utilizzando la convalida. La convalida segnala se uno specifico Sottoscrittore è sincronizzato con il server di pubblicazione. Per altre informazioni, vedere [Convalidare i dati replicati](../validate-data-at-the-subscriber.md). A differenza dell' [utilità tablediff](../../../tools/tablediff-utility.md) , la convalida non offre informazioni sulle eventuali righe che non sono sincronizzate correttamente.  
  
### <a name="how-do-i-add-a-table-to-an-existing-publication"></a>Come si aggiunge una tabella a una pubblicazione esistente?  
 Per aggiungere una tabella o un altro oggetto, non è necessario arrestare l'attività sui database di pubblicazione o di sottoscrizione. Aggiungere una tabella a una pubblicazione usando la finestra di dialogo **Proprietà pubblicazione - \<Pubblicazione>** o le stored procedure [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) e [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Per altre informazioni, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="how-do-i-remove-a-table-from-a-publication"></a>Come si rimuove una tabella da una pubblicazione?  
 Rimuovere una tabella dalla pubblicazione usando [sp_droparticle](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql), [sp_dropmergearticle](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql) o la finestra di dialogo **Proprietà pubblicazione - \<Publication>**. Dopo l'aggiunta di sottoscrizioni non è possibile eliminare articoli dalle pubblicazioni snapshot o transazionali: è necessario eliminare prima le sottoscrizioni. Per altre informazioni, vedere [Aggiungere ed eliminare articoli in pubblicazioni esistenti](../publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="what-actions-require-subscriptions-to-be-reinitialized"></a>Quali azioni richiedono la reinizializzazione delle sottoscrizioni?  
 La reinizializzazione delle sottoscrizioni è necessaria per diverse modifiche degli articoli e delle pubblicazioni. Per altre informazioni, vedere [Modificare le proprietà di pubblicazioni e articoli](../publish/change-publication-and-article-properties.md).  
  
### <a name="what-actions-cause-snapshots-to-be-invalidated"></a>Quali azioni rendono non validi gli snapshot?  
 Vi sono diverse modifiche degli articoli e delle pubblicazioni che rendono non validi gli snapshot e richiedono la generazione di un nuovo snapshot. Per altre informazioni, vedere [Modificare le proprietà di pubblicazioni e articoli](../publish/change-publication-and-article-properties.md).  
  
### <a name="how-do-i-remove-replication"></a>Come si rimuove la replica?  
 Le azioni necessarie per rimuovere la replica da un database dipendono dalla funzione del database come database di pubblicazione, di sottoscrizione o entrambi.  
  
### <a name="how-do-i-determine-whether-there-are-transactions-or-rows-to-be-replicated"></a>In che modo è possibile determinare se vi sono transazioni o righe da replicare?  
 Per la replica transazionale, utilizzare le stored procedure o la scheda **Comandi non distribuiti** di Monitoraggio replica. Per altre informazioni, vedere [visualizzare comandi replicati e altre informazioni nel Database di distribuzione &#40;programmazione Transact-SQL della replica&#41; ](../monitor/view-replicated-commands-and-information-in-distribution-database.md) e [visualizzare le informazioni ed eseguire attività con Monitoraggio replica](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Per la replica di tipo merge, utilizzare la stored procedure **sp_showpendingchanges**. Per altre informazioni, vedere [sp_showpendingchanges &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql).  
  
### <a name="how-far-behind-is-the-distribution-agent-should-i-reinitialize"></a>Quanto rimane indietro l'agente di distribuzione? È necessario ripetere l'inizializzazione?  
 Utilizzare la stored procedure **sp_replmonitorsubscriptionpendingcmds** o la scheda **Comandi non distribuiti** di Monitoraggio replica. La stored procedure e la scheda mostrano:  
  
-   Numero di comandi nel database di distribuzione che non sono stati recapitati al Sottoscrittore selezionato. Un comando è composto da un'istruzione DDL (Data Definition Language) o da un'istruzione DML (Data Manipulation Language) Transact-SQL.  
  
-   Tempo stimato per il recapito dei comandi al Sottoscrittore. Se questo valore è maggiore del tempo necessario per generare uno snapshot e applicarlo al Sottoscrittore, potrebbe risultare conveniente reinizializzare il Sottoscrittore. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](../reinitialize-subscriptions.md).  
  
 Per altre informazioni, vedere [sp_replmonitorsubscriptionpendingcmds &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql) e [visualizzare le informazioni ed eseguire attività con Monitoraggio replica](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="replication-and-other-database-features"></a>Replica e altre funzionalità del database  
  
### <a name="does-replication-work-in-conjunction-with-log-shipping-and-database-mirroring"></a>La replica funziona insieme al log shipping e al mirroring del database?  
 Sì. Per altre informazioni, vedere [Log shipping e replica &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md) e [Mirroring e replica del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
### <a name="does-replication-work-in-conjunction-with-clustering"></a>La replica funziona insieme al clustering?  
 Sì. Non vi sono considerazioni speciali, poiché tutti i dati vengono archiviati su un solo set di dischi nel cluster.  
  
## <a name="see-also"></a>Vedere anche  
 [Domande frequenti sull'amministrazione della replica](frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](best-practices-for-replication-administration.md)  
  
  
