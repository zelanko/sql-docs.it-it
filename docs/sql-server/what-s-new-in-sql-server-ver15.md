---
title: Novità di SQL Server 2019 | Microsoft Docs
ms.date: 02/28/2019
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8fdc1191b5f0ef7d475e23bbcb56081821d6882b
ms.sourcegitcommit: 670082cb47f7d3d82e987b549b6f8e3a8968b5db
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57334818"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>Novità di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] si basa sulle versioni precedenti per sviluppare SQL Server come piattaforma che offre una scelta di linguaggi di sviluppo, tipi di dati, sistemi operativi ed elaborazione locale o nel cloud. Questo articolo riepiloga le novità di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Per altre informazioni e problemi noti, vedere le [Note sulla versione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

**Provare[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]**
- [![Download da Evaluation Center](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [Scaricare [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] per l'installazione in Windows](https://go.microsoft.com/fwlink/?LinkID=862101)
- Installazione in Linux per [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) e [Ubuntu](../linux/quickstart-install-connect-ubuntu.md).
- [Eseguire [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] con Docker](../linux/quickstart-install-connect-docker.md).

**Usare gli [strumenti più recenti](#tools) per un'esperienza ottimale con SQL Server 2019.**

## <a name="ctp-23"></a>CTP 2.3

Community Technology Preview (CTP) 2.3 è la versione pubblica più recente di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Questa versione include miglioramenti delle versioni CTP precedenti per la correzione di bug, il miglioramento della sicurezza e l'ottimizzazione delle prestazioni. In [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 sono state anche aggiunte o migliorate le funzionalità seguenti.

- [Cluster Big Data](#bigdatacluster)
  - Inviare processi Spark in cluster Big Data di SQL Server 2019 in IntelliJ
  - Esperienza di distribuzione e gestione di applicazioni per una serie di app con dati correlati, inclusa l'operatività di modelli di Machine Learning che usano R e Python, l'esecuzione di processi SSI e così via
  - Usare Sparklyr in cluster Big Data di SQL Server 2019
  - Montare un'archiviazione esterna compatibile con HDFS in un cluster Big Data con la suddivisione in livelli HDFS

- [Motore di database](#databaseengine)
  - Recupero del database accelerato
  - Riduzione delle ricompilazioni per carichi di lavoro che usano tabelle temporanee in più ambiti
  - Scalabilità migliorata per il checkpoint indiretto
  - Uso forzato del piano di Query Store per cursori statici e fast forward
  - Eliminazione propagata degli archi quando si eliminano i nodi in SQL Graph
  - Supporto della libreria esterna in Windows per Java e Python

- [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS)](#ssas)
  - I gruppi di calcolo nei modelli tabulari riducono il numero di misure grazie al riutilizzo della logica di calcolo.

## <a name="previous-ctps"></a>Versioni di CTP precedenti

Le versioni di CTP precedenti hanno aggiunto o modificato le funzionalità seguenti per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

- [Cluster Big Data](#bigdatacluster) 
  - Distribuire un cluster Big Data con contenitori SQL e Spark Linux in Kubernetes (CTP 2.0)
  - Accedere ai Big Data da HDFS (CTP 2.0)
  - Eseguire l'analisi avanzata e l'apprendimento automatico con Spark (CTP 2.0)
  - Usare lo streaming Spark per i dati dei pool di dati SQL (CTP 2.0)
  - Usare Azure Data Studio per eseguire volumi Query che offrono un'esperienza di tipo notebook (CTP 2.0)
  - Usare SparkR da Azure Data Studio in un cluster Big Data (CTP 2.2)
  - Distribuire app Python e R (CTP 2.2)

- [Motore di database](#databaseengine)
  - Supporto UTF-8 (CTP 2.0)
  - L'istruzione di creazione indici online ripristinabili consente di ripristinare la creazione di indici dopo l'interruzione (CTP 2.0)
  - Compilazione e ricompilazione degli indici columnstore cluster online (CTP 2.0)
  - Always Encrypted con enclave sicuri (CTP 2.0)
  - Elaborazione di query intelligenti (CTP 2.0)
  - Estensione di programmabilità per il linguaggio Java (CTP 2.0)
  - Funzionalità SQL Graph (CTP 2.0)
  - Impostazione di configurazione con ambito database per operazioni DDL online e ripristinabili (CTP 2.0)
  - Gruppi di disponibilità Always On - Reindirizzamento della connessione di replica secondaria (CTP 2.0)
  - Individuazione e classificazione dei dati - Integrata in modo nativo in SQL Server (CTP 2.0)
  - Supporto esteso per i dispositivi con memoria persistente (CTP 2.0)
  - Supporto delle statistiche columnstore in `DBCC CLONEDATABASE` (CTP 2.0)
  - Nuove opzioni aggiunte a `sp_estimate_data_compression_savings` (CTP 2.0)
  - Cluster di failover di SQL Server Machine Learning Services (CTP 2.0)
  - Infrastruttura leggera di profilatura query abilitata per impostazione predefinita (CTP 2.0)
  - Nuovi connettori PolyBase (CTP 2.0)
  - La nuova funzione di sistema `sys.dm_db_page_info` restituisce informazioni sulla pagina (CTP 2.0)
  - L'elaborazione di query intelligente aggiunge l'inlining di funzioni definite dall'utente scalari (CTP 2.1)
  - Messaggio di errore di troncamento migliorato in modo da includere i nomi di tabelle e colonne e il valore troncato (CTP 2.1)
  - Usare alias di tabelle o viste derivate nelle query corrispondenti ai grafi (CTP 2.1)
  - Dati di diagnostica migliorati per il blocco delle statistiche (CTP 2.1)
  - Pool di buffer ibrido (CTP 2.1)
  - Mascheramento dei dati statico (CTP 2.1)

- [SQL Server in Linux](#sqllinux)
  - Supporto replica (CTP 2.0)
  - Supporto di Microsoft Distributed Transaction Coordinator (MSDTC) (CTP 2.0)
  - Gruppo di disponibilità AlwaysOn in contenitori Docker con Kubernetes (CTP 2.0)
  - Supporto OpenLDAP per provider AD di terze parti (CTP 2.0)
  - Machine Learning in Linux (CTP 2.0)
  - Nuovo registro contenitori (CTP 2.0)
  - Nuove immagini del contenitore basate su RHEL (CTP 2.0)
  - Notifica dell'utilizzo elevato della memoria (CTP 2.0)

- [Master Data Services](#mds)
  - Controlli Silverlight sostituiti (CTP 2.0)

- [Sicurezza](#security)
  - Gestione dei certificati in Gestione configurazione SQL Server (CTP 2.0)

- [Strumenti](#tools)
  - Azure Data Studio
  - SQL Server Management Studio (SSMS) 18.0 (anteprima)

Continuare a leggere per altri dettagli su queste funzionalità.

## <a id="bigdatacluster"></a>Cluster Big Data

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] I [cluster Big Data](../big-data-cluster/big-data-cluster-overview.md) rendono disponibili nuovi scenari come i seguenti:

- [Inviare processi Spark in cluster Big Data di SQL Server 2019 in IntelliJ](../big-data-cluster/spark-submit-job-intellij-tool-plugin.md) (CTP 2.3)
- [Esperienza di distribuzione e gestione di applicazioni](../big-data-cluster/big-data-cluster-create-apps.md) per una serie di app con dati correlati, inclusa l'operatività di modelli di Machine Learning che usano R e Python, l'esecuzione di processi SSI e così via (CTP 2.3)
- [Usare Sparklyr in cluster Big Data di SQL Server 2019](../big-data-cluster/sparklyr-from-RStudio.md) (CTP 2.3)
- Montare un'archiviazione esterna compatibile con HDFS in cluster Big Data usando la [suddivisione in livelli HDFS](../big-data-cluster/hdfs-tiering.md) (CTP 2.3)
- Usare SparkR da Azure Data Studio in un cluster Big Data (CTP 2.2)
- [Distribuire app Python e R](../big-data-cluster/big-data-cluster-create-apps.md) (CTP 2.2)
- Distribuire un cluster Big Data con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e contenitori Spark Linux in Kubernetes (CTP 2.0)
- Accedere ai Big Data da HDFS (CTP 2.0)
- Eseguire l'analisi avanzata e l'apprendimento automatico con Spark (CTP 2.0)
- Usare lo streaming Spark per i dati dei pool di dati SQL (CTP 2.0)
- Eseguire volumi Query che offrono un'esperienza di tipo notebook in [**Azure Data Studio**](../sql-operations-studio/what-is.md) (CTP 2.0)
 
[!INCLUDE [Big data clusters preview](../includes/big-data-cluster-preview-note.md)]

## Motore di database <a id="databaseengine"></a>

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce o migliora le nuove funzionalità seguenti per [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]

### <a name="accelerated-database-recovery-ctp-23"></a>Recupero del database accelerato (CTP 2.3)

Il [recupero del database accelerato](http://docs.microsoft.com/azure/sql-database/sql-database-accelerated-database-recovery
) migliora considerevolmente la disponibilità del database, in particolare in presenza di transazioni a esecuzione prolungata, riprogettando il processo di recupero del motore di database di SQL Server. Il [recupero del database](../relational-databases/logs/the-transaction-log-sql-server.md?#recovery-of-all-incomplete-transactions-when--is-started) è il processo che SQL Server usa per avviare ogni database in uno stato coerente a livello di transazioni o in uno stato normale. Un database in cui è abilitato il recupero del database accelerato completa l'operazione di recupero in modo considerevolmente più veloce dopo un failover o una chiusura non normale. In CTP 2.3 il recupero del database accelerato può essere abilitato per ogni database usando la sintassi seguente:

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
```

>[!NOTE]
>Questa sintassi non è necessaria per sfruttare i vantaggi di questa funzionalità nel database SQL di Azure in cui è la funzione è abilitata per impostazione predefinita.

In caso di database critici con possibili transazioni di grandi dimensioni, provare a usare questa funzionalità durante l'anteprima. Inviare commenti al [team di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](<https://aka.ms/sqlfeedback>).

### <a name="query-store-plan-forcing-support-for-fast-forward-and-static-cursors-ctp-23"></a>Uso forzato del piano di Query Store per cursori statici e fast forward (CTP 2.3)

Query Store ora supporta la possibilità di forzare i piani di esecuzione query per i cursori T-SQL e API statici e fast forward. L'uso forzato è ora supportato tramite `sp_query_store_force_plan` o tramite i report di Query Store in SQL Server Management Studio.

### <a name="reduced-recompilations-for-workloads-using-temporary-tables-across-multiple-scopes-ctp-23"></a>Riduzione delle ricompilazioni per carichi di lavoro che usano tabelle temporanee in più ambiti (CTP 2.3)

Prima di questa funzionalità, quando si faceva riferimento a una tabella temporanea con un'istruzione DML (`SELECT`, `INSERT`, `UPDATE`, `DELETE`), se la tabella temporanea era stata creata da un batch di ambito esterno, l'istruzione DML veniva ricompilata ogni volta che veniva eseguita. Grazie a questo miglioramento, SQL Server esegue semplici controlli aggiuntivi per evitare ricompilazioni non necessarie:

- Controlla se il modulo di ambito esterno usato per creare la tabella temporanea in fase di compilazione è uguale a quello usato per le esecuzioni consecutive. 
- Tiene traccia di eventuali modifiche di Data Definition Language (DDL) apportate alla compilazione iniziale e le confronta con le operazioni DDL per le esecuzioni consecutive. 

Il risultato finale è la riduzione di ricompilazioni estranee e di overhead della CPU.

### <a name="improved-indirect-checkpoint-scalability-ctp-23"></a>Scalabilità migliorata per il checkpoint indiretto (CTP 2.3)

Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gli utenti possono riscontrare errori con l'utilità di pianificazione che non cede il controllo quando il database genera un numero elevato di pagine dirty, ad esempio tempdb. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce una scalabilità migliorata per il checkpoint indiretto che consente di evitare questi errori nei database che hanno un carico di lavoro di UPDATE/INSERT eccessivo.

### <a name="scalar-udf-inlining-ctp-21"></a>Inlining di funzioni definite dall'utente scalari (CTP 2.1)

L'inlining di funzioni definite dall'utente scalari trasforma automaticamente le funzioni definite dall'utente (UDF) scalari in espressioni relazionali e le incorpora nella query SQL chiamante, migliorando così le prestazioni dei carichi di lavoro che usano funzioni definite dall'utente scalari. L'inlining di funzioni definite dall'utente scalari facilita l'ottimizzazione basata sui costi delle operazioni all'interno di funzioni definite dall'utente e genera piani efficienti orientati ai set e paralleli, invece di piani di esecuzione seriali, inefficienti e iterativi. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150.

Per altre informazioni, vedere [Inlining di funzioni definite dall'utente scalari](../relational-databases/user-defined-functions/scalar-udf-inlining.md).

### <a name="truncation-error-message-improved-to-include-table-and-column-names-and-truncated-value-ctp-21"></a>Messaggio di errore di troncamento migliorato in modo da includere i nomi di tabelle e colonne e il valore troncato (CTP 2.1)

Il messaggio di errore con ID 8152 `String or binary data would be truncated` è familiare a molti sviluppatori e amministratori di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che sviluppano e gestiscono carichi di lavoro di spostamento dei dati. Questo errore viene generato durante il trasferimento di dati tra un'origine e una destinazione con schemi diversi quando l'origine dati è troppo grande per adattarsi al tipo di dati di destinazione. Questo messaggio di errore può richiedere molto tempo per la risoluzione. [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce un nuovo messaggio di errore più specifico (2628) per questo scenario:  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

Il nuovo messaggio di errore 2628 fornisce altre informazioni di contesto per il problema di troncamento dei dati, semplificando il processo di risoluzione dei problemi. Per CTP 2.1 e CTP 2.2 si tratta di un messaggio di errore che prevede il consenso esplicito e richiede l'abilitazione del [flag di traccia](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460.

### <a name="improved-diagnostic-data-for-stats-blocking-ctp-21"></a>Dati di diagnostica migliorati per il blocco delle statistiche (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] offre dati di diagnostica migliorati per le query con esecuzione prolungata in attesa di operazioni di aggiornamento delle statistiche sincrone. La colonna `command` della vista a gestione dinamica `sys.dm_exec_requests` mostra `SELECT (STATMAN)` se un'operazione `SELECT` è in attesa del completamento di un'operazione di aggiornamento delle statistiche sincrona prima di continuare l'esecuzione di query. Inoltre, viene esposto il nuovo tipo di attesa `WAIT_ON_SYNC_STATISTICS_REFRESH` nella vista a gestione dinamica `sys.dm_os_wait_stats`. Mostra il tempo accumulato a livello di istanza dedicato alle operazioni di aggiornamento delle statistiche sincrone.

### <a name="static-data-masking-ctp-21"></a>Mascheramento dei dati statico (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce il mascheramento dei dati statico. È possibile usare il mascheramento dei dati statico per purificare i dati sensibili in copie di database di SQL Server. Il mascheramento dei dati statico consente di creare una copia purificata dei database in cui tutte le informazioni sensibili vengono modificate in modo che la copia diventi condivisibile con gli utenti non di produzione. Il mascheramento dei dati statico può essere usato per scopi di sviluppo, test, analisi e creazione di report aziendali, conformità, risoluzione dei problemi e in qualsiasi altro scenario in cui i dati specifici non possono essere copiati in ambienti diversi.

Il mascheramento dei dati statico opera a livello di colonna. Selezionare le colonne da mascherare e per ogni colonna selezionata, specificare una funzione di mascheramento. Il mascheramento dei dati statico copia il database e quindi applica le funzioni di mascheramento specificate nelle colonne.

#### <a name="static-data-masking-vs-dynamic-data-masking"></a>Mascheramento dei dati statico e mascheramento dei dati dinamico

Il mascheramento dei dati è il processo di applicazione di una maschera a un database per nascondere le informazioni sensibili del database e sostituirle con nuovi dati o dati ripuliti. Microsoft offre due opzioni di mascheramento, ovvero il mascheramento dei dati statico e il mascheramento dei dati dinamico. Il mascheramento dei dati dinamico è stato introdotto in [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Nella tabella seguente vengono messe a confronto questi due soluzioni:

|Mascheramento dei dati statico |Mascheramento dati dinamici|
|:----|:----|
|Applicato a una copia del database <br/><br/>I dati originali non sono recuperabili<br/><br/>Il mascheramento avviene a livello di archiviazione<br/><br/>Tutti gli utenti hanno accesso agli stessi dati mascherati<br/><br/>Pensato per l'accesso continuo a livello di team|Applicato al database originale<br/><br/>I dati originali rimangono intatti<br/><br/>Il mascheramento avviene in tempo reale in fase di query<br/><br/>Il mascheramento varia in base alle autorizzazioni dell'utente <br/><br/>Pensato per l'accesso puntuale da parte di utenti specifici|

### <a name="database-compatibility-level-ctp-20"></a>Livello di compatibilità del database (CTP 2.0)

È stata aggiunto il livello **COMPATIBILITY_LEVEL 150** del database. Per attivarlo per un database utente specifico, eseguire:

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="utf-8-support-ctp-22"></a>Supporto UTF-8 (CTP 2.2)

Supporto completo per la codifica dei caratteri di grande diffusione UTF-8 come codifica di importazione o esportazione o come regola di confronto di livello database o colonna per i dati di testo. La codifica UTF-8 è consentita nei tipi di dati `CHAR` e `VARCHAR` ed è abilitata quando si crea o si modifica la regola di confronto di un oggetto convertendola in una regola di confronto con il suffisso `UTF8`. 

Ad esempio da `LATIN1_GENERAL_100_CI_AS_SC` a `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. UTF-8 è disponibile solo per le regole di confronto di Windows che supportano i caratteri supplementari. Questa funzionalità è stata introdotta in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. `NCHAR` e `NVARCHAR` consentono solo la codifica UTF-16 e rimangono invariati.

A seconda del set di caratteri in uso, questa funzionalità può offrire importanti risparmi di risorse di archiviazione. Se ad esempio si cambia il tipo di dati di una colonna esistente e contenente stringhe Latin da `NCHAR(10)` a `CHAR(10)` usando una regola di confronto con supporto di UTF-8, i requisiti di risorse di archiviazione vengono ridotti del 50%. Questa riduzione deriva dal fatto che `NCHAR(10)` richiede 20 byte per l'archiviazione, mentre `CHAR(10)` richiede solo 10 byte per la stessa stringa Unicode.

Per altre informazioni, vedere [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).

CTP 2.1 aggiunge il supporto per la selezione delle regole di confronto UTF-8 come impostazione predefinita durante il programma di installazione di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

CTP 2.2 aggiunge il supporto per l'uso della codifica dei caratteri UTF-8 con la replica di Microsoft SQL Server.

### <a name="resumable-online-index-create-ctp-20"></a>Creazione di indici online ripristinabili (CTP 2.0)

- Con la **creazione di indici online ripristinabili** un'operazione di creazione indice può essere sospesa e ripresa in seguito dal punto in cui è stata interrotta, anziché riavviarla dall'inizio.

  La creazione di indici online ripristinabili supporta gli scenari seguenti:
  - Ripristino di un'operazione di creazione indice dopo un errore di creazione indice, ad esempio in seguito a un failover del database o all'esaurimento dello spazio su disco.
  - Sospensione temporanea di un'operazione di creazione indice e ripresa in un secondo momento, per consentire di liberare temporaneamente risorse di sistema in base alle esigenze e quindi riprendere l'esecuzione.
  - Creazione di indici di grandi dimensioni senza usare grandi quantità spazio di registro, senza un'esecuzione prolungata che blocca altre attività di manutenzione e con la possibilità di troncare il log.

  In caso di un errore di creazione indice, senza questa funzionalità la creazione indice online va eseguita di nuovo e l'operazione deve essere riavviata dall'inizio.

In questa versione, la funzionalità ripristinabile viene estesa con l'aggiunta di questa funzionalità alla [ricompilazione dell'indice online ripristinabile](https://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/), già disponibile.

È anche possibile impostare questa funzionalità come valore predefinito per un database specifico usando l'[impostazione predefinita con ambito database per le operazioni DDL online e ripristinabili](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Per altre informazioni, vedere [Creazione di indici online ripristinabili](../t-sql/statements/create-index-transact-sql.md#resumable-indexes).

### <a name="build-and-rebuild-clustered-columnstore-indexes-online-ctp-20"></a>Compilare e ricompilare gli indici columnstore cluster online (CTP 2.0)

È possibile convertire le tabelle rowstore al formato columnstore. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] la creazione di indici columnstore cluster (CCI) era un processo offline la cui esecuzione richiedeva la sospensione di tutte le modifiche. Con [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] è possibile creare o ricreare indici columnstore cluster online. Il carico di lavoro non viene bloccato e tutte le modifiche apportate ai dati sottostanti vengono aggiunte in modo trasparente nella tabella columnstore di destinazione. Di seguito sono elencati alcuni esempi di nuove istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] che è possibile usare:

  ```sql
  CREATE CLUSTERED COLUMNSTORE INDEX cci
    ON <tableName>
    WITH (ONLINE = ON);
  ```

  ```sql
  ALTER INDEX cci
    ON <tableName>
    REBUILD WITH (ONLINE = ON);
  ```

### <a name="always-encrypted-with-secure-enclaves-ctp-20"></a>Always Encrypted con enclave sicuri (CTP 2.0)

Espansione di Always Encrypted con crittografia sul posto e calcoli avanzati. Le espansioni provengono dall'abilitazione di calcoli sui dati di testo non crittografato all'interno di un enclave sicuro sul lato server.

Le operazioni di crittografia includono la crittografia delle colonne e la rotazione delle chiavi di crittografia della colonna. Queste operazioni possono ora essere trasmesse usando [!INCLUDE[tsql](../includes/tsql-md.md)] e non richiedono lo spostamento dei dati fuori dal database. Gli enclave sicuri rendono disponibile Always Encrypted per una vasta gamma di scenari, che dispongono di entrambi i requisiti seguenti:  

- L'esigenza di proteggere i dati sensibili da utenti con privilegi elevati ma non provvisti delle autorizzazioni necessarie, quali amministratori di database, amministratori di sistema, operatori cloud o istanze di malware.
- L'esigenza di supportare calcoli avanzati sui dati protetti all'interno del sistema di database.

Per informazioni dettagliate, vedere [Always Encrypted con enclave sicuri](../relational-databases/security/encryption/always-encrypted-enclaves.md).

> [!NOTE]
> Always Encrypted con enclave sicuri è disponibile solo nel sistema operativo Windows.

### <a name="intelligent-query-processing-ctp-20"></a>Elaborazione di query intelligenti (CTP 2.0)

- Il **feedback delle concessioni di memoria in modalità riga** estende la funzionalità di feedback delle concessioni di memoria, adattando le dimensioni delle concessioni di memoria introdotte in [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] sia per gli operatori in modalità batch che per quelli in modalità riga. Per una condizione di concessione di memoria di dimensioni eccessive, se la memoria concessa supera di oltre due volte la quantità di memoria realmente usata, il feedback delle concessioni di memoria ricalcola la concessione. Le esecuzioni consecutive richiederanno quindi una quantità di memoria inferiore. Per le concessioni di memoria di dimensioni insufficienti che generano distribuzioni su disco, il feedback delle concessioni di memoria attiva il ricalcolo della concessione di memoria. Le esecuzioni consecutive richiederanno quindi una quantità di memoria superiore. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150.

- **Approximate COUNT DISTINCT** restituisce il numero approssimativo di valori univoci non Null in un gruppo. Questa funzione è progettata per l'uso in scenari Big Data. È ottimizzata per le query in cui sono vere tutte le condizioni seguenti:
   - Accede a set di dati costituiti da milioni di righe.
   - Definisce l'aggregazione di una o più colonne con un numero elevato di valori distinti.
   - La velocità di risposta è più importante della precisione assoluta.
      - `APPROX_COUNT_DISTINCT` restituisce i risultati con un'approssimazione alla risposta precisa pari al 2%.
      - La risposta approssimata viene restituita in una frazione minima del tempo necessario per la risposta esatta.

- La **modalità batch per rowstore** non richiede più un indice columnstore per l'elaborazione di una query in modalità batch. La modalità batch consente agli operatori di query di funzionare su un set di righe, anziché su una sola riga alla volta. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150. La modalità batch migliora la velocità delle query che accedono a tabelle rowstore quando sono soddisfatte le condizioni seguenti:
   - La query usa operatori analitici, ad esempio operatori di join o di aggregazione.
   - La query implica un numero di righe non inferiore a 100.000.
   - La query è associata alla CPU anziché all'input/output di dati.
   - La creazione e l'uso di un indice columnstore può comportare uno degli svantaggi seguenti:
      - Aggiunge un sovraccarico eccessivo alla query.
      - Non è implementabile perché l'applicazione dipende da una funzionalità non ancora supportata con gli indici columnstore.

- **La compilazione posticipata delle variabili di tabella** migliora la qualità del piano e le prestazioni generali per le query che fanno riferimento a variabili di tabella. Durante l'ottimizzazione e la compilazione iniziale, questa funzionalità propagherà le stime della cardinalità basate sui conteggi effettivi delle righe di variabili di tabella. Queste informazioni accurate sui conteggi di righe verranno usate per l'ottimizzazione delle operazioni del piano downstream. Questa funzionalità è abilitata per impostazione predefinita nel livello di compatibilità del database 150.

Per usare la funzionalità di elaborazione di query intelligenti impostare l'opzione del database `COMPATIBILITY_LEVEL = 150`.

### <a id="programmability"></a> Estensioni di programmabilità per il linguaggio Java (CTP 2.0)

- **Estensione per il linguaggio Java (anteprima)**: usare l'estensione per il linguaggio Java per eseguire codice Java in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. In [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] questa estensione viene installata quando si aggiunge la funzionalità "Machine Learning Services (in-database)" all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

### <a id="sqlgraph"></a> Funzionalità SQL Graph

- **Usare alias di tabelle o viste derivate nelle query corrispondenti ai grafi (CTP 2.1)** Le query per grafi nell'anteprima di [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] supportano l'uso di alias di tabelle e viste derivate nella sintassi di `MATCH`. Per usare questi alias in `MATCH`, le viste e tabelle derivate devono essere create su un set di tabelle nodi o un set di tabelle archi, usando l'operatore `UNION ALL`. Le tabelle nodi o le tabelle archi possono o meno avere filtri applicati. La possibilità di usare alias di tabelle o viste derivate nelle query `MATCH` può essere molto utile in scenari in cui si intende eseguire query su entità eterogenee o connessioni eterogenee tra due o più entità nel grafo.

- **Il supporto delle corrispondenze in `MERGE` DML (CTP 2.0)** consente di specificare relazioni grafo in un'unica istruzione anziché in istruzioni `INSERT`, `UPDATE` o `DELETE` separate. È possibile unire i dati grafo correnti da tabelle nodi o tabelle archi a nuovi dati usando i predicati `MATCH` nell'istruzione `MERGE`. Questa funzionalità abilita gli scenari `UPSERT` nelle tabelle bordi. Ora gli utenti possono usare un'istruzione merge singola per inserire un nuovo bordo o aggiornarne uno esistente tra due nodi.

- Sono stati introdotti i **vincoli di arco (CTP 2.0)** per le tabelle archi in SQL Graph. Le tabelle bordi possono connettere qualsiasi nodo a qualsiasi altro nodo del database. Con l'introduzione di vincoli di bordo, è ora possibile applicare determinate restrizioni a questo comportamento. Il nuovo vincolo `CONNECTION` consente di specificare il tipo di nodi ai quali può connettersi una tabella bordi nello schema. 

  **(CTP 2.3)**  Estendendo ancora di più questa funzionalità, è possibile definire azioni di eliminazione propagata in un vincolo di arco. È possibile definire le azioni eseguite dal motore di database quando un utente elimina i nodi che un arco specifico connette.

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations--ctp-20"></a>Impostazione predefinita con ambito database per operazioni DDL online e ripristinabili (CTP 2.0)

- L'**impostazione predefinita con ambito database per operazioni DDL online e ripristinabili** supporta un'impostazione di funzionamento predefinita per le operazioni indice `ONLINE` e `RESUMABLE` a livello del database, anziché definire tali opzioni per ogni singola istruzione DDL dell'indice, quali le operazioni di creazione o ricompilazione dell'indice.

- Impostare questi valori predefiniti usando le opzioni di configurazione con ambito database `ELEVATE_ONLINE` e `ELEVATE_RESUMABLE`. Entrambe le opzioni fanno sì che il motore del database imposti automaticamente le operazioni dell'indice supportate per l'esecuzione online o ripristinabili. È possibile abilitare i comportamenti seguenti tramite queste opzioni:

  - L'opzione `FAIL_UNSUPPORTED` autorizza tutte le operazioni sugli indici online o ripristinabili e non consente le operazioni sugli indici online o ripristinabili non supportate.
  - L'opzione `WHEN_SUPPPORTED` consente le operazioni online o ripristinabili supportate ed esegue le operazioni sugli indici non supportate non in linea o in modo non ripristinabile.
  - L'opzione `OFF` supporta il comportamento corrente di esecuzione di tutte le operazioni sugli indici come offline e non ripristinabili, salvo diversa indicazione esplicita nell'istruzione DDL.

Per eseguire l'override dell'impostazione predefinita, includere l'opzione `ONLINE` o l'opzione `RESUMABLE` nei comandi di creazione e ricompilazione dell'indice. 

Senza questa funzionalità è necessario specificare le opzioni online e ripristinabili direttamente nell'istruzione DDL dell'indice, ad esempio nell'istruzione di creazione e ricompilazione dell'indice.

Per altre informazioni sulle operazioni ripristinabili, vedere [Creazione di indici online ripristinabili](https://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/).

### <a id="ha"></a>Gruppi di disponibilità AlwaysOn - Più repliche sincrone (CTP 2.0)

- **Fino a cinque repliche sincrone**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta il numero massimo di repliche sincrone fino a 5. Il numero massimo era 3 in [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. È possibile configurare questo gruppo di cinque repliche per il failover automatico all'interno del gruppo. Sono presenti una replica primaria e 4 repliche secondarie sincrone.

- **Reindirizzamento della connessione di replica da secondaria a primaria**: consente di orientare le connessioni dell'applicazione client alla replica primaria, indipendentemente dal server di destinazione specificato nella stringa di connessione. Questa funzionalità consente il reindirizzamento della connessione senza un listener. Usare il reindirizzamento della connessione di replica da secondaria a primaria se si verificano le condizioni seguenti:

  - La tecnologia cluster non offre una funzionalità listener.
  - È implementata una configurazione con più subnet in cui il reindirizzamento diventa complesso.
  - Scenari di scalabilità in lettura o ripristino di emergenza in cui il tipo di cluster è `NONE`.

Per informazioni dettagliate, vedere [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Reindirizzamento connessione in lettura/scrittura dalla replica secondaria alla primaria (Gruppi di disponibilità AlwaysOn)).

### <a name="data-discovery-and-classification-ctp-20"></a>Individuazione e classificazione dei dati (CTP 2.0)

Funzionalità avanzate di individuazione e classificazione dei dati incorporate a livello nativo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La classificazione e l'assegnazione di etichette ai dati più sensibili offre i vantaggi seguenti:
- Contribuisce a soddisfare i requisiti in materia di privacy e di conformità alle normative.
- Supporta scenari di sicurezza quali il monitoraggio (controllo) e gli avvisi in caso di accesso anomalo ai dati sensibili.
- Semplifica l'identificazione della posizione dei dati sensibili nell'organizzazione, in modo che gli amministratori possano adottare le misure necessarie per la protezione del database.

Per altre informazioni, vedere [Individuazione dati e classificazione SQL](../relational-databases/security/sql-data-discovery-and-classification.md).

Anche il [controllo](../relational-databases/security/auditing/sql-server-audit-database-engine.md) è stato migliorato e il log di controllo ora include un nuovo campo denominato `data_sensitivity_information`, che registra le classificazioni (etichette punteggio) di riservatezza dei dati effettivi restituiti dalla query. Per dettagli ed esempi vedere [ADD SENSITIVITY CLASSIFICATION](../t-sql/statements/add-sensitivity-classification-transact-sql.md).

>[!NOTE]
>Non sono state apportate modifiche alle modalità di abilitazione del controllo. È stato aggiunto ai record di controllo un nuovo campo `data_sensitivity_information`, che registra le classificazioni (etichette punteggio) di riservatezza dei dati effettivi restituiti dalla query. Vedere [Controllo dell'accesso ai dati sensibili](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification#subheading-3).

### <a name="expanded-support-for-persistent-memory-devices-ctp-20"></a>Supporto esteso per i dispositivi con memoria persistente (CTP 2.0)

Qualsiasi file [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inserito in un dispositivo con memoria persistente può ora essere eseguito in modalità *con riconoscimento*. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] accede direttamente al dispositivo, ignorando lo stack di archiviazione del sistema operativo e usando operazioni memcpy efficienti. Questa modalità migliora le prestazioni poiché consente input/output a bassa latenza su tali dispositivi.
    - Esempi di file [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] includono:
        - File di database
        - File di log delle transazioni
        - File del checkpoint OLTP in memoria
    - La memoria persistente è anche detta memoria della classe di archiviazione.
    - La memoria persistente è talvolta denominata in modo informale *pmem* in siti Web non Microsoft.

> [!NOTE]
> Per questa versione di anteprima il riconoscimento dei file nei dispositivi con memoria persistente è disponibile solo per Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Windows supporta i dispositivi con memoria persistente a partire da [!INCLUDE[ssSQL15](../includes/sssql15-md.md)].

### <a name="hybrid-buffer-pool-ctp-21"></a>Pool di buffer ibrido (CTP 2.1)

Il pool di buffer ibrido è una nuova funzionalità del motore di database di SQL Server con la quale le pagine del database che si trovano in file di database posizionati in un dispositivo di memoria persistente (PMEM) saranno accessibili direttamente quando necessario. Dato che i dispositivi PMEM offrono una latenza molto bassa per l'accesso ai dati, il motore può evitare di creare una copia dei dati in un'area di "pagine pulite" del pool di buffer e semplicemente accedere alla pagina direttamente nel dispositivo PMEM. L'accesso viene eseguito tramite I/O mappato alla memoria, come appropriato per il riconoscimento. Ciò offre vantaggi a livello di prestazioni grazie alla possibilità di evitare la creazione di una copia della pagina nella DRAM e di evitare che lo stack di I/O del sistema operativo acceda alla pagina in uno spazio di archiviazione permanente. Questa funzionalità è disponibile sia in SQL Server in Windows che in SQL Server in Linux.

Per altre informazioni, vedere [Pool di buffer ibrido](../database-engine/configure-windows/hybrid-buffer-pool.md)

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase-ctp-20"></a>Supporto delle statistiche columnstore in DBCC CLONEDATABASE (CTP 2.0)

`DBCC CLONEDATABASE` crea una copia di un database con il solo schema, che include tutti gli elementi necessari per la risoluzione dei problemi di prestazioni delle query senza copiare i dati. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] il comando non copiava le statistiche necessarie per rilevare con precisione i problemi delle query dell'indice columnstore e per acquisire queste informazioni erano necessari passaggi manuali. In [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ora `DBCC CLONEDATABASE` acquisisce automaticamente i BLOB di statistiche per gli indici columnstore. Di conseguenza non sono necessari passaggi manuali.

### <a name="new-options-added-to-spestimatedatacompressionsavings-ctp-20"></a>Nuove opzioni aggiunte a sp_estimate_data_compression_savings (CTP 2.0)

`sp_estimate_data_compression_savings` restituisce le dimensioni correnti degli oggetti richiesti e stima le dimensioni dell'oggetto per lo stato di compressione richiesto. Questa procedura supporta attualmente tre opzioni: `NONE`, `ROW` e `PAGE`. `COLUMNSTORE_ARCHIVE` introduce due nuove opzioni: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e `COLUMNSTORE`. Le nuove opzioni consentono di stimare il risparmio di spazio ottenibile con la creazione di un indice columnstore sulla tabella usando la compressione del columnstore standard o archivio.

### <a id="ml"></a> Cluster di failover di SQL Server Machine Learning Services e modellazione basata sulle partizioni (CTP 2.0)

- **Modellazione basata sulle partizioni**: elabora gli script esterni per le singole partizioni dei dati usando i nuovi parametri aggiunti a `sp_execute_external_script`. Questa funzionalità supporta il training di molti modelli di dimensioni ridotte (un modello per ogni partizione dei dati) invece del training di un solo modello di grandi dimensioni.

- **Cluster di failover di Windows Server**: è possibile configurare la disponibilità elevata per Machine Learning Services in un cluster di failover di Windows Server.

Per informazioni dettagliate, vedere [What's new in SQL Server Machine Learning Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md) (Novità di SQL Server Machine Learning Services).

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default-ctp-20"></a>Infrastruttura leggera di profilatura query abilitata per impostazione predefinita (CTP 2.0)

L'infrastruttura leggera di profilatura query (LWP) restituisce dati sulle prestazioni delle query in modo più efficiente rispetto ai meccanismi di profilatura standard. Ora la profilatura leggera è abilitata per impostazione predefinita. È stata introdotta in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. La profilatura leggera offre un meccanismo per la raccolta di statistiche sull'esecuzione query con un sovraccarico previsto pari al 2% della capacità della CPU, rispetto a un sovraccarico che può raggiungere il 75% della capacità della CPU per il meccanismo di profilatura query standard. Nelle versioni precedenti, questa funzionalità era OFF per impostazione predefinita. Gli amministratori di database potevano abilitarla con il [flag di traccia 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md). 

Per altre informazioni sulla profilatura leggera, vedere [Infrastruttura di profilatura query](../relational-databases/performance/query-profiling-infrastructure.md).

### <a id="polybase"></a>Nuovi connettori PolyBase

- **Nuovi connettori per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata e MongoDB**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] presentazione di nuovi connettori a dati esterni per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Oracle, Teradata e MongoDB.

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information-ctp-20"></a>La nuova funzione di sistema sys.dm_db_page_info restituisce informazioni sulla pagina (CTP 2.0)

`sys.dm_db_page_info(database_id, file_id, page_id, mode)` restituisce informazioni su una pagina di un database. La funzione restituisce una riga che contiene le informazioni di intestazione della pagina, tra cui `object_id`, `index_id` e `partition_id`. Questa funzione sostituisce l'uso di `DBCC PAGE` nella maggior parte dei casi. 

Per facilitare la risoluzione dei problemi associati alle attese correlate alla pagina è stata anche aggiunta a `sys.dm_exec_requests` e `sys.sysprocesses` la nuova colonna page_resource. La nuova colonna consente di unire `sys.dm_db_page_info` a queste viste tramite un'altra nuova funzione di sistema: `sys.fn_PageResCracker`. Vedere come esempio lo script seguente:

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d 
  CROSS APPLY sys.fn_PageResCracker(d.page_resource) AS r
  CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id,'DETAILED')
    AS page_info;
```

## <a id="sqllinux"></a> SQL Server in Linux

- **Supporto della replica (CTP 2.0)**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] supporta la replica di SQL Server in Linux. Una macchina virtuale Linux con SQL Agent può essere un'entità di pubblicazione, di distribuzione o un sottoscrittore. 

  Creare i seguenti tipi di pubblicazioni:
  - Transazionale
  - Snapshot
  - Merge

  Configurare la replica [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] oppure usare le [stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

- **Supporto per Microsoft Distributed Transaction Coordinator (MSDTC) (CTP 2.0)**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] in Linux supporta Microsoft Distributed Transaction Coordinator (MSDTC). Per informazioni dettagliate, vedere [Come configurare Microsoft Distributed Transaction Coordinator (MSDTC) in Linux](../linux/sql-server-linux-configure-msdtc.md).

- **Gruppo di disponibilità AlwaysOn in contenitori Docker con Kubernetes (CTP 2.2)**: Kubernetes può orchestrare i contenitori che eseguono istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per restituire un set di database a disponibilità elevata con Gruppi di disponibilità Always On di SQL Server. Un operatore Kubernetes distribuisce un elemento StatefulSet che include un contenitore con **mssql-server** e un monitoraggio di integrità.

- **Supporto OpenLDAP per provider AD di terze parti (CTP 2.0)**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] in Linux è supportato OpenLDAP, che consente ai fornitori di terze parti di accedere a Active Directory.

- **Machine Learning in Linux (CTP 2.0)**: [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Machine Learning Services (In-Database) è ora supportato in Linux. Il supporto include la stored procedure `sp_execute_external_script`. Per istruzioni su come installare Machine Learning Services in Linux, vedere [Installare [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Machine Learning Services (R, Python, Java) in Linux](../linux/sql-server-linux-setup-machine-learning.md).

- **Nuovo Registro Container (CTP 2.1)**: tutte le immagini del contenitore per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e per [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] si trovano ora nel Registro Container Microsoft. Il Registro Container Microsoft è il registro contenitori ufficiale per la distribuzione di contenitori prodotto Microsoft. Ora vengono anche pubblicate le immagini certificate basate su RHEL.

  - Registro Container Microsoft: `mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - Immagini del contenitore certificate basate su RHEL: `mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

## <a id="mds"></a> Master Data Services 

- **Controlli Silverlight sostituiti con HTML (CTP 2.0)**: il portale Master Data Services (MDS) non è più dipendente da Silverlight. Tutti i componenti Silverlight precedenti sono stati sostituiti con controlli HTML.

## <a id="security"></a>Security

- **Gestione certificati in Gestione configurazione SQL Server (CTP 2.0)**: i certificati SSL/TLS sono usati in modo estensivo per proteggere l'accesso alle istanze di SQL Server. La gestione dei certificati è ora integrata in Gestione configurazione SQL Server e questo semplifica varie attività comuni, ad esempio:

  - Visualizzazione e convalida di certificati installati in un'istanza [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  - Visualizzazione di certificati prossimi alla scadenza.
  - Distribuzione di certificati tra computer appartenenti a gruppi di disponibilità AlwaysOn (dal nodo che contiene la replica primaria).
  - Distribuzione di certificati tra computer appartenenti a un'istanza del cluster di failover (dal nodo attivo).

  > [!NOTE]
  > L'utente deve avere autorizzazioni amministratore per tutti i nodi del cluster.

## <a id="tools"></a>Strumenti

- [**Azure Data Studio**](../azure-data-studio/what-is.md): rilasciato in precedenza con il nome di anteprima di SQL Operations Studio, Azure Data Studio è uno strumento desktop leggero, moderno, open source e multipiattaforma per le attività più comuni di sviluppo e amministrazione di dati. Con Azure Data Studio e l'[estensione di SQL Server 2019 Preview](../azure-data-studio/sql-server-2019-extension.md) è possibile connettersi a SQL Server in locale e nel cloud in Windows, macOS e Linux. Con Azure Data Studio è possibile:

  - È ora incluso il supporto per AAD. (CTP 2.3)
  - L'interfaccia utente di visualizzazione di Notebooks è stata spostata nella memoria centrale di Azure Data Studio. (CTP 2.3)
  - Aggiunta una nuova procedura guidata per creare origini dati esterne da HDFS a cluster Big Data di SQL Server 2019. (CTP 2.3)
  - Interfaccia utente di visualizzazione di Notebooks. (CTP 2.3)
  - Aggiunte nuove API Notebooks. (CTP 2.3)
  - Aggiunto il comando "Reinstall Notebook dependencies" (Reinstalla dipendenze Notebooks) per assistenza durante gli aggiornamenti dei pacchetti Python. (CTP 2.3)
  - Connettersi e gestire i cluster Big Data di SQL Server 2019. (CTP 2.1)
  - Modificare ed eseguire query in un ambiente di sviluppo moderno, con esecuzione rapida di Intellisense, frammenti di codice e integrazione del controllo codice sorgente. (CTP 2.0) 
  - Visualizzare rapidamente i dati con la funzionalità predefinita di creazione grafici dai set di risultati. (CTP 2.0)
  - Creare dashboard personalizzati per i server e i database mediante widget personalizzabili. (CTP 2.0)  
  - Gestire facilmente l'ambiente nel suo complesso, grazie al terminale incorporato. (CTP 2.0)
  - Analizzare i dati con un'esperienza di tipo notebook integrata basata su Jupyter. (CTP 2.0)
  - Migliorare l'esperienza con estensioni e temi personalizzati. (CTP 2.0)
  - Esplorare le risorse di Azure con un browser incorporato degli abbonamenti e delle risorse. (CTP 2.0)
  - Supporta gli scenari che usano il cluster Big Data di SQL Server. (CTP 2.0)
  
  > [!TIP]
  > Per i miglioramenti più recenti ad Azure Data Studio, vedere le [Note sulla versione per Azure Data Studio](../azure-data-studio/release-notes.md).

- [**SQL Server Management Studio (SSMS) 18.0 (anteprima)**](../ssms/sql-server-management-studio-ssms.md): Supporta [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

  - Avvio di Azure Data Studio da SSMS. (CTP 2.3)
  - Supporto di Always Encrypted con enclave sicuri. (CTP 2.0)
  - File di download di dimensioni più piccole. (CTP 2.0)
  - Ora basato su Visual Studio 2017 Isolated Shell. (CTP 2.0)
  - Per l'elenco completo, vedere il [log delle modifiche SSMS](../ssms/sql-server-management-studio-changelog-ssms.md). (CTP 2.0)

- [**Modulo SQL Server PowerShell**](https://www.powershellgallery.com/packages/SqlServer/21.1.18080): Il modulo SQL Server PowerShell consente agli sviluppatori e amministratori di SQL Server, nonché ai professionisti di Business Intelligence di automatizzare la distribuzione del database e l'amministrazione del server.

  - Aggiornamento da 21.0 a 21.1 per supportare SMO v150.
  - Aggiornato il provider di SQL Server (SQLRegistration) per visualizzare i gruppi AS/IS/RS.
  - Corretto il problema nel cmdlet `New-SqlAvailabilityGroup` quando la destinazione è SQL Server 2014.
  - Aggiunto il parametro `–LoadBalancedReadOnlyRoutingList` a `Set-SqlAvailabilityReplica` e `New-SqlAvailabilityReplica`.
  - Aggiornato il cmdlet `AnalysisService` per usare l'accesso memorizzato nella cache di `Login-AzureAsAccount` per Azure Analysis Services.

## <a id="ssas"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS) 

### <a name="calculation-groups-in-tabular-models-ctp-23"></a>Gruppi di calcolo in modelli tabulari (CTP 2.3) 

I gruppi di calcolo consentono di risolvere un problema comune nei modelli complessi in cui si può assistere a una proliferazione di misure con gli stessi calcoli, ad esempio la funzionalità di Business Intelligence per le gerarchie temporali. I gruppi di calcolo vengono visualizzati nei client di creazione report sotto forma di tabella con una singola colonna. Ogni valore nella colonna rappresenta un calcolo riutilizzabile o un elemento di calcolo che può essere applicato a qualsiasi misura.  

Un gruppo di calcolo può avere qualsiasi numero di elementi di calcolo. Ogni elemento di calcolo è definito da un'espressione DAX. Sono state introdotte tre nuove funzioni DAX per poter usare i gruppi di calcolo: 

- `SELECTEDMEASURE()`: restituisce un riferimento alla misura attualmente nel contesto.  

- `SELECTEDMEASURENAME()`: restituisce una stringa contenente il nome della misura attualmente nel contesto.  

- `ISSELECTEDMEASURE(M1, M2, …)`: restituisce un valore booleano che indica se la misura attualmente nel contesto è una di quelle specificate come argomento.

Oltre alle nuove funzioni DAX, vengono introdotte due nuove DMV:

- `TMSCHEMA_CALCULATION_GROUPS`  
- `TMSCHEMA_CALCULATION_ITEMS`  

Per questa versione, i gruppi di calcolo presentano alcune limitazioni:

- La funzione `ALLSELECTED DAX` non è ancora supportata.
- La funzionalità Sicurezza a livello di riga definita nella tabella del gruppo di calcolo non è ancora supportata.
- La funzionalità Sicurezza a livello di oggetto definita nella tabella del gruppo di calcolo non è ancora supportata.
- Le espressioni DetailsRows che fanno riferimento agli elementi di calcolo non sono ancora supportate.
- La dimensione MDX non è ancora supportata.

I gruppi di calcolo richiedono modelli con livello di compatibilità 1470 che è attualmente supportato solo in SQL Server 2019 CTP 2.3 e versioni successive. Attualmente è possibile creare gruppi di calcolo tramite l'API del Modello a oggetti tabulare, TMSL (Tabular Model Scripting Language) e l'editor di modelli tabulari open source. Il supporto in SQL Server Data Tools verrà incluso in una versione futura. Seguirà documentazione. Informazioni aggiuntive per questa e altre funzionalità CTP rilasciate saranno disponibili nel blog di Analysis Services.

## <a name="other-services"></a>Altri servizi

In CTP 2.3 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] non introduce nuove funzionalità per i servizi seguenti:

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="next-steps"></a>Passaggi successivi

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Note sulla versione](sql-server-ver15-release-notes.md)

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: white paper tecnico](https://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Pubblicato in settembre 2018. Si applica a Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 per Windows, Linux e i contenitori Docker.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
