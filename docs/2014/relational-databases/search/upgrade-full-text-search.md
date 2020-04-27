---
title: Aggiornare la ricerca full-text | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], installing
- migrating full-text indexes [SQL Server]
- upgrading Full-Text Search
- installing Full-Text Search
- full-text search [SQL Server], upgrading
ms.assetid: 2fee4691-f2b5-472f-8ccc-fa625b654520
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43ef487dc2049d3ca95f4cddff72a005c98a5d19
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010956"
---
# <a name="upgrade-full-text-search"></a>Aggiornamento della ricerca full-text
  L'aggiornamento della ricerca full-text a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene effettuato in fase di installazione e durante il collegamento, il ripristino o la copia dei file di database e dei cataloghi full-text di una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la Copia guidata database.  
  
 In questo argomento si illustrano i seguenti aspetti dell'aggiornamento della ricerca full-text:  
  
-   [Aggiornamento di un'istanza del server](#Upgrade_Server)  
  
-   [Opzioni di aggiornamento full-text](#FT_Upgrade_Options)  
  
-   [Considerazioni per la scelta di un'opzione di aggiornamento full-text](#Choosing_Upgade_Option)  
  
-   [Migrazione degli indici full-text durante l'aggiornamento di un database a SQL Server 2014](#Upgrade_Db)  
  
-   [Considerazioni per il ripristino di un catalogo full-text di SQL Server 2005 in SQL Server 2014](#Considerations_for_Restore)  
  
-   [Collegamento di un database di SQL Server 2005 a SQL Server 2014](#Attaching_2005_ft_catalogs)  
  
##  <a name="upgrading-a-server-instance"></a><a name="Upgrade_Server"></a>Aggiornamento di un'istanza del server  
 Per un aggiornamento sul posto, un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene installata in modalità side-by-side con la versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quindi viene eseguita la migrazione dei dati. Se nella versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è installata la ricerca full-text, viene installata automaticamente una nuova versione della ricerca full-text. L'installazione side-by-side implica l'esistenza di ognuno dei componenti seguenti a livello di istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Word breaker, stemmer e filtri  
 In ogni istanza viene utilizzato ora un proprio set di word breaker, stemmer e filtri, anziché ricorrere alla versione di tali componenti disponibile nel sistema operativo. A livello di istanza, inoltre, la registrazione e la configurazione di questi componenti risulta più semplice. Per altre informazioni, vedere [Configurazione e gestione di word breaker e stemmer per la ricerca](configure-and-manage-word-breakers-and-stemmers-for-search.md) e [Configurazione e gestione di filtri per la ricerca](configure-and-manage-filters-for-search.md).  
  
 Host del daemon di filtri  
 Gli host del daemon di filtri full-text sono processi che consentono di caricare e controllare in modo sicuro i componenti estensibili esterni utilizzati per indici e query, quali word breaker, stemmer e filtri, senza compromettere l'integrità del motore di ricerca full-text. In un'istanza del server viene utilizzato un processo a thread multipli per tutti i filtri a thread multipli e un processo a thread singolo per tutti i filtri a thread singolo.  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ha introdotto un account del servizio per l'utilità di avvio FDHOST (MSSQLFDLauncher). Questo servizio propaga le informazioni sull'account del servizio nei processi dell'host del daemon di filtri di un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni sulla configurazione dell'account del servizio, vedere [Impostazione dell'account del servizio dell'Utilità di avvio del daemon di filtri full-text](set-the-service-account-for-the-full-text-filter-daemon-launcher.md).  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ogni indice full-text risiede in un catalogo full-text che appartiene a un filegroup, dispone di un percorso fisico e viene considerato un file di database. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive un catalogo full-text è un oggetto logico o virtuale che contiene un gruppo di indici full-text. Pertanto, un nuovo catalogo full-text non viene considerato un file di database con un percorso fisico. Tuttavia, durante l'aggiornamento di un catalogo full-text contenente file di dati viene creato un nuovo filegroup nello stesso disco mantenendo in questo modo il vecchio comportamento I/O su disco dopo l'aggiornamento. Tutti gli indici full-text di quel catalogo vengono posizionati nel nuovo filegroup se esiste il percorso radice. Se il percorso precedente del catalogo full-text non è valido, l'indice full-text rimane nello stesso filegroup della tabella di base o nel filegroup primario nel caso di una tabella partizionata.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] Le istruzioni DDL che specificano cataloghi full-text continuano a funzionare correttamente.  
  
##  <a name="full-text-upgrade-options"></a><a name="FT_Upgrade_Options"></a>Opzioni di aggiornamento full-text  
 Quando si aggiorna un'istanza del server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], l'interfaccia utente consente di scegliere una delle opzioni di aggiornamento full-text seguenti.  
  
 Importa  
 I cataloghi full-text vengono importati. In genere, l'importazione è molto più veloce della ricompilazione. Se ad esempio si utilizza solo una CPU, l'importazione è di circa 10 volte più veloce della ricompilazione. Un catalogo full-text importato, tuttavia, non utilizza i nuovi word breaker installati nella versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ricompilare i cataloghi full-text per garantire la coerenza nei risultati delle query.  
  
> [!NOTE]  
>  La ricompilazione può essere eseguita in modalità a thread multipli e, nel caso in cui siano disponibili più di 10 CPU, può risultare più veloce dell'importazione se si consente alla ricompilazione di utilizzare tutte le CPU.  
  
 Se un catalogo full-text non è disponibile, gli indici full-text associati vengono ricreati. Questa opzione è disponibile solo per i database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 Per informazioni sull'impatto dell'importazione di un indice full-text, vedere "Considerazioni per la scelta di un'opzione di aggiornamento full-text" più avanti in questo argomento.  
  
 Ricompila  
 I cataloghi full-text vengono ricompilati utilizzando i nuovi word breaker ottimizzati. La ricompilazione degli indici può richiedere tempo. Dopo l'aggiornamento, inoltre, potrebbe essere necessaria una quantità significativa di CPU e di memoria.  
  
 Reset  
 I cataloghi full-text vengono ripristinati. Quando si esegue l'aggiornamento da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], i file dei cataloghi full-text vengono rimossi, ma i metadati per i cataloghi full-text e gli indici full-text vengono mantenuti. Dopo l'aggiornamento, in tutti gli indici full-text il rilevamento delle modifiche viene disabilitato e le ricerche per indicizzazione non vengono avviate automaticamente. Il catalogo resterà vuoto fino a quando non si eseguirà manualmente un popolamento completo al termine dell'aggiornamento.  
  
##  <a name="considerations-for-choosing-a-full-text-upgrade-option"></a><a name="Choosing_Upgade_Option"></a>Considerazioni per la scelta di un'opzione di aggiornamento full-text  
 Quando si sceglie l'opzione di aggiornamento, considerare gli elementi seguenti:  
  
-   È richiesta coerenza nei risultati delle query?  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] offre nuovi word breaker da usare per la ricerca full-text e semantica. I word breaker vengono utilizzati sia in fase di indicizzazione che di esecuzione delle query. Se non si ricompilano i cataloghi full-text, i risultati di ricerca potrebbero risultare incoerenti. Se si esegue una query full-text che esegue la ricerca di una frase divisa in modo diverso dal word breaker in una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rispetto a quello corrente, è possibile che si verifichi il mancato recupero di una riga o documento contenente la frase. Questo problema si verifica perché le frasi indicizzate sono state divise in base a una logica diversa da quella utilizzata dalla query. Per risolvere il problema, ripopolare (ricompilare) i cataloghi full-text con i nuovi word breaker in modo che il comportamento in fase di indicizzazione e di esecuzione delle query sia lo stesso. A tale scopo, è possibile scegliere l'opzione Ricompila oppure scegliere l'opzione Importa e avviare manualmente la ricompilazione.  
  
-   Eventuale presenza di indici full-text compilati in colonne chiave full-text di tipo integer  
  
     Con la ricompilazione vengono eseguite ottimizzazioni interne che in alcuni casi migliorano le prestazioni di esecuzione delle query dell'indice full-text aggiornato. In particolare, se si dispone di cataloghi full-text che contengono indici full-text per i quali la colonna chiave full-text della tabella di base è un tipo di dati integer, la ricompilazione consente di ottenere prestazioni ideali delle query full-text dopo l'aggiornamento. In questo caso, è consigliabile usare l'opzione **Ricompila** .  
  
    > [!NOTE]  
    >  Per gli indici full-text in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è consigliabile che la colonna utilizzata come chiave full-text sia un tipo di dati integer. Per altre informazioni, vedere [Miglioramento delle prestazioni di indici full-text](improve-the-performance-of-full-text-indexes.md).  
  
-   Priorità della disponibilità online dell'istanza del server  
  
     L'importazione o la ricompilazione durante l'aggiornamento richiede l'utilizzo di molte risorse della CPU ritardando in questo modo l'aggiornamento del resto dell'istanza del server e la disponibilità online dell'istanza stessa. Se la disponibilità online dell'istanza del server è essenziale e si desidera eseguire un popolamento manuale dopo l'aggiornamento, è consigliabile utilizzare l'opzione **Reimposta** .  
  
## <a name="ensuring-consistent-query-results-after-importing-a-sql-server-2005-full-text-index"></a>Garanzia di coerenza dei risultati delle query dopo l'importazione di un indice full-text di SQL Server 2005  
 Se un catalogo full-text viene importato durante l'aggiornamento di un database da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], potrebbero verificarsi mancate corrispondenze tra la query e il contenuto dell'indice full-text a causa di differenze nel comportamento dei vecchi e dei nuovi word breaker. In tal caso, per garantire una totale corrispondenza tra le query e il contenuto dell'indice full-text, utilizzare una delle opzioni seguenti:  
  
-   Ricompilare il catalogo full-text che contiene l'indice full-text ([ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)*nome_catalogo* REBUILD)  
  
-   Eseguire un'istruzione FULL POPULATION sull'indice full-text ([ALTER FULLTEXT INDEX](/sql/t-sql/statements/alter-fulltext-index-transact-sql) ON *nome_tabella* START FULL POPULATION).  
  
 Per altre informazioni sui word breaker, vedere [Configurazione e gestione di word breaker e stemmer per la ricerca](configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
## <a name="upgrading-noise-word-files-to-stoplists"></a>Aggiornamento di file di parole non significative agli elenchi corrispondenti  
 I file di parole non significative di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] sono stati sostituiti da elenchi di parole non significative in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive. Quando un database viene aggiornato a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], i file delle parole non significative non vengono più utilizzati. Tali file vengono tuttavia archiviati nella cartella FTDATA\FTNoiseThesaurusBak e possono essere utilizzati in seguito durante l'aggiornamento o la compilazione degli elenchi di parole non significative corrispondenti di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 Dopo l'aggiornamento da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]:  
  
-   Se nell'installazione di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]non sono mai stati aggiunti, modificati o eliminati file di parole non significative, l'elenco di parole non significative di sistema dovrebbe soddisfare le esigenze dell'utente.  
  
-   Se i file di parole non significative sono stati modificati in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], tali modifiche vengono perse durante l'aggiornamento. Per ricreare tali aggiornamenti, è possibile rieseguire manualmente le modifiche apportate nell'elenco di parole non significative di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] corrispondente. Per altre informazioni, vedere [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql).  
  
-   Se non si desidera applicare alcuna parola non significativa agli indici full-text (ad esempio, se sono stati eliminati o cancellati i file di parole non significative nell'installazione di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), è necessario disabilitare l'elenco di parole non significative per ogni indice full-text aggiornato. Eseguire l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] riportata di seguito, sostituendo *database* con il nome del database aggiornato e *table* con il nome della *tabella*:  
  
    ```  
    Use database;   
    ALTER FULLTEXT INDEX ON table  
       SET STOPLIST OFF;  
    GO  
    ```  
  
     La clausola STOPLIST OFF rimuove l'applicazione di filtri alle parole non significative e attiva la popolazione della tabella senza filtrare le parole considerate non significative.  
  
## <a name="backup-and-imported-full-text-catalogs"></a>Backup e cataloghi full-text importati  
 Per i cataloghi full-text ricompilati o reimpostati durante l'aggiornamento e per i nuovi cataloghi full-text, il catalogo full-text è un concetto logico e non risiede in un filegroup. Per eseguire il backup di un catalogo full-text in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è pertanto necessario identificare ogni filegroup contenente un indice full-text del catalogo ed eseguirne il backup uno alla volta. Per altre informazioni, vedere [Backup e ripristino di indici e cataloghi full-text](back-up-and-restore-full-text-catalogs-and-indexes.md).  
  
 I cataloghi full-text importati da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]rappresentano ancora file di database nel proprio filegroup. Il processo di backup di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] continua a essere applicato per i cataloghi full-text ad eccezione del fatto che il servizio MSFTESQL non esiste in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per informazioni sul processo in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , vedere [Backup e ripristino di cataloghi full-text](https://go.microsoft.com/fwlink/?LinkId=209154) nella documentazione online di SQL Server 2005.  
  
##  <a name="migrating-full-text-indexes-when-upgrading-a-database-to-sscurrent"></a><a name="Upgrade_Db"></a>Migrazione degli indici full-text durante l'aggiornamento di un database a[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 I file di database e i cataloghi full-text di una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere aggiornati a un'istanza del server di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] esistente mediante il collegamento, il ripristino o la Copia guidata database. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Gli indici full-text, se presenti, vengono importati, reimpostati o ricompilati. La proprietà del server **upgrade_option** consente di controllare l'opzione di aggiornamento full-text usata dall'istanza del server durante questi aggiornamenti del database.  
  
 Una volta collegato, ripristinato o copiato un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il database viene reso immediatamente disponibile e viene aggiornato automaticamente. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga. Si noti inoltre che quando l'opzione di aggiornamento è impostata sull'importazione, se non è disponibile un catalogo full-text vengono ricompilati gli indici full-text associati.  
  
 **Per modificare il comportamento dell'aggiornamento full-text in un'istanza del server**  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]: Usare l' **azione\_opzione di aggiornamento** di [\_SP\_FULLTEXT Service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **:** Usare l'opzione di **aggiornamento full-text** della finestra di dialogo **Proprietà server** . Per altre informazioni, vedere [Gestione e monitoraggio della ricerca full-text per un'istanza del server](manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
##  <a name="considerations-for-restoring-a-ssversion2005-full-text-catalog-to-sscurrent"></a><a name="Considerations_for_Restore"></a> Considerazioni per il ripristino di un catalogo full-text di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Un metodo di aggiornamento dei dati full-text da un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] consiste nel ripristinare il backup completo di un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Durante l'importazione di un catalogo di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] è possibile eseguire il backup e ripristinare il file di database e di catalogo. Il comportamento è uguale a quello di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]:  
  
-   Il backup completo del database includerà il catalogo full-text. Per fare riferimento al catalogo full-text, usare il relativo nome file di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , sysft_+*nome-catalogo*.  
  
-   Se il catalogo full-text è offline, il backup non verrà eseguito correttamente.  
  
 Per altre informazioni sul backup e il ripristino dei cataloghi full-text di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , vedere [Backup e ripristino di cataloghi full-text](https://go.microsoft.com/fwlink/?LinkId=121052) e [Backup e ripristino di file e cataloghi full-text](https://go.microsoft.com/fwlink/?LinkId=121053)nella documentazione online di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 Quando viene ripristinato il database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], viene creato un nuovo file di database per il catalogo full-text. Il nome predefinito di questo file è ftrow_*nome-catalogo*.ndf. Se ad esempio *nome-catalogo* è `cat1`, il nome predefinito del database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sarà `ftrow_cat1.ndf`. Tuttavia, se il nome predefinito è già in uso nella directory di destinazione, il nuovo file di database sarà `ftrow_`denominato nome *-Catalogo-*`{`*GUID*`}.ndf`, dove *GUID* è l'identificatore univoco globale del nuovo file.  
  
 Dopo l'importazione dei cataloghi, **sys.database_files** e **sys.master_files**vengono aggiornati in modo da rimuovere le voci di catalogo e la colonna **path** in **sys.fulltext_catalogs** viene impostata su NULL.  
  
 **Per eseguire il backup di un database**  
  
-   [Backup completo del database &#40;SQL Server&#41;](../backup-restore/full-database-backups-sql-server.md)  
  
-   [Backup del Log delle transazioni & #40;SQL Server & #41;](../backup-restore/transaction-log-backups-sql-server.md) (solo modello di recupero con registrazione completa)  
  
 **Per ripristinare un backup del database**  
  
-   [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](../backup-restore/complete-database-restores-full-recovery-model.md)  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la clausola MOVE nell'istruzione [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) per ripristinare un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] denominato `ftdb1`. I file di database, di log e di catalogo di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] vengono spostati nei nuovi percorsi nell'istanza del server di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , come segue:  
  
-   Il file di database, `ftdb1.mdf`, viene spostato in `C:\Program Files\Microsoft SQL Server\MSSQL.1MSSQL12.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf`.  
  
-   Il file di log `ftdb1_log.ldf`,, viene spostato in una directory di log nell'unità disco di log, *log_drive*`:\`*log_directory*`\ftdb1_log.ldf`.  
  
-   I file di catalogo che corrispondono al catalogo `sysft_cat90` vengono spostati in `C:\temp`. Dopo essere stati importati, gli indici full-text vengono automaticamente posizionati in un file di database, C:\ftrow_sysft_cat90.ndf, e C:\temp verrà eliminato.  
  
```  
RESTORE DATABASE [ftdb1] FROM  DISK = N'C:\temp\ftdb1.bak' WITH  FILE = 1,  
   MOVE N'ftdb1' TO N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf',  
    MOVE N'ftdb1_log' TO N'log_drive:\log_directory\ftdb1_log.ldf',  
    MOVE N'sysft_cat90' TO N'C:\temp';  
```  
  
##  <a name="attaching-a-sql-server-2005-database-to-sscurrent"></a><a name="Attaching_2005_ft_catalogs"></a>Connessione di un database SQL Server 2005 a[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive, un catalogo full-text è un concetto logico che fa riferimento a un gruppo di indici full-text. Il catalogo full-text è un oggetto virtuale che non appartiene ad alcun filegroup. Tuttavia, quando si collega un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] contenente file di cataloghi full-text in un'istanza del server di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , i file di catalogo vengono collegati dal percorso precedente insieme agli altri file del database, come in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Lo stato di ogni catalogo full-text collegato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] corrisponde a quello di quando il database è scollegato da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Se il popolamento dell'indice full-text è stato sospeso mediante un'operazione di scollegamento, esso viene ripreso in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]e l'indice full-text viene reso disponibile per la ricerca full-text.  
  
 Se in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non è possibile trovare un file del catalogo full-text o se il file full-text è stato spostato durante l'operazione di collegamento senza specificare un nuovo percorso, il comportamento dipende dall'opzione di aggiornamento full-text selezionata. Se l'opzione di aggiornamento full-text è **Importa** o **Ricompila**, il catalogo full-text collegato viene ricompilato. Se l'opzione di aggiornamento full-text è **Reimposta**, il catalogo full-text collegato viene reimpostato.  
  
 Per altre informazioni sul collegamento e scollegamento di un database, vedere [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md), [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql), [sp_attach_db](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql) e [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alla ricerca full-text](get-started-with-full-text-search.md)   
 [Configurare e gestire Word breaker e stemmer per la ricerca](configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurazione e gestione di filtri per la ricerca](configure-and-manage-filters-for-search.md)  
  
  
