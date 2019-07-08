---
title: Ripristinare pagine (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restorepage.general.f1
helpviewer_keywords:
- restoring pages [SQL Server]
- pages [SQL Server], restoring
- databases [SQL Server], damaged
- page restores [SQL Server]
- pages [SQL Server], damaged
- restoring [SQL Server], pages
ms.assetid: 07e40950-384e-4d84-9ac5-84da6dd27a91
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 65d16a118ccdf5714e0f4b5493c1c0d3266a1d33
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67583734"
---
# <a name="restore-pages-sql-server"></a>Ripristino di pagine (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento viene descritto come ripristinare le pagine in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. L'obiettivo di un ripristino della pagina è ripristinare una o più pagine danneggiate senza ripristinare l'intero database. In genere, le pagine candidate al ripristino sono state contrassegnate come "sospette" a causa di un errore verificatosi all'accesso alla pagina. Le pagine sospette vengono identificate nella tabella [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) del database **msdb** .  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Casi in cui è utile il ripristino della pagina](#WhenUseful)  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Security](#Security)  
  
-   **Per ripristinare le pagine usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="WhenUseful"></a> Casi in cui è utile il ripristino della pagina  
 Il ripristino di una pagina è destinato alla correzione di pagine danneggiate isolate. Il ripristino e il recupero di poche pagine singole possono essere eseguiti in modo più rapido rispetto al ripristino di un file, riducendo la quantità di dati offline durante l'operazione di ripristino. Tuttavia, se è necessario ripristinare un certo numero di pagine in un file, in genere è più efficiente ripristinare l'intero file. Se, ad esempio, numerose pagine in un dispositivo indicano la possibilità di un guasto imminente del dispositivo, prendere in considerazione il ripristino del file, se possibile in un percorso diverso, e la riparazione del dispositivo.  
  
 Non tutti gli errori di pagina richiedono inoltre un ripristino. Nei dati della cache, ad esempio in un indice secondario, può verificarsi un problema risolvibile ricalcolando i dati. Se, ad esempio, l'amministratore del database elimina un indice secondario e lo ricompila, i dati danneggiati, sebbene corretti, non sono indicati come tali nella tabella [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) .  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Il ripristino delle pagine si applica ai database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano i modelli di recupero con registrazione completa o con registrazione minima delle operazioni bulk. Il ripristino della pagina è supportato solo per i filegroup di lettura/scrittura.  
  
-   È possibile ripristinare solo le pagine di database. Non è possibile usare il ripristino della pagina per gli elementi seguenti:  
  
    -   Log delle transazioni  
  
    -   Pagine di allocazione: pagine GAM (Global Allocation Map), pagine SGAM ( Shared Global Allocation Map) e pagine PFS (Page Free Space).  
  
    -   Pagina 0 di tutti i file di dati (pagina di avvio del file)  
  
    -   Pagina 1:9 (pagina di avvio del database)  
  
    -   Catalogo full-text  
  
-   Nel caso di un database che usa il modello di recupero con registrazione minima delle operazioni bulk, per il ripristino della pagina sono previste le condizioni aggiuntive seguenti:  
  
    -   Il backup dei dati con registrazione minima delle operazioni bulk risulta problematico se il filegroup o i dati della pagina sono offline, poiché i dati offline non vengono registrati nel log. Una pagina offline può impedire il backup del log. In questo caso, prendere in considerazione l'utilizzo di DBCC REPAIR, che può consentire una minore perdita di dati rispetto al ripristino del backup più recente.  
  
    -   Se un backup del log di un database con registrazione minima delle operazioni bulk rileva una pagina contenente errori, non sarà possibile completarlo, a meno che non sia specificata la clausola WITH CONTINUE_AFTER_ERROR.  
  
    -   Il ripristino della pagina in genere non funziona con il recupero con registrazione minima delle operazioni bulk.  
  
         Una procedura consigliata per l'esecuzione del ripristino della pagina consiste nell'impostare il database sul modello di recupero con registrazione completa e tentare un backup del log. Se il backup del log funziona, è possibile procedere con il ripristino della pagina. Se l'esecuzione del backup del log ha invece esito negativo, le modifiche eseguite dopo il backup del log precedente verranno perse oppure sarà necessario tentare di eseguire DBCC con l'opzione REPAIR_ALLOW_DATA_LOSS.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Scenari di ripristino della pagina:  
  
     Ripristino della pagina offline  
     Tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportano il ripristino delle pagine quando il database è offline. Durante un ripristino della pagina offline, il database è offline mentre le pagine danneggiate vengono ripristinate. Al termine della sequenza di ripristino, il database torna online.  
  
     Ripristino della pagina online  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition supporta il ripristino della pagina online, anche se nei casi in cui il database è offline viene usato il ripristino non in linea. Nella maggior parte dei casi, una pagina danneggiata può essere ripristinata mentre il database, incluso il filegroup in cui una pagina viene ripristinata, rimane online. Quando il filegroup primario è online, anche se uno o più filegroup secondari sono offline, il ripristino della pagina viene in genere eseguito online. Talvolta, tuttavia, una pagina danneggiata può richiedere un ripristino offline. Un danno a determinate pagine di importanza critica può ad esempio impedire l'avvio del database.  
  
    > [!WARNING]  
    >  Se nelle pagine danneggiate sono archiviati metadati del database di importanza critica, gli aggiornamenti necessari ai metadati potrebbero non riuscire durante un tentativo di ripristino della pagina online. In questo caso è possibile eseguire un ripristino della pagina non in linea, ma è prima necessario creare un [backup della parte finale del log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) eseguendo il backup del log delle transazioni tramite RESTORE WITH NORECOVERY.  
  
-   Il ripristino della pagina sfrutta le funzionalità ottimizzate di segnalazione e rilevamento degli errori a livello di pagina, inclusi i checksum di pagina. Le pagine rilevate come *danneggiate*da un errore di checksum o di scrittura incompleta possono essere ripristinate tramite un'operazione di ripristino della pagina. Vengono ripristinate solo le pagine specificate in modo esplicito. Ogni pagina specificata viene sostituita dalla copia di tale pagina dal backup dei dati specificato.  
  
     Quando si ripristinano i backup del log successivi, questi vengono applicati solo ai file di database che contengono almeno una pagina recuperata. È inoltre necessario che una catena non interrotta di backup del log venga applicata all'ultimo ripristino completo o differenziale per aggiornare il filegroup che include la pagina rispetto al file di log attuale. Analogamente al ripristino del file, il set di rollforward viene avanzato con un unico passaggio di rollforward del log. Affinché il ripristino delle pagine avvenga correttamente, è necessario che le pagine ripristinate vengano recuperate fino a uno stato consistente con il database.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Se il database da ripristinare non esiste, per eseguire un'operazione RESTORE l'utente deve disporre delle autorizzazioni CREATE DATABASE. Se il database esiste, le autorizzazioni per l'istruzione RESTORE vengono assegnate per impostazione predefinita ai membri dei ruoli predefiniti del server **sysadmin** e **dbcreator** e al proprietario (**dbo**) del database. Per l'opzione FROM DATABASE_SNAPSHOT, il database esiste sempre.  
  
 Le autorizzazioni per l'istruzione RESTORE vengono assegnate ai ruoli in cui le informazioni sull'appartenenza sono sempre disponibili per il server. Poiché è possibile controllare l'appartenenza ai ruoli predefiniti del database solo quando il database è accessibile e non è danneggiato, condizioni che non risultano sempre vere quando si esegue un'operazione RESTORE, i membri del ruolo predefinito del database **db_owner** non dispongono delle autorizzazioni per l'istruzione RESTORE.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 A partire da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] supporta il ripristino della pagina.  
  
#### <a name="to-restore-pages"></a>Per ripristinare le pagine  
  
1.  Stabilire una connessione all'istanza appropriata di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi fare clic sul nome del server in Esplora oggetti per espandere l'albero di server.  
  
2.  Espandere **Database**. A seconda del database, selezionare un database utente oppure espandere **Database di sistema**e selezionare un database di sistema.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**, **Ripristina**, quindi fare clic su **Pagina**. Verrà aperta la finestra di dialogo **Ripristina pagina** .  
  
     **Restore**  
     Questa sezione ha la stessa funzione di **Ripristina fino a** in [Ripristina database (pagina Generale)](../../relational-databases/backup-restore/restore-database-general-page.md).  
  
     **Database**  
     Consente di specificare il database da ripristinare. È possibile immettere un nuovo database oppure selezionarne uno esistente nell'elenco a discesa. Nell'elenco sono inclusi tutti i database disponibili nel server, ad eccezione dei database di sistema **master** e **tempdb**.  
  
    > [!WARNING]  
    >  Per ripristinare un backup protetto da password, è necessario usare l'istruzione [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) .  
  
     **Backup della parte finale del log**  
     Immettere o selezionare un nome di file in **Dispositivo di backup** per indicare dove verrà archiviato il backup della parte finale del log per il database.  
  
     **Set di backup**  
     In questa sezione vengono visualizzati i set di backup coinvolti nel ripristino.  
  
    |Intestazione|Valori|  
    |------------|------------|  
    |**Nome**|Nome del set di backup.|  
    |**Componente**|Componente di cui è stato eseguito il backup: **Database**, **File** o **\<vuoto>** (per i log delle transazioni).|  
    |**Tipo**|Tipo di operazione di backup eseguita: **Completo**, **Differenziale** o **Log delle transazioni**.|  
    |**Server**|Nome dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ha eseguito l'operazione di backup.|  
    |**Database**|Nome del database interessato dall'operazione di backup.|  
    |**Posizione**|Posizione del set di backup nel volume.|  
    |**Primo LSN**|Numero di sequenza del file di log (LSN) della prima transazione nel set di backup. Vuoto per i backup dei file.|  
    |**Ultimo LSN**|Numero di sequenza del file di log (LSN) dell'ultima transazione nel set di backup. Vuoto per i backup dei file.|  
    |**LSN checkpoint**|Numero di sequenza del file di log (LSN) del checkpoint più recente al momento della creazione del backup.|  
    |**LSN completo**|Numero di sequenza del file di log (LSN) dell'operazione di backup completo del database più recente.|  
    |**Data inizio**|Data e ora di inizio dell'operazione di backup, visualizzate in base alle impostazioni internazionali del client.|  
    |**Data fine**|Data e ora di fine dell'operazione di backup, visualizzate in base alle impostazioni internazionali del client.|  
    |**Dimensione**|Dimensioni in byte del set di backup.|  
    |**Nome utente**|Nome dell'utente che ha eseguito l'operazione di backup.|  
    |**Scadenza**|Data e ora di scadenza del set di backup.|  
  
     Fare clic su **Verifica** per controllare l'integrità dei file di backup necessaria per eseguire l'operazione di ripristino della pagina.  
  
4.  Per identificare pagine danneggiate, con il database corretto selezionato nella casella **Database** , fare clic su **Controlla pagine di database**. L'operazione può richiedere molto tempo.  
  
    > [!WARNING]  
    >  Per ripristinare pagine specifiche non danneggiate, fare clic su **Aggiungi** e immettere l' **ID file** e l' **ID pagina** delle pagine da ripristinare.  
  
5.  La griglia di pagine viene usata per identificare le pagine da ripristinare. All'inizio questa griglia viene popolata dalla tabella di sistema [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) . Per aggiungere o rimuovere pagine dalla griglia, fare clic su **Aggiungi** o su **Rimuovi**. Per altre informazioni, vedere [Gestione della tabella suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md).  
  
6.  Nella griglia **Set di backup** sono elencati i set di backup inclusi nel piano di ripristino predefinito. Facoltativamente, fare clic su **Verifica** per verificare che i backup siano leggibili e che i set di backup siano completi, senza ripristinarli. Per altre informazioni, vedere [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
     **Pagine**  
  
7.  Per ripristinare le pagine elencate nella griglia, fare clic su **OK**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 Per specificare una pagina in un'istruzione RESTORE DATABASE, sono necessari l'ID del file contenente la pagina e l'ID della pagina. La sintassi necessaria è la seguente:  
  
 `RESTORE DATABASE <database_name>`  
  
 `PAGE = '<file: page> [ ,... n ] ' [ ,... n ]`  
  
 `FROM <backup_device> [ ,... n ]`  
  
 `WITH NORECOVERY`  
  
 Per altre informazioni sui parametri dell'opzione PAGE, vedere [Argomenti dell'istruzione RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md). Per altre informazioni sulla sintassi di RESTORE DATABASE, vedere [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
#### <a name="to-restore-pages"></a>Per ripristinare le pagine  
  
1.  Ottenere gli ID di pagina delle pagine danneggiate da ripristinare. Un errore di checksum o di scrittura incompleta restituisce l'ID della pagina, con le informazioni necessarie per specificare le pagine. Per cercare l'ID di una pagina danneggiata, usare una delle origini seguenti:  
  
    |Origine dell'ID di pagina|Argomento|  
    |-----------------------|-----------|  
    |**msdb..suspect_pages**|[Gestione della tabella suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)|  
    |Log degli errori|[Visualizzazione del log degli errori di SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)|  
    |Tracce degli eventi|[Monitoraggio e risposta agli eventi](../../ssms/agent/monitor-and-respond-to-events.md)|  
    |DBCC|[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)|  
    |Provider WMI|[Concetti relativi al provider WMI per eventi del server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)|  
  
2.  Avviare un ripristino della pagina con un backup completo del database, del file o del filegroup contenente la pagina desiderata. Nell'istruzione RESTORE DATABASE usare la clausola PAGE per elencare gli ID di tutte le pagine da ripristinare.  
  
3.  Applicare i backup differenziali più recenti.  
  
4.  Applicare i backup del log successivi.  
  
5.  Creare un nuovo backup del log del database che include l'LSN finale delle pagine ripristinate, ovvero il punto in corrispondenza del quale viene portata offline l'ultima pagina ripristinata. L'LSN finale, impostato come parte del primo ripristino nella sequenza, è l'LSN di destinazione di rollforward. Il rollforward online del file che include la pagina è in grado di arrestarsi in corrispondenza dell'LSN di destinazione di rollforward. Per conoscere l'LSN di destinazione della fase di rollforward corrente di un file, vedere la colonna **redo_target_lsn** di **sys.master_files**. Per altre informazioni, vedere [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md).  
  
6.  Ripristinare il nuovo backup del log. Una volta applicato il nuovo backup del log, il ripristino della pagina è completo e le pagine sono utilizzabili.  
  
    > [!NOTE]  
    >  Questa sequenza è analoga a una sequenza di ripristino del file. In effetti, il ripristino della pagina e i ripristini dei file possono essere eseguiti entrambi come parte della stessa sequenza.  
  
###  <a name="TsqlExample"></a> Esempio (Transact-SQL)  
 Nell'esempio seguente vengono ripristinate quattro pagine danneggiate del file `B` con `NORECOVERY`. Successivamente, vengono applicati due backup del log con `NORECOVERY`, seguiti dal backup della parte finale del log, ripristinato con `RECOVERY`. Nell'esempio seguente viene eseguito un ripristino in linea. Nell'esempio l'ID del file `B` è `1`e gli ID delle pagine danneggiate sono `57`, `202`, `916`e `1016`.  
  
```sql  
RESTORE DATABASE <database> PAGE='1:57, 1:202, 1:916, 1:1016'  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;   
BACKUP LOG <database> TO <new_log_backup>;   
RESTORE LOG <database> FROM <new_log_backup> WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Applicazione dei backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Gestione della tabella suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)   
 [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
