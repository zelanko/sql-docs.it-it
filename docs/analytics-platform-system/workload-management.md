---
title: Gestione del carico di lavoro nel sistema di piattaforma Analitica | Microsoft Docs
description: Gestione del carico di lavoro nel sistema di piattaforma Analitica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: adc3928e1b7464d93970d280af6acf303ebc6d16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959745"
---
# <a name="workload-management-in-analytics-platform-system"></a>Gestione del carico di lavoro nel sistema di piattaforma Analitica

Funzionalità di gestione del carico di lavoro di SQL Server PDW consente a utenti e agli amministratori di assegnare le richieste di pre-impostare le configurazioni di memoria e concorrenza. Gestione del carico di lavoro consente di migliorare le prestazioni del carico di lavoro, sia coerente o mista, consentendo alle richieste di avere risorse appropriate senza starvation tutte le richieste all'infinito.  
  
Ad esempio, con le tecniche di gestione del carico di lavoro in SQL Server PDW, è possibile:  
  
-   Allocare un numero elevato di risorse per un processo di caricamento.  
  
-   Specificare più risorse per la creazione di un indice columnstore.  
  
-   Risolvere i problemi di un hash join lente per verificare se è necessario maggiore quantità di memoria e quindi assegnarle maggiore quantità di memoria.  
  
## <a name="Basics"></a>Nozioni fondamentali sulla gestione del carico di lavoro  
  
### <a name="key-terms"></a>Termini chiave  
Gestione del carico di lavoro  
*Gestione del carico di lavoro* consiste nella possibilità di comprendere e regolare l'utilizzo delle risorse di sistema per ottenere prestazioni ottimali per le richieste simultanee.  
  
Classe di risorse  
In SQL Server PDW, un *classe di risorse* è un ruolo predefinito del server che dispone di limiti di pre-assegnati per la memoria e concorrenza. SQL Server PDW alloca le risorse per le richieste in base all'appartenenza al ruolo di risorsa classe server dell'account di accesso invia le richieste.  
  
Nei nodi di calcolo, l'implementazione di classi di risorse utilizza la funzionalità Resource Governor in SQL Server. Per altre informazioni su Resource Governor, vedere [Resource Governor](../relational-databases/resource-governor/resource-governor.md) su MSDN.  
  
### <a name="understand-current-resource-utilization"></a>Comprendere l'utilizzo delle risorse correnti  
Per comprendere l'utilizzo delle risorse di sistema per le richieste attualmente in esecuzione, usare le viste DMV di SQL Server PDW. Ad esempio, è possibile utilizzare viste a gestione dinamica per capire se un join hash di grandi dimensioni con esecuzione prolungata può trarre vantaggio dalla presenza di più memoria.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Regolare le allocazioni di risorse  
Per regolare l'utilizzo delle risorse, modificare l'appartenenza a classe di risorse dell'account di accesso che viene inviata la richiesta. I ruoli del server di classe di risorse sono denominate **mediumrc**, **largerc**, e **xlargerc**. Che rappresentano rispettivamente le allocazioni di risorse Media, grande e molto grande.  
  
Ad esempio, per allocare una grande quantità di risorse di sistema per una richiesta, aggiungere l'account di accesso che viene inviata la richiesta per il **largerc** ruolo del server. L'istruzione ALTER SERVER ROLE seguente aggiunge l'account di accesso Anna al ruolo del server largerc.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>Descrizioni delle classi di risorse  
Nella tabella seguente descrive le classi di risorse e le allocazioni di risorse di sistema.  
  
|Classe di risorse|Priorità richiesta|Utilizzo di memoria massima *|Slot di concorrenza (massimo = 32)|Descrizione|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|default|Media|400 MB|1|Per impostazione predefinita, ogni account di accesso è consentita una piccola quantità di risorse di memoria e concorrenza per le richieste.<br /><br />Quando un account di accesso viene aggiunto a una classe di risorse, la nuova classe ha la precedenza. Quando viene eliminato un account di accesso da tutte le classi di risorse, l'account di accesso torna all'allocazione delle risorse predefinito.|  
|MediumRC|Media|1200 MB|3|Esempi di richieste che potrebbero essere la classe di risorse Media:<br /><br />Operazioni di CTAS dotati di grandi dimensioni hash join.<br /><br />Selezionare le operazioni che richiedono più memoria per evitare la memorizzazione nella cache su disco.<br /><br />Caricamento di dati in indici columnstore cluster.<br /><br />La compilazione, ricompilazione e la riorganizzazione degli indici columnstore cluster per tabelle di dimensioni minori con 10 a 15 colonne.|  
|Largerc|Alto|2,8 GB|7|Esempi di richieste che potrebbero essere la classe di risorse di grandi dimensioni:<br /><br />Operazioni di CTAS molto grandi che hanno enorme hash join o deve contenere aggregazioni di grandi dimensioni, ad esempio grandi clausole ORDER BY o GROUP BY.<br /><br />Selezionare le operazioni che richiedono grandi quantità di memoria per operazioni quali hash join o aggregazioni, ad esempio le clausole ORDER BY o GROUP BY<br /><br />Caricamento di dati in indici columnstore cluster.<br /><br />La compilazione, ricompilazione e la riorganizzazione degli indici columnstore cluster per tabelle di dimensioni minori con 10 a 15 colonne.|  
|xlargerc|Alto|8.4 GB|22|La classe di risorse molto grande è per le richieste che potrebbero richiedere il consumo di risorse molto grande in fase di esecuzione.|  
  
<sup>*</sup>Utilizzo massimo della memoria è un'approssimazione.  
  
### <a name="request-importance"></a>Priorità richiesta  
L'importanza di richiesta viene eseguito il mapping alla quantità di tempo di CPU che concederà a SQL Server, in esecuzione nei nodi di calcolo, per le richieste.  Le richieste con priorità più alta ricevono più tempo della CPU.  
  
### <a name="maximum-memory-usage"></a>Utilizzo massimo della memoria  
Utilizzo massimo della memoria è la quantità massima di memoria disponibile che può essere utilizzata una richiesta all'interno di ogni spazio di elaborazione. Ad esempio una richiesta di mediumrc può usare un massimo di 1200 MB per l'elaborazione all'interno di ogni distribuzione. È comunque importante per assicurarsi che i dati non sono sfasati per evitare che alcune distribuzioni eseguendo la maggior parte del lavoro.  
  
### <a name="concurrency-slots"></a>Slot di concorrenza  
L'obiettivo di allocare 1, 3, 7 e 22 slot di concorrenza è consentire i processi di piccoli e grandi dimensioni per l'esecuzione nello stesso momento, senza bloccare il processo di piccole dimensioni quando è in esecuzione un processo di grandi dimensioni.  Ad esempio, SQL Server PDW può allocare al massimo 32 slot di concorrenza per l'esecuzione 1 richiesta molto grande (22 slot), 1 richiesta di grandi dimensioni (7 slot) e 1 richiesta medio (3 slot) nello stesso momento.  
  
Esempi di allocare un massimo di 32 slot di concorrenza per le richieste simultanee:  
  
-   gli slot di 28 = 4 di grandi dimensioni  
  
-   gli slot di 30 = 10 medium  
  
-   gli slot di 32 = default 32  
  
-   gli slot di 32 = molto grande di 1 + 1-medio elevato + 1  
  
-   gli slot di 32 = 2-medio elevato + 4 + 6 predefinito  
  
Si supponga che 6 richieste di grandi dimensioni vengono inviate a SQL Server PDW, e quindi vengono inviate le richieste predefinite di 10. SQL Server PDW elaborerà le richieste in ordine di priorità nel modo seguente:  
  
-   È possibile allocare 28 slot di concorrenza per avviare l'elaborazione 4 richieste di grandi dimensioni quando diventa disponibile la memoria e mantenere 2 richieste di grandi dimensioni nella coda.  
  
-   Allocare 4 slot di concorrenza per avviare l'elaborazione delle richieste predefinito 4 e mantenere le richieste predefinite di 6 della coda di attesa.  
  
Come completare le richieste e diventano disponibili slot di concorrenza, SQL Server PDW dovrà allocare le richieste rimanenti in base alla priorità e le risorse disponibili. Ad esempio, quando sono presenti 7 concorrenza aprire slot, in attesa di richieste di grandi dimensioni verrà avranno la priorità per gli 7 slot rispetto all'attesa media delle richieste.  Se si apre 6 slot, SQL Server PDW allocherà 6 richieste altre dimensioni predefinite. Tuttavia, gli slot di memoria e concorrenza devono essere tutti disponibili prima di SQL Server PDW consente a una richiesta per l'esecuzione.  
  
All'interno di ogni classe di risorse, le richieste di esecuzione nella prima nell'ordine first-out (FIFO).  
  
## <a name="GeneralRemarks"></a>Osservazioni generali  
Se un account di accesso è un membro di più di una classe di risorse, la classe con la maggior parte delle risorse ha la precedenza.  
  
Quando un account di accesso viene aggiunto o eliminato da una classe di risorse, la modifica diventa effettiva immediatamente per tutte le richieste future; non sono interessate le richieste correnti che sono in esecuzione o in attesa. L'account di accesso non è necessario disconnettersi e riconnettersi in ordine per la modifica si verificano.  
  
Per ogni account di accesso, le impostazioni di classe di risorse vengono applicate alle operazioni e le singole istruzioni e non alla sessione.  
  
Prima di SQL Server PDW esegue un'istruzione, tenta di acquisire gli slot di concorrenza necessari per la richiesta. Se non è possibile acquisire slot di concorrenza sufficienti, SQL Server PDW Sposta la richiesta in uno stato di attesa di esecuzione. Tutte le risorse di sistema che sono stati già allocati alla richiesta vengono restituiti al sistema.  
  
La maggior parte delle istruzioni SQL che richiedono sempre le allocazioni di risorse predefinito e pertanto non vengono controllata dalle classi di risorse. Ad esempio, creare account di accesso solo richiede una piccola quantità di risorse e vengono allocate le risorse predefinite anche se l'account di accesso chiama CREATE LOGIN è un membro di una classe di risorse.  Se, ad esempio, Anna è un membro della classe di risorse largerc e Anna invia un'istruzione CREATE LOGIN, l'istruzione CREATE LOGIN eseguirà con il numero predefinito di risorse.  
  
Le istruzioni SQL e operazioni regolate dalle classi di risorse:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   MODIFICA TABELLA RICOMPILAZIONE  
  
-   CREARE L'INDICE CLUSTER  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   CREATE TABLE AS SELECT  
  
-   CREATE REMOTE TABLE AS SELECT  
  
-   Caricamento dei dati con **dwloader**.  
  
-   INSERT-SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   RESTORE DATABASE durante il ripristino in un'appliance con più nodi di calcolo.  
  
-   Selezionare, escluse le query DMV-only  
  
## <a name="Limits"></a>Limitazioni e restrizioni  
Le classi di risorse determinano le allocazioni di memoria e concorrenza.  Non controllano le operazioni di input/output.  
  
## <a name="Metadata"></a>Metadata  
Viste a gestione dinamica che contengono informazioni sulle classi di risorse e i membri di classe di risorse.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
Viste a gestione dinamica che contengono informazioni sullo stato delle richieste e le risorse che necessarie:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Viste di sistema correlati esposte dalle DMV SQL Server nei nodi di calcolo. Visualizzare [SQL Server viste a gestione dinamica](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) per collegamenti a queste DMV in MSDN.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>Attività correlate  
[Attività di gestione del carico di lavoro](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
