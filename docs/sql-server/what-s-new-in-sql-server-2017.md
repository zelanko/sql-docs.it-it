---
title: Novità di SQL Server 2017 | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 8c2950e677537ee6a6bc35d930e124f285bc24df
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69494305"
---
# <a name="whats-new-in-sql-server-2017"></a>Novità di SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]
SQL Server 2017 rappresenta un importante passo avanti verso una piattaforma che offre opzioni di linguaggi di sviluppo, tipi di dati, memorizzazione in locale e nel cloud e sistemi operativi rendendo disponibili le funzionalità di SQL Server in Linux, nei contenitori Docker basati su Linux e in Windows. Questo argomento offre un riepilogo delle novità delle aree di funzionalità specifiche e include collegamenti ad altre informazioni. Per altre informazioni correlate a SQL Server in Linux, vedere [Documentazione di SQL Server in Linux](https://docs.microsoft.com/sql/linux/).

[![Download da Evaluation Center](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=829477) **Prova:** [Scaricare SQL Server 2017, ottobre 2017](https://go.microsoft.com/fwlink/?LinkID=829477).

> [!NOTE]
> Con la disponibilità generale, vengono rilasciati a intervalli regolari aggiornamenti cumulativi che mettono a disposizione numerosi miglioramenti e diverse correzioni. Per informazioni sul rilascio dell'aggiornamento cumulativo più recente, vedere [Aggiornamenti cumulativi di SQL Server 2017](https://aka.ms/sql2017cu).

## <a name="sql-server-2017-database-engine"></a>Motore di database di SQL Server 2017

SQL Server 2017 include numerose nuove funzionalità del motore di database, miglioramenti e aumenti delle prestazioni. 
- Gli **assembly CLR** possono ora essere aggiunti a un elenco elementi consentiti come soluzione alternativa per la funzionalità `clr strict security` descritta in CTP 2.0. [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md), [sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) e [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) sono stati aggiunti per supportare l'elenco elementi consentiti di assembly attendibili (RC1).  
- La **ricompilazione dell'indice online ripristinabile** consente di ripristinare un'operazione di ricompilazione dell'indice online dal punto in cui è stata arrestata a causa di un errore, ad esempio un failover in una replica o lo spazio su disco insufficiente, o di sospendere e successivamente ripristinare l'operazione. Vedere [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) e [Linee guida per le operazioni sugli indici online](../relational-databases/indexes/guidelines-for-online-index-operations.md). (CTP 2.0)
- L'opzione **IDENTITY_CACHE** per ALTER DATABASE SCOPED CONFIGURATION consente di evitare gap nei valori delle colonne Identity nel caso in cui un server viene riavviato in modo imprevisto o esegue un failover in un server secondario. Vedere [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). (CTP 2.0)
- Una nuova generazione di miglioramenti di elaborazione delle query che adatterà le strategie di ottimizzazione alle condizioni di runtime del carico di lavoro dell'applicazione. Per questa prima versione della famiglia di funzionalità di **elaborazione di query adattive**, sono disponibili tre nuovi miglioramenti: **join adattivi in modalità batch**, **feedback delle concessioni di memoria in modalità batch** ed **esecuzione interleaved** per le funzioni con valori di tabella a istruzioni multiple.  Vedere [Elaborazione di query intelligenti nei database SQL](../relational-databases/performance/intelligent-query-processing.md).
- L'**ottimizzazione di database automatica** offre informazioni su potenziali problemi di prestazioni delle query, suggerisce soluzioni e consente di correggere automaticamente i problemi rilevati. Vedere [Automatic tuning](../relational-databases/automatic-tuning/automatic-tuning.md) (Ottimizzazione automatica). (CTP 2.0)
- Le nuove **funzionalità dei database dei grafici** per la modellazione delle relazioni molti-a-molti includono la nuova sintassi [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) per la creazione di tabelle dei nodi e tabelle edge e la parola chiave [MATCH](../t-sql/queries/match-sql-graph.md) per le query. Vedere [Graph Processing with SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md) (Elaborazione di grafici con SQL Server 2017). (CTP 2.0)
- Un'opzione sp_configure denominata `clr strict security` è abilitata per impostazione predefinita per migliorare la sicurezza degli assembly CLR. Vedere [CLR strict security](../database-engine/configure-windows/clr-strict-security.md). (CTP 2.0)
- Il programma di installazione consente ora di specificare una dimensione del file tempdb iniziale massima di **256 GB** (262,144 MB) per singolo file con un avviso se viene impostata una dimensione del file maggiore di 1 GB con l'inizializzazione immediata dei file non abilitata. (CTP 2.0)
- La colonna **modified_extent_page_count** in [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) tiene traccia delle modifiche differenziali in ogni file di database abilitando soluzioni di backup intelligente che eseguono un backup differenziale o un backup completo in base alla percentuale di pagine modificate nel database. (CTP 2.0)
- La sintassi T-SQL [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) supporta ora il caricamento di una tabella in un filegroup diverso da quello predefinito dell'utente usando la parola chiave **ON**. (CTP 2.0)
- Le transazioni tra database sono ora supportate in tutti i database che appartengono a un **gruppo di disponibilità Always On**, inclusi i database che appartengono alla stessa istanza. Vedere [Transactions - Always On Availability Groups and Database Mirroring](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md) (Transazioni: gruppi di disponibilità Always On e mirroring del database) (CTP 2.0)
- La nuova funzionalità **Gruppi di disponibilità** include il supporto della scalabilità in lettura senza cluster, l'impostazione Minimum Replica Commit Availability Groups (Gruppi di disponibilità con commit di un numero minimo di repliche), le migrazioni tra sistemi operativi Windows e Linux e i test. (CTP 1.3)
- Nuove viste di gestione dinamiche:
    - [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) espone attributi a livello di riepilogo e informazioni sui file di log delle transazioni utili per il monitoraggio dello stato dei log delle transazioni. (CTP 2.1)
    - [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) tiene traccia dell'utilizzo dell'archivio versioni per ogni database e consente di pianificare in modo proattivo la dimensione del file tempdb in base all'utilizzo dell'archivio versioni di ogni singolo database. (CTP 2.0)
    - [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) espone le informazioni VLF per monitorare, segnalare ed evitare problemi potenziali dei log delle transazioni. (CTP 2.0)
    - [sys.dm_db_stats_histogram](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) è una nuova vista di gestione dinamica per l'esame delle statistiche. (CTP 1.3)
    - **sys.dm_os_host_info** offre informazioni sul sistema operativo per Windows e Linux. (CTP 1.0)
- L'**Ottimizzazione guidata motore di database (DTA)** include opzioni aggiuntive e prestazioni migliorate. (CTP 1.2)
- I **miglioramenti in memoria** includono il supporto per le colonne calcolate nelle tabelle ottimizzate per la memoria, il supporto completo delle funzioni JSON nei moduli compilati in modo nativo e l'operatore CROSS APPLY nei moduli compilati in modo nativo. (CTP 1.1)
- Le nuove **funzioni di stringa** sono CONCAT_WS, TRANSLATE e TRIM e WITHIN GROUP è ora supportata per la funzione STRING_AGG. (CTP 1.1)
- Sono disponibili nuove **opzioni di accesso in blocco** (BULK INSERT e OPENROWSET(BULK...) ) per i file con estensione csv e i file del BLOB di Azure. (CTP 1.1)
- I **miglioramenti degli oggetti ottimizzati per la memoria** includono sp_spaceused e l'eliminazione del limite di 8 indici per le tabelle ottimizzate per la memoria, sp_rename per le tabelle ottimizzate per la memoria e i moduli T-SQL compilati in modo nativo e CASE e TOP (N) WITH TIES per i moduli T-SQL compilati in modo nativo. I file di filegroup con ottimizzazione per la memoria possono ora essere archiviati ed è possibile eseguirne il backup e il ripristino nell'archiviazione di Azure. (CTP 1.0)
- **DATABASE SCOPED CREDENTIAL** è una nuova classe di autorizzazioni a protezione diretta che supportano CONTROL, ALTER, REFERENCES, TAKE OWNERSHIP e VIEW DEFINITION. ADMINISTER DATABASE BULK OPERATIONS è ora visibile in sys.fn_builtin_permissions. (CTP 1.0)
- È stata aggiunto il livello **COMPATIBILITY_LEVEL 140** del database. (CTP 1.0).  

Per altre informazioni, vedere [What's new in SQL Server 2017 Database Engine](~/database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md) (Novità del motore di database di SQL Server 2017).

## <a name="sql-server-2017-integration-services-ssis"></a>SQL Server 2017 Integration Services (SSIS)
- La nuova funzionalità **Scalabilità orizzontale** di SSIS include le seguenti funzionalità nuove e modificate. Per altre informazioni, vedere [What's New in Integration Services in SQL Server 2017](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md) (Novità di Integration Services in SQL Server 2017). (RC1)
    -   Il master di scalabilità orizzontale supporta ora la disponibilità elevata.
    -   La gestione del failover dei log di esecuzione dai ruoli di lavoro di scalabilità orizzontale è stata migliorata.
    -   Il parametro *runincluster* della stored procedure **[catalog].[create_execution]** è stato rinominato in *runinscaleout* per coerenza e leggibilità.
    -   Il catalogo SSIS include una nuova proprietà globale che consente di specificare la modalità predefinita per l'esecuzione dei pacchetti SSIS.
- Nella nuova funzionalità **Scalabilità orizzontale di SSIS** è ora possibile usare il parametro **Use32BitRuntime** quando si attiva l'esecuzione. (CTP 2.1)
- SQL Server 2017 Integration Services (SSIS) supporta ora **SQL Server in Linux** e un nuovo pacchetto consente di eseguire i pacchetti SSIS in Linux dalla riga di comando. Per altre informazioni, vedere il [post del blog che annuncia il supporto SSIS per Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). (CTP 2.1)
- La nuova funzionalità **Scalabilità orizzontale di SSIS** semplifica l'esecuzione di SSIS su più computer. Vedere [Scalabilità orizzontale di Integration Services (SSIS)](~/integration-services/scale-out/integration-services-ssis-scale-out.md). (CTP 1.0)
- L'origine OData e la gestione connessione OData supportano ora la connessione ai feed OData di Microsoft Dynamics AX Online e Microsoft Dynamics CRM Online. (CTP 1.0)

Per altre informazioni, vedere [What's New in Integration Services in SQL Server 2017](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md) (Novità di Integration Services in SQL Server 2017).

## <a name="sql-server-2017-master-data-services-mds"></a>SQL Server 2017 Master Data Services (MDS)
- L'esperienza e le prestazioni risultano migliori per l'aggiornamento da SQL Server 2012, SQL Server 2014 e SQL Server 2016 a SQL Server 2017 Master Data Services. 
- Ora è possibile visualizzare gli elenchi ordinati di entità, raccolte e gerarchie nella pagina **Explorer** dell'applicazione Web.
- Sono state migliorate le prestazioni per lo staging di milioni di record mediante la stored procedure di staging.
- Sono state migliorate le prestazioni quando si espande la cartella **Entità** nella pagina **Gestisci gruppi** per assegnare le autorizzazioni del modello. La pagina **Gestisci gruppi** si trova nella sezione **Sicurezza** dell'applicazione Web. Per altre informazioni sui miglioramenti per le prestazioni, vedere [https://support.microsoft.com/help/4023865?preview](https://support.microsoft.com/help/4023865?preview). Per altre informazioni sull'assegnazione di autorizzazioni, vedere [Assegnare autorizzazioni per oggetti modello (Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md).

## <a name="sql-server-2017-analysis-services-ssas"></a>SQL Server 2017 Analysis Services (SSAS) 
SQL Server Analysis Services 2017 include numerosi miglioramenti per i modelli tabulari. tra cui:
- Modalità tabulare come opzione di installazione predefinita per Analysis Services. (CTP 2.0)
- Sicurezza a livello di oggetto per la protezione dei metadati dei modelli tabulari. (CTP 2.0)
- Relazioni di date per creare facilmente relazioni basate sui campi data. (CTP 2.0)
- Supporto delle nuove origini dati **Get Data** (Power Query) e delle origini dati DirectQuery esistenti per query M. (CTP 2.0) 
- Editor DAX per SSDT. (CTP 2.0)
- Suggerimenti di codifica, una funzione avanzata per l'ottimizzazione dell'aggiornamento dei dati di modelli tabulari in memoria di grandi dimensioni. (CTP 1.3)
- Supporto del **livello di compatibilità 1400** per i modelli tabulari. Per creare nuovi progetti di modelli tabulari o aggiornare quelli esistenti con il livello di compatibilità 1400, scaricare e installare [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939). (CTP 1.1)
- Una nuova funzione **Recupera dati** per modelli tabulari al livello di compatibilità 1400. Vedere il [blog del team di Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-vnext-on-windows-ctp-1-1-for-analysis-services/). (CTP 1.1)
- Proprietà **Nascondi membri** per nascondere i membri vuoti nelle gerarchie incomplete. (CTP 1.1)
- Nuova azione dell'utente finale **Righe di dettaglio** in **Mostra dettagli** per informazioni aggregate. Funzioni [SELECTCOLUMNS](/dax/selectcolumns-function-dax) e **DETAILROWS** per la creazione di espressioni Righe di dettaglio. (CTP 1.1)
- Operatore **IN** DAX per la specifica di più valori. (CTP 1.1)

Per altre informazioni, vedere [Novità di SQL Server Analysis Services](/analysis-services/what-s-new-in-analysis-services).

## <a name="sql-server-2017-reporting-services-ssrs"></a>SQL Server 2017 Reporting Services (SSRS)
SQL Server Reporting Services non può più essere installato tramite l'installazione di SQL Server. Accedere all'Area download Microsoft per [scaricare Microsoft SQL Server 2017 Reporting Services](https://www.microsoft.com/download/details.aspx?id=55252). 
- I commenti sono ora disponibili per i report per una maggior prospettiva e collaborazione con altri utenti. È anche possibile includere allegati nei commenti.
- Nelle versioni più recenti di Generatore Report e SQL Server Data Tools è possibile creare query DAX native nei modelli di dati tabulari di SQL Server Analysis Services supportati trascinando i campi desiderati nelle finestre di progettazione delle query. Vedere il [blog di Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/).
- Per consentire lo sviluppo di applicazioni e personalizzazioni moderne, SSRS ora supporta completamente un'API RESTful conforme a OpenAPI. La documentazione e le specifiche complete dell'API sono ora disponibili in [swaggerhub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0).

Per altre informazioni, vedere [Novità di SQL Server Reporting Services (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

## <a name="machine-learning-in-sql-server-2017"></a>Machine Learning in SQL Server 2017 

SQL Server R Services è stato rinominato **SQL Server Machine Learning Services** per indicare il supporto per Python in aggiunta al linguaggio R. È possibile usare Machine Learning Services (In-Database) per eseguire script R o Python in SQL Server o installare **Microsoft Machine Learning Server (Standalone)** per distribuire e usare modelli R e Python che non richiedono SQL Server. 

Gli sviluppatori di SQL Server ora hanno accesso alle ampie librerie Python di Machine Learning e intelligenza artificiale, disponibili nell'ecosistema open source insieme alle innovazioni più recenti di Microsoft:

- **revoscalepy**: questa versione Python equivalente di RevoScaleR include algoritmi paralleli per la regressione lineare e logistica, albero delle decisioni, alberi con boosting e foreste casuali, nonché una vasta gamma di API per la trasformazione e lo spostamento dei dati, contesti di calcolo remoti e origini dati.
- **microsoftml**: questo pacchetto all'avanguardia di algoritmi di apprendimento automatico e trasformazioni con associazioni Python include reti neurali profonde, alberi delle decisioni e foreste delle decisioni veloci e algoritmi ottimizzati per la regressione lineare e logistica. Vengono anche modelli già sottoposti a training basati su modelli ResNet che è possibile usare per l'estrazione di immagini o l'analisi del sentiment.
- **Messa in funzione di Python con T-SQL**: è possibile distribuire facilmente il codice Python con la stored procedure `sp_execute_external_script`. Il flusso dei dati dai processi SQL ai processi Python e la parallelizzazione dei segnali MPI permettono di ottenere prestazioni ottimali.
- **Python in contesti di calcolo di SQL Server**: data scientist e sviluppatori possono eseguire il codice Python in remoto dai relativi ambienti di sviluppo per esplorare i dati e sviluppare modelli senza dover spostare i dati.
- **Punteggio nativo**: è possibile usare la funzione PREDICT in Transact-SQL per eseguire l'assegnazione dei punteggi in qualsiasi istanza di SQL Server 2017, anche se non è installato R. Tutto ciò che serve è l'esecuzione del training del modello tramite uno degli algoritmi supportati RevoScaleR e revoscalepy e il successivo salvataggio del modello in un nuovo formato binario compatto.
- **Gestione dei pacchetti**: T-SQL supporta ora l'istruzione CREATE EXTERNAL LIBRARY per offrire agli amministratori di database maggiori capacità di gestione per i pacchetti R. Usare i ruoli per controllare l'accesso ai pacchetti privati o condivisi, archiviare pacchetti R nel database e condividerli tra gli utenti.
- **Miglioramenti delle prestazioni**: la stored procedure `sp_execute_external_script` è stata ottimizzata per supportare l'esecuzione in modalità batch per i dati columnstore.


Per altre informazioni, vedere [What's new in SQL Server Machine Learning Services](~/advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md) (Novità di SQL Server Machine Learning Services).

## <a name="next-steps"></a>Passaggi successivi
- Vedere [Note sulla versione di SQL Server 2017](sql-server-2017-release-notes.md).
- Vedere [Novità di SQL Server 2017 su Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new).
- Vedere [Novità di SQL Server 2016](what-s-new-in-sql-server-2016.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
