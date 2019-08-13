---
title: Novità del motore di database di SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2d2ade42e25593911ea25b2a16ad53372ced0438
ms.sourcegitcommit: c2052b2bf7261b3294a3a40e8fed8b9e9c588c37
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941113"
---
# <a name="whats-new-in-database-engine---sql-server-2016"></a>Novità del motore di database - SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Questo argomento riepiloga i miglioramenti introdotti nella versione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].  I nuovi miglioramenti e funzionalità offrono maggiore potenza a progettisti, sviluppatori e amministratori che progettano, sviluppano e gestiscono sistemi di archiviazione dati e consentono loro di lavorare in modo più produttivo.

Per informazioni sulle novità negli altri componenti di SQL Server, vedere [Novità di SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).

> [!NOTE]
>  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] è un'applicazione a 64 bit. L'installazione a 32 bit è stata sospesa, ma alcuni elementi vengono eseguiti come componenti a 32 bit.

#### <a name="try-it-out"></a>Per provarlo

- Per scaricare [SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016).

- Se si ha un account di Azure,  fare clic **[qui](https://azure.microsoft.com/services/virtual-machines/sql-server/)** per creare rapidamente una macchina virtuale in cui è già installato [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] .

> [!NOTE]
> Per le note sulla versione correnti, vedere [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md).
  
## <a name="sql-server-2016-service-pack-1-sp1"></a>SQL Server 2016 Service Pack 1 (SP1)  
-  La sintassi`CREATE OR ALTER <object>` è ora disponibile per [procedure](../t-sql/statements/create-procedure-transact-sql.md), [viste](../t-sql/statements/create-view-transact-sql.md), [funzioni](../t-sql/statements/create-function-transact-sql.md)e [trigger](../t-sql/statements/create-trigger-transact-sql.md).
-   È stato aggiunto il supporto per un modello di hint per query più generico: `OPTION (USE HINT('<hint1>', '<hint2>'))`. Per altre informazioni, vedere [Hint per la query (Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md).  
- È stata aggiunta la DMV [sys.dm_exec_valid_use_hints](../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) per elencare gli hint.  
- È stata aggiunta la DMV [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) per restituire le statistiche temporanee dello showplan XML.  
- È stata aggiunta la DMV [sys.dm_db_incremental_stats_properties](../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md) alle statistiche incrementali per la tabella specificata.  
- È stata aggiunta la colonna `instant_file_initialization_enabled` a [sys.dm_server_services](../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md).  
- È stata aggiunta la colonna of    `estimated_read_row_count` a [sys.dm_exec_query_profiles](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md).  
-  Sono state aggiunte le colonne `sql_memory_model` e `sql_memory_model_desc` a [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) per fornire informazioni sul modello di blocco per le pagine di memoria.
-  Le edizioni che supportano una serie di funzionalità sono state espanse. Sono stati aggiunti a tutte le edizioni sicurezza a livello di riga, Crittografia sempre attiva, maschera dati dinamica, controllo del database, OLTP in memoria e diverse altre funzionalità. Per altre informazioni, vedere [Edizioni e funzionalità supportate per SQL Server 2016](../sql-server/editions-and-supported-features-for-sql-server-2016.md).   
-  [sp_refresh_parameter_encryption](../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) abilita la crittografia AlwaysOn per aggiornare i metadati quando vengono ridefiniti gli oggetti crittografati tramite AlwaysOn.  


##  <a name="Feature"></a> SQL Server 2016 RTM
Questa sezione contiene le sottosezioni seguenti:

-   [Indici columnstore](#columnstore-indexes)
-   [Configurazioni con ambito database](#database-scoped-configurations)
-   [OLTP in memoria](#in-memory-oltp)
-   [Query Optimizer](#query-optimizer)
-   [Statistiche sulle query dinamiche](#live-query-statistics)
-   [Archivio query](#query-store)
-   [Tabelle temporali](#temporal-tables)
-   [Backup con striping in Archiviazione BLOB di Microsoft Azure](#striped-backups-to-microsoft-azure-blob-storage)
-   [Backup di snapshot dei file in Archiviazione BLOB di Microsoft Azure](#file-snapshot-backups-to-microsoft-azure-blob-storage)
-   [Backup gestito](#managed-backup)
-   [Database tempdb](#tempdb-database)
-   [Supporto JSON integrato](#built-in-json-support)
-   [PolyBase](#polybase)
-   [Estensione database](#stretch-database)
-   [Supporto per UTF-8](#support-for-utf-8)
-   [Nuove dimensioni predefinite del database e nuovi valori di aumento automatico](#new-default-database-size-and-autogrow-values)
-   [Miglioramenti di Transact-SQL](#transact-sql-enhancements)
-   [Miglioramenti alle viste di sistema](#system-view-enhancements)
-   [Miglioramenti della sicurezza](#security-enhancements)
-   [Miglioramenti della disponibilità elevata](#high-availability-enhancements)
-   [Miglioramenti della replica](#replication-enhancements)
-   [Miglioramenti degli strumenti](#tools-enhancements)

## <a name="columnstore-indexes"></a>Indici columnstore

Questa versione offre miglioramenti per gli indici columnstore, inclusi gli indici columnstore non cluster aggiornabili, gli indici columnstore nelle tabelle in memoria e molte altre nuove funzionalità per l'analisi operativa.

- Un indice columnstore non cluster di sola lettura può essere aggiornato dopo il passaggio a una versione successiva.  Non è necessario ricompilare l'indice per renderlo aggiornabile.

- Sono stati introdotti miglioramenti delle prestazioni per le query di analisi sugli indici columnstore, in particolare per quanto riguarda aggregati e predicati di tipo stringa.

- Sono stati introdotti miglioramenti del supporto per DMV e XEvent.

Per altre informazioni, vedere gli argomenti nella sezione [Guida agli indici columnstore](../relational-databases/indexes/columnstore-indexes-overview.md) della documentazione online:

- [Riepilogo delle funzionalità con versione degli indici columnstore](~/relational-databases/indexes/columnstore-indexes-what-s-new.md) - include informazioni sulle novità.

- [Caricamento dati di indici columnstore](../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)

- [Prestazioni delle query per gli indici columnstore](~/relational-databases/indexes/columnstore-indexes-query-performance.md)

- [Introduzione a columnstore per l'analisi operativa in tempo reale](../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

- [Indici columnstore per il data warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

- [Deframmentazione degli indici columnstore](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)


## <a name="database-scoped-configurations"></a>Configurazioni con ambito database


La nuova istruzione [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) consente di gestire alcune configurazioni per il database specifico. Le impostazioni di configurazione influenzano il comportamento dell'applicazione.

La nuova istruzione è disponibile in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] e [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)].



## <a name="in-memory-oltp"></a>OLTP in memoria


### <a name="storage-format-change"></a>Modifica del formato di archiviazione

Il formato di archiviazione per le tabelle con ottimizzazione per la memoria è cambiato da SQL Server 2014 alla versione 2016. Per l'aggiornamento e il collegamento/ripristino da SQL Server 2014, viene serializzato il nuovo formato di archiviazione e il database viene riavviato una volta durante il recupero del database.

- [Eseguire l'aggiornamento a SQL Server 2016](../database-engine/install-windows/upgrade-sql-server.md)


### <a name="alter-table-is-log-optimized-and-runs-in-parallel"></a>ALTER TABLE è ottimizzata per il log e viene eseguita in parallelo

Quando ora si esegue un'istruzione ALTER TABLE in una tabella con ottimizzazione per la memoria, solo le modifiche dei metadati vengono scritte nel log. Questo riduce notevolmente l'IO del log. La maggior parte degli scenari di ALTER TABLE vengono ora eseguiti in parallelo, con una significativa riduzione della durata dell'istruzione.

- Per le eccezioni non parallele, inclusi i LOB, vedere [Modifica di tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).



### <a name="statistics"></a>Statistiche

[Le statistiche per le tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md) vengono ora aggiornate automaticamente. Il campionamento è ora un metodo supportato per raccogliere statistiche, consentendo di evitare il metodo fullscan più dispendioso.


### <a name="parallel-and-heap-scan-for-memory-optimized-tables"></a>Analisi parallela e heap per le tabelle con ottimizzazione per la memoria

Le tabelle con ottimizzazione per la memoria e gli indici in tali tabelle supportano ora l'analisi parallela. Ciò migliora le prestazioni delle query di analisi.

Inoltre, l'analisi dell'heap è supportata e può essere eseguita in parallelo. Nel caso di una tabella con ottimizzazione per la memoria, l'analisi dell'heap si riferisce all'analisi di tutte le righe in una tabella usando la struttura dei dati heap in memoria usata per archiviare le righe. Per un'analisi completa delle tabelle, l'analisi dell'heap è più efficiente rispetto all'uso di un indice.

### <a name="transact-sql-improvements-for-memory-optimized-tables"></a>Miglioramenti di Transact-SQL per tabelle con ottimizzazione per la memoria

Numerosi elementi di Transact-SQL non supportati per le tabelle con ottimizzazione per la memoria in SQL Server 2014 sono ora supportati in SQL Server 2016:


- Sono supportati gli indici e i vincoli UNIQUE.


- I riferimenti FOREIGN KEY tra tabelle con ottimizzazione per la memoria sono supportati.
  - Queste chiavi esterne possono fare riferimento solo una chiave primaria e non possono fare riferimento a una chiave univoca.


- I vincoli CHECK sono supportati.

- Un indice non univoco può consentire valori NULL nella chiave.

- I TRIGGER sono supportati nelle tabelle con ottimizzazione per la memoria.
  - Sono supportati solo i trigger AFTER. I trigger INSTEADOF non sono supportati.
  - I trigger sulle tabelle con ottimizzazione per la memoria devono usare WITH NATIVE_COMPILATION.

- Supporto completo di tutte le pagine di codice di SQL Server e delle regole di confronto con gli indici e altri elementi nelle tabelle con ottimizzazione per la memoria e nei moduli T-SQL compilati in modo nativo.


- Supporto per la [modifica di tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md):
  - Indici ADD e DROP. Modificare bucket_count degli indici hash.
  - Apportare modifiche allo schema: aggiungere/eliminare/modificare colonne e aggiungere/eliminare vincoli.

- Una tabella con ottimizzazione per la memoria può ora includere più colonne la cui lunghezza complessiva supera la lunghezza della pagina da 8.060 byte. Un esempio è una tabella con tre colonne di tipo `nvarchar(4000)`. In questi esempi, alcune colonne vengono ora archiviate all'esterno di righe. Le query non rilevano alcuna differenza tra colonne all'interno di righe e all'esterno di righe.

- [I tipi LOB (Large Object)](../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) `varbinary(max)`, `nvarchar(max)`e `varchar(max)` ora sono supportati nelle tabelle con ottimizzazione per la memoria.


Per informazioni generali, vedere:

- [Costrutti Transact-SQL non supportati da OLTP in memoria](../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)
- [Funzionalità di SQL Server non supportate per OLTP in memoria](~/relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)



### <a name="performance-and-scaling-improvements"></a>Miglioramenti delle prestazioni e della scalabilità

- Non esistono più limitazioni per le dimensioni dei dati. Vedere [Stimare i requisiti di memoria delle tabelle con ottimizzazione per la memoria](~/relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md).

- Sono ora disponibili più thread simultanei responsabili della [persistenza nel disco delle modifiche nelle tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/scalability.md).

- Supporto dei piani paralleli per l' [accesso alle tabelle con ottimizzazione per la memoria tramite codice Transact-SQL interpretato](../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md).


### <a name="enhancements-in-sql-server-management-studio"></a>Miglioramenti in SQL Server Management Studio

- L'operazione per [determinare se una tabella o una stored procedure deve essere trasferita a OLTP in memoria](../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) non richiede più la configurazione di agenti di raccolta dati o del data warehouse di gestione. Il report può ora essere eseguito direttamente in un database di produzione.

- [Cmdlet di PowerShell per la valutazione della migrazione](../relational-databases/in-memory-oltp/powershell-cmdlet-for-migration-evaluation.md) per valutare l'idoneità della migrazione di più oggetti in un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

- Generazione di elenchi di controllo della migrazione facendo clic con il pulsante destro del mouse su un database e scegliendo Attività -> Generazione guidata elenchi di controllo per migrazione OLTP in memoria.

### <a name="cross-feature-support"></a>Supporto per combinazioni di funzionalità

- Supporto per l'uso del controllo delle versioni di sistema temporale con OLTP in memoria. Per altre informazioni, vedere [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)

- Supporto dell'archivio query per codice compilato in modo nativo da carichi di lavoro OLTP in memoria. Per altre informazioni, vedere [Uso di Archivio query con OLTP in memoria](../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md).

- [Sicurezza a livello di riga nelle tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md#rls)

- Le connessioni con [Multiple Active Result Set &#40;MARS&#41;](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)possono ora accedere alle tabelle con ottimizzazione per la memoria e alle stored procedure compilate in modo nativo.

- Supporto di [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md). Se un database è configurato per la crittografia, ora i file del [filegroup con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md) vengono anch'essi crittografati.

Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).


## <a name="query-optimizer"></a>Query Optimizer
### <a name="compatibility-level-guarantees"></a>Garanzie del livello di compatibilità
Quando si aggiorna un database di SQL Server 2016, non sono previste variazioni di piano se si mantengono i livelli di compatibilità precedentemente in uso, ad esempio 120 o 110. Le nuove funzionalità e i miglioramenti correlati a Query Optimizer saranno disponibili solo con il livello di compatibilità più recente. 
### <a name="trace-flag-4199"></a>Flag di traccia 4199
In generale, non è necessario usare il flag di traccia 4199 in SQL Server 2016 perché la maggior parte dei comportamenti di Query Optimizer controllati da questo flag di traccia viene abilitata incondizionatamente con il più recente livello di compatibilità (130) in SQL Server 2016.
### <a name="new-referential-integrity-operator"></a>Nuovo operatore di integrità referenziale
Una tabella può fare riferimento a un massimo di 253 altre tabelle e colonne come chiavi esterne (riferimenti in uscita). [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] incrementa da 253 a 10.000 il limite per il numero di altre tabelle e colonne che possono fare riferimento alle colonne in una singola tabella (riferimenti in ingresso). Per informazioni sulle restrizioni, vedere [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md). È stato introdotto un nuovo operatore di integrità referenziale (con il livello di compatibilità 130) che esegue i controlli di integrità referenziale sul posto. Ciò migliora le prestazioni generali per le operazioni UPDATE e DELETE, nelle tabelle che contengono un numero elevato di riferimenti in ingresso, consentendo di fatto la presenza di un numero elevato di riferimenti in ingresso. Per altre informazioni, vedere [Query Optimizer Additions in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/23/query-optimizer-additions-in-sql-server/)(Aggiunte a Query Optimizer in SQL Server 2016)
### <a name="parallel-update-of-sampled-statistics"></a>Aggiornamento parallelo delle statistiche campionate
Il campionamento dei dati per la generazione di statistiche ora avviene in parallelo (con il livello di compatibilità 130), per migliorare le prestazioni della raccolta delle statistiche. Per altre informazioni, vedere [UPDATE STATISTICS (Transact-SQL)](../t-sql/statements/update-statistics-transact-sql.md).
### <a name="sublinear-threshold-for-update-of-statistics"></a>Soglia sublineare per l'aggiornamento delle statistiche
L'aggiornamento automatico delle statistiche ora è più aggressivo sulle tabelle di grandi dimensioni (con il livello di compatibilità 130). A partire da SQL Server 2016, la soglia per l'attivazione dell'aggiornamento automatico delle statistiche è 20%; per le tabelle più grandi questa soglia inizierà a decrescere (sempre in percentuale) man mano che aumentano le righe nella tabella. Non è necessario impostare il flag di traccia 2371 per ridurre la soglia. 
### <a name="other-enhancements"></a>Altri miglioramenti
Insert in un'istruzione Insert-select è multi-thread o può avere un piano parallelo (con il livello di compatibilità 130). Per ottenere un piano parallelo, l'istruzione INSERT ... SELECT deve usare l'hint TABLOCK. Per altre informazioni, vedere il post di blog su [Insert Select in parallelo](https://blogs.msdn.microsoft.com/sqlcat/2016/07/06/sqlsweet16-episode-3-parallel-insert-select/)

## <a name="live-query-statistics"></a>Statistiche sulle query dinamiche
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] consente di visualizzare il piano di esecuzione dinamico di una query attiva. Il piano dinamico delle query offre informazioni approfondite in tempo reale sul processo di esecuzione della query, man mano che i controlli passano da un operatore del piano di query a un altro. Per altre informazioni, vedere [Live Query Statistics](../relational-databases/performance/live-query-statistics.md).

## <a name="query-store"></a>Archivio query
L'archivio query è una nuova funzionalità che mette a disposizione degli amministratori del database informazioni approfondite sulle prestazioni e sulla scelta del piano di query. Semplifica la risoluzione dei problemi in quanto consente di individuare rapidamente le variazioni delle prestazioni causate da modifiche nei piani di query. La funzionalità acquisisce automaticamente una cronologia delle query, dei piani e delle statistiche di runtime e li conserva in modo che sia possibile esaminarli successivamente. I dati vengono separati dagli intervalli di tempo, consentendo di visualizzare i modelli di utilizzo del database e capire quando sono state apportate modifiche al piano di query nel server. L'archivio query fornisce informazioni usando una finestra di dialogo di [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e consente di forzare la query in uno dei piani di query selezionati. Per altre informazioni, vedere [Monitoring Performance By Using the Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).


## <a name="temporal-tables"></a>Tabelle temporali
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] supporta ora tabelle temporali con controllo delle versioni di sistema. Una tabella temporale è un nuovo tipo di tabella che fornisce informazioni corrette sui fatti archiviati in qualsiasi momento. In realtà, ogni tabella temporale è costituita da due tabelle, una per i dati correnti e una per i dati cronologici. Il sistema garantisce che quando i dati cambiano nella tabella con i dati correnti, i valori precedenti vengono archiviati nella tabella di dati cronologici. Vengono forniti costrutti di query per evitare agli utenti di affrontare questa complessità. Per altre informazioni, vedere [Temporal Tables](../relational-databases/tables/temporal-tables.md).

## <a name="backups"></a>Backup

### <a name="striped-backups-to-microsoft-azure-blob-storage"></a>Backup con striping in Archiviazione BLOB di Microsoft Azure
In [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]il backup di SQL Server in un URL con il servizio Archiviazione BLOB di Microsoft Azure supporta ora set di backup con striping con BLOB in blocchi per supportare dimensioni massime di backup pari a 12,8 TB. Per gli esempi, vedere [Code Examples](../relational-databases/backup-restore/sql-server-backup-to-url.md#Examples).

### <a name="file-snapshot-backups-to-microsoft-azure-blob-storage"></a>Backup di snapshot di file in Archiviazione BLOB di Microsoft Azure
 In [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]il backup di SQL Server in un URL ora supporta l'uso di snapshot di Azure per il backup di database in cui tutti i file di database vengono archiviati usando il servizio Archiviazione BLOB di Microsoft Azure. Per altre informazioni, vedere [Backup di snapshot di file per i file di database in Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).

### <a name="managed-backup"></a>Backup gestito
In [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , il backup gestito da SQL Server in Microsoft Azure usa il nuovo archivio BLOB in blocchi per i file di backup. Sono stati apportati anche numerosi miglioramenti e modifiche al backup gestito.

-   Supporto per la pianificazione personalizzata e automatica dei backup.

-   Supporto dei backup per i database di sistema.

-   Supporto per i database che usano il modello di recupero con registrazione minima.

 Per altre informazioni, vedere [SQL Server Managed Backup to Microsoft Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)

> [!NOTE]
>  Per [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], queste nuove funzionalità di backup gestito non hanno ancora il supporto dell'interfaccia utente corrispondente in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

## <a name="tempdb-database"></a>Database tempdb
 Sono stati apportati numerosi miglioramenti a tempdb:

-   I flag di traccia 1117 e 1118 non sono più necessari per tempdb. Se ci sono più file di database tempdb, le dimensioni di tutti i file aumenteranno contemporaneamente a seconda delle impostazioni di aumento delle dimensioni. Inoltre, tutte le allocazioni in tempdb useranno extent uniformi.

-   Per impostazione predefinita, il programma di installazione aggiunge un numero di file tempdb pari al numero di CPU oppure 8 file, a seconda di quale sia il valore inferiore.

-   Durante l'installazione, è possibile configurare il numero di file di database tempdb, le dimensioni iniziali, l'impostazione di aumento automatico delle dimensioni e il posizionamento nella directory usando il nuovo controllo di input dell'interfaccia utente nella sezione relativa alla Configurazione del motore di database e a tempdb dell'Installazione guidata di SQL Server.

-   Le dimensioni iniziali predefinite sono di 8 MB e l'aumento automatico delle dimensioni predefinito è di 64 MB.

-   È possibile specificare più volumi per il file di database tempdb. Se vengono specificate più directory, i file di dati tempdb verranno distribuiti tra le directory secondo uno schema round-robin.

## <a name="built-in-json-support"></a>Supporto JSON integrato
SQL Server 2016 aggiunge il supporto predefinito per l'importazione e l'esportazione di JSON e l'uso di stringhe JSON. Questo supporto predefinito include le istruzioni e funzioni seguenti.

-   È possibile formattare i risultati di query come JSON o esportare JSON aggiungendo la clausola **FOR JSON** in un'istruzione **SELECT** . Usare ad esempio la clausola **FOR JSON** per delegare la formattazione dell'output JSON dalle applicazioni client a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Formattare i risultati delle query in formato JSON con FOR JSON &#40;SQL Server&#41;](../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).

-   È possibile convertire i dati JSON in righe e colonne o importare JSON chiamando la funzione **OPENJSON** del provider di set di righe. Usare **OPENJSON** per importare i dati JSON in SQL Server o convertire dati JSON in righe e colonne per un'app o un servizio che al momento non può utilizzare direttamente JSON. Per altre informazioni, vedere [Convertire dati JSON in righe e colonne con la funzione OPENJSON &#40;SQL Server&#41;](../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).

-   La funzione **ISJSON** verifica se una stringa include contenuto JSON valido. Per altre informazioni, vedere [ISJSON &#40;Transact-SQL&#41;](../t-sql/functions/isjson-transact-sql.md)

-   La funzione **JSON_VALUE** estrae un valore scalare da una stringa JSON. Per altre informazioni, vedere [JSON_VALUE &#40;Transact-SQL&#41;](../t-sql/functions/json-value-transact-sql.md).

-   La funzione **JSON_QUERY** estrae un oggetto o una matrice da una stringa JSON. Per altre informazioni, vedere [JSON_QUERY &#40;Transact-SQL&#41;](../t-sql/functions/json-query-transact-sql.md).

-   La funzione **JSON_MODIFY** aggiorna il valore di una proprietà in una stringa JSON e restituisce la stringa JSON aggiornata. Per altre informazioni, vedere [JSON_MODIFY &#40;Transact-SQL&#41;](../t-sql/functions/json-modify-transact-sql.md).

## <a name="polybase"></a>PolyBase
 PolyBase consente di usare le istruzioni T-SQL per accedere ai dati archiviati in Hadoop o nell'archivio BLOB di Azure ed eseguire query su di essi in modalità ad hoc. Consente anche di eseguire query sui dati semistrutturati e unire i risultati con set di dati relazionali archiviati in SQL Server. PolyBase è ottimizzato per carichi di lavoro di data warehouse e destinato a scenari di query di analisi.

 Per altre informazioni, vedere [PolyBase Guide](../relational-databases/polybase/polybase-guide.md)(Guida a PolyBase).

## <a name="stretch-database"></a>Stretch database
 Stretch Database è una nuova funzionalità di [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] che esegue la migrazione dei dati cronologici in modo trasparente e sicuro nel cloud di Microsoft Azure. È possibile accedere direttamente ai dati di SQL Server a prescindere dal fatto che si trovino in locale o siano stati estesi nel cloud. Impostare i criteri che determinano le posizioni di archiviazione dei dati e SQL Server gestisce il trasferimento dei dati in background. L'intera tabella è sempre online e disponibile per le query. Stretch Database non richiede modifiche alle query o alle applicazioni esistenti: il percorso dei dati è completamente disponibile per l'applicazione. Per ulteriori informazioni, vedere [Stretch Database](../sql-server/stretch-database/stretch-database.md).
 
## <a name="support-for-utf-8"></a>Supporto per UTF-8
[L'utilità bcp](../tools/bcp-utility.md), [BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) e [OPENROWSET](../t-sql/functions/openrowset-transact-sql.md) supportano ora la tabella codici UTF-8. Per altre informazioni, vedere questi argomenti in [Creare un file di formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).

## <a name="new-default-database-size-and-autogrow-values"></a>Nuove dimensioni predefinite del database e nuovi valori di aumento automatico
Nuovi valori per il database modello e nuovi valori predefiniti per i nuovi database (basati sul modello). Le dimensioni iniziali di file di log e dati sono ora di 8 MB. L'aumento automatico predefinito di file di log e dati è ora di 64 MB.


## <a name="transact-sql-enhancements"></a>Miglioramenti di Transact-SQL
Numerosi miglioramenti supportano le funzionalità descritte nella altre sezioni di questo argomento. Sono disponibili i miglioramenti aggiuntivi seguenti.
- L'istruzione TRUNCATE TABLE consente ora di troncare partizioni specificate. Per altre informazioni, vedere [TRUNCATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/truncate-table-transact-sql.md).
- [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md) consente ora l'esecuzione di molte azioni di modifica di colonna mentre la tabella rimane disponibile.
- La DMV dell'indice full-text [sys.dm_fts_index_keywords_position_by_document &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-position-by-document-transact-sql.md) restituisce la posizione delle parole chiave nei documenti. Questa DMV è stata aggiunta anche in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP2 e [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1.
- Un nuovo hint per la query **NO_PERFORMANCE_SPOOL** può impedire l'aggiunta di un operatore spool ai piani di query. Ciò può migliorare le prestazioni quando vengono eseguite numerose query simultanee con operazioni di spooling. Per altre informazioni, vedere [Hint per la query &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md).
- L'istruzione [FORMATMESSAGE &#40;Transact-SQL&#41;](../t-sql/functions/formatmessage-transact-sql.md) è stata migliorata per accettare un argomento msg_string.
- Le dimensioni massime per la chiave di indice per gli indici NONCLUSTERED sono state aumentate a 1700 byte.
- È stata aggiunta la nuova sintassi DROP IF per le istruzioni DROP correlate ad AGGREGATE, ASSEMBLY, COLUMN, CONSTRAINT, DATABASE, DEFAULT, FUNCTION, INDEX, PROCEDURE, ROLE, RULE, SCHEMA, SECURITY POLICY, SEQUENCE, SYNONYM, TABLE, TRIGGER, TYPE, USER e VIEW. Per la sintassi, vedere i singoli argomenti.
- È stata aggiunta un'opzione MAXDOP a [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checktable-transact-sql.md), [DBCC CHECKDB &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) e [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md) per specificare il grado di parallelismo.
- È ora possibile impostare SESSION_CONTEXT. Include la funzione [SESSION_CONTEXT &#40;Transact-SQL&#41;](../t-sql/functions/session-context-transact-sql.md), la funzione [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../t-sql/functions/current-transaction-id-transact-sql.md) e la procedura [sp_set_session_context &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md).
- Advanced Analytics Extensions consente agli utenti di eseguire script scritti in un linguaggio supportato, ad esempio R. [!INCLUDE[tsql](../includes/tsql-md.md)] supporta R con l'introduzione della stored procedure [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e della [opzione di configurazione del server external scripts enabled](../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md). Per altre informazioni, vedere [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md).
- Supporto aggiuntivo per R, possibilità di creare un pool di risorse esterne. Per altre informazioni, vedere [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-external-resource-pool-transact-sql.md).  Nuove viste del catalogo e DMV ([sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) e [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)). Sono disponibili argomenti aggiuntivi per [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md). Sono state aggiunte altre colonne ad alcune DMV e viste del catalogo di Resource Governor esistenti.
- La sintassi di [CREATE USER](../t-sql/statements/create-user-transact-sql.md) è stata migliorata con l'opzione ALLOW_ENCRYPTED_VALUE_MODIFICATIONS per supportare la funzionalità Always Encrypted. Per altre informazioni, vedere [Migrare dati sensibili protetti da Always Encrypted](../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).
- Le funzioni [COMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/compress-transact-sql.md) e [DECOMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/decompress-transact-sql.md) convertono i valori in ingresso e in uscita dall'algoritmo GZIP.
- Le funzioni [DATEDIFF_BIG &#40;Transact-SQL&#41;](../t-sql/functions/datediff-big-transact-sql.md) e [AT TIME ZONE &#40;Transact-SQL&#41;](../t-sql/queries/at-time-zone-transact-sql.md) e la vista [sys.time_zone_info &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) sono state aggiunte a supporto delle interazioni di data e ora.
- È ora possibile creare credenziali a livello di database, oltre alle credenziali a livello di server già disponibili in precedenza. Per altre informazioni, vedere [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md).
- Sono state aggiunte otto nuove proprietà a [SERVERPROPERTY &#40;Transact-SQL&#41;](../t-sql/functions/serverproperty-transact-sql.md): InstanceDefaultDataPath, InstanceDefaultLogPath, ProductBuild, ProductBuildType, ProductMajorVersion, ProductMinorVersion, ProductUpdateLevel e ProductUpdateReference.
- Il limite di lunghezza di input di 8.000 byte per la funzione [HASHBYTES &#40;Transact-SQL&#41;](../t-sql/functions/hashbytes-transact-sql.md) è stato rimosso.
- Sono state aggiunte nuove funzioni di stringa [STRING_SPLIT &#40;Transact-SQL&#41;](../t-sql/functions/string-split-transact-sql.md) e [STRING_ESCAPE &#40;Transact-SQL&#41;](../t-sql/functions/string-escape-transact-sql.md).
- Opzioni di aumento automatico: il flag di traccia 1117 è stato sostituito dalle opzioni AUTOGROW_SINGLE_FILE e AUTOGROW_ALL_FILES di ALTER DATABASE e il flag di traccia 1117 non ha alcun effetto. Per altre informazioni, vedere [Opzioni file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) e la nuova colonna is_autogrow_all_files di [sys.filegroups &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md).
- Allocazione di extent misti: per i database utente, l'allocazione predefinita per le prime 8 pagine di un oggetto ora usa extent uniformi al posto di extent di pagina misti. Il flag di traccia 1118 è stato sostituito dall'opzione SET MIXED_PAGE_ALLOCATION di ALTER DATABASE e il flag di traccia 1118 non ha alcun effetto. Per altre informazioni, vedere [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md) e la nuova colonna `is_mixed_page_allocation_on` di [sys.databases &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

### <a name="transact-sql-improvements-for-natively-compiled-modules"></a>Miglioramenti di Transact-SQL per i moduli compilati in modo nativo

Alcuni elementi di Transact-SQL non supportati per i moduli compilati in modo nativo in SQL Server 2014 sono ora supportati in SQL Server 2016:


- Costrutti di query:
  - UNION e UNION ALL
  - SELECT DISTINCT
  - OUTER JOIN
  - Sottoquery in SELECT


- Ora le istruzioni INSERT, UPDATE e DELETE possono includere la [clausola OUTPUT](../t-sql/queries/output-clause-transact-sql.md).

- È ora possibile usare i LOB nei modi seguenti in una procedura nativa:
  - Dichiarazione di variabili.
  - Parametri di input ricevuti.
  - Parametri passati a funzioni di stringa, ad esempio in LTrim o una sottostringa, in una procedura nativa.


- Le funzioni con valori di tabella (TVF) inline (singola istruzione) possono ora essere compilate in modo nativo.

- Le funzioni scalari definite dall'utente (UDF) possono ora essere compilate in modo nativo.

- Maggiore supporto per le chiamate seguenti da una procedura nativa:
  - [Funzioni di sicurezza](../t-sql/functions/security-functions-transact-sql.md)predefinite.
  - [Funzioni matematiche](../t-sql/functions/mathematical-functions-transact-sql.md)predefinite.
  - Funzione predefinita `@@SPID`.


- EXECUTE AS CALLER ora è supportata, che significa che la clausola EXECUTE AS non è più necessaria quando si crea un modulo T-SQL compilato in modo nativo.


Per informazioni generali, vedere:

- [Funzionalità supportate per i moduli T-SQL compilati in modo nativo](../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)
- [Altering Natively Compiled T-SQL Modules](../relational-databases/in-memory-oltp/altering-natively-compiled-t-sql-modules.md)

## <a name="system-view-enhancements"></a>Miglioramenti alle viste di sistema
- Due nuove viste supportano la sicurezza a livello di riga. Per altre informazioni, vedere [sys.security_predicates &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md) e [sys.security_policies &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md).
- Sette nuove viste supportano la funzionalità Archivio query. Per altre informazioni, vedere [Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md).
- Sono state aggiunte 24 nuove colonne a [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) per fornire informazioni sulle concessioni di memoria.
- Sono stati aggiunti due nuovi hint per la query (MIN_GRANT_PERCENT e MAX_GRANT_PERCENT) per specificare le concessioni di memoria. Vedere [Hint di query &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md).
- [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) offre un report per sessione simile a [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) a livello di server.
- [sys.dm_exec_function_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-function-stats-transact-sql.md) offre le statistiche di esecuzione relative alle funzioni a valori scalari.
- A partire da [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], le voci in [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md) vengono mantenute come avveniva prima di [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].
- Le informazioni sulle istruzioni inviate a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] possono essere restituite dalla nuova funzione a gestione dinamica [sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md).
- Due nuove viste supportano [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md): [sys.dm_external_script_requests](../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) e [sys.dm_external_script_execution_stats](../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 


## <a name="security-enhancements"></a>Miglioramenti della sicurezza

### <a name="row-level-security"></a>Sicurezza a livello di riga
La sicurezza a livello di riga introduce il controllo di accesso basato su predicato. Questa funzione offre una valutazione basata su predicato flessibile e centralizzata che può prendere in considerazione i metadati (ad esempio le etichette) o altri criteri ritenuti appropriati dall'amministratore. Il predicato viene usato come criterio per determinare se l'utente dispone o meno dell'accesso appropriato ai dati in base agli attributi utente. Il controllo di accesso basato su etichetta può essere implementato usando il controllo dei accesso basato su predicato. Per altre informazioni, vedere [Sicurezza a livello di riga](../relational-databases/security/row-level-security.md).


### <a name="always-encrypted"></a>Always Encrypted
Con Always Encrypted, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è in grado di eseguire operazioni sui dati crittografati e la chiave di crittografia risiede con l'applicazione all'interno dell'ambiente attendibile del cliente e non nel server. La funzionalità Crittografia sempre attiva protegge i dati dei clienti, in modo che gli amministratori del database non abbiano accesso ai dati di testo normale. Le operazioni di crittografia e decrittografia dei dati avvengono in modo trasparente a livello di driver, riducendo al minimo le modifiche da apportare alle applicazioni esistenti. Per altre informazioni, vedere [Always Encrypted &#40;Motore di database&#41;](../relational-databases/security/encryption/always-encrypted-database-engine.md).


### <a name="dynamic-data-masking"></a>Dynamic Data Masking
La maschera dati dinamica limita l'esposizione dei dati sensibili nascondendoli agli utenti senza privilegi. La maschera dati dinamica aiuta a impedire l'accesso non autorizzato ai dati sensibili consentendo agli utenti di definire la quantità di dati sensibili da rivelare, con un impatto minimo sul livello dell'applicazione. Si tratta di una funzionalità di sicurezza basata su criteri che consente di nascondere i dati sensibili nel set di risultati di una query in campi di database designati, senza modificare i dati nel database. Per altre informazioni, vedere [Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md).


### <a name="new-permissions"></a>Nuove autorizzazioni
- L'autorizzazione **ALTER ANY SECURITY POLICY** è disponibile come parte dell'implementazione della sicurezza a livello di riga.
- Le autorizzazioni **ALTER ANY MASK** e **UNMASK** sono disponibili come parte dell'implementazione della maschera dati dinamica.
- Le autorizzazioni **ALTER ANY COLUMN ENCRYPTION KEY**, **VIEW ANY COLUMN ENCRYPTION KEY**, **ALTER ANY COLUMN MASTER KEY DEFINITION**e **VIEW ANY COLUMN MASTER KEY DEFINITION** sono disponibili come parte dell'implementazione della funzionalità Crittografia sempre attiva.
- Le autorizzazioni **ALTER ANY EXTERNAL DATA SOURCE** e **ALTER ANY EXTERNAL FILE FORMAT** sono visibili in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , ma si applicano solo alla [!INCLUDE[ssAPS](../includes/ssaps-md.md)] ([!INCLUDE[ssDW](../includes/ssdw-md.md)]).
- Le autorizzazioni **EXECUTE ANY EXTERNAL SCRIPT** sono disponibili come parte del supporto per gli script R.
 - L'autorizzazione **ALTER ANY DATABASE SCOPED CONFIGURATION** è disponibile per autorizzare l'uso dell'istruzione [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

### <a name="transparent-data-encryption"></a>Transparent Data Encryption
- La tecnologia Transparent Data Encryption è stata migliorata con il supporto per l'accelerazione hardware Intel AES-NI della crittografia. Ciò riduce l'overhead della CPU quando si attiva Transparent Data Encryption.

### <a name="aes-encryption-for-endpoints"></a>Crittografia AES per gli endpoint
- La crittografia predefinita per gli endpoint è stata modificata da RC4 ad AES.

### <a name="new-credential-type"></a>Nuovo tipo di credenziali
- È ora possibile creare credenziali a livello di database, oltre alle credenziali a livello di server già disponibili in precedenza. Per altre informazioni, vedere [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md).


## <a name="high-availability-enhancements"></a>Miglioramenti della disponibilità elevata
SQL Server 2016 Standard supporta ora i gruppi di disponibilità Always On di base. I gruppi di disponibilità di base forniscono supporto per una replica primaria e una secondaria. Questa funzionalità sostituisce la tecnologia obsoleta di mirroring del database per la disponibilità elevata. Per altre informazioni sulle differenze tra gruppi di disponibilità di base e avanzati, vedere [Gruppi di disponibilità di base &#40;gruppi di disponibilità Always On&#41;](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).

Il bilanciamento del carico delle richieste di connessione con finalità di lettura è ora supportato in un set di repliche di sola lettura. Il comportamento precedente indirizzava sempre le connessioni alla prima replica di sola lettura disponibile nell'elenco di routing. Per altre informazioni, vedere [Configurare il bilanciamento del carico tra le repliche di sola lettura](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).

 Il numero di repliche che supportano il failover automatico è stato aumentato da due a tre.

 Gli account del servizio gestito di gruppo sono ora supportati per i cluster di failover Always On. Per altre informazioni, vedere [Account del servizio gestito di gruppo](https://technet.microsoft.com/library/hh831782.aspx). Per Windows Server 2012 R2, è necessario un aggiornamento per evitare tempo di inattività temporaneo dopo una modifica della password. Per ottenere l'aggiornamento, vedere [gMSA-based services can't log on after a password change in a Windows Server 2012 R2 domain](https://support.microsoft.com/kb/2998082/)(I servizi basati su gMSA non possono accedere dopo una modifica della password in un dominio di Windows Server 2012 R2).

 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] supporta le transazioni distribuite e il servizio DTC in Windows Server 2016. Per altre informazioni, vedere [Supporto delle transazioni distribuite](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md#dtcsupport).

 È ora possibile configurare [!INCLUDE[ssHADR](../includes/sshadr-md.md)] per eseguire il failover quando un database passa alla modalità offline. Questa modifica richiede l'impostazione dell'opzione **DB_FAILOVER** su **ON** nelle istruzioni [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) oppure [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md).

Always On supporta ora i database crittografati. Le procedure guidate relative ai gruppi di disponibilità chiedono ora di immettere una password per tutti i database che contengono una chiave master del database quando si crea un nuovo gruppo di disponibilità o quando si aggiungono database o repliche a un gruppo di disponibilità esistente.

Due gruppi di disponibilità in due istanze distinte di Windows Server Failover Cluster (WSFC) possono ora essere combinati in un gruppo di disponibilità distribuito. Per altre informazioni, vedere [Gruppi di disponibilità distribuiti &#40;gruppi di disponibilità Always On&#41;](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md).

Il seeding diretto consente di eseguire automaticamente il seeding di una replica secondaria in rete invece di eseguire il seeding manuale, che richiede il ripristino di un backup fisico del database di destinazione nella replica secondaria. Il seeding diretto viene specificato impostando **SEEDING_MODE=AUTOMATIC** nell'istruzione [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) o [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md). È anche necessario specificare **GRANT CREATE ANY DATABASE** con [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) in ogni replica secondaria usata con il seeding diretto.

**Miglioramenti delle prestazioni**: la velocità effettiva di sincronizzazione dei gruppi di disponibilità è stata aumentata di ~10 volte sfruttando la compressione parallela e più veloce dei blocchi di log nella replica primaria, un protocollo di sincronizzazione ottimizzato e la decompressione e il rollforward paralleli dei record di log nella replica secondaria. Ciò ottimizza l'aggiornamento delle repliche secondarie leggibili e riduce il tempo di ripristino del database in caso di failover. Si noti che il ripristino per le tabelle ottimizzate per la memoria non è ancora parallelo in SQL Server 2016.

## <a name="replication-enhancements"></a>Miglioramenti della replica
- È ora supportata la replica delle tabelle ottimizzate per la memoria. Per altre informazioni, vedere [Replica in sottoscrittori di tabelle con ottimizzazione per la memoria](../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).
- È ora supportata la replica nel [!INCLUDE[ssSDSFull](../includes/sssdsfull-md.md)]. Per altre informazioni, vedere [Replication to SQL Database](../relational-databases/replication/replication-to-sql-database.md).

## <a name="tools-enhancements"></a>Miglioramenti degli strumenti

### <a name="management-studio"></a>Management Studio
Scaricare la versione più recente di [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] supporta Active Directory Authentication Library (ADAL), che è in fase di sviluppo per la connessione a Microsoft Azure. Questo strumento sostituisce l'autenticazione basata su certificati usata in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].
- Una nuova opzione della griglia di risultati di query supporta il mantenimento di un ritorno a capo/avanzamento riga (caratteri di nuova riga) quando si copia o si salva il testo dalla griglia di risultati. È possibile impostare questa opzione dal menu Strumenti/Opzioni.
- Strumenti di gestione di SQL Server non viene più installato dall'albero delle funzionalità principale. Per informazioni dettagliate, vedere [Installare gli strumenti di gestione di SQL Server con SSMS](https://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381).

### <a name="upgrade-advisor"></a>Preparazione aggiornamento
La versione di anteprima di Gestione spazio aggiornamenti di SQL Server 2016 è uno strumento autonomo che consente agli utenti di versioni precedenti di eseguire un set di regole di aggiornamento nel database di SQL Server per trovare le modifiche di rilievo, le differenze di comportamento e le funzionalità deprecate, fornendo assistenza per l'adozione di nuove funzionalità come Stretch Database.

 È possibile scaricare la versione di anteprima di Gestione spazio aggiornamenti [qui](https://docs.microsoft.com/sql/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades#how-to-install-and-run-upgrade-advisor) oppure è possibile installare questo strumento con l'installazione guidata piattaforma Web.

## <a name="see-also"></a>Vedere anche
[Novità di SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)
 
[Note sulla versione di SQL Server 2016](../sql-server/sql-server-2016-release-notes.md) 
 
[Installare gli strumenti di gestione di SQL Server con SSMS](https://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)
