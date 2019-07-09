---
title: Risolvere i problemi di memoria insufficiente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e31f36624e8923722612810836df5d2a57b6b686
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624404"
---
# <a name="resolve-out-of-memory-issues"></a>Risolvere i problemi di memoria insufficiente
  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] usa più memoria e in modi diversi rispetto a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile che la quantità di memoria installata e allocata per [!INCLUDE[hek_2](../../includes/hek-2-md.md)] diventi inadeguata con l'aumentare delle esigenze. In tal caso, è possibile che la memoria risulti insufficiente. In questo argomento viene descritto come risolvere una situazione di memoria insufficiente. Per le linee guida che consentono di evitare molte situazioni di memoria insufficiente, vedere [Monitorare e risolvere i problemi relativi all'utilizzo della memoria](monitor-and-troubleshoot-memory-usage.md) .  
  
## <a name="covered-in-this-topic"></a>Sezioni dell'argomento  
  
|Argomento|Panoramica|  
|-----------|--------------|  
| [Risoluzione degli errori di ripristino del database dovuti a memoria insufficiente](#resolve-database-restore-failures-due-to-oom) |Operazioni da eseguire se viene visualizzato il messaggio di errore "Operazione di ripristino non riuscita per il database ' *\<NomeDatabase>* '. Memoria insufficiente nel pool di risorse ' *\<NomePoolRisorse>* '."|  
| [Risoluzione dell'impatto delle condizioni di memoria insufficiente sul carico di lavoro](#resolve-impact-of-low-memory-or-oom-conditions-on-the-workload)|Operazioni da eseguire nel caso in cui i problemi di memoria insufficiente incidono negativamente sulle prestazioni.|  
| [Risoluzione degli errori di allocazione della pagina dovuti a memoria insufficiente quando è disponibile memoria sufficiente](#resolve-page-allocation-failures-due-to-insufficient-memory-when-sufficient-memory-is-available) |Operazioni da eseguire se viene visualizzato il messaggio di errore "È in corso la disabilitazione delle allocazioni di pagine per il database ' *\<NomeDatabase>* '. Memoria insufficiente nel pool di risorse ' *\<NomePoolRisorse>* '. ..." quando la memoria disponibile è sufficiente per l'operazione.|  
  
## <a name="resolve-database-restore-failures-due-to-oom"></a>Risoluzione degli errori di ripristino del database dovuti a memoria insufficiente  
 Quando si tenta di ripristinare un database è possibile ottenere il messaggio di errore: "Operazione non riuscita per il database di ripristino ' *\<databaseName >* 'a causa di memoria insufficiente nel pool di risorse' *\<Nomepoolrisorse >* '." Prima di poter ripristinare correttamente il database, è necessario risolvere il problema di memoria insufficiente rendendo disponibile una maggiore quantità di memoria.  
  
 Per risolvere l'errore di recupero a causa delle memoria insufficiente, aumentare la memoria disponibile usando uno o tutti questi metodi per aumentare temporaneamente la memoria disponibile per l'operazione di recupero.  
  
-   Chiudere temporaneamente le applicazioni in esecuzione.   
    Chiudendo una o più applicazioni in esecuzione, ad esempio Visual Studio, Internet Explorer, OneNote e altre, si libera la memoria usata da tali applicazioni rendendola disponibile per l'operazione di ripristino. È possibile riavviarle dopo il completamento del ripristino.  
  
-   Aumentare il valore di MAX_MEMORY_PERCENT.   
    Nel frammento di codice seguente il valore di MAX_MEMORY_PERCENT per il pool di risorse PoolHk viene modificato al 70% della memoria installata.  
  
    > [!IMPORTANT]  
    >  Se il server è in esecuzione in una VM e non è dedicato, impostare il valore di MIN_MEMORY_PERCENT sullo stesso valore di MAX_MEMORY_PERCENT.   
    > Vedere l'argomento [le procedure consigliate: Uso di OLTP In memoria in un ambiente di VM](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) per altre informazioni.  
  
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
  
     Per informazioni sui valori massimi per MAX_MEMORY_PERCENT, vedere la sezione dell'argomento [percentuale di memoria disponibile per indici e tabelle ottimizzate per la memoria](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#percent-of-memory-available-for-memory-optimized-tables-and-indexes)
  
-   Riconfigurare **max server memory**.  
    Per informazioni sulla configurazione di **max server memory** vedere l'argomento [Ottimizzazione delle prestazioni del server tramite le opzioni di configurazione della memoria](https://technet.microsoft.com/library/ms177455\(v=SQL.105\).aspx).  
  
## <a name="resolve-impact-of-low-memory-or-oom-conditions-on-the-workload"></a>Risoluzione dell'impatto delle condizioni di memoria insufficiente sul carico di lavoro  
 Ovviamente, è consigliabile non trovarsi in una situazione di memoria insufficiente. Una buona pianificazione e un buon monitoraggio consentono di evitare le situazioni di memoria insufficiente. Tuttavia, nonostante l'accurata pianificazione non sempre è possibile prevedere le effettive esigenze e potrebbero verificarsi situazioni di memoria insufficiente. Sono disponibili due passaggi per risolvere una situazione di memoria insufficiente:  
  
1.  [Aprire una connessione amministrativa dedicata (DAC)](#open-a-dac-dedicated-administrator-connection) 
  
2.  [Intraprendere un'azione correttiva](#take-corrective-action) 
  
### <a name="open-a-dac-dedicated-administrator-connection"></a>Aprire una connessione amministrativa dedicata (DAC)  
 Microsoft SQL Server fornisce una connessione amministrativa dedicata (DAC). La connessione DAC consente a un amministratore di accedere a un'istanza in esecuzione del motore di database di SQL Server per risolvere i problemi presenti nel server, anche quando il server non risponde ad altre connessioni client. La connessione DAC è disponibile tramite l'utilità `sqlcmd` e SQL Server Management Studio (SSMS).  
  
 Per informazioni sull'uso di `sqlcmd` e della connessione DAC, vedere [Utilizzo di una connessione amministrativa dedicata](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md). Per indicazioni sull'uso della connessione DAC tramite SSMS vedere [come: Usare la connessione amministrativa dedicata con SQL Server Management Studio](https://msdn.microsoft.com/library/ms178068.aspx).  
  
### <a name="take-corrective-action"></a>Intraprendere un'azione correttiva  
 Per risolvere la condizione di memoria insufficiente, è necessario liberare la memoria esistente riducendone l'utilizzo o rendere disponibile una maggiore quantità di memoria per le tabelle in memoria.  
  
#### <a name="free-up-existing-memory"></a>Liberare memoria esistente  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>Eliminare le righe non essenziali delle tabelle con ottimizzazione per la memoria e attendere la procedura di Garbage Collection  
 È possibile rimuovere le righe non essenziali da una tabella con ottimizzazione per la memoria. Il Garbage Collector restituisce la memoria usata da queste righe alla memoria disponibile. . Il motore OLTP in memoria raccoglie rapidamente le righe di Garbage Collection. Tuttavia, una transazione con esecuzione prolungata può impedire il processo di Garbage Collection. Ad esempio, nel caso di una transazione in esecuzione per 5 minuti, le versioni di riga create a causa delle operazioni di aggiornamento/eliminazione mentre la transazione era attiva non possono essere sottoposte al processo di Garbage Collection.  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>Spostare una o più righe in una tabella basata su disco  
 Gli articoli di Technet riportati di seguito offrono istruzioni sullo spostamento di righe da una tabella ottimizzata per la memoria a una tabella basata su disco.  
  
-   [Partizionamento a livello di applicazione](https://technet.microsoft.com/library/dn296452\(v=sql.120\).aspx)  
  
-   [Modello di applicazione per il partizionamento di tabelle con ottimizzazione per la memoria](https://technet.microsoft.com/library/dn133171\(v=sql.120\).aspx)  
  
#### <a name="increase-available-memory"></a>Aumentare la memoria disponibile  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>Aumentare il valore di MAX_MEMORY_PERCENT nel pool di risorse  
 Se non è stato creato un pool di risorse denominato per le tabelle in memoria, è consigliabile eseguire tale operazione e associare al pool i database di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] . Per istruzioni sulla creazione e l'associazione dei database [a un pool di risorse, vedere l'argomento](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) Associazione di un database con tabelle con ottimizzazione per la memoria a un pool di risorse [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
 Se il database di [!INCLUDE[hek_2](../../includes/hek-2-md.md)] è associato a un pool di risorse, è possibile aumentare la percentuale di memoria a cui il pool può accedere. Per informazioni sulla modifica del valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT per un pool di risorse, vedere l'argomento secondario [Cambiare MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT in un pool esistente](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#change-min-memory-percent-and-max-memory-percent-on-an-existing-pool) .  
  
 Aumentare il valore di MAX_MEMORY_PERCENT.   
Nel frammento di codice seguente il valore di MAX_MEMORY_PERCENT per il pool di risorse PoolHk viene modificato al 70% della memoria installata.  
  
> [!IMPORTANT]  
>  Se il server è in esecuzione in una VM e non è dedicato, impostare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT sullo stesso valore.   
> Vedere l'argomento [le procedure consigliate: Uso di OLTP In memoria in un ambiente di VM](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) per altre informazioni.  
  
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
  
 Per informazioni sui valori massimi per MAX_MEMORY_PERCENT, vedere la sezione dell'argomento che riporta le [percentuali di memoria disponibile per indici e tabelle ottimizzate per la memoria](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#percent-of-memory-available-for-memory-optimized-tables-and-indexes).  
  
##### <a name="install-additional-memory"></a>Installare memoria aggiuntiva  
 Infine, la soluzione migliore, se possibile, prevede l'installazione di ulteriore memoria fisica. In questo caso, tenere presente che probabilmente sarà possibile aumentare anche il valore di MAX_MEMORY_PERCENT (vedere l'argomento [Modificare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT in un pool esistente](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#change-min-memory-percent-and-max-memory-percent-on-an-existing-pool)) poiché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe non necessitare di ulteriore memoria, consentendo di rendere disponibile la maggior parte se non tutta la memoria appena installata per il pool di risorse.  
  
> [!IMPORTANT]  
>  Se il server è in esecuzione in una VM e non è dedicato, impostare il valore di MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT sullo stesso valore.   
> Vedere l'argomento [le procedure consigliate: Uso di OLTP In memoria in un ambiente di VM](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) per altre informazioni.  
  
## <a name="resolve-page-allocation-failures-due-to-insufficient-memory-when-sufficient-memory-is-available"></a>Risoluzione degli errori di allocazione della pagina dovuti a memoria insufficiente quando è disponibile memoria sufficiente  
 Se viene visualizzato il messaggio di errore "corso la disabilitazione delle allocazioni di pagine per il database ' *\<databaseName >* 'a causa di memoria insufficiente nel pool di risorse' *\<Nomepoolrisorse >* '. Vedere '<https://go.microsoft.com/fwlink/?LinkId=330673>' per ulteriori informazioni. " nel log degli errori quando la memoria fisica disponibile è sufficiente per allocare pagina, il problema può essere dovuto a Resource Governor disabilitato. Quando Resource Governor è disabilitato MEMORYBROKER_FOR_RESERVE genera richieste di memoria artificiali.  
  
 Per risolvere questo problema, è necessario abilitare Resource Governor.  
  
 Per informazioni sui limiti e sulle restrizioni e per istruzioni sull'abilitazione di Resource Governor usando Esplora oggetti, proprietà di Resource Governor o Transact-SQL, vedere [Abilitare Resource Governor](https://technet.microsoft.com/library/bb895149.aspx) .  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione della memoria per OLTP in memoria](../../database-engine/managing-memory-for-in-memory-oltp.md)   
 [Monitorare e risolvere i problemi relativi all'utilizzo della memoria](monitor-and-troubleshoot-memory-usage.md)   
 [a un pool di risorse, vedere l'argomento](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Procedure consigliate: Uso di OLTP In memoria in un ambiente di VM](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)  
  
  
