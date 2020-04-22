---
title: Database tempdb | Microsoft Docs
description: Questo argomento illustra i dettagli relativi alla configurazione e all'uso del database tempdb in SQL Server e nel database SQL di Azure
ms.custom: P360
ms.date: 04/17/2020
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
ms.reviewer: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5c324d19a0e5005261a1c5a14834ea2d9c2f4f73
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635349"
---
# <a name="tempdb-database"></a>Database tempdb

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Il database di sistema **TempDB** è una risorsa globale disponibile per tutti gli utenti connessi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o al database SQL. Tempdb viene usato per contenere:  
  
- **Oggetti utente** temporanei creati in modo esplicito, ad esempio tabelle e indici temporanei globali o locali, stored procedure temporanee, variabili di tabella, tabelle restituite in funzioni con valori di tabella o cursori.  
- **Oggetti interni** creati dal motore di database. incluse le seguenti:
  - Tabelle di lavoro in cui archiviare i risultati intermedi di operazioni di spooling e di ordinamento e cursori, nonché in cui archiviare LOB (Large Object) temporanei.
  - File di lavoro per operazioni hash join o hash aggregate.
  - Risultati intermedi dell'ordinamento per operazioni quali la creazione o la ricompilazione di indici (se SORT_IN_TEMPDB è specificato) o per alcune query GROUP BY, ORDER BY o UNION.

  > [!NOTE]
  > Ogni oggetto interno usa un minimo di nove pagine: una pagina IAM e un extent di otto pagine. Per altre informazioni sulle pagine e sugli extent, vedere [Pagine ed extent](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).
  > [!IMPORTANT]
  > I database singoli e i pool elastici di database SQL di Azure supportano tabelle temporanee globali e stored procedure temporanee globali archiviate in TempDB e con ambito a livello di database. Le tabelle temporanee globali e le stored procedure temporanee globali vengono condivise per le sessioni di tutti gli utenti all'interno dello stesso database SQL di Azure. Le sessioni utente di altri database SQL di Azure non possono accedere alle tabelle temporanee globali. Per altre informazioni, vedere [Tabelle temporanee globali con ambito database (database SQL di Azure)](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database). [Istanza gestita di Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)) supporta gli stessi oggetti temporanei di SQL Server.
  > Per i database singoli e i pool elastici di database SQL di Azure si applicano solo il database master e il database TempDB. Per altre informazioni, vedere [Informazioni sul server di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server). Per una descrizione di TempDB nel contesto di database singoli e pool elastici di database SQL di Azure, vedere [Database TempDB nel database SQL](#tempdb-database-in-sql-database). Per Istanza gestita di database SQL di Azure si applicano tutti i database di sistema.

- **Archivi delle versioni**, raccolte di pagine di dati che contengono le righe di dati usate dalle caratteristiche che supportano il controllo delle versioni delle righe. Vengono utilizzati due archivi delle versioni: uno comune e uno per la compilazione di indici online. Gli archivi delle versioni contengono:
  - Versioni di riga generate dalle transazioni di modifica dei dati in un database in cui viene usato il Read committed tramite isolamento del controllo delle versioni delle righe o transazioni di isolamento dello snapshot.  
  - Versioni di riga generate dalle transazioni di modifica dei dati per le caratteristiche, ad esempio le operazioni sugli indici online, la caratteristica MARS (Multiple Active Result Set) e i trigger AFTER.  
  
Le operazioni all'interno di **TempDB** sono a registrazione minima in modo che sia possibile eseguire il rollback delle transazioni. **TempDB** viene ricreato ogni volta che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene avviato in modo che il sistema inizi sempre con una copia pulita del database. Poiché le tabelle e le stored procedure temporanee vengono eliminate automaticamente al momento della disconnessione e poiché al momento della chiusura del sistema non vi sono connessioni attive, nessuna parte del database **TempDB** viene salvata per le sessioni successive di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le operazioni di backup e ripristino non sono consentite nel database **TempDB**.  

## <a name="physical-properties-of-tempdb-in-sql-server"></a>Proprietà fisiche di TempDB in SQL Server

La tabella seguente elenca i valori di configurazione iniziali di file di dati e di log di **TempDB** in SQL Server, basati sulle impostazioni predefinite per il database modello. Le dimensioni di questi file possono variare leggermente a seconda dell'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|File|Nome logico|Nome fisico|Dimensioni iniziali|Aumento di dimensioni del file|  
|----------|------------------|-------------------|------------------|-----------------|  
|Dati primari|tempdev|tempdb.mdf|8 megabyte|Aumento automatico di 64 MB fino a quando il disco risulta pieno|  
|File di dati secondari*|temp#|tempdb_mssql_#.ndf|8 megabyte|Aumento automatico di 64 MB fino a quando il disco risulta pieno|  
|File di log|templog|templog.ldf|8 megabyte|Aumento automatico di 64 megabyte fino a un massimo di 2 terabyte|  
  
\* Il numero di file dipende dal numero di processori (logici) del computer. In generale, se il numero di processori logici è minore o uguale a otto, usare un numero di file di dati pari al numero dei processori logici. Se il numero di processori logici è maggiore di otto, usare otto file di dati e, se la contesa persiste, aumentare il numero di file di dati per multipli di 4 fino a quando la contesa si riduce a livelli accettabili o modificare il carico di lavoro o il codice.

> [!NOTE]
> Il valore predefinito per il numero di file di dati si basa sulle linee guida generali in [KB 2154845](https://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>Spostamento dei file di dati e di log di TempDB in SQL Server

Per spostare i file di dati e di log di **TempDB**, vedere [Spostare i database di sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>Opzioni di database per TempDB in SQL Server

Nella tabella seguente sono elencati i valori predefiniti delle singole opzioni di database in **TempDB** e viene indicato se l'opzione è modificabile. Per visualizzare le impostazioni correnti di queste opzioni, usare la vista del catalogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Opzione di database|Valore predefinito|Modificabile|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sì|  
|ANSI_NULL_DEFAULT|OFF|Sì|  
|ANSI_NULLS|OFF|Sì|  
|ANSI_PADDING|OFF|Sì|  
|ANSI_WARNINGS|OFF|Sì|  
|ARITHABORT|OFF|Sì|  
|AUTO_CLOSE|OFF|No|  
|AUTO_CREATE_STATISTICS|ON|Sì|  
|AUTO_SHRINK|OFF|No|  
|AUTO_UPDATE_STATISTICS|ON|Sì|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sì|  
|CHANGE_TRACKING|OFF|No|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sì|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sì|  
|CURSOR_DEFAULT|GLOBAL|Sì|  
|Opzioni relative alla disponibilità del database|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|No<br /><br /> No<br /><br /> No|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sì|  
|DB_CHAINING|ON|No|  
|ENCRYPTION|OFF|No|  
|MIXED_PAGE_ALLOCATION|OFF|No|  
|NUMERIC_ROUNDABORT|OFF|Sì|  
|PAGE_VERIFY|CHECKSUM per nuove installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE per aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sì|  
|PARAMETERIZATION|SEMPLICE|Sì|  
|QUOTED_IDENTIFIER|OFF|Sì|  
|READ_COMMITTED_SNAPSHOT|OFF|No|  
|RECOVERY|SEMPLICE|No|  
|RECURSIVE_TRIGGERS|OFF|Sì|  
|Opzioni relative a Service Broker|ENABLE_BROKER|Sì|  
|TRUSTWORTHY|OFF|No|  
  
Per una descrizione di queste opzioni di database, vedere [Opzioni ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="tempdb-database-in-sql-database"></a>Database TempDB nel database SQL

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>Dimensioni di TempDB per i livelli di servizio basati su DTU

|SLO|Dimensioni massime file di dati TempDB (GB)|N. di file di dati TempDB|Dimensioni massime dei dati TempDB (GB)|
|---|---:|---:|---:|
|Basic|13,9|1|13,9|
|S0|13,9|1|13,9|
|S1|13,9|1|13,9|
|S2|13,9|1|13,9|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13,9|12|166,7|
|P2|13,9|12|166,7|
|P4|13,9|12|166,7|
|P6|13,9|12|166,7|
|P11|13,9|12|166,7|
|P15|13,9|12|166,7|
|Pool elastici Premium (tutte le configurazioni DTU)|13,9|12|166,7|
|Pool elastici standard (S0-S2)|13,9|12|166,7|
|Pool elastici standard (S3 e versioni successive) |32|12|384|
|Pool elastici Basic (tutte le configurazioni DTU)|13,9|12|166,7|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>Dimensioni di TempDB per i livelli di servizio basati su vCore

Vedere [Limiti delle risorse basati su vCore](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits)

## <a name="restrictions"></a>Restrizioni

Di seguito sono riportate le operazioni che non è possibile eseguire nel database **TempDB**:  
  
- Aggiunta di filegroup
- Backup o ripristino del database
- Modifica delle regole di confronto. Le regole di confronto predefinite corrispondono a quelle del server
- Modifica del proprietario del database. **TempDB** è di proprietà di **sa**
- Creazione di uno snapshot del database
- Eliminazione del database
- Eliminazione dell'utente **guest** dal database
- Abilitazione dell'acquisizione dei dati delle modifiche
- Partecipazione al mirroring del database
- Rimozione del filegroup primario, del file di dati primario o del file di log
- Ridenominazione del filegroup primario o del database
- Esecuzione di DBCC CHECKALLOC
- Esecuzione di DBCC CHECKCATALOG
- Impostazione del database su OFFLINE
- Impostazione del database o del filegroup primario su READ_ONLY
  
## <a name="permissions"></a>Autorizzazioni

Qualsiasi utente può creare oggetti temporanei in TempDB. Gli utenti possono accedere solo ai propri oggetti, a meno che non ottengano ulteriori autorizzazioni. È possibile revocare l'autorizzazione per la connessione a TempDB per impedire a un utente di usarlo, tuttavia questa scelta non è consigliata poiché alcune operazioni di routine richiedono l'uso di TempDB.  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>Ottimizzazione delle prestazioni di TempDB in SQL Server
Le dimensioni e la posizione fisica del database TempDB possono influire sulle prestazioni di un sistema. Se, ad esempio, le dimensioni definite per TempDB sono eccessivamente ridotte, il carico di elaborazione del sistema può essere in parte gestito aumentando automaticamente le dimensioni di TempDB fino a raggiungere quelle necessarie per supportare il carico di lavoro a ogni riavvio dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Se possibile, usare l'[inizializzazione immediata dei file di database](../../relational-databases/databases/database-instant-file-initialization.md) per migliorare le prestazioni delle operazioni di aumento delle dimensioni.

Preallocare lo spazio per tutti i file di TempDB impostando le relative dimensioni su un valore adeguato per il carico di lavoro tipico dell'ambiente. La preallocazione evita che il database TempDB si espanda con una frequenza eccessiva deteriorando le prestazioni. È opportuno impostare il database TempDB per l'aumento automatico delle dimensioni. Questa funzionalità deve tuttavia essere usata per aumentare lo spazio su disco per le eccezioni non pianificate.

All'interno di ogni [filegroup](../../relational-databases/databases/database-files-and-filegroups.md#filegroups) i file di dati devono avere le stesse dimensioni, perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa un algoritmo di riempimento proporzionale che favorisce le allocazioni all'interno di file con maggiore spazio disponibile. La suddivisione di TempDB in più file di dati di dimensioni uguali garantisce un livello elevato di efficienza parallela nelle operazioni che usano TempDB.

Impostare un valore di aumento delle dimensioni del file tale da evitare aumenti troppo ridotti delle dimensioni dei file del database TempDB. Se l'aumento delle dimensioni dei file è troppo ridotto in confronto alla quantità di dati scritti nel database TempDB, quest'ultimo potrebbe espandersi costantemente e influire sulle prestazioni.

Per controllare i parametri di dimensione e crescita correnti di TempDB, usare la query seguente:

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

Posizionare il database TempDB in un sottosistema I/O veloce. In presenza di molti dischi collegati direttamente, utilizzare lo striping del disco. File singoli o gruppi di file di dati di TempDB non devono necessariamente trovarsi in dischi o spindle diversi, a meno che non si verifichino anche colli di bottiglia di I/O.

Posizionare il database TempDB in dischi diversi da quelli usati dai database utente.

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>Miglioramenti delle prestazioni in TempDB per SQL Server
A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], le prestazioni di **TempDB** vengono ulteriormente ottimizzate nei modi seguenti:  
  
- Le tabelle temporanee e le variabili di tabella vengono memorizzate nella cache. La memorizzazione nella cache consente di eseguire molto rapidamente le operazioni di eliminazione e creazione degli oggetti temporanei e di ridurre i problemi di contesa nell'allocazione delle pagine.  
- Il protocollo di latch delle pagine di allocazione è stato migliorato per ridurre il numero di latch di aggiornamento (UP) usati.  
- L'overhead di registrazione per **TempDB** è stato ridotto per diminuire l'uso della larghezza di banda per le operazioni di I/O del disco nel file di log di **TempDB**.  
- Durante l'installazione di una nuova istanza vengono aggiunti più file di dati di TempDB. Questa attività può essere eseguita con il nuovo controllo input dell'interfaccia utente nella sezione **Configurazione del motore di database** e con un parametro della riga di comando `/SQLTEMPDBFILECOUNT`. Per impostazione predefinita, il programma di installazione aggiunge un numero di file di dati TempDB pari al numero di processori logici oppure a otto, a seconda di quale sia il valore inferiore.  
- Se ci sono più file di dati **TempDB**, le dimensioni di tutti i file aumentano contemporaneamente e della stessa quantità in base alle impostazioni di espansione specificate. Il [flag di traccia 1117](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) non è più necessario.  
- Tutte le allocazioni in **TempDB** usano extent uniformi. Il [flag di traccia 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) non è più necessario.  
- Per il filegroup primario, la proprietà AUTOGROW_ALL_FILES è attivata e non può essere modificata.

Per altre informazioni sui miglioramenti delle prestazioni in TempDB, vedere l'articolo di blog seguente:

[TEMPDB - Files and Trace Flags and Updates, Oh My!](https://blogs.msdn.microsoft.com/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my/) (TEMPDB - File, flag di traccia e aggiornamenti)

## <a name="memory-optimized-tempdb-metadata"></a>Metadati tempdb ottimizzati per la memoria
La contesa tra metadati TempDB è tipicamente un collo di bottiglia per la scalabilità per molti carichi di lavoro in esecuzione su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] introduce una nuova funzionalità della famiglia di funzionalità [Database in memoria](../in-memory-database.md), i metadati TempDB ottimizzati per la memoria, che rimuove questo collo di bottiglia e sblocca un nuovo livello di scalabilità per i carichi di lavoro TempDB eccessivi. In [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] le tabelle di sistema coinvolte nella gestione dei metadati delle tabelle temporanee possono essere spostate in tabelle ottimizzate per la memoria non durevoli senza latch.

Guardare questo video di 7 minuti per una panoramica su come e quando usare i metadati TempDB ottimizzati per la memoria:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/How-and-When-To-Memory-Optimized-TempDB-Metadata/player?WT.mc_id=dataexposed-c9-niner]


Per accettare questa nuova funzionalità, usare lo script seguente:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON 
```

Per rendere effettiva questa modifica della configurazione è necessario riavviare il servizio.

Questa implementazione presenta alcune limitazioni che è importante prendere in considerazione:

1. L'attivazione o la disattivazione della funzionalità non avviene in modo dinamico. A causa delle modifiche intrinseche che devono essere apportate alla struttura del database TempDB, è necessario un riavvio per abilitare o disabilitare la funzionalità.

2. È possibile che una singola transazione non possa accedere alle tabelle ottimizzate per la memoria in più di un database.  Ciò significa che tutte le transazioni che interessano una tabella ottimizzata per la memoria in un database utente non saranno in grado di accedere alle viste di sistema tempdb nella stessa transazione.  Se si tenta di accedere alle viste di sistema tempdb nella stessa transazione della tabella ottimizzata per la memoria in un database utente, verrà visualizzato l'errore seguente:
    
    ```
    A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
    ```
    
    Esempio:
    
    ```sql
    BEGIN TRAN
    SELECT *
    FROM tempdb.sys.tables  -----> Creates a user In-Memory OLTP Transaction on Tempdb
    INSERT INTO <user database>.<schema>.<mem-optimized table>
    VALUES (1)  ----> Attempts to create user In-Memory OLTP transaction but will fail
    COMMIT TRAN
    ```
    
3. Poiché le query eseguite nelle tabelle ottimizzate per la memoria non supportano gli hint di blocco e isolamento, le query eseguite nelle viste di catalogo tempdb ottimizzate per la memoria non rispetteranno gli hint di blocco e isolamento. Come nelle altre viste del catalogo di sistema in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tutte le transazioni eseguite nelle viste di sistema saranno nell'isolamento READ COMMITTED (o in questo caso READ COMMITTED SNAPSHOT).

4. Non è possibile creare [indici columnstore](../indexes/columnstore-indexes-overview.md) nelle tabelle temporanee quando sono abilitati i metadati tempdb ottimizzati per la memoria.

5. A causa della limitazione per gli indici columnstore, l'uso della stored procedure di sistema sp_estimate_data_compression_savings con il parametro di compressione dei dati COLUMNSTORE o COLUMNSTORE_ARCHIVE non è supportato quando i metadati tempdb ottimizzati per la memoria sono abilitati.

> [!NOTE] 
> Queste limitazioni si applicano solo quando si fa riferimento a viste di sistema tempdb. Se si desidera, sarà possibile creare una tabella temporanea nella stessa transazione non appena si accede a una tabella con ottimizzazione per la memoria in un database utente.

È possibile verificare se tempdb è ottimizzato per la memoria usando il comando T-SQL seguente:
```
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized')
```

Se il server non viene avviato per qualsiasi motivo dopo aver abilitato i metadati TempDB ottimizzati per la memoria, è possibile ignorare la funzionalità avviando SQL Server con la [configurazione minima](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md) usando l'opzione di avvio **-f**. In questo modo sarà possibile disabilitare la funzionalità e quindi riavviare SQL Server in modalità normale.

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>Pianificazione delle capacità per TempDB in SQL Server
La determinazione delle dimensioni appropriate per TempDB in un ambiente di produzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dipende da molti fattori. Come precedentemente descritto in questo articolo, questi fattori includono il carico di lavoro esistente e le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usate. È consigliabile analizzare il carico di lavoro esistente eseguendo le attività seguenti in un ambiente di test di SQL Server:

- Attivare l'aumento automatico delle dimensioni di TempDB.
- Eseguire singole query o file di traccia del carico di lavoro e monitorare l'uso dello spazio da parte di TempDB.
- Eseguire operazioni di manutenzione degli indici, ad esempio la ricompilazione degli indici stessi, e monitorare lo spazio occupato da TempDB.
- Impiegare i valori di uso dello spazio ottenuti con i passaggi precedenti per prevedere l'utilizzo totale da parte del carico di lavoro. Regolare poi tali valori in funzione delle attività simultanee previste e quindi impostare di conseguenza le dimensioni di TempDB.

## <a name="how-to-monitor-tempdb-use"></a>Come monitorare l'uso di TempDB
L'esaurimento dello spazio disponibile in TempDB può provocare interruzioni significative nell'ambiente di produzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e può impedire alle applicazioni in esecuzione di completare le operazioni in corso. Per eseguire il monitoraggio dello spazio su disco usato dai file di TempDB, è possibile usare la vista a gestione dinamica (DMV, Dynamic Management View) [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md):

```sql
 -- Determining the Amount of Free Space in TempDB
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount Space Used by the Version Store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by Internal Objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by User Objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

Per eseguire il monitoraggio dell'allocazione delle pagine o dell'attività di deallocazione in TempDB a livello di sessione o di attività, poi, è possibile usare le DMV [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) e [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md). Queste viste consentono di identificare le query, le tabelle temporanee o le variabili di tabella che usano una grande quantità di spazio su disco in TempDB. Sono anche disponibili diversi contatori che consentono di monitorare lo spazio libero disponibile in TempDB e le risorse che stanno usando TempDB. Per ulteriori informazioni, vedere la sezione successiva.

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>Contenuto correlato
[Opzione SORT_IN_TEMPDB per gli indici](../../relational-databases/indexes/sort-in-TempDB-option-for-indexes.md)    
[Database di sistema](../../relational-databases/databases/system-databases.md)    
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)    
[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)    
[Spostare file del database](../../relational-databases/databases/move-database-files.md)    
  
