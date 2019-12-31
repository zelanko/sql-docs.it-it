---
title: Novità di SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 23a1392256e103fa1bc112f11b5c5b97f5c398f1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75237709"
---
# <a name="whats-new-in-sql-server-2014"></a>Novità di SQL Server 2014

In questo argomento vengono riepilogati i collegamenti dettagliati [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] alle nuove funzionalità di e vengono riepilogati i Service Pack per[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Prova:** ![la macchina virtuale di Azure Small](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) ha un account Azure?  Passare a https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2 per avviare una macchina virtuale con SQL Server 2014 Service Pack 1 (SP1) già installato.

> [!TIP]
> [Fare clic qui](../2014-toc/index.yml) per la pagina della documentazione home di SQL Server 2014.

<!--
Do not let this file's filename fool you.
This filename contains "2016", but nevertheless...
This file, at this exact GitHub path, is dedicated to SQL Server version 2014.
-->

## <a name="whats-new-articles"></a>Articoli sulle novità

-   [Novità &#40;motore di database&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Novità di Analysis Services e Business Intelligence](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [Novità nell'installazione di SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]in non sono state introdotte nuove funzionalità significative per le seguenti funzionalità:**  
  
-   [Novità &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [Novità &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) non introduce nuove funzionalità significative.
-  [Informazioni sulla versione di SQL Server 2014 Service Pack 1](https://support.microsoft.com/kb/3058865).
-  [Scaricare il Service Pack 1 per Microsoft SQL Server 2014 scaricare il Service Pack 1 per Microsoft SQL Server 2014. ![](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=46694) [](https://www.microsoft.com/download/details.aspx?id=46694)


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [Informazioni sulla versione di SQL Server 2014 Service Pack 2](https://support.microsoft.com/kb/3171021).
-  [Scaricare il Service Pack 2 per Microsoft SQL Server 2014 scaricare il Service Pack 2 per Microsoft SQL Server 2014. ![](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [](https://go.microsoft.com/fwlink/?LinkID=821558)
-  [Scaricare SQL Server il Feature Pack di 2014 SP2 scaricare il Feature Pack di SQL Server 2014 SP2. ![](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=53164) [](https://www.microsoft.com/download/details.aspx?id=53164)

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 In sono inclusi i miglioramenti seguenti:

### <a name="performance-and-scalability-improvements"></a>Miglioramenti delle prestazioni e della scalabilità 
-   **Partizionamento soft-NUMA automatico:** Con [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, la funzionalità Soft NUMA automatica viene abilitata quando il flag di traccia 8079 è acceso durante l'avvio dell'istanza. Quando il flag di traccia 8079 è abilitato durante [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] l'avvio, SP2 interroga il layout hardware e configura automaticamente soft-NUMA sui sistemi che segnalano 8 o più CPU per ogni nodo NUMA. Il comportamento NUMA automatico e soft è compatibile con l'Hyper-thread (HT/processore logico). Il partizionamento e la creazione di nodi aggiuntivi ridimensionano l'elaborazione in background aumentando il numero di listener tramite scalabilità e le funzionalità di crittografia e di rete. È consigliabile testare prima di tutto il carico di lavoro delle prestazioni con NUMA Soft automatico, prima di ottimizzarlo nell'ambiente di produzione. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Memoria dinamica ridimensionamento** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] degli oggetti: SP2 partiziona dinamicamente gli oggetti di memoria in base al numero di nodi e Core per la scalabilità su hardware moderno. L'obiettivo della promozione dinamica è quello di partizionare automaticamente un oggetto memoria thread-safe (CMEMTHREAD) se diventa un collo di bottiglia. Gli oggetti di memoria non partizionati possono essere partizionati in modo dinamico in base al nodo (il numero di partizioni è uguale al numero di nodi NUMA). Gli oggetti memoria partizionati per nodo possono essere ulteriormente partizionati in base alla CPU (il numero di partizioni è uguale al numero di CPU). [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Hint MAXDOP per i comandi\* DBCC check:** questo miglioramento risolve il [feedback di Connect (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). È ora possibile eseguire DBCC CHECKDB con un'impostazione MAXDOP diversa da sp_configure valore. Se MAXDOP supera il valore configurato con Resource Governor, il motore di database usa il valore MAXDOP di Resource Governor descritto in ALTER WORKLOAD GROUP (Transact-SQL). Quando si utilizza l'hint per la query MAXDOP sono valide tutte le regole semantiche utilizzate con l'opzione di configurazione max degree of parallelism. Per ulteriori informazioni, vedere [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Abilita >8 TB per il pool di buffer:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 Abilita 128 TB di spazio degli indirizzi virtuali per l'utilizzo del pool di buffer. Questo miglioramento consente la scalabilità di SQL Server pool di buffer oltre 8 TB nell'hardware moderno.
-   **Miglioramento di SOS_RWLock spinlock:** Il SOS_RWLock è una primitiva di sincronizzazione utilizzata in varie posizioni nell'intero SQL Server codebase.  Come suggerisce il nome, il codice può avere più proprietà condivise (Readers) o Single (writer). Questo miglioramento Elimina la necessità di SpinLock per SOS_RWLock e usa invece tecniche senza blocchi simili a OLTP in memoria. Con questa modifica, molti thread possono leggere una struttura di dati protetta da SOS_RWLock in parallelo, senza bloccarsi a vicenda. Questa parallelizzazione garantisce una maggiore scalabilità. Prima di questa modifica, l'implementazione di SpinLock consentiva a un solo thread di acquisire la SOS_RWLock alla volta, anche per la lettura di una struttura di dati. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementazione nativa spaziale:** Un miglioramento significativo delle prestazioni delle query spaziali è [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] stato introdotto in SP2 tramite l'implementazione nativa. Per ulteriori informazioni, vedere l' [articolo della Knowledge base KB3107399](https://support.microsoft.com/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Miglioramenti al supporto e alla diagnostica
-   **Clonazione del database:** Clone database è un nuovo comando DBCC che migliora la risoluzione dei problemi relativi ai database di produzione esistenti clonando lo schema e i metadati senza i dati. Il clone viene creato con il comando `DBCC clonedatabase('source_database_name', 'clone_database_name')`.  **Nota:** I database clonati non devono essere utilizzati in ambienti di produzione. Usare il comando seguente per determinare se un database è stato generato da un database clonato `select DATABASEPROPERTYEX('clonedb', 'isClone')`:. Il valore restituito **1** indica che il database è stato creato da clonedatabase, mentre **0** indica che non si tratta di un clone.
-   **Supporto di tempdb:**  Un nuovo messaggio del log degli errori che indica all'avvio sia il numero di file tempdb sia la dimensione e l'aumento automatico dei file di dati tempdb.
-   **Registrazione inizializzazione file immediata database:** Un nuovo messaggio del log degli errori che indica l'avvio del server, lo stato dell'inizializzazione immediata dei file di database (abilitato/disabilitato).
-   **Nomi dei moduli in stack:** L'evento esteso (XEvent) stack include ora i nomi dei moduli più l'offset, anziché gli indirizzi assoluti.
-   **Nuova DMF per statistiche incrementali:** Questo miglioramento risolve il [feedback di Connect (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) per abilitare il rilevamento delle statistiche incrementali a livello di partizione. Viene introdotta una nuova DMF sys. dm_db_incremental_stats_properties per esporre le informazioni per partizione per le statistiche incrementali.
-   **Comportamento della DMV di utilizzo dell'indice aggiornato:** Questo miglioramento risolve il [feedback di Connect (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) dai clienti in cui la ricompilazione di un indice *non* eliminerà alcuna voce di riga esistente da sys. dm_db_index_usage_stats per tale indice. Il comportamento ora sarà identico a quello di SQL 2008 e SQL Server 2016. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Correlazione migliorata tra la diagnostica XE e DMV:** Questo miglioramento risolve il [feedback di Connect (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). `Query_hash`e `query_plan_hash` vengono utilizzati per l'identificazione univoca di una query. Nelle DMV sono definiti come varbinary (8), mentre in XEvent come UINT64. Poiché SQL Server non dispone di "bigint senza segno", il cast non sempre funziona. Questo miglioramento introduce nuove colonne di azione e filtro XEvent. Le colonne sono equivalenti `query_hash` a `query_plan_hash`e, ad eccezione del fatto che sono definite come Int64. La definizione INT64 consente di correlare le query tra XE e DMV.
-   **Supporto per UTF-8 in BULK INSERT e bcp:** Questo miglioramento risolve il [feedback di Connect (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001). BULK INSERT e BCP ora possono esportare o importare dati codificati nel set di caratteri UTF-8.
-   **Profilatura leggera dell'esecuzione di query per operatore:** Showplan fornisce informazioni sul costo di ogni operatore del piano. Tuttavia, le statistiche di runtime effettive sono limitate per operazioni quali CPU, letture di I/O e tempo trascorso per thread. SQL Server 2014 SP2 introduce queste statistiche di runtime aggiuntive per operatore nello Showplan. R2 introduce anche un XEvent denominato `query_thread_profile` per facilitare la risoluzione dei problemi relativi alle prestazioni delle query. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Pulizia rilevamento modifiche:** Viene introdotta `sp_flush_CT_internal_table_on_demand` una nuova stored procedure per pulire le tabelle interne di rilevamento delle modifiche su richiesta.
-   **Registrazione timeout lease AlwaysOn** Aggiunta di una nuova funzionalità di registrazione per i messaggi di timeout dei lease in modo da registrare l'ora corrente e i tempi di rinnovo previsti. Inoltre, nel log degli errori SQL è stato introdotto un nuovo messaggio relativo ai timeout. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Nuova DMF per il recupero del buffer di input nei SQL Server:** È ora disponibile una nuova DMF per il recupero del buffer di input per una sessione/richiesta (sys. dm_exec_input_buffer). Questa DMF è funzionalmente equivalente a DBCC INPUTBUFFER. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigazione per la concessione di memoria sottovalutata e sovrastima:** Aggiunta di nuovi hint per la query per Resource Governor tramite MIN_GRANT_PERCENT e MAX_GRANT_PERCENT. Questa nuova query consente di sfruttare questi suggerimenti durante l'esecuzione delle query, limitando le concessioni di memoria per impedire la contesa di memoria. Per ulteriori informazioni, vedere l' [articolo della Knowledge base KB310740](https://support.microsoft.com/kb/3107401).
-   **Migliore concessione di memoria e diagnostica di utilizzo:** Un nuovo evento esteso denominato `query_memory_grant_usage` è stato aggiunto all'elenco delle funzionalità di traccia in SQL Server. Questo evento tiene traccia delle concessioni di memoria richieste e concesse. Questo evento fornisce funzionalità di analisi e analisi migliori per la risoluzione di eventuali problemi di esecuzione delle query correlati alle concessioni di memoria. Per ulteriori informazioni, vedere l' [articolo della Knowledge base KB3107173](https://support.microsoft.com/kb/3107173).
-   **Diagnostica di esecuzione delle query per la distribuzione di tempdb:** gli avvisi hash e di ordinamento ora includono colonne aggiuntive per tenere traccia delle statistiche di I/O fisiche, della memoria utilizzata e delle righe interessate. È stato anche introdotto un nuovo hash_spill_details evento esteso. È ora possibile tenere traccia di informazioni più granulari per gli avvisi di hash e ordinamento ([KB3107172](https://support.microsoft.com/kb/3107172)). Questo miglioramento è ora esposto anche tramite i piani di XML Query sotto forma di un nuovo attributo al tipo complesso SpillToTempDbType ([KB3107400](https://support.microsoft.com/kb/3107400)). Set Statistics `ON` Now Mostra ordinare le statistiche di tabella di lavoro.
-   **Diagnostica migliorata per i piani di esecuzione delle query che coinvolgono il predicato residuo distribuzione:** Le righe effettive lette vengono ora segnalate nei piani di esecuzione delle query, per migliorare la risoluzione dei problemi relativi alle prestazioni delle query. Queste righe negano la necessità di acquisire separatamente SET STATISTICs IO. Queste righe consentono inoltre di visualizzare le informazioni correlate a un predicato residuo in un piano di query. Per ulteriori informazioni, vedere l' [articolo della Knowledge base KB3107397](https://support.microsoft.com/kb/3107397).


## <a name="additional-information"></a>Informazioni aggiuntive  
 [Risorse di SQL Server 2014](../2014-toc/index.yml)  
  
 [Note sulla versione di SQL Server 2014](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Centro risorse di SQL Server 2014](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Sito Web SQLCat](https://go.microsoft.com/fwlink/p/?linkID=220963)  
