---
title: Gestione dei carichi di lavoro
description: Gestione del carico di lavoro nel sistema della piattaforma Analytics.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d14714cb23a9f6b0d6cc63ddca5049cb6741017c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399439"
---
# <a name="workload-management-in-analytics-platform-system"></a>Gestione del carico di lavoro nel sistema della piattaforma Analytics

Le funzionalità di gestione del carico di lavoro di SQL Server PDW consentono a utenti e amministratori di assegnare richieste a configurazioni predefinite di memoria e concorrenza. Usare la gestione del carico di lavoro per migliorare le prestazioni del carico di lavoro, coerente o misto, consentendo alle richieste di disporre delle risorse appropriate senza affamare le richieste per sempre.  
  
Con le tecniche di gestione del carico di lavoro in SQL Server PDW, ad esempio, è possibile:  
  
-   Allocare un numero elevato di risorse a un processo di caricamento.  
  
-   Specificare più risorse per la compilazione di un indice columnstore.  
  
-   Risolvere i problemi relativi a un hash join con esecuzione prolungata per verificare se è necessaria una maggiore quantità di memoria e quindi assegnare una maggiore quantità di memoria.  
  
## <a name="Basics"></a>Nozioni fondamentali sulla gestione del carico  
  
### <a name="key-terms"></a>Termini chiave  
Gestione del carico di lavoro  
*Gestione del carico di lavoro* è la capacità di comprendere e modificare l'utilizzo delle risorse di sistema per ottenere prestazioni ottimali per le richieste simultanee.  
  
Classe di risorse  
In SQL Server PDW, una *classe di risorse* è un ruolo predefinito del server che dispone di limiti preassegnati per la memoria e la concorrenza. SQL Server PDW alloca le risorse alle richieste in base all'appartenenza al ruolo del server della classe di risorse dell'account di accesso che invia le richieste.  
  
Nei nodi di calcolo, l'implementazione delle classi di risorse usa la funzionalità Resource Governor in SQL Server. Per ulteriori informazioni su Resource Governor, vedere [Resource Governor](../relational-databases/resource-governor/resource-governor.md) su MSDN.  
  
### <a name="understand-current-resource-utilization"></a>Informazioni sull'utilizzo delle risorse corrente  
Per comprendere l'utilizzo delle risorse di sistema per le richieste attualmente in esecuzione, utilizzare le viste a gestione dinamica SQL Server PDW. Ad esempio, è possibile usare DMV per capire se un hash join di grandi dimensioni con esecuzione prolungata può trarre vantaggio da una maggiore quantità di memoria.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Modificare le allocazioni delle risorse  
Per modificare l'utilizzo delle risorse, modificare l'appartenenza alla classe di risorse dell'account di accesso che invia la richiesta. I ruoli del server della classe di risorse sono denominati **mediumrc**, **largerc**e **xlargerc**. Rappresentano rispettivamente le allocazioni di risorse medie, grandi e molto grandi.  
  
Per allocare, ad esempio, una grande quantità di risorse di sistema a una richiesta, aggiungere l'account di accesso che invia la richiesta al ruolo del server **largerc** . L'istruzione ALTER SERVER ROLE seguente aggiunge l'account di accesso Anna al ruolo del server largerc.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>Descrizioni delle classi di risorse  
Nella tabella seguente vengono descritte le classi di risorse e le relative allocazioni di risorse di sistema.  
  
|Classe di risorse|Importanza della richiesta|Utilizzo massimo della memoria *|Slot di concorrenza (massimo = 32)|Descrizione|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|default|Media|400 MB|1|Per impostazione predefinita, a ogni account di accesso è consentita una piccola quantità di memoria e risorse di concorrenza per le relative richieste.<br /><br />Quando un account di accesso viene aggiunto a una classe di risorse, la nuova classe ha la precedenza. Quando un account di accesso viene eliminato da tutte le classi di risorse, viene ripristinata l'allocazione di risorse predefinita.|  
|MediumRC|Media|1200 MB|3|Esempi di richieste che potrebbero richiedere la classe di risorse media:<br /><br />Operazioni CTAS con hash join di grandi dimensioni.<br /><br />Selezionare le operazioni che richiedono una maggiore quantità di memoria per evitare la memorizzazione nella cache su disco.<br /><br />Caricamento dei dati negli indici columnstore cluster.<br /><br />Compilazione, ricompilazione e riorganizzazione di indici columnstore cluster per tabelle di dimensioni ridotte con 10-15 colonne.|  
|Largerc|Alto|2,8 GB|7|Esempi di richieste che potrebbero richiedere la classe di risorse di grandi dimensioni:<br /><br />Operazioni CTAS di grandi dimensioni con hash join di grandi dimensioni o aggregazioni di grandi dimensioni, ad esempio clausole ORDER BY o GROUP BY di grandi dimensioni.<br /><br />Selezionare le operazioni che richiedono una quantità di memoria molto elevata per operazioni quali hash join o aggregazioni come le clausole ORDER BY o GROUP BY<br /><br />Caricamento dei dati negli indici columnstore cluster.<br /><br />Compilazione, ricompilazione e riorganizzazione di indici columnstore cluster per tabelle di dimensioni ridotte con 10-15 colonne.|  
|xlargerc|Alto|8,4 GB|22|La classe di risorse molto grande è destinata alle richieste che potrebbero richiedere un consumo di risorse molto elevato in fase di esecuzione.|  
  
<sup>*</sup>L'utilizzo massimo della memoria è un'approssimazione.  
  
### <a name="request-importance"></a>Importanza della richiesta  
L'importanza della richiesta viene mappata alla quantità di tempo della CPU che SQL Server, in esecuzione nei nodi di calcolo, assegna alle richieste.  Le richieste con priorità più elevata ricevono più tempo della CPU.  
  
### <a name="maximum-memory-usage"></a>Utilizzo massimo della memoria  
L'utilizzo massimo della memoria è la quantità massima di memoria disponibile che può essere utilizzata da una richiesta all'interno di ogni spazio di elaborazione. Ad esempio, una richiesta mediumrc può usare fino a 1200 MB per l'elaborazione all'interno di ogni distribuzione. È ancora importante assicurarsi che i dati non siano inclinati per evitare che alcune distribuzioni eseguano la maggior parte del lavoro.  
  
### <a name="concurrency-slots"></a>Slot di concorrenza  
L'obiettivo dell'allocazione di slot di concorrenza 1, 3, 7 e 22 consiste nel consentire l'esecuzione simultanea di processi di grandi dimensioni e di dimensioni ridotte, senza bloccare il processo di piccole dimensioni durante l'esecuzione di un processo di grandi dimensioni.  Ad esempio, SQL Server PDW possibile allocare un massimo di 32 slot di concorrenza per eseguire 1 richiesta molto grande (22 slot), una richiesta di grandi dimensioni (7 slot) e una richiesta media (3 slot) allo stesso tempo.  
  
Esempi di allocazione di un massimo di 32 slot di concorrenza alle richieste simultanee:  
  
-   28 slot = 4 grandi  
  
-   30 slot = 10 medio  
  
-   32 slot = 32 predefinito  
  
-   32 slot = 1 molto grande + 1 grande + 1 medio  
  
-   32 slot = 2 large + 4 medium + 6 default  
  
Si supponga che 6 richieste di grandi dimensioni vengano inviate a SQL Server PDW e che vengano inviate 10 richieste predefinite. In SQL Server PDW le richieste vengono elaborate in ordine di priorità, come indicato di seguito:  
  
-   Allocare 28 slot di concorrenza per avviare l'elaborazione di 4 richieste di grandi dimensioni, perché la memoria diventa disponibile e mantiene 2 richieste di grandi dimensioni nella coda.  
  
-   Allocare 4 slot di concorrenza per avviare l'elaborazione di 4 richieste predefinite e per rispettare 6 richieste predefinite nella coda di attesa.  
  
Man mano che le richieste Finish e slot di concorrenza diventano disponibili, SQL Server PDW alloca le richieste rimanenti in base alle risorse e alla priorità disponibili. Ad esempio, quando sono presenti 7 slot di concorrenza aperti, le richieste di grandi dimensioni in attesa avranno una priorità maggiore per i 7 slot rispetto alle richieste medie in attesa.  Se vengono aperti 6 slot, SQL Server PDW alloca 6 richieste di dimensioni più predefinite. Tuttavia, è necessario che tutti gli slot di memoria e concorrenza siano disponibili prima che SQL Server PDW consenta l'esecuzione di una richiesta.  
  
All'interno di ogni classe di risorse, le richieste vengono eseguite in un ordine FIFO (First in First out).  
  
## <a name="GeneralRemarks"></a>Osservazioni generali  
Se un account di accesso è membro di più di una classe di risorse, la classe con la maggior parte delle risorse avrà la precedenza.  
  
Quando un account di accesso viene aggiunto o eliminato da una classe di risorse, la modifica viene applicata immediatamente per tutte le richieste future; le richieste correnti in esecuzione o in attesa non sono interessate. Non è necessario che l'account di accesso venga disconnesso e riconnesso per consentire la modifica.  
  
Per ogni account di accesso, le impostazioni della classe di risorse vengono applicate a singole istruzioni e operazioni e non alla sessione.  
  
Prima che SQL Server PDW esegua un'istruzione, tenta di acquisire gli slot di concorrenza necessari per la richiesta. Se non è in grado di acquisire un numero sufficiente di slot di concorrenza, SQL Server PDW sposta la richiesta in uno stato di attesa per l'esecuzione. Tutte le risorse del sistema già allocate alla richiesta vengono restituite al sistema.  
  
Per la maggior parte delle istruzioni SQL sono sempre necessarie le allocazioni delle risorse predefinite e pertanto non sono controllate dalle classi di risorse. Ad esempio, CREATE LOGIN richiede solo una piccola quantità di risorse e vengono allocate le risorse predefinite anche se l'account di accesso che chiama CREATE LOGIN è un membro di una classe di risorse.  Se ad esempio Anna è membro della classe di risorse largerc e invia un'istruzione CREATE LOGIN, l'istruzione CREATE LOGIN verrà eseguita con il numero predefinito di risorse.  
  
Istruzioni e operazioni SQL regolate dalle classi di risorse:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   MODIFICA TABELLA RICOMPILAZIONE  
  
-   CREA INDICE CLUSTER  
  
-   CREARE L'INDICE COLUMNSTORE CLUSTER  
  
-   CREATE TABLE AS SELECT  
  
-   CREA TABELLA REMOTA COME SELECT  
  
-   Caricamento dei dati con **dwloader**.  
  
-   INSERT SELECT  
  
-   UPDATE  
  
-   Elimina  
  
-   RIPRISTINARE il DATABASE durante il ripristino in un'appliance con più nodi di calcolo.  
  
-   SELECT, escluse le query solo DMV  
  
## <a name="Limits"></a>Limitazioni e restrizioni  
Le classi di risorse regolano le allocazioni di memoria e concorrenza.  Non regolano le operazioni di input/output.  
  
## <a name="Metadata"></a>Metadati  
DMV che contengono informazioni sulle classi di risorse e i membri della classe di risorse.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
DMV che contengono informazioni sullo stato delle richieste e sulle risorse necessarie:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Viste di sistema correlate esposte dal SQL Server DMV nei nodi di calcolo. Vedere [SQL Server](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) DMV per i collegamenti a questi DMV su MSDN.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys. dm_pdw_nodws_resource_governor_workload_groups  
  
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
  
