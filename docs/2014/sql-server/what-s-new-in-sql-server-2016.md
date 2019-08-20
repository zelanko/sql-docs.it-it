---
title: '&#39;Novità di SQL Server 2014 | Microsoft Docs'
ms.custom: ''
ms.date: 05/25/2017
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
ms.openlocfilehash: f368da503c90595624f476344724719206cdb77c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893703"
---
# <a name="what39s-new-in-sql-server-2014"></a>&#39;Novità di SQL Server 2014
  In questo argomento vengono riepilogati i collegamenti dettagliati [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] alle nuove funzionalità di e vengono riepilogati i Service Pack per[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Per provarlo:** ![La macchina virtuale di](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) Azure Small ha un account Azure?  Fare clic **[qui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** per creare rapidamente una macchina virtuale con SQL Server 2014 Service Pack 1 (SP1) già installato. 
  
-   [Novità &#40;motore di database&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Novità di Analysis Services e Business Intelligence](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [Novità relative all'installazione di SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]in non sono state introdotte nuove funzionalità significative per le seguenti:**  
  
-   [Novità &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [Novità &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) non introduce nuove funzionalità significative.
-  [Informazioni sulla versione di SQL Server 2014 Service Pack 1](https://support.microsoft.com/en-us/kb/3058865).
-  [![Scaricare il Service Pack 1 per Microsoft? SQL Server? ](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) 2014[scaricare il Service Pack 1 per Microsoft? SQL Server? 2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694).


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [Informazioni sulla versione di SQL Server 2014 Service Pack 2](https://support.microsoft.com/en-us/kb/3171021).
-  [![Scaricare il Service Pack 2 per Microsoft? SQL Server? ](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) 2014[scaricare il Service Pack 2 per Microsoft? SQL Server? 2014](https://go.microsoft.com/fwlink/?LinkID=821558).
-  [![Scaricare SQL Server 2014 SP2 Feature Pack](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [Scaricare SQL Server 2014 SP2 Feature Pack](https://www.microsoft.com/en-us/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 In sono inclusi i miglioramenti seguenti:

### <a name="performance-and-scalability-improvements"></a>Miglioramenti delle prestazioni e della scalabilità 
-   **Partizionamento soft-NUMA automatico:** Con [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, la funzionalità Soft NUMA automatica viene abilitata quando il flag di traccia 8079 è acceso durante l'avvio dell'istanza. Quando il flag di traccia 8079 è abilitato durante [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] l'avvio, SP2 interroga il layout hardware e configura automaticamente soft-NUMA sui sistemi che segnalano 8 o più CPU per ogni nodo NUMA. Il comportamento NUMA automatico e soft è compatibile con l'Hyper-thread (HT/processore logico). Il partizionamento e la creazione di nodi aggiuntivi ridimensionano l'elaborazione in background aumentando il numero di listener tramite scalabilità e le funzionalità di crittografia e di rete. È consigliabile testare prima il carico di lavoro delle prestazioni con NUMA automatico prima di attivarlo nell'ambiente di produzione. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Ridimensionamento di oggetti memoria dinamica:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 consente di partizionare dinamicamente gli oggetti di memoria in base al numero di nodi e Core per la scalabilità su hardware moderno. L'obiettivo della promozione dinamica è quello di partizionare automaticamente un oggetto memoria thread-safe (CMEMTHREAD) se diventa un collo di bottiglia. Gli oggetti di memoria non partizionati possono essere promossi dinamicamente per essere partizionati in base al nodo (il numero di partizioni è uguale al numero di nodi NUMA) e gli oggetti memoria partizionati in base al nodo possono essere ulteriormente promossi per essere partizionati in base alla CPU (il numero di partizioni è uguale al numero di CPU). [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Hint MAXDOP per i comandi\* DBCC check:** Questo miglioramento risolve il [feedback di Connect (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). È ora possibile eseguire DBCC CHECKDB con un'impostazione MAXDOP diversa dal valore sp_configure. Se MAXDOP supera il valore configurato con Resource Governor, il motore di database usa il valore MAXDOP di Resource Governor descritto in ALTER WORKLOAD GROUP (Transact-SQL). Quando si utilizza l'hint per la query MAXDOP sono valide tutte le regole semantiche utilizzate con l'opzione di configurazione max degree of parallelism. Per ulteriori informazioni, vedere [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Abilitare > 8 TB per il pool di buffer:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 Abilita 128TB di spazio degli indirizzi virtuali per l'utilizzo del pool di buffer. Questo miglioramento consente la scalabilità di SQL Server pool di buffer oltre 8 TB nell'hardware moderno.
-   **Miglioramento di SOS_RWLock spinlock:** SOS_RWLock è una primitiva di sincronizzazione utilizzata in varie posizioni nell'intero SQL Server Code codebase.  Come suggerisce il nome, il codice può avere più proprietà condivise (Readers) o Single (writer). Questo miglioramento Elimina la necessità di SpinLock per SOS_RWLock e usa invece tecniche senza blocchi simili a OLTP in memoria. Con questa modifica, molti thread possono leggere una struttura di dati protetta da SOS_RWLock in parallelo senza bloccarsi reciprocamente e garantendo così una maggiore scalabilità. Prima di questa modifica, l'implementazione di SpinLock consentiva a un solo thread di acquisire SOS_RWLock alla volta, anche per la lettura di una struttura di dati.  [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementazione nativa spaziale:** Un miglioramento significativo delle prestazioni delle query spaziali è [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] stato introdotto in SP2 tramite l'implementazione nativa. Per ulteriori informazioni, vedere l' [articolo della Knowledge base KB3107399](https://support.microsoft.com/en-us/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Miglioramenti al supporto e alla diagnostica
-   **Clonazione del database:** Clone database è un nuovo comando DBCC che migliora la risoluzione dei problemi relativi ai database di produzione esistenti clonando lo schema e i metadati senza i dati. Il clone viene creato con il comando `DBCC clonedatabase('source_database_name', 'clone_database_name')`.  **Nota:** È consigliabile non usare i database clonati in ambienti di produzione. Usare il comando seguente per determinare se un database è stato generato da un database clonato `select DATABASEPROPERTYEX('clonedb', 'isClone')`:. Il valore restituito **1** indica che il database è stato creato da clonedatabase, mentre **0** indica che non si tratta di un clone.
-   **Supporto di tempdb:**  Nuovo messaggio del log degli errori che indica il numero di file tempdb e la crescita automatica e delle dimensioni dei file di dati tempdb presenti all'avvio del server.
-   **Registrazione inizializzazione file immediata database:** Nuovo messaggio del log degli errori che indica sul server statup, lo stato dell'inizializzazione immediata dei file di database (abilitato/disabilitato).
-   **Nomi dei moduli in stack:** Il stack XEvent include ora i nomi dei moduli + offset invece degli indirizzi assoluti.
-   **Nuova DMF per statistiche incrementali:** Questo miglioramento risolve il [feedback di Connect (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) per abilitare il rilevamento delle statistiche incrementali a livello di partizione. Viene introdotta una nuova DMF sys. dm _db_incremental_stats_properties per esporre le informazioni per partizione per le statistiche incrementali.
-   **Comportamento della DMV di utilizzo dell'indice aggiornato:** Questo miglioramento risolve il [feedback di Connect (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) dai clienti in cui la ricompilazione di un indice *non* eliminerà alcuna voce di riga esistente da sys. dm _db_index_usage_stats per tale indice. Il comportamento ora sarà identico a quello di SQL 2008 e SQL Server 2016. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Correlazione migliorata tra la diagnostica XE e DMV:** Questo miglioramento risolve il [feedback di Connect (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). Query_hash e query_plan_hash vengono utilizzati per l'identificazione univoca di una query. Nelle DMV sono definiti come varbinary (8), mentre in XEvent come UINT64. Poiché in SQL Server non è presente un "bigint unifirmato", il cast non sempre funziona. Questo miglioramento introduce nuove colonne azione/filtro di XEvent equivalenti ai campi query_hash e query_plan_hash ad eccezione del fatto che tali valori sono definiti come INT64. In questo modo è possibile correlare le query tra XEvent e le viste a gestione dinamica.
-   **Supporto per UTF-8 in BULK INSERT e BCP:** Questo miglioramento risolve il [feedback di Connect (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) , in cui il supporto per l'esportazione e l'importazione di dati codificati in set di caratteri UTF-8 è ora abilitato in BULK INSERT e bcp.
-   **Profilatura dell'esecuzione di query per operatore Lightweight:** Durante la risoluzione dei problemi relativi alle prestazioni delle query, sebbene Showplan fornisca numerose informazioni sul piano di esecuzione della query e sul costo dell'operatore nel piano, ma contiene informazioni limitate sulle statistiche di runtime effettive, ad esempio (CPU, letture di I/O, tempo trascorso per thread). SQL 2014 SP2 introduce queste statistiche di runtime aggiuntive per operatore nello Showplan e un XEvent (query_thread_profile) per facilitare la risoluzione dei problemi relativi alle prestazioni delle query. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Pulizia Rilevamento modifiche:** Viene introdotta `sp_flush_CT_internal_table_on_demand` una nuova stored procedure per pulire le tabelle interne di rilevamento modifiche su richiesta.
-   **Registrazione timeout lease AlwaysOn** Aggiunta di una nuova funzionalità di registrazione per i messaggi di timeout dei lease in modo da registrare l'ora corrente e i tempi di rinnovo previsti. È stato inoltre introdotto un nuovo messaggio nel log degli errori SQL relativo ai timeout. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Nuova DMF per il recupero del buffer di input nei SQL Server:** Disponibile una nuova DMF per il recupero del buffer di input per una sessione o una richiesta (sys.dm_exec_input_buffer). Dal punto di vista funzionale equivale a DBCC INPUTBUFFER. [Per ulteriori informazioni, vedere il Blog](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigazione per la concessione di memoria sottovalutata e sovrastima:** Aggiunta di nuovi hint per la query per Resource Governor tramite MIN_GRANT_PERCENT e MAX_GRANT_PERCENT. In questo modo è possibile sfruttare questi suggerimenti durante l'esecuzione delle query limitando le concessioni di memoria per evitare conflitti di memoria. Per ulteriori informazioni, vedere l' [articolo della Knowledge base KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **Migliore diagnostica di concessione/utilizzo di memoria:** Un nuovo evento esteso è stato aggiunto all'elenco delle funzionalità di traccia in SQL Server (query_memory_grant_usage) per tenere traccia delle concessioni di memoria richieste e concesse. Questo fornisce funzionalità di analisi e analisi migliori per la risoluzione dei problemi di esecuzione delle query correlati alle concessioni di memoria. Per ulteriori informazioni, vedere l' [articolo della Knowledge base KB3107173](https://support.microsoft.com/en-us/kb/3107173).
-   **Diagnostica di esecuzione delle query per la distribuzione di tempdb:** gli avvisi hash e di ordinamento ora includono colonne aggiuntive per tenere traccia delle statistiche di I/O fisiche, della memoria usata e delle righe interessate. È stato anche introdotto un nuovo evento esteso hash_spill_details. È ora possibile tenere traccia di informazioni più granulari per gli avvisi di hash e ordinamento ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). Questo miglioramento è ora esposto anche tramite i piani di XML Query sotto forma di un nuovo attributo al tipo complesso SpillToTempDbType ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). Set Statistics on Now Mostra l'ordinamento delle statistiche di tabella. .
-   **Diagnostica migliorata per i piani di esecuzione delle query che coinvolgono il predicato residuo distribuzione:** Le righe effettive lette verranno ora segnalate nei piani di esecuzione delle query per contribuire a migliorare la risoluzione dei problemi di prestazioni delle query. Questa operazione dovrebbe negare la necessità di acquisire SET STATISTICs IO separatamente. Questo consente ora di visualizzare le informazioni correlate a un predicato residuo distribuzione in un piano di query. Per ulteriori informazioni, vedere l' [articolo della Knowledge base KB3107397](https://support.microsoft.com/en-us/kb/3107397).


## <a name="additional-information"></a>Informazioni aggiuntive  
 [Risorse SQL Server 2014](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Centro risorse SQL Server 2014](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Sito Web SQLCat](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
