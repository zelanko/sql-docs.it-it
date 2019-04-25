---
title: Livello di compatibilità ALTER DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs:
- TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
- db compatibility level
- db compat level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
author: CarlRabeler
ms.author: carlrab
manager: craigg'
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d535d50bde7c05629d23be85c2c64083dd455965
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583374"
---
# <a name="alter-database-transact-sql-compatibility-level"></a>Livello di compatibilità ALTER DATABASE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Imposta aspetti specifici del comportamento del database in modo che risultino compatibili con la versione specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre opzioni di ALTER DATABASE, vedere [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).

Per altre informazioni sulle convenzioni di sintassi, vedere [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintassi

```
ALTER DATABASE database_name
SET COMPATIBILITY_LEVEL = { 150 | 140 | 130 | 120 | 110 | 100 | 90 }
```

## <a name="arguments"></a>Argomenti

*database_name* è il nome del database da modificare.

COMPATIBILITY_LEVEL { 150 | 140 | 130 | 120 | 110 | 100 | 90 | 80 } è la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con cui il database deve essere reso compatibile. È possibile configurare i valori di livello di compatibilità seguenti (non tutte le versioni supportano tutti i livelli di compatibilità elencati):

|Prodotto|Versione del motore di database|Designazione di livello di compatibilità|Valori del livello di compatibilità supportato|
|-------------|-----------------------------|-------------------------------------|------------------------------------------|
|[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]|15|150|150, 140, 130, 120, 110, 100|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|14|140|140, 130, 120, 110, 100|
|Database singolo/pool elastico di [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|150, 140, 130, 120, 110, 100|
|Istanza gestita di [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|150, 140, 130, 120, 110, 100|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|9|90|90, 80|
|SQL Server 2000|8|80|80|

> [!NOTE]
> A partire da **gennaio 2018**, nel [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], il livello di compatibilità predefinito è 140 per i nuovi database. Per i database esistenti, il livello di compatibilità del database non viene aggiornato. I clienti possono decidere l'approccio da adottare in base alle proprie esigenze. È tuttavia consigliabile pianificare il passaggio al livello di compatibilità più recente per trarre vantaggio dai miglioramenti apportati.
>
> Se si vuole sfruttare in generale il livello di compatibilità 140 del database, ma per qualche motivo si preferisce il modello di **stima della cardinalità** di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], che corrisponde al livello di compatibilità 110 del database, vedere [ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) e in particolare la parola chiave `LEGACY_CARDINALITY_ESTIMATION = ON`.
>
> Per informazioni dettagliate su come valutare le variazioni delle prestazioni delle query più importanti tra i due livelli di compatibilità [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] vedere [Prestazioni delle query migliorate con il livello di compatibilità 130 in Database SQL di Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/). Si noti che questo articolo si riferisce al livello di compatibilità 130 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma la stessa metodologia si applica ai passaggi al livello 140 per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Eseguire la query seguente per determinare la versione del [!INCLUDE[ssDE](../../includes/ssde-md.md)] a cui si è connessi. 

```sql
SELECT SERVERPROPERTY('ProductVersion');
```

> [!NOTE]
> Non tutte le funzionalità che variano in base al livello di compatibilità sono supportate nel [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

Per determinare il livello di compatibilità corrente, eseguire una query sulla colonna **compatibility_level** di [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

```sql
SELECT name, compatibility_level FROM sys.databases;
```

## <a name="remarks"></a>Remarks

Per tutte le installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il livello di compatibilità predefinito è impostato in base alla versione del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Per i database viene impostato questo livello, a meno che per il database **model** non sia impostato un livello di compatibilità inferiore. Quando si aggiorna un database da una qualsiasi versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il database mantiene il livello di compatibilità esistente, se questo è almeno il livello minimo ammesso per quell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se in fase di aggiornamento di un database viene usato un livello di compatibilità inferiore a quello consentito, il database viene automaticamente impostato al livello più basso di compatibilità consentito. Questo comportamento si applica sia ai database di sistema che ai database utente.

Sono previsti i comportamenti seguenti per [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] quando un database viene collegato o ripristinato e dopo un aggiornamento sul posto:

- Se il livello di compatibilità di un database utente era 100 o superiore prima dell'aggiornamento, rimane invariato dopo l'aggiornamento.
- Se il livello di compatibilità di un database utente è 90 prima dell'aggiornamento, nel database aggiornato viene impostato su 100, ovvero sul livello di compatibilità supportato più basso in [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].
- I livelli di compatibilità dei database tempdb, model, msdb e Resource vengono impostati sul livello di compatibilità corrente dopo l'aggiornamento.
- Per il database di sistema master viene mantenuto il livello di compatibilità precedente l'aggiornamento.

Usare `ALTER DATABASE` per modificare il livello di compatibilità del database. L'impostazione del nuovo livello di compatibilità per un database diventa effettiva quando si esegue un comando `USE <database>` o quando viene elaborato un nuovo accesso con quel database come contesto di database predefinito.
Per visualizzare il livello di compatibilità corrente di un database, eseguire una query sulla colonna **compatibility_level** nella vista del catalogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).

> [!NOTE]
> Un [database di distribuzione](../../relational-databases/replication/distribution-database.md) creato in una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aggiornato a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM o Service Pack 1 ha il livello di compatibilità 90 che non è supportato per altri database. Ciò non determina alcun impatto sulle funzionalità di replica. L'aggiornamento a Service Pack e versioni più recenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determinerà l'innalzamento del livello di compatibilità del database di distribuzione in modo da corrispondere a quello del database **master**.

## <a name="compatibility-levels-and-sql-server-upgrades"></a>Livelli di compatibilità e aggiornamenti di SQL Server

Il livello di compatibilità del database è un utile strumento nella modernizzazione dei database poiché consente di aggiornare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e di preservare lo stato funzionale delle applicazioni che si connettono mantenendo lo stesso livello di compatibilità del database precedente all'aggiornamento.
Se l'applicazione non richiede l'uso dei miglioramenti disponibili solo in un livello di compatibilità superiore, esso costituisce un valido approccio per aggiornare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e mantenere il precedente livello di compatibilità del database. Per altre informazioni sull'uso del livello di compatibilità per la compatibilità con le versioni precedenti, vedere [Uso del livello di compatibilità per garantire la compatibilità con le versioni precedenti](#using-compatibility-level-for-backward-compatibility) più avanti in questo articolo.

Per i nuovi progetti di sviluppo o quando un'applicazione esistente richiede l'uso di nuove funzionalità o dei miglioramenti in termini di prestazioni offerti da Query Optimizer, pianificare l'aggiornamento del livello di compatibilità del database a quello più recente disponibile in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e certificare l'applicazione per l'uso di questo livello di compatibilità. Per altri dettagli sull'aggiornamento del livello di compatibilità del database, vedere [Procedure consigliate per aggiornare il livello di compatibilità del database](#best-practices-for-upgrading-database-compatibility-level) più avanti in questo articolo.

> [!TIP]
> Se un'applicazione è stata testata e certificata in una determinata versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa è stata implicitamente testata e certificata nel livello di compatibilità del database nativo di questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
>
> Quando si usa il livello di compatibilità del database corrispondente alla versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] testata, il livello di compatibilità del database offre pertanto un facile percorso di certificazione per un'applicazione esistente.
>
> Per altre informazioni sulle differenze tra i livelli di compatibilità, vedere le sezioni appropriate più avanti in questo articolo.

Per aggiornare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] alla versione più recente, mantenendo il livello di compatibilità del database che esisteva prima dell'aggiornamento e il relativo stato di supporto, è consigliabile eseguire la convalida della superficie di attacco funzionale statica del codice dell'applicazione nel database usando lo strumento [Microsoft Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA). L'assenza di errori nell'output dello strumento DMA, relativi a funzionalità mancanti o non compatibili, protegge l'applicazione da regressioni funzionali nella nuova versione di destinazione. Per altre informazioni sullo strumento DMA, vedere [qui](https://blogs.msdn.microsoft.com/datamigration/dma).

> [!NOTE]
> DMA supporta il livello di compatibilità del database 100 e superiore. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] come versione di origine è escluso.
> [!IMPORTANT]
> Microsoft consiglia di eseguire una quantità minima di test per convalidare l'esito positivo di un aggiornamento mantenendo il livello di compatibilità del database precedente. Determinare questa quantità minima di test in base all'applicazione e allo scenario specifici.
> [!NOTE]
> Microsoft offre protezione della forma del piano di query quando:
>
> - La nuova versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (destinazione) viene eseguita su hardware simile a quello in cui veniva eseguita la versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (origine).
> - Viene usato lo stesso [livello di compatibilità del database supportato](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#remarks) nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione e nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di origine.
>
> Eventuali regressioni della forma del piano di query (rispetto all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di origine) che si dovessero verificare nelle condizioni sopra riportate verranno risolte. A questo scopo, contattare il supporto tecnico Microsoft.

## <a name="using-compatibility-level-for-backward-compatibility"></a>Utilizzo del livello di compatibilità per garantire la compatibilità con le versioni precedenti

L'impostazione del *livello di compatibilità del database* influisce sui comportamenti solo del database specificato, non dell'intero server. Il livello di compatibilità del database offre solo una compatibilità parziale con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

> [!TIP]
> Poiché il *livello di compatibilità del database* è un'impostazione a livello di database, un'applicazione in esecuzione su un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] più recente con un livello di compatibilità del database meno recente può comunque sfruttare i miglioramenti a livello di server senza alcun bisogno di modifiche all'applicazione.
>
> Questi includono miglioramenti del monitoraggio e della risoluzione dei problemi, con le nuove [Viste a gestione dinamica (DMV) di sistema](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) e gli [Eventi estesi](../../relational-databases/extended-events/extended-events.md). È stata inoltre migliorata la scalabilità, ad esempio con l'[Architettura soft-NUMA automatica](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa).

A partire dalla modalità di compatibilità 130, tutte le nuove funzionalità che influiscono sul piano di query sono state aggiunte intenzionalmente solo al nuovo livello di compatibilità. In questo modo si riduce al minimo il rischio che si corre durante gli aggiornamenti di ridurre il livello delle prestazioni per modifiche apportate al piano di query. Dal punto di vista dell'applicazione, l'obiettivo dovrebbe essere sempre l'aggiornamento al livello di compatibilità più recente per ereditare alcune delle nuove funzionalità e sfruttare i miglioramenti in termini di prestazioni offerti da Query Optimizer, il tutto eseguito in modo controllato. Per una migrazione più sicura in cui sia possibile risolvere i problemi correlati alle differenze tra le versioni usare il livello di compatibilità inferiore nei comportamenti controllati dall'impostazione del livello di compatibilità pertinente.
Per altri dettagli, incluso il flusso di lavoro consigliato per aggiornare il livello di compatibilità del database, vedere [Procedure consigliate per aggiornare il livello di compatibilità del database](#best-practices-for-upgrading-database-compatibility-level) più avanti in questo articolo.

> [!IMPORTANT]
> Le funzionalità che non sono più supportate in una determinata versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sono protette dal livello di compatibilità. Ciò si riferisce alle funzionalità rimosse dal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].
> Ad esempio, l'hint `FASTFIRSTROW` non è più supportato in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ed è stato sostituito dall'hint `OPTION (FAST n )`. Se il livello di compatibilità del database viene impostato su 110, l'hint che non è più supportato non viene ripristinato.
> Per altre informazioni sulle funzionalità non più disponibili, vedere [Funzionalità del motore di database non più usate in SQL Server 2016](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [Funzionalità del motore di database non più usate in SQL Server 2014](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [Funzionalità del motore di database non più usate in SQL Server 2012](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md) e [Funzionalità del motore di database non più usate in SQL Server 2008](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md).
> [!IMPORTANT]
> Le modifiche di rilievo introdotte in una determinata versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **potrebbero** non essere protette dal livello di compatibilità. Ciò si riferisce alle modifiche funzionali tra le versioni del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Il comportamento di [!INCLUDE[tsql](../../includes/tsql-md.md)] è generalmente protetto dal livello di compatibilità. Gli oggetti di sistema modificati o rimossi **non** sono tuttavia protetti dal livello di compatibilità.
>
> Un esempio di modifica di rilievo **protetta** dal livello di compatibilità è la conversione implicita di un tipo di dati datetime in datetime2. Con il livello di compatibilità del database 130, in questi tipi di dati si rileva una maggiore precisione prevedendo i millisecondi frazionari, risultanti in diversi valori convertiti. Per ripristinare il comportamento di conversione precedente, impostare il livello di compatibilità del database su 120 o un livello inferiore.
>
> Di seguito sono elencati esempi di modifiche di rilievo **non protette** dal livello di compatibilità:
>
> - Nomi di colonna modificati in oggetti di sistema. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] la colonna *single_pages_kb* in sys.dm_os_sys_info è rinominata in *pages_kb*. Indipendentemente dal livello di compatibilità, la query `SELECT single_pages_kb FROM sys.dm_os_sys_info` genererà l'errore 207 (nome di colonna non valido).
> - Oggetti di sistema rimossi. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] la store procedure `sp_dboption` è rimossa. Indipendentemente dal livello di compatibilità, l'istruzione `EXEC sp_dboption 'AdventureWorks2016CTP3', 'autoshrink', 'FALSE';` genererà l'errore 2812 (Impossibile trovare la stored procedure 'sp_dboption').
>
> Per altre informazioni sulle modifiche di rilievo, vedere [Modifiche di rilievo apportate alle funzionalità del motore di database in SQL Server 2017](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2017.md), [Modifiche di rilievo apportate alle funzionalità del motore di database in SQL Server 2016](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [Modifiche di rilievo apportate alle funzionalità del motore di database in SQL Server 2014](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [Modifiche di rilievo apportate alle funzionalità del motore di database in SQL Server 2012](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md) e [Modifiche di rilievo apportate alle funzionalità del motore di database in SQL Server 2008](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).

## <a name="best-practices-for-upgrading-database-compatibility-level"></a>Procedure consigliate per aggiornare il livello di compatibilità del database

Per il flusso di lavoro consigliato per l'aggiornamento del livello di compatibilità, vedere [Modificare la modalità di compatibilità del database e usare il Query Store](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).

## <a name="compatibility-levels-and-stored-procedures"></a>Livelli di compatibilità e stored procedure

Quando si esegue una stored procedure, viene utilizzato il livello di compatibilità corrente del database in cui la procedura è definita. Se si modifica l'impostazione di compatibilità di un database, tutte le relative stored procedure vengono ricompilate automaticamente al fine di riflettere tale modifica. 

## <a name="differences-between-compatibility-level-140-and-level-150"></a>Differenze tra il livello di compatibilità 140 e 150

In questa sezione vengono descritti i nuovi comportamenti introdotti con il livello di compatibilità 150.

Il livello di compatibilità del database 150 è attualmente in anteprima pubblica per [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]. Questo livello di compatibilità del database verrà associato alla prossima generazione di miglioramenti per l'elaborazione delle query, in aggiunta a quelli introdotti per il livello di compatibilità 140.

|Livello di compatibilità 140 o inferiore|Livello di compatibilità 150|
|--------------------------------------------------|-----------------------------------------|
|I carichi di lavoro analitici e per data warehouse relazionali potrebbero non essere in grado di sfruttare gli indici columnstore a causa dell'overhead OLTP, della mancanza di supporto dei fornitori o di altre limitazioni.  Senza gli indici columnstore, questi carichi di lavoro non possono trarre vantaggio dalla modalità di esecuzione batch.|La modalità di esecuzione batch è ora disponibile per i carichi di lavoro analitici senza richiedere indici columnstore. Per altre informazioni, vedere [Modalità batch per rowstore](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore).|
|Le query in modalità riga per le quali sono necessarie concessioni di memoria di dimensioni insufficienti che causano distribuzioni su disco possono essere problematiche su esecuzioni consecutive.|Le query in modalità riga per le quali sono necessarie concessioni di memoria di dimensioni insufficienti che causano distribuzioni su disco possono evidenziare miglioramenti in termini di prestazioni su esecuzioni consecutive. Per altre informazioni, vedere [Feedback delle concessioni di memoria in modalità riga](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback).|
|Le query in modalità riga per le quali sono necessarie concessioni di memoria di dimensioni eccessive che causano problemi di concorrenza possono essere problematiche su esecuzioni consecutive.|Le query in modalità riga per le quali sono necessarie concessioni di memoria di dimensioni eccessive che causano problemi di concorrenza possono evidenziare miglioramenti in termini di concorrenza su esecuzioni consecutive. Per altre informazioni, vedere [Feedback delle concessioni di memoria in modalità riga](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback).|
|Le query che fanno riferimento a funzioni definite dall'utente scalari T-SQL useranno la chiamata iterativa, senza calcolo dei costi e con esecuzione seriale imposta. |Le funzioni definite dall'utente scalari T-SQL vengono trasformate in espressioni relazionali equivalenti che vengono rese inline nella query chiamante, ottenendo spesso significativi miglioramenti delle prestazioni. Per altre informazioni, vedere [Inlining di funzioni definite dall'utente scalari T-SQL](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining).|
|Le variabili di tabella usano un'ipotesi fissa per la stima della cardinalità.  Se il numero effettivo di righe è molto superiore al valore ipotizzato, possono esserci effetti negativi sulle prestazioni delle operazioni downstream. |I nuovi piani useranno la cardinalità effettiva della variabile tabella rilevata nella prima compilazione invece di una stima fissa. Per altre informazioni, vedere [Compilazione posticipata delle variabili di tabella](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation).|

Per altre informazioni sulle funzionalità di elaborazione delle query abilitate nel livello di compatibilità del database 150, vedere [Novità di SQL Server 2019](../../sql-server/what-s-new-in-sql-server-ver15.md) ed [Elaborazione di query intelligenti nei database SQL](https://docs.microsoft.com/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017).

## <a name="differences-between-compatibility-level-130-and-level-140"></a>Differenze tra il livello di compatibilità 130 e 140 

In questa sezione vengono descritti i nuovi comportamenti introdotti con il livello di compatibilità 140.

|Livello di compatibilità 130 o inferiore|Livello di compatibilità 140|
|--------------------------------------------------|-----------------------------------------|
|Le stime della cardinalità per istruzioni che fanno riferimento a funzioni composte da più istruzioni con valori di tabella usano un'ipotesi a riga fissa.|Le stime della cardinalità per istruzioni idonee che fanno riferimento a funzioni composte da più istruzioni con valori di tabella usano la cardinalità effettiva dell'output della funzione. Questo comportamento è abilitato dall'**esecuzione interleaved** per funzioni composte da più istruzioni con valori di tabella.|
|Le query in modalità batch per le quali sono necessarie concessioni di memoria di dimensioni insufficienti che causano distribuzioni su disco possono essere problematiche su esecuzioni consecutive.|Le query in modalità batch per le quali sono necessarie concessioni di memoria di dimensioni insufficienti che causano distribuzioni su disco possono evidenziare miglioramenti in termini di prestazioni su esecuzioni consecutive. Questo comportamento è abilitato tramite i **commenti della concessione di memoria della modalità batch**  che aggiornerà le dimensioni della concessione di memoria di un piano memorizzato nella cache se si sono verificate distribuzioni per gli operatori della modalità batch. |
|Le query in modalità batch per le quali sono necessarie concessioni di memoria di dimensioni eccessive che causano problemi di concorrenza possono essere problematiche su esecuzioni consecutive.|Le query in modalità batch per le quali sono necessarie concessioni di memoria di dimensioni eccessive che causano problemi di concorrenza possono evidenziare miglioramenti in termini di concorrenza su esecuzioni consecutive. Questo comportamento è abilitato tramite i **commenti della concessione di memoria della modalità batch**  che aggiornerà le dimensioni della concessione di memoria di un piano memorizzato nella cache se inizialmente era richiesta una memoria di dimensioni eccessive.|
|Le query in modalità batch contenenti operatori di join sono idonee per tre algoritmi di join fisico, tra cui join annidato dei cicli, hash join e merge join. Se le stime della cardinalità non sono corrette per gli input di join, può essere selezionato un algoritmo di join non appropriato. In questo caso le prestazioni ne risentiranno e l'algoritmo di join non appropriato rimarrà in uso fino a quando il piano memorizzato nella cache sarà ricompilato.|Esiste un operatore di join aggiuntivo denominato **join adattivo**. Se le stime della cardinalità non sono corrette per l'input dell'outer join di compilazione, può essere selezionato un algoritmo di join non appropriato. In questo caso e se l'istruzione è idonea per un join adattivo, verranno usati in modo dinamico un join annidato dei cicli per gli input di join più piccoli e un hash join per gli input di join più grandi senza richiedere la ricompilazione. |
|I piani semplici che fanno riferimento agli indici Columnstore non sono idonei per l'esecuzione in modalità batch. |Un piano semplice che fa riferimento agli indici Columnstore sarà eliminato e sostituito da un piano idoneo per l'esecuzione in modalità batch.|
|L'operatore UDX `sp_execute_external_script` può essere eseguito solo in modalità riga.|L'operatore UDX `sp_execute_external_script` è idoneo per l'esecuzione in modalità batch.|
|Le funzioni composte da più istruzioni con valori di tabella non presentano un'esecuzione interleaved |Esecuzione interleaved per funzioni con valori di tabella con istruzioni multiple per migliorare la qualità del piano.|

Le correzioni nel flag di traccia 4199 delle versioni precedenti di SQL Server precedenti a SQL Server 2017 sono ora abilitate per impostazione predefinita. Con la modalità di compatibilità 140, il flag di traccia 4199 continuerà a essere applicabile alle nuove correzioni di Query Optimizer rilasciate dopo SQL Server 2017. Per informazioni sul flag di traccia 4199, vedere [Flag di traccia 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).

## <a name="differences-between-compatibility-level-120-and-level-130"></a>Differenze tra i livelli di compatibilità 120 e 130

In questa sezione vengono descritti i nuovi comportamenti introdotti con il livello di compatibilità 130.

|Livello di compatibilità 120 o inferiore|Livello di compatibilità 130|
|--------------------------------------------------|-----------------------------------------|
|INSERT in un'istruzione INSERT-SELECT è a thread singolo.|INSERT in un'istruzione INSERT-SELECT è multithread o può avere un piano parallelo.|
|Le query in una tabella ottimizzata per la memoria vengono eseguite a thread singolo.|Le query in una tabella ottimizzata per la memoria ora possono avere piani paralleli.|
|Introduzione della stima di cardinalità di SQL 2014 **CardinalityEstimationModelVersion="120"**|Miglioramenti della stima di cardinalità grazie al modello di stima di cardinalità 130, visibile da un piano di query. **CardinalityEstimationModelVersion="130"**|
|Modifiche in modalità batch e modifiche in modalità riga con indici Columnstore:<br /><ul><li>Gli ordinamenti in una tabella con indice Columnstore sono in modalità riga <li>Le aggregazioni di funzioni finestra sono usate in modalità riga, ad esempio `LAG` o `LEAD` <li>Le query su tabelle Columnstore con più clausole Distinct sono usate in modalità riga <li>Le query in esecuzione con MAXDOP 1 o con un piano seriale sono usate in modalità riga</li></ul>| Modifiche in modalità batch e modifiche in modalità riga con indici Columnstore:<br /><ul><li>Gli ordinamenti in una tabella con indice Columnstore sono ora in modalità riga <li>Le aggregazioni di funzioni finestra sono ora usate in modalità batch, ad esempio `LAG` o `LEAD` <li>Le query su tabelle Columnstore con più clausole Distinct sono usate in modalità batch <li>Le query in esecuzione con MAXDOP 1 o con un piano seriale vengono eseguite in modalità batch</li></ul>|
|Le statistiche vengono aggiornate automaticamente. | La logica su cui si basa l'aggiornamento automatico delle statistiche è più aggressiva in tabelle di grandi dimensioni. In pratica, si dovrebbero ridurre i casi in cui i clienti registrano problemi di prestazioni in termini di quey laddove le righe appena inserite vengono frequentemente sottoposte a query senza però che le statistiche siano state ancora aggiornate con i valori attuali. |
|La traccia 2371 è disattivata per impostazione predefinita in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. | La [traccia 2371](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/) è attivata per impostazione predefinita in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Il flag di traccia 2371 indica allo strumento di aggiornamento delle statistiche automatico di prendere come esempio un subset di righe più piccolo ma più idoneo, in una tabella con un elevato numero di righe. <br/> <br/> Al fine di un miglioramento, è possibile includere nell'esempio più righe rispetto a quelle che sono state inserite di recente. <br/> <br/> Un altro miglioramento prevede di eseguire le query, anziché bloccarle, nello stesso momento in cui viene eseguito il processo di aggiornamento delle statistiche. |
|Per il livello 120, le statistiche vengono campionate da un processo a threaded *singolo*.|Per il livello 130, le statistiche vengono campionate da un processo a threaded *multiplo*. |
|253 è il limite di chiavi esterne in ingresso.| A una tabella possono fare riferimento fino a 10.000 chiavi esterne in ingresso o riferimenti simili. Per informazioni sulle restrizioni, vedere [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md). |
|Gli algoritmi di join hash MD2, MD4, MD5, SHA e SHA1 sono consentiti.|Sono consentiti solo gli algoritmi di join hash SHA2_256 e SHA2_512.|
||[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] include miglioramenti in alcune conversioni di tipi di dati e alcune operazioni (in genere non comuni). Per informazioni dettagliate, vedere [Miglioramenti di SQL Server 2016 relativi alla gestione di alcuni tipi di dati e operazioni non comuni](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon).|
|La funzione STRING_SPLIT non è disponibile.|La funzione STRING_SPLIT è disponibile nel livello di compatibilità 130 o superiore. Se il livello di compatibilità del database è inferiore a 130, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sarà in grado di trovare ed eseguire la funzione STRING_SPLIT.|

Le correzioni nel flag di traccia 4199 delle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] sono ora abilitate per impostazione predefinita. Con la modalità di compatibilità 130, il flag di traccia 4199 continuerà a essere applicabile alle nuove correzioni di Query Optimizer rilasciate dopo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Per usare la versione precedente di Query Optimizer in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] è necessario selezionare il livello di compatibilità 110. Per informazioni sul flag di traccia 4199, vedere [Flag di traccia 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).

## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>Differenze tra i livelli di compatibilità inferiori e il livello 120

Questa sezione descrive i nuovi comportamenti introdotti con il livello di compatibilità 120.

|Livello di compatibilità 110 o inferiore|Livello di compatibilità 120|
|--------------------------------------------------|-----------------------------------------|
|Viene utilizzata la versione precedente di Query Optimizer.|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] include miglioramenti sostanziali al componente per la creazione e l'ottimizzazione dei piani di query. Questa nuova funzionalità di Query Optimizer dipende dall'utilizzo del livello di compatibilità del database 120. Per sfruttare al meglio questi miglioramenti, sarebbe opportuno sviluppare le nuove applicazioni di database utilizzando il livello di compatibilità del database 120. Le applicazioni di cui si esegue la migrazione da versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere testate con attenzione per assicurarsi che le prestazioni vengano mantenute o migliorate. Se si verifica un calo delle prestazioni, è possibile impostare il livello di compatibilità del database su 110 o su un valore inferiore per utilizzare la metodologia precedente di Query Optimizer.<br /><br /> Il livello di compatibilità 120 del database utilizza un nuovo strumento di stima della cardinalità ottimizzato per i carichi di lavoro OLTP e di data warehouse più recenti. Prima di impostare il livello di compatibilità del database su 110 a causa di problemi di prestazioni, vedere le indicazioni riportate nella sezione Piani di query dell'argomento [Novità del motore di database](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md) di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].|
|Nei livelli di compatibilità inferiori a 120, l'impostazione della lingua viene ignorata durante la conversione di un valore **date** in un valore stringa. Si noti che questo comportamento è specifico solo del tipo **date**. Vedere l'esempio B nella sezione Esempi riportata più avanti.|L'impostazione della lingua non viene ignorata durante la conversione di un valore **date** in un valore stringa.|
|I riferimenti ricorsivi a destra di una clausola `EXCEPT` creano un ciclo infinito. L'esempio C nella sezione Esempi riportata più avanti illustra questo comportamento.|I riferimenti ricorsivi in una clausola `EXCEPT` generano un errore in conformità allo standard ANSI SQL.|
|L'espressione di tabella comune (CTE) ricorsiva consente l'uso di nomi colonna duplicati.|Una CTE ricorsiva non consente i nomi di colonna duplicati.|
|I trigger disabilitati vengono abilitati se i trigger vengono modificati.|La modifica di un trigger non cambia lo stato (abilitato o disabilitato) del trigger.|
|La clausola della tabella OUTPUT INTO ignora `IDENTITY_INSERT SETTING = OFF` e consente l'inserimento di valori espliciti.|Non è possibile inserire valori espliciti per un colonna Identity in una tabella se `IDENTITY_INSERT` è impostato su OFF.|
|Quando il contenimento del database è impostato su parziale, la convalida del campo `$action` nella clausola `OUTPUT` di un'istruzione `MERGE` può restituire un errore nelle regole di confronto.|Le regole di confronto dei valori restituiti dalla clausola `$action` di un'istruzione `MERGE` sono le regole di confronto del database anziché le regole di confronto del server e non viene restituito alcun errore di conflitto tra regole di confronto.|
|Tramite un'istruzione `SELECT INTO` viene sempre creata un'operazione di inserimento a thread singolo.|Tramite un'istruzione `SELECT INTO` è possibile creare un'operazione di inserimento parallela. Quando si inserisce un numero elevato di righe, con un'operazione parallela è possibile migliorare le prestazioni.|

## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>Differenze tra i livelli di compatibilità inferiori e i livelli 110 e 120

Questa sezione descrive i nuovi comportamenti introdotti con il livello di compatibilità 110. Questa sezione si applica al livello 120.

|Livello di compatibilità 100 o inferiore|Impostazione del livello di compatibilità 110 o inferiore|
|--------------------------------------------------|--------------------------------------------------|
|Gli oggetti di database CLR (Common Language Runtime) vengono eseguiti con la versione 4 di CLR. Non sono tuttavia presenti alcune modifiche del comportamento introdotte con la versione 4 di CLR. Per altre informazioni, vedere [Novità dell'integrazione CLR](../../relational-databases/clr-integration/clr-integration-what-s-new.md).|Gli oggetti di database CLR vengono eseguiti con la versione 4 di CLR.|
|Le funzioni XQuery **string-length** e **substring** considerano ogni surrogato come due caratteri.|Le funzioni XQuery **string-length** e **substring** considerano ogni surrogato come un carattere.|
|La parola chiave `PIVOT` è consentita in una query ricorsiva dell'espressione di tabella comune. La query tuttavia restituisce risultati non corretti quando sono presenti più righe per raggruppamento.|La parola chiave `PIVOT` non è consentita in una query ricorsiva dell'espressione di tabella comune. Viene restituito un errore.|
|L'algoritmo RC4 è supportato solo per motivi di compatibilità con le versioni precedenti. È possibile crittografare il nuovo materiale usando RC4 o RC4_128 solo quando il livello di compatibilità del database è 90 o 100. (Non consigliato.) In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] il materiale crittografato utilizzando RC4 o RC4_128 può essere decrittografato in qualsiasi livello di compatibilità.|Il nuovo materiale non può essere crittografato utilizzando RC4 o RC4_128. Usare un algoritmo più recente, ad esempio uno degli algoritmi AES. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] il materiale crittografato utilizzando RC4 o RC4_128 può essere decrittografato in qualsiasi livello di compatibilità.|
|Lo stile predefinito per le operazioni `CAST` e `CONVERT` sui tipi di dati **time** e **datetime2** è 121, tranne quando uno dei due tipi viene usato in un'espressione della colonna calcolata. Per le colonne calcolate, lo stile predefinito è 0. Questo comportamento influisce sulle colonne calcolate quando vengono create o usate nelle query con parametrizzazione automatica o nelle definizioni dei vincoli.<br /><br /> L'esempio D nella sezione Esempi riportata più avanti illustra la differenza tra gli stili 0 e 121. Non viene illustrato il comportamento descritto sopra. Per altre informazioni sugli stili di data e ora, vedere [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md).|Con il livello di compatibilità 110, lo stile predefinito per `CAST` e `CONVERT` sui tipi di dati **time** e **datetime2** è sempre 121. Se la query si basa sul comportamento obsoleto, usare un livello di compatibilità inferiore a 110 oppure specificare in modo esplicito lo stile 0 nella query interessata.<br /><br /> L'aggiornamento del database al livello di compatibilità 110 non comporta la modifica dei dati utente archiviati su disco. È necessario correggere manualmente questi dati nel modo opportuno. Se ad esempio si usa `SELECT INTO` per creare una tabella da un'origine che contiene un'espressione della colonna calcolata descritta in precedenza, verranno archiviati i dati (con stile 0), anziché la definizione della colonna calcolata. Sarà necessario aggiornare manualmente questi dati in base allo stile 121.|
|Per tutte le colonne delle tabelle remote di tipo **smalldatetime** a cui viene fatto riferimento in una vista partizionata viene eseguito il mapping come **datetime**. Le colonne corrispondenti delle tabelle locali, ovvero le colonne che occupano la stessa posizione ordinale nell'elenco di selezione, devono essere di tipo **datetime**.|Per tutte le colonne delle tabelle remote di tipo **smalldatetime** a cui viene fatto riferimento in una vista partizionata viene eseguito il mapping come **smalldatetime**. Le colonne corrispondenti delle tabelle locali, ovvero le colonne che occupano la stessa posizione ordinale nell'elenco di selezione, devono essere di tipo **smalldatetime**.<br /><br /> Dopo aver effettuato l'aggiornamento al livello di compatibilità 110, la vista partizionata distribuita avrà esito negativo poiché i tipi di dati non corrisponderanno. È possibile risolvere questo problema impostando il tipo di dati nella tabella remota su **datetime** o impostando il livello di compatibilità del database locale su 100 o su un valore inferiore.|
|Tramite la funzione `SOUNDEX` vengono implementate le regole seguenti:<br /><br /> 1) La H o W maiuscola viene ignorata se separa due consonanti aventi lo stesso numero nel codice `SOUNDEX`.<br /><br /> 2) Se il numero dei primi 2 caratteri di *character_expression* è uguale nel codice `SOUNDEX`, entrambi i caratteri vengono inclusi. Altrimenti, se il numero di un set di consonanti affiancate è uguale nel codice `SOUNDEX`, vengono escluse tutte le consonanti eccetto la prima.|Tramite la funzione `SOUNDEX` vengono implementate le regole seguenti:<br /><br /> 1) Se la H o W maiuscola separa due consonanti aventi lo stesso numero nel codice `SOUNDEX`, la consonante a destra viene ignorata<br /><br /> 2) Se il numero di un set di consonanti affiancate è uguale nel codice `SOUNDEX`, vengono escluse tutte le consonanti eccetto la prima.<br /><br /> <br /><br /> Le regole aggiuntive potrebbero generare una differenza tra i valori calcolati dalla funzione `SOUNDEX` e quelli calcolati con livelli di compatibilità precedenti. Dopo aver eseguito l'aggiornamento al livello di compatibilità 110, potrebbe essere necessario ricompilare gli indici, gli heap o i vincoli CHECK in cui viene usata la funzione `SOUNDEX`. Per altre informazioni, vedere [SOUNDEX](../../t-sql/functions/soundex-transact-sql.md).|

## <a name="differences-between-compatibility-level-90-and-level-100"></a>Differenze tra i livelli di compatibilità 90 e 100

In questa sezione vengono descritti i nuovi comportamenti introdotti con il livello di compatibilità 100.

|Livello di compatibilità 90|Livello di compatibilità 100|Probabilità di impatto|
|----------------------------------------|-----------------------------------------|---------------------------|
|L'impostazione QUOTED_IDENTIFER è sempre impostata su ON per le funzioni con valori di tabella composte da più istruzioni quando tali funzioni vengono create indipendentemente dall'impostazione del livello di sessione.|L'impostazione della sessione QUOTED IDENTIFIER viene applicata quando vengono create funzioni con valori di tabella composte da più istruzioni.|Media|
|Quando si crea o si modifica una funzione di partizione, i valori letterali **datetime** e **smalldatetime** nella funzione vengono valutati presupponendo che l'impostazione della lingua sia US_English.|L'impostazione della lingua corrente viene usata per valutare i valori letterali **datetime** e **smalldatetime** nella funzione di partizione.|Media|
|La clausola `FOR BROWSE` è consentita (e ignorata) nelle istruzioni `INSERT` e `SELECT INTO`.|La clausola `FOR BROWSE` non è consentita nelle istruzioni `INSERT` e `SELECT INTO`.|Media|
|Nella clausola `OUTPUT` sono consentiti predicati full-text.|Nella clausola `OUTPUT` non sono consentiti predicati full-text.|Bassa|
|Le istruzioni `CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` e `DROP FULLTEXT STOPLIST` non sono supportate. Per impostazione predefinita, ai nuovi indici full-text viene associato automaticamente l'elenco di parole non significative di sistema.|Le istruzioni `CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST` e `DROP FULLTEXT STOPLIST` sono supportate.|Bassa|
|L'istruzione `MERGE` non viene applicata come parola chiave riservata.|MERGE è una parola chiave completamente riservata. L'istruzione `MERGE` è supportata con i livelli di compatibilità 100 e 90.|Bassa|
|Se si usa l'argomento \<dml_table_source> dell'istruzione INSERT, viene generato un errore di sintassi.|È possibile acquisire i risultati di una clausola OUTPUT in un'istruzione INSERT, UPDATE, DELETE o MERGE nidificata e inserire tali risultati in una vista o tabella di destinazione. A tale scopo, usare l'argomento \<dml_table_source> dell'istruzione INSERT.|Bassa|
|A meno che non sia specificato `NOINDEX`, `DBCC CHECKDB` o `DBCC CHECKTABLE` esegue controlli di consistenza sia fisica sia logica in una singola tabella o vista indicizzata e in tutti i relativi indici non cluster e XML. Gli indici spaziali non sono supportati.|A meno che non sia specificato `NOINDEX`, `DBCC CHECKDB` o `DBCC CHECKTABLE` esegue controlli di consistenza sia fisica sia logica in una singola tabella e in tutti i relativi indici non cluster. Per impostazione predefinita, tuttavia, negli indici XML, negli indici spaziali e nelle viste indicizzate vengono eseguiti solo controlli di consistenza fisica.<br /><br /> Se è specificato `WITH EXTENDED_LOGICAL_CHECKS`, vengono eseguiti controlli logici su viste indicizzate, indici XML e indici spaziali, laddove presenti. Per impostazione predefinita, i controlli di consistenza fisica vengono eseguiti prima di quelli di consistenza logica. Se viene specificato anche `NOINDEX`, vengono eseguiti solo i controlli logici.|Bassa|
|Quando una clausola OUTPUT viene utilizzata con un'istruzione DML (Data Manipulation Language) e si verifica un errore di run-time durante l'esecuzione di istruzioni, l'intera transazione viene terminata e ne viene eseguito il rollback.|Quando una clausola `OUTPUT` viene usata con un'istruzione DML (Data Manipulation Language) e si verifica un errore di runtime durante l'esecuzione delle istruzioni, il comportamento dipende dall'impostazione di `SET XACT_ABORT`. Se `SET XACT_ABORT` è impostato su OFF, un errore di interruzione dell'istruzione generato dall'istruzione DML tramite la clausola `OUTPUT` terminerà l'istruzione, ma l'esecuzione del batch continuerà e non verrà eseguito il rollback della transazione. Se `SET XACT_ABORT` è impostato su ON, tutti gli errori di runtime generati dall'istruzione DML tramite la clausola OUTPUT termineranno il batch e verrà eseguito il rollback della transazione.|Bassa|
|CUBE e ROLLUP non vengono applicate come parole chiave riservate.|`CUBE` e `ROLLUP` sono parole chiave riservate all'interno della clausola GROUP BY.|Bassa|
|Agli elementi del tipo **anyType** XML viene applicata una convalida di tipo strict.|Agli elementi del tipo **anyType** viene applicata una convalida di tipo lax. Per altre informazioni, vedere [Componenti jolly e convalida del contenuto](../../relational-databases/xml/wildcard-components-and-content-validation.md).|Bassa|
|Non è possibile eseguire query sugli attributi speciali **xsi:nil** e **xsi:type**, né modificarli tramite istruzioni DML.<br /><br /> Di conseguenza, `/e/@xsi:nil` ha esito negativo, mentre `/e/@*` ignora gli attributi **xsi:nil** e **xsi:type**. `/e` restituisce tuttavia gli attributi **xsi:nil** e **xsi:type** per la consistenza con `SELECT xmlCol`, anche se `xsi:nil = "false"`.|Gli attributi speciali **xsi:nil** e **xsi:type** vengono archiviati come attributi regolari e possono essere sottoposti a query o modificati.<br /><br /> L'esecuzione della query `SELECT x.query('a/b/@*')` restituisce ad esempio tutti gli attributi, inclusi **xsi:nil** e **xsi:type**. Per escludere questi tipi nella query, sostituire `@*` con `@*[namespace-uri(.) != "`*insert xsi namespace uri*`"` e non `(local-name(.) = "type"` o `local-name(.) ="nil".`|Bassa|
|Una funzione definita dall'utente che converte un valore stringa costante XML in un tipo datetime di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene contrassegnata come deterministica.|Una funzione definita dall'utente che converte un valore stringa costante XML in un tipo datetime di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene contrassegnata come non deterministica.|Bassa|
|I tipi unione ed elenco XML non sono supportati completamente.|I tipi unione ed elenco sono supportati completamente, incluse le funzionalità seguenti.<br /><br /> Unione di elenco<br /><br /> Unione di unione<br /><br /> Elenco di tipi atomici<br /><br /> Elenco di unione|Bassa|
|Le opzioni SET necessarie per un metodo xQuery non vengono convalidate quando il metodo è contenuto in una vista o in una funzione inline con valori di tabella.|Le opzioni SET necessarie per un metodo xQuery vengono convalidate quando il metodo è contenuto in una vista o in una funzione inline con valori di tabella. Se le opzioni SET del metodo non sono impostate correttamente, viene generato un errore.|Bassa|
|I valori di attributo XML contenenti caratteri di fine riga (ritorno a capo e avanzamento riga) non vengono normalizzati in base allo standard XML, ovvero vengono restituiti entrambi i caratteri anziché un singolo carattere di avanzamento riga.|I valori di attributo XML contenenti caratteri di fine riga (ritorno a capo e avanzamento riga) vengono normalizzati in base allo standard XML, ovvero tutte le interruzioni di riga in entità analizzate esterne (inclusa l'entità del documento) vengono normalizzate in fase di input traducendo sia la sequenza di due caratteri #xD #xA sia qualsiasi carattere #xD non seguito da #XA in un singolo carattere #xA.<br /><br /> Le applicazioni che utilizzano attributi per trasportare valori stringa contenenti caratteri di fine riga non riceveranno di nuovo tali caratteri quando questi vengono inviati. Per evitare il processo di normalizzazione, utilizzare entità di caratteri numerici XML per codificare tutti i caratteri di fine riga.|Bassa|
|Le proprietà di colonna `ROWGUIDCOL` e `IDENTITY` possono essere erroneamente denominate come vincolo. L'istruzione `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)`, ad esempio, viene eseguita correttamente, ma il nome del vincolo non viene mantenuto e non è accessibile per l'utente.|Le proprietà di colonna `ROWGUIDCOL` e `IDENTITY` non possono essere denominate come vincolo. In caso contrario, verrà restituito l'errore 156.|Bassa|
|L'aggiornamento di colonne con un'assegnazione bidirezionale, ad esempio `UPDATE T1 SET @v = column_name = <expression>`, può produrre risultati imprevisti, poiché è possibile che durante l'esecuzione dell'istruzione in altre clausole, ad esempio `WHERE` e `ON`, venga usato il valore attivo della variabile anziché il valore iniziale dell'istruzione. Ciò può comportare una modifica imprevista dei significati dei predicati per ciascuna riga.<br /><br /> Questo comportamento è applicabile solo quando il livello di compatibilità è impostato su 90.|L'aggiornamento di colonne tramite un'assegnazione bidirezionale produce i risultati previsti, in quanto durante l'esecuzione dell'istruzione è possibile accedere solo al valore iniziale dell'istruzione per la colonna.|Bassa|
|Vedere l'esempio E nella sezione Esempi riportata più avanti.|Vedere l'esempio F nella sezione Esempi riportata più avanti.|Bassa|
|La funzione ODBC {fn CONVERT()} utilizza il formato di data predefinito della lingua specifica. Per alcune lingue il formato predefinito è AGM, che può comportare errori di conversione quando la funzione CONVERT() è combinata con altre funzioni, ad esempio `{fn CURDATE()}`, che prevedono l'uso del formato AMG.|La funzione ODBC `{fn CONVERT()}` usa lo stile 121, un formato AMG indipendente dalla lingua, per la conversione nei tipi di dati ODBC SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP.|Bassa|
|Le funzioni intrinseche datetime, ad esempio DATEPART, non richiedono che i valori di input di tipo stringa siano valori letterali datetime validi. Ad esempio, `SELECT DATEPART (year, '2007/05-30')` viene compilato correttamente.|Le funzioni intrinseche datetime, ad esempio `DATEPART`, richiedono che i valori di input di tipo stringa siano valori letterali datetime validi. Quando si utilizza un valore letterale datetime non valido, viene restituito l'errore 241.|Bassa|

## <a name="reserved-keywords"></a>Parole chiave riservate

L'impostazione di compatibilità determina anche le parole chiave riservate dal [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Nella tabella seguente sono elencate le parole chiave riservate introdotte per ogni livello di compatibilità.

|Livello di compatibilità|Parole chiave riservate|
|----------------------------------|-----------------------|
|130|Da determinare.|
|120|Nessuna.|
|110|WITHIN GROUP, TRY_CONVERT, SEMANTICKEYPHRASETABLE, SEMANTICSIMILARITYDETAILSTABLE, SEMANTICSIMILARITYTABLE|
|100|CUBE, MERGE, ROLLUP|
|90|EXTERNAL, PIVOT, UNPIVOT, REVERT, TABLESAMPLE|

A un determinato livello di compatibilità, le parole chiave riservate includono tutte le parole chiave introdotte per tale livello e per quelli precedenti. Pertanto, ad esempio, per le applicazioni con livello 110 tutte le parole chiave elencate nella tabella precedente sono parole chiave riservate. Per i livelli di compatibilità inferiori, le parole chiave del livello 100 rimangono nomi di oggetti validi ma le funzionalità del linguaggio di livello 110 corrispondenti a tale parole chiave non sono disponibili.

Una volta introdotta, una parola chiave rimane riservata. La parola chiave riservata PIVOT, ad esempio, introdotta per il livello di compatibilità 90, è riservata per i livelli 100, 110 e 120.

Se per un'applicazione si utilizza un identificatore che rappresenta una parola chiave riservata nel livello di compatibilità relativo, viene generato un errore. In alternativa, racchiudere l'identificatore tra parentesi quadre (**[]**) o virgolette (**""**. Per aggiornare ad esempio un'applicazione che usa l'identificatore **EXTERNAL** al livello di compatibilità 90, è possibile modificare l'identificatore in **[EXTERNAL]** o **"EXTERNAL"**.

Per altre informazioni, vedere [Parole chiave riservate](../../t-sql/language-elements/reserved-keywords-transact-sql.md).

## <a name="permissions"></a>Autorizzazioni

È richiesta l'autorizzazione ALTER per il database.

## <a name="examples"></a>Esempi

### <a name="a-changing-the-compatibility-level"></a>A. Modifica del livello di compatibilità

Nell'esempio seguente il livello di compatibilità del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] viene modificato e impostato su `110,`[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

```sql
ALTER DATABASE AdventureWorks2012
SET COMPATIBILITY_LEVEL = 110;
GO
```

Nell'esempio seguente viene restituito il livello di compatibilità del database corrente.

```sql
SELECT name, compatibility_level
FROM sys.databases
WHERE name = db_name();
```

### <a name="b-ignoring-the-set-language-statement-except-under-compatibility-level-120"></a>B. L'istruzione SET LANGUAGE viene ignorata tranne con il livello di compatibilità 120

Nella query seguente viene ignorata l'istruzione SET LANGUAGE tranne con il livello di compatibilità 120.

```sql
SET DATEFORMAT dmy;
DECLARE @t2 date = '12/5/2011' ;
SET LANGUAGE dutch;
SELECT CONVERT(varchar(11), @t2, 106);

-- Results when the compatibility level is less than 120.
12 May 2011

-- Results when the compatibility level is set to 120).
12 mei 2011
```

### <a name="c-for-compatibility-level-setting-of-110-or-lower-recursive-references-on-the-right-hand-side-of-an-except-clause-create-an-infinite-loop"></a>C. Per il livello di compatibilità impostato su 110 o un valore inferiore, i riferimenti ricorsivi a destra di una clausola EXCEPT creano un ciclo infinito

```sql
WITH
cte AS (SELECT * FROM (VALUES (1),(2),(3)) v (a)),
r
AS (SELECT a FROM Table1
UNION ALL
(SELECT a FROM Table1 EXCEPT SELECT a FROM r) )
SELECT a
FROM r;

```

### <a name="d-the-difference-between-styles-0-and-121"></a>D. La differenza tra gli stili 0 e 121

Per altre informazioni sugli stili di data e ora, vedere [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md).

```sql
CREATE TABLE t1 (c1 time(7), c2 datetime2);

INSERT t1 (c1,c2) VALUES (GETDATE(), GETDATE());

SELECT CONVERT(nvarchar(16),c1,0) AS TimeStyle0
       ,CONVERT(nvarchar(16),c1,121)AS TimeStyle121
       ,CONVERT(nvarchar(32),c2,0) AS Datetime2Style0
       ,CONVERT(nvarchar(32),c2,121)AS Datetime2Style121
FROM t1;

-- Returns values such as the following.
TimeStyle0       TimeStyle121
Datetime2Style0      Datetime2Style121
---------------- ----------------
-------------------- --------------------------
3:15PM           15:15:35.8100000
Jun  7 2011  3:15PM  2011-06-07 15:15:35.8130000
```

### <a name="e-variable-assignment---top-level-union-operator"></a>E. Assegnazione di variabile - Operatore UNION di livello principale

L'assegnazione di variabile è consentita in un'istruzione contenente un operatore UNION di livello principale, ma restituisce risultati imprevisti. Nelle istruzioni seguenti, ad esempio, alla variabile locale `@v` è assegnato il valore della colonna `BusinessEntityID` dall'unione di due tabelle. Per definizione, quando l'istruzione SELECT restituisce più valori, alla variabile viene assegnato l'ultimo valore restituito. In questo caso, alla variabile viene assegnato correttamente l'ultimo valore, ma viene restituito anche il set di risultati dell'istruzione SELECT UNION.

```sql
ALTER DATABASE AdventureWorks2012
SET compatibility_level = 110;
GO
USE AdventureWorks2012;
GO
DECLARE @v int;
SELECT @v = BusinessEntityID FROM HumanResources.Employee
UNION ALL
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;
SELECT @v;
```

L'assegnazione di variabile non è consentita in un'istruzione contenente un operatore UNION di livello principale. In caso contrario, verrà restituito l'errore 10734. Per risolvere questo errore, riscrivere la query come illustrato nell'esempio seguente.

```sql
DECLARE @v int;
SELECT @v = BusinessEntityID FROM
    (SELECT BusinessEntityID FROM HumanResources.Employee
     UNION ALL
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;
SELECT @v;
```

## <a name="see-also-alter-databaset-sqlstatementsalter-database-transact-sqlmd"></a>Vedere anche [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)

- [Parole chiave riservate](../../t-sql/language-elements/reserved-keywords-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)
- [Visualizzare o modificare il livello di compatibilità di un database](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)
