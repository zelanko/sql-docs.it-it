---
title: Risolvere i problemi di memoria insufficiente | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8171a91d18650285c7bcaf4eb780083e958a8789
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "72908444"
---
# <a name="resolve-out-of-memory-issues"></a>Risolvere i problemi di memoria insufficiente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] usa più memoria e in modi diversi rispetto a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile che la quantità di memoria installata e allocata per [!INCLUDE[hek_2](../../includes/hek-2-md.md)] diventi inadeguata con l'aumentare delle esigenze. In tal caso, è possibile che la memoria risulti insufficiente. In questo argomento viene descritto come risolvere una situazione di memoria insufficiente. Per le linee guida che consentono di evitare molte situazioni di memoria insufficiente, vedere [Monitorare e risolvere i problemi relativi all'utilizzo della memoria](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md) .  
  
## <a name="covered-in-this-topic"></a>Sezioni dell'argomento  
  
|Argomento|Panoramica|  
|-----------|--------------|  
|[Risoluzione degli errori di ripristino del database dovuti a memoria insufficiente](#bkmk_resolveRecoveryFailures)|Operazioni da eseguire se viene visualizzato il messaggio di errore "Operazione di ripristino non riuscita per il database ' *\<NomeDatabase>* '. Memoria insufficiente nel pool di risorse ' *\<NomePoolRisorse>* '."|  
|[Risoluzione dell'impatto delle condizioni di memoria insufficiente sul carico di lavoro](#bkmk_recoverFromOOM)|Operazioni da eseguire nel caso in cui i problemi di memoria insufficiente incidono negativamente sulle prestazioni.|  
|[Risoluzione degli errori di allocazione della pagina dovuti a memoria insufficiente quando è disponibile memoria sufficiente](#bkmk_PageAllocFailure)|Operazioni da eseguire se viene visualizzato il messaggio di errore "È in corso la disabilitazione delle allocazioni di pagine per il database ' *\<NomeDatabase>* '. Memoria insufficiente nel pool di risorse ' *\<NomePoolRisorse>* '. ..." quando la memoria disponibile è sufficiente per l'operazione.|
|[Procedure consigliate sull'uso di OLTP in memoria in un ambiente di VM](#bkmk_VMs)|Aspetti da tenere presenti quando si usa OLTP in memoria in un ambiente virtualizzato.|
  
##  <a name="resolve-database-restore-failures-due-to-oom"></a><a name="bkmk_resolveRecoveryFailures"></a> Risoluzione degli errori di ripristino del database dovuti a memoria insufficiente  
 Quando si tenta di ripristinare un database è possibile che venga visualizzato il messaggio di errore: "Operazione di ripristino non riuscita per il database ' *\<NomeDatabase>* '. Memoria insufficiente nel pool di risorse ' *\<NomePoolRisorse>* '." Questo errore indica che la memoria disponibile del server non è sufficiente per il ripristino del database. 
   
La memoria disponibile del server in cui viene ripristinato un database deve essere sufficiente per le tabelle ottimizzate per la memoria nel backup del database. In caso contrario, il database non verrà portato online e verrà contrassegnato come sospetto.  
  
Se la memoria fisica del server è sufficiente, ma viene comunque visualizzato questo errore, altri processi potrebbero star usando troppa memoria oppure un problema di configurazione rende la memoria disponibile insufficiente per il ripristino. Per questo tipo di problemi usare le seguenti misure per aumentare la memoria disponibile per l'operazione di ripristino: 
  
-   Chiudere temporaneamente le applicazioni in esecuzione.   
    Chiudendo una o più applicazioni in esecuzione o arrestando i servizi non necessari al momento, si libera la memoria usata da tali applicazioni rendendola disponibile per l'operazione di ripristino. È possibile riavviarle dopo il completamento del ripristino.  
  
-   Aumentare il valore di MAX_MEMORY_PERCENT.   
    Se il database è [associato a un pool di risorse](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md), che rappresenta la procedura consigliata, la memoria disponibile per il ripristino viene regolata da MAX_MEMORY_PERCENT. Se il valore è troppo basso, il ripristino non riuscirà. Nel frammento di codice seguente il valore di MAX_MEMORY_PERCENT per il pool di risorse PoolHk viene modificato al 70% della memoria installata.  
  
    > [!IMPORTANT]  
    > Se il server è in esecuzione in una VM e non è dedicato, impostare il valore di MIN_MEMORY_PERCENT sullo stesso valore di MAX_MEMORY_PERCENT.   
    > Per altre informazioni, vedere l'argomento [Procedure consigliate sull'uso di OLTP in memoria in un ambiente di VM](#bkmk_VMs).  
  
    ```sql  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     Per informazioni sui valori massimi per MAX_MEMORY_PERCENT, vedere la sezione dell'argomento che riporta le [percentuali di memoria disponibile per indici e tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
-   Aumentare **max server memory**.  
    Per informazioni sulla configurazione di **max server memory** vedere l'argomento [Opzioni di configurazione del server Server Memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
##  <a name="resolve-impact-of-low-memory-or-oom-conditions-on-the-workload"></a><a name="bkmk_recoverFromOOM"></a> Risoluzione dell'impatto delle condizioni di memoria insufficiente sul carico di lavoro  
 Ovviamente, è consigliabile non trovarsi in una situazione di memoria insufficiente. Una buona pianificazione e un buon monitoraggio consentono di evitare le situazioni di memoria insufficiente. Tuttavia, nonostante l'accurata pianificazione non sempre è possibile prevedere le effettive esigenze e potrebbero verificarsi situazioni di memoria insufficiente. Sono disponibili due passaggi per risolvere una situazione di memoria insufficiente:  
  
1.  [Aprire una connessione amministrativa dedicata (DAC)](#bkmk_openDAC)  
  
2.  [Intraprendere un'azione correttiva](#bkmk_takeCorrectiveAction)  

###  <a name="open-a-dac-dedicated-administrator-connection"></a><a name="bkmk_openDAC"></a> Aprire una connessione amministrativa dedicata (DAC)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre una connessione amministrativa dedicata (DAC). La connessione DAC consente a un amministratore di accedere a un'istanza in esecuzione del motore di database di SQL Server per risolvere i problemi presenti nel server, anche quando il server non risponde ad altre connessioni client. La connessione DAC è disponibile tramite l'utilità `sqlcmd` e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Per informazioni sull'uso della connessione DAC tramite SSMS o `sqlcmd`, vedere [Connessione di diagnostica per gli amministratori di database](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
###  <a name="take-corrective-action"></a><a name="bkmk_takeCorrectiveAction"></a> Intraprendere un'azione correttiva  
 Per risolvere la condizione di memoria insufficiente, è necessario liberare la memoria esistente riducendone l'utilizzo o rendere disponibile una maggiore quantità di memoria per le tabelle in memoria.  
  
#### <a name="free-up-existing-memory"></a>Liberare memoria esistente  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>Eliminare le righe non essenziali delle tabelle con ottimizzazione per la memoria e attendere la procedura di Garbage Collection  
 È possibile rimuovere le righe non essenziali da una tabella con ottimizzazione per la memoria. Il Garbage Collector restituisce la memoria usata da queste righe alla memoria disponibile. Il motore OLTP in memoria raccoglie rapidamente le righe di Garbage Collection. Tuttavia, una transazione con esecuzione prolungata può impedire il processo di Garbage Collection. Ad esempio, nel caso di una transazione in esecuzione per 5 minuti, le versioni di riga create a causa delle operazioni di aggiornamento/eliminazione mentre la transazione era attiva non possono essere sottoposte al processo di Garbage Collection.  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>Spostare una o più righe in una tabella basata su disco  
 Gli articoli di Technet riportati di seguito offrono istruzioni sullo spostamento di righe da una tabella ottimizzata per la memoria a una tabella basata su disco.  
  
-   [Partizionamento a livello di applicazione](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
  
-   [Modello di applicazione per il partizionamento di tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
#### <a name="increase-available-memory"></a>Aumentare la memoria disponibile  
  
##### <a name="increase-value-of-max_memory_percent-on-the-resource-pool"></a>Aumentare il valore di MAX_MEMORY_PERCENT nel pool di risorse  
 Se non è stato creato un pool di risorse denominato per le tabelle in memoria, è consigliabile eseguire tale operazione e associare al pool i database di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] . Per istruzioni sulla creazione e l'associazione dei database [a un pool di risorse, vedere l'argomento](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) Associazione di un database con tabelle con ottimizzazione per la memoria a un pool di risorse [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
 Se il database di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] è associato a un pool di risorse, è possibile aumentare la percentuale di memoria a cui il pool può accedere. Per informazioni sulla modifica del valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT per un pool di risorse, vedere l'argomento secondario [Cambiare MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT in un pool esistente](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) .  
  
 Aumentare il valore di MAX_MEMORY_PERCENT.   
Nel frammento di codice seguente il valore di MAX_MEMORY_PERCENT per il pool di risorse PoolHk viene modificato al 70% della memoria installata.  
  
> [!IMPORTANT]  
>  Se il server è in esecuzione in una VM e non è dedicato, impostare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT sullo stesso valore.   
> Per altre informazioni, vedere l'argomento [Procedure consigliate sull'uso di OLTP in memoria in un ambiente di VM](#bkmk_VMs).  
  
```sql  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor to enabled it
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
 Per informazioni sui valori massimi per MAX_MEMORY_PERCENT, vedere la sezione dell'argomento che riporta le [percentuali di memoria disponibile per indici e tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
##### <a name="install-additional-memory"></a>Installare memoria aggiuntiva  
 Infine, la soluzione migliore, se possibile, prevede l'installazione di ulteriore memoria fisica. In questo caso, tenere presente che probabilmente sarà possibile aumentare anche il valore di MAX_MEMORY_PERCENT (vedere l'argomento [Modificare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT in un pool esistente](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)) poiché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe non necessitare di ulteriore memoria, consentendo di rendere disponibile la maggior parte se non tutta la memoria appena installata per il pool di risorse.  
  
> [!IMPORTANT]  
>  Se il server è in esecuzione in una VM e non è dedicato, impostare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT sullo stesso valore.   
> Per altre informazioni, vedere l'argomento [Procedure consigliate sull'uso di OLTP in memoria in un ambiente di VM](#bkmk_VMs).  
  
##  <a name="resolve-page-allocation-failures-due-to-insufficient-memory-when-sufficient-memory-is-available"></a><a name="bkmk_PageAllocFailure"></a> Risoluzione degli errori di allocazione della pagina dovuti a memoria insufficiente quando è disponibile memoria sufficiente  
 Se viene restituito il messaggio di errore `Disallowing page allocations for database '*\<databaseName>*' due to insufficient memory in the resource pool '*\<resourcePoolName>*'. See 'https://go.microsoft.com/fwlink/?LinkId=330673' for more information.` nel log degli errori quando la memoria fisica disponibile è sufficiente per allocare la pagina, il problema può essere dovuto a Resource Governor disabilitato. Quando Resource Governor è disabilitato MEMORYBROKER_FOR_RESERVE genera richieste di memoria artificiali.  
  
 Per risolvere questo problema, è necessario abilitare Resource Governor.  
  
 Per informazioni sui limiti e sulle restrizioni e per istruzioni sull'abilitazione di Resource Governor usando Esplora oggetti, proprietà di Resource Governor o Transact-SQL, vedere [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md) .  
 
## <a name="best-practices-using-in-memory-oltp-in-a-vm-environment"></a><a name="bkmk_VMs"></a> Procedure consigliate sull'uso di OLTP in memoria in un ambiente di VM
La virtualizzazione del server può aiutare a ridurre i costi operativi e il capitale IT aumentandone l'efficienza grazie a provisioning di applicazioni, manutenzione, disponibilità e processi di backup/recupero migliorati. Grazie ai recenti progressi tecnologici, ora è possibile consolidare più rapidamente complessi carichi di lavoro del database utilizzando la virtualizzazione. Questo argomento illustra le procedure consigliate per l'uso di OLTP in memoria di SQL Server in un ambiente virtualizzato.

### <a name="memory-pre-allocation"></a>Preallocazione di memoria
Per la memoria in un ambiente virtualizzato, prestazioni e supporto migliorati sono fattori molto importanti. È necessario essere in grado di allocare rapidamente la memoria alle macchine virtuali a seconda dei requisiti e dei carichi di lavoro nonché di fare in modo che non ci siano sprechi di memoria. La funzionalità di memoria dinamica di Hyper-V migliora la flessibilità nell'allocazione e gestione della memoria tra le macchine virtuali in esecuzione in un host.

Quando si esegue la virtualizzazione di un database con tabelle ottimizzate per la memoria è necessario modificare alcune procedure consigliate per la virtualizzazione e la gestione di SQL Server. Senza tabelle ottimizzate per la memoria, due delle procedure consigliate sono:
-  Se si usa min server memory, è consigliabile assegnare solo la quantità di memoria necessaria in modo che rimanga memoria sufficiente per altri processi (evitando quindi il paging).
-  Non impostare un valore di preallocazione della memoria troppo elevato. In caso contrario, è possibile che non ci sia memoria sufficiente per altri processi che la richiedono, con conseguente paging della memoria.

Se si seguono le procedure sopra indicate per un database con tabelle ottimizzate per la memoria, un tentativo di ripristinare e recuperare il database potrebbe determinare lo stato di "Recupero in sospeso" anche se la quantità di memoria disponibile è sufficiente per il recupero del database. Il motivo è che all'avvio di OLTP in memoria i dati vengono inseriti nella memoria in maniera più drastica rispetto all'allocazione della memoria al database da parte dell'allocazione dinamica della memoria.

### <a name="resolution"></a>Risoluzione
Per risolvere questo problema, preallocare al database una quantità di memoria sufficiente per il recupero o il riavvio del database, anziché un valore minimo che si basa sulla memoria dinamica per ottenere memoria aggiuntiva se necessario.
  
## <a name="see-also"></a>Vedere anche  
 [Gestione della memoria per OLTP in memoria](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)   
 [Monitorare e risolvere i problemi relativi all'utilizzo della memoria](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)   
 [a un pool di risorse, vedere l'argomento](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Guida all'architettura di gestione della memoria](../../relational-databases/memory-management-architecture-guide.md)  
 [Opzioni di configurazione del server Server Memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) 
  
