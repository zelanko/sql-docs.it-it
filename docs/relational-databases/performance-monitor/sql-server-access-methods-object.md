---
title: Oggetto Metodi di accesso di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Access Methods object
- SQLServer:Access Methods
ms.assetid: 27558585-e780-48bb-a042-30d664662ebc
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 296cdb3433ff0e40ea73987ef5a53b985a550f1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787406"
---
# <a name="sql-server-access-methods-object"></a>Oggetto Metodi di accesso di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'oggetto **Metodi di accesso** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include contatori che consentono di monitorare l'accesso ai dati logici all'interno del database. L'accesso fisico alle pagine del database su disco viene monitorato tramite i contatori di **Gestione buffer** . Il monitoraggio dei metodi utilizzati per accedere ai dati archiviati nel database consente di determinare se è possibile migliorare le prestazioni delle query aggiungendo o modificando gli indici, aggiungendo o spostando partizioni, aggiungendo file o gruppi di file, deframmentando gli indici o riscrivendo le query. I contatori dell'oggetto **Metodi di accesso** possono essere utilizzati anche per monitorare la quantità di dati, gli indici e lo spazio libero all'interno del database e determinare in tal modo il volume e la frammentazione dei dati per ogni istanza del server. Un'eccessiva frammentazione dell'indice può ridurre le prestazioni.  
  
 Per informazioni più dettagliate sul volume, la frammentazione e l'utilizzo dei dati, utilizzare le viste a gestione dinamica seguenti:  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)  
  
-   [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)  
  
 Per informazioni sull'utilizzo di spazio in **tempdb** a livello di file, attività e sessione, utilizzare le viste a gestione dinamica seguenti:  
  
-   [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
-   [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)  
  
-   [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
  
 Nella tabella seguente vengono descritti i contatori dell'oggetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access Methods**di**.  
  
|Contatori di SQLServer:Metodi di accesso|Descrizione|  
|----------------------------------------|-----------------|  
|**Batch pulizia unità di allocazione/sec**|Numero di batch al secondo completati correttamente dall'attività in background che consente di eliminare unità di allocazione rimosse posticipate.|  
|**Pulizia unità di allocazione/sec**|Numero di unità di allocazione al secondo rimosse correttamente dall'attività in background che consente di eliminare unità di allocazione rimosse posticipate. Per la rimozione di ogni unità di allocazione sono necessari più batch.|  
|**Conteggio LOB creati per riferimento**|Conteggio di valori LOB passati per riferimento. Gli oggetti LOB per riferimento vengono utilizzati in determinate operazioni bulk per evitare il costo relativo al passaggio per valore.|  
|**Conteggio utilizzi LOB per riferimento**|Conteggio di valori LOB per riferimento utilizzati. Gli oggetti LOB per riferimento vengono utilizzati in determinate operazioni bulk per evitare il costo relativo al passaggio per valore.|  
|**Conteggio read-ahead LOB**|Conteggio di pagine LOB in cui è stato generato un read-ahead.|  
|**Conteggio pull interno di righe**|Conteggio dei valori di colonna di cui è stato eseguito il pull all'interno di righe dall'esterno di righe.|  
|**Conteggio push all'esterno di righe**|Conteggio dei valori di colonna di cui è stato eseguito il push all'interno di righe dall'esterno di righe.|  
|**Unità di allocazione rimosse posticipate**|Numero di unità di allocazione in attesa di rimozione da parte dell'attività in background che consente di eliminare unità di allocazione rimosse posticipate.|  
|**Set di righe rimossi posticipati**|Numero di set di righe creati come risultato di operazioni di compilazione dell'indice online interrotte in attesa di rimozione da parte dell'attività in background che consente di eliminare set di righe rimossi posticipati.|  
|**Pulizia set di righe rimossi/sec**|Numero di set di righe al secondo creati come risultato di operazioni di compilazione dell'indice online interrotte rimossi correttamente dall'attività in background che consente di eliminare set di righe rimossi posticipati.|  
|**Set di righe rimossi ignorati/sec**|Numero di set di righe al secondo creati come risultato di operazioni di compilazione dell'indice online interrotte ignorati dall'attività in background che consente di eliminare set di righe rimossi posticipati creati.|  
|**Extent deallocati/sec**|Numero di extent deallocati al secondo in tutti i database di questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Extent allocati/sec**|Numero di extent allocati al secondo in tutti i database di questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Batch pulizia unità di allocazione non riusciti/sec**|Numero di batch al secondo non riusciti e che hanno richiesto un nuovo tentativo da parte dell'attività in background che consente di eliminare unità di allocazione rimosse posticipate. L'errore potrebbe essere stato causato da memoria o spazio su disco insufficiente, problemi hardware e altre ragioni.|  
|**Cookie pagina foglia non utilizzato**|Numero di volte in cui non è stato possibile utilizzare un cookie pagina foglia durante una ricerca nell'indice in seguito a modifiche apportate alla pagina foglia. Il cookie viene utilizzato per velocizzare le ricerche nell'indice.|  
|**Cookie pagina albero non utilizzato**|Numero di volte in cui non è stato possibile utilizzare un cookie pagina albero durante una ricerca nell'indice in seguito a modifiche apportate alle pagine padre di tali pagine albero. Il cookie viene utilizzato per velocizzare le ricerche nell'indice.|  
|**Record inoltrati/sec**|Numero di record recuperati al secondo tramite puntatori di record inoltrati.|  
|**Pagine di spazio disponibile/sec**|Numero di pagine recuperate al secondo dalle analisi per la ricerca di spazio disponibile. Tali analisi consentono di cercare spazio disponibile nelle pagine già allocate a un'unità di allocazione, in modo da soddisfare la richiesta di inserimento o di modifica di frammenti di record.|  
|**Analisi spazio disponibile/sec**|Numero di analisi al secondo iniziate per cercare spazio disponibile nelle pagine già allocate a un'unità di allocazione, in modo da inserire o modificare un frammento di record. È possibile che a ogni analisi vengano trovate più pagine.|  
|**Analisi complete/sec**|Numero di analisi complete senza restrizioni al secondo. Possono essere analisi di tabelle di base o di indici completi.|  
|**Ricerche indice/sec**|Numero di ricerche eseguite nell'indice al secondo. Tali ricerche consentono di avviare un'analisi dell'intervallo, riposizionare un'analisi dell'intervallo, riconvalidare un punto di analisi, recuperare un singolo record di indice ed eseguire ricerche nell'indice per individuare il punto in cui inserire una nuova riga.|  
|**Attese InSysXact/sec**|Numero di volte in cui un lettore deve rimanere in attesa di una pagina perché è impostato il bit InSysXact.|  
|**Conteggio LobHandle creati**|Conteggio degli oggetti LOB temporanei creati.|  
|**Conteggio LobHandle eliminati**|Conteggio degli oggetti LOB temporanei eliminati.|  
|**Conteggio provider LobSS creati**|Conteggio dei provider del servizio di archiviazione LOB (LobSSP, LOB Storage Service Providers) creati. Una tabella di lavoro creata per ogni provider LobSS.|  
|**Conteggio provider LobSS eliminati**|Conteggio di provider LobSS eliminati.|  
|**Conteggio provider LobSS troncati**|Conteggio di provider LobSS troncati.|  
|**Allocazioni pagine miste/sec**|Numero di pagine allocate al secondo con extent misti. È possibile utilizzarli per archiviare le pagine IAM e le prime otto pagine allocate a un'unità di allocazione.|  
|**Tentativi di compressione di pagina/sec**|Numero di pagine valutate per la compressione a livello di pagina. Vengono incluse le pagine che non sono state compresse perché la compressione non avrebbe comportato risparmi significativi. Vengono inclusi tutti gli oggetti dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni su oggetti specifici, vedere [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md).|  
|**Pagine deallocate/sec**|Numero di pagine deallocate al secondo in tutti i database di questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sono incluse le pagine da extent misti e uniformi.|  
|**Suddivisioni di pagina/sec**|Numero di suddivisioni di pagina al secondo eseguite in seguito all'overflow di pagine di indice.|  
|**Pagine allocate/sec**|Numero di pagine allocate al secondo in tutti i database di questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Include le allocazioni di pagina da extent misti ed extent uniformi.|  
|**Pagine compresse/sec**|Numero di pagine di dati compresse utilizzando l'opzione di compressione PAGE. Vengono inclusi tutti gli oggetti dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni su oggetti specifici, vedere [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md).|  
|**Analisi di tipo probe/sec**|Numero di analisi di tipo probe al secondo utilizzate per trovare al massimo un'unica riga restituita direttamente in un indice o in una tabella di base.|  
|**Analisi intervallo/sec**|Numero di analisi al secondo dell'intervallo qualificato eseguite tramite indici.|  
|**Riconvalide punto di analisi/sec**|Numero di riconvalide al secondo del punto di analisi che è stato necessario eseguire per continuare l'analisi.|  
|**Record fantasma ignorati/sec**|Numero di record fantasma ignorati al secondo durante le operazioni di analisi.|  
|**Escalation blocchi di tabella/sec**|Numero di escalation dei blocchi eseguite in una tabella alla granularità TABLE o HoBT.|  
|**Cookie pagina foglia utilizzato**|Numero di volte in cui un cookie pagina foglia viene utilizzato correttamente durante una ricerca nell'indice non essendosi verificate modifiche nella pagina foglia. Il cookie viene utilizzato per velocizzare le ricerche nell'indice.|  
|**Cookie pagina albero utilizzato**|Numero di volte in cui un cookie pagina albero viene utilizzato correttamente durante una ricerca nell'indice non essendosi verificate modifiche nella pagina padre della pagina albero. Il cookie viene utilizzato per velocizzare le ricerche nell'indice.|  
|**File di lavoro creati/sec**|Numero di file di lavoro creati al secondo. Ad esempio, è possibile utilizzare i file di lavoro per l'archiviazione dei risultati temporanei di hash join e aggregazioni hash.|  
|**Tabelle di lavoro create/sec**|Numero di tabelle di lavoro create al secondo. Ad esempio, è possibile utilizzare le tabelle di lavoro per l'archiviazione dei risultati temporanei di spool di query, variabili LOB, variabili XML e cursori.|  
|**Base tabelle di lavoro dalla cache**|Solo per uso interno.|  
|**Percentuale tabelle di lavoro dalla cache**|Percentuale di tabelle di lavoro create in cui le due pagine iniziali della tabella di lavoro non sono state allocate ma sono risultate immediatamente disponibili dalla cache della tabella di lavoro. Quando si rimuove una tabella di lavoro, è possibile che due pagine rimangano allocate e vengano restituite alla cache della tabella di lavoro, incrementando le prestazioni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
