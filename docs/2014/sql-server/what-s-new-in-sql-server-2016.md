---
title: Cosa&#39;s New in SQL Server 2014 | Microsoft Docs
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
ms.openlocfilehash: 26d0c84194f6f2aafb8bc499ff5404a1438ee577
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63295237"
---
# <a name="what39s-new-in-sql-server-2014"></a>Cosa&#39;s New in SQL Server 2014
  In questo argomento riepiloga i collegamenti dettagliati alle nuove funzionalità di [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e riepiloga i pacchetti di servizi per [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Per provarlo:** ![Macchina virtuale di Azure piccola](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) ha un account Azure?  Quindi andare **[qui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** creare rapidamente una macchina virtuale con SQL Server 2014 Service Pack 1 (SP1) già installato. 
  
-   [Novità &#40;motore di Database&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [What ' s New in Analysis Services e Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [Novità relative all'installazione di SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] non sono state introdotte funzionalità significative nuove per quanto segue:**  
  
-   [Novità &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [Novità &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) non sono stati introdotti nuove funzionalità significative.
-  [Informazioni sulla versione di SQL Server 2014 Service Pack 1](https://support.microsoft.com/en-us/kb/3058865).
-  [![Scarica Service Pack 1 per Microsoft? SQL Server?? 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [Scarica Service Pack 1 per Microsoft? SQL Server?? 2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694).


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 2 (SP2)
- [Informazioni sulla versione di SQL Server 2014 Service Pack 2](https://support.microsoft.com/en-us/kb/3171021).
-  [![Scaricare il Service Pack 2 per Microsoft? SQL Server?? 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [download del Service Pack 2 per Microsoft? SQL Server?? 2014](https://go.microsoft.com/fwlink/?LinkID=821558).
-  [![Scaricare SQL Server 2014 SP2 Feature Pack](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [scaricare il Feature Pack SQL Server 2014 SP2](https://www.microsoft.com/en-us/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2) Include i miglioramenti seguenti:

### <a name="performance-and-scalability-improvements"></a>Miglioramenti di prestazioni e scalabilità 
-   **Partizionamento soft-NUMA automatico:** Con [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, soft-NUMA automatica è abilitata quando il Flag di traccia 8079 è abilitato durante l'avvio di istanze. Quando il Flag di traccia 8079 è abilitato durante l'avvio, [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 verrà interrogare il layout hardware e configurare automaticamente soft-NUMA sui sistemi che segnalano 8 o più CPU per nodo NUMA. Il comportamento NUMA automatico, temporanea è l'Hyperthread (HT/processore logico) compatibile con. Il partizionamento e la creazione di nodi aggiuntivi ridimensionano l'elaborazione in background aumentando il numero di listener tramite scalabilità e le funzionalità di crittografia e di rete. È consigliabile testare il carico di lavoro delle prestazioni con configurazione automaticamente Soft-NUMA prima di attivarlo nell'ambiente di produzione. [Vedere il Blog per informazioni dettagliate](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Scalabilità dell'oggetto memoria dinamica:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 partiziona in modo dinamico gli oggetti basati sul numero di core per ridimensionare l'hardware moderno e nodi di memoria. L'obiettivo della promozione dinamica consiste nel partizionare automaticamente un oggetto di memoria sicuro di thread (CMEMTHREAD) se diventa un collo di bottiglia. È possibile promuovere dinamicamente gli oggetti di memoria non partizionati perché siano partizionati per nodo (numero di partizioni è uguale a numero di nodi NUMA) e memoria oggetti partizionati in base al nodo possono ulteriormente promossi perché siano partizionati dalla CPU (numero di partizioni è uguale a del CPU). [Vedere il blog per informazioni dettagliate](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Hint MAXDOP per DBCC CHECK\* comandi:** Questo miglioramento riguarda [commenti (468694) connect](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). È ora possibile eseguire DBCC CHECKDB con un'impostazione di MAXDOP diversa del valore di sp_configure. Se MAXDOP supera il valore configurato con Resource Governor, il motore di database usa il valore MAXDOP di Resource Governor descritto in ALTER WORKLOAD GROUP (Transact-SQL). Quando si utilizza l'hint per la query MAXDOP sono valide tutte le regole semantiche utilizzate con l'opzione di configurazione max degree of parallelism. Per altre informazioni, vedere [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Abilitare > 8TB per Pool di Buffer:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 supporta 128TB di spazio degli indirizzi virtuali per l'utilizzo del pool di buffer. Questo miglioramento consente a Pool di Buffer di SQL Server per scalabilità superiore a 8TB in hardware moderni.
-   **Spinlock SOS_RWLock analisi utilizzo software:** Il SOS_RWLock è una primitiva di sincronizzazione usata in vari punti in tutta la codebase di SQL Server.  Come suggerisce il nome, il codice può contenere più condivisi (con i lettori) o la proprietà singola (writer). Questo miglioramento Elimina la necessità di spinlock per SOS_RWLock e Usa invece tecniche senza blocco simili a OLTP in memoria. Con questa modifica, numero di thread può leggere una struttura di dati protetta da SOS_RWLock in parallelo senza blocco tra loro e offrendo maggiore scalabilità. Prima di questa modifica, l'implementazione di spinlock è consentito un solo thread acquisire il SOS_RWLock alla volta, anche per leggere una struttura di dati.  [Vedere il blog per informazioni dettagliate](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementazione spaziale nativa:** È stato introdotto un miglioramento significativo delle prestazioni delle query spaziali in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 tramite l'implementazione nativa. Per altre informazioni, vedere la [articolo della knowledge base KB3107399](https://support.microsoft.com/en-us/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Al supporto e miglioramenti della diagnostica
-   **La clonazione del database:** Database clone è un nuovo comando DBCC che migliora la risoluzione dei problemi di database di produzione esistenti clonando lo schema e i metadati senza i dati. Il clone viene creato con il comando `DBCC clonedatabase('source_database_name', 'clone_database_name')`.  **Nota:** È consigliabile non usare i database clonati in ambienti di produzione. Usare il comando seguente determinare se un database è stato generato da un database clonato: `select DATABASEPROPERTYEX('clonedb', 'isClone')`. Il valore restituito di **1** indica il database viene creato da clonedatabase durante **0** indica non è un clone.
-   **Supporto di tempdb:**  Un nuovo messaggio di log degli errori che indica il numero di file tempdb e le dimensioni/aumento automatico delle dimensioni del file di dati tempdb presenti all'avvio del server.
-   **Registrazione di inizializzazione immediata dei File di database:** Un nuovo messaggio di log degli errori che indica il server statup, lo stato di inizializzazione File immediata dei Database (abilitato/disabilitato).
-   **Nomi dei moduli nello stack chiamate:** Lo stack di chiamate Xevent ora include i nomi dei moduli + offset anziché gli indirizzi assoluti.
-   **Nuova DMF per le statistiche incrementali:** Questo miglioramento riguarda [commenti (797156) connect](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) per abilitare le statistiche incrementali a livello di partizione di rilevamento. È stato introdotto un nuovo DM db_incremental_stats_properties DMF per esporre le informazioni per ogni partizione statistiche incrementali.
-   **Comportamento di DMV di indici dell'utilizzo aggiornato:** Questo miglioramento riguarda [commenti (739566) connect](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) da parte dei clienti dove la ricompilazione di un indice viene *non* deselezionare qualsiasi voce di riga esistente da db_index_usage_stats per quell'indice. Il comportamento sarà ora le stesse di SQL 2008 e SQL Server 2016. [Vedere il blog per informazioni dettagliate](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Migliore correlazione tra la diagnostica di Xevent e DMV:** Questo miglioramento riguarda [commenti (1934583) connect](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). Query_hash e query_plan_hash vengono usati per identificare in modo univoco una query. Nelle DMV sono definiti come varbinary (8), mentre in XEvent come UINT64. Poiché SQL server non esiste un "bigint unisigned", eseguire il cast non sempre funziona. Questo miglioramento introduce nuove colonne azione/filtro di XEvent equivalenti ai campi query_hash e query_plan_hash ad eccezione del fatto che tali valori sono definiti come INT64. In questo modo è possibile correlare le query tra XEvent e le viste a gestione dinamica.
-   **Supporto per UTF-8 in BULK INSERT e BCP:** Questo miglioramento riguarda [commenti (370419) connect](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) in cui il supporto per l'esportazione e importazione di dati con codificati in set di caratteri UTF-8 è ora abilitato in BULK INSERT e BCP.
-   **Operatore leggero query l'esecuzione di profilatura:** Durante la risoluzione dei problemi di query prestazioni, sebbene showplan fornisce molte informazioni sul piano di esecuzione di query e il costo dell'operatore nel piano, ma è limitata informazioni sull'effettivo delle statistiche di runtime, ad esempio (CPU, letture dei / o, tempo trascorso per ogni thread). SQL 2014 SP2 introduce queste statistiche di runtime aggiuntive per ogni operatore Showplan, nonché un XEvent (query_thread_profile) per semplificare la risoluzione dei problemi delle prestazioni delle query. [Vedere il blog per informazioni dettagliate](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Pulizia rilevamento modifiche:** Nuova stored procedure `sp_flush_CT_internal_table_on_demand` è stato introdotto alla modifica di pulizia delle tabelle interne di rilevamento su richiesta.
-   **Registrazione Timeout Lease AlwaysON** aggiunto nuove funzionalità di registrazione per i messaggi di Timeout di Lease in modo che l'ora corrente e le ore previste per il rinnovo vengono registrate. Anche un nuovo messaggio è stato introdotto in SQL Errorlog riguardanti i timeout. [Vedere il blog per informazioni dettagliate](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Nuova DMF per il recupero del buffer di input in SQL Server:** Disponibile una nuova DMF per il recupero del buffer di input per una sessione o una richiesta (sys.dm_exec_input_buffer). Dal punto di vista funzionale equivale a DBCC INPUTBUFFER. [Vedere il blog per informazioni dettagliate](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigazione dei rischi per la concessione di memoria sottostimati e sopravvalutati:** Aggiunto nuovo hint per la query per Resource Governor tramite MIN_GRANT_PERCENT e MAX_GRANT_PERCENT. Ciò consente di sfruttare questi hint durante l'esecuzione di query limitando le concessioni di memoria per evitare una contesa di memoria. Per altre informazioni, vedere [KB310740 articolo della knowledge base](https://support.microsoft.com/en-us/kb/3107401)
-   **Migliore diagnostica di concessione/utilizzo memoria:** Un nuovo evento esteso è stato aggiunto all'elenco delle funzionalità di traccia in SQL Server (query_memory_grant_usage) per tenere traccia delle concessioni di memoria richiesta e concesso. Fornisce funzionalità di traccia e analisi migliorate per la risoluzione dei problemi di esecuzione query con concessioni di memoria. Per altre informazioni, vedere [articolo della knowledge base KB3107173](https://support.microsoft.com/en-us/kb/3107173).
-   **Eseguire query di diagnostica di esecuzione per spill tempdb:** -avviso di Hash e Sort Warnings ora hanno colonne aggiuntive per tenere traccia delle statistiche i/o fisico, memoria utilizzata e righe interessate. È stato anche introdotto un nuovo evento esteso hash_spill_details. A questo punto è possibile tenere traccia delle informazioni più granulari per gli avvisi di hash e ordinamento ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). Questo miglioramento è ora anche esposto attraverso i piani di Query XML sotto forma di un nuovo attributo al tipo complesso SpillToTempDbType ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). Impostare le statistiche su ora Mostra Ordina le statistiche della tabella di lavoro. .
-   **Diagnostica migliorata per i piani di esecuzione di query che implicano la distribuzione del predicato residua:** Le righe effettive lette verranno ora segnalate nei piani di esecuzione query per migliorare la risoluzione dei problemi delle prestazioni di query. Questa deve annullare la necessità per acquisire SET STATISTICS IO separatamente. Questa ora consente di visualizzare le informazioni relative a una distribuzione del predicato residua in un piano di query. Per altre informazioni, vedere [articolo della knowledge base KB3107397](https://support.microsoft.com/en-us/kb/3107397).


## <a name="additional-information"></a>Informazioni aggiuntive  
 [Risorse di SQL Server 2014](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Centro risorse di SQL Server 2014](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Sito Web SQLCat](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
