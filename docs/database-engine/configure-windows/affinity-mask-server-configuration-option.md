---
title: Opzione di configurazione del server affinity mask
description: Informazioni sull'opzione affinity mask in SQL Server. Visualizzare un esempio che usa questa opzione per associare i processori a thread specifici.
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default affinity mask option
- reloading processor cache
- processor cache [SQL Server]
- CPU [SQL Server], licensing
- deferred process call
- affinity mask option
- processor affinity [SQL Server]
- SMP
- DPC
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: 94f8406af013bc0720bc16063d1a9881eda94c5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715590"
---
# <a name="affinity-mask-server-configuration-option"></a>Opzione di configurazione del server affinity mask

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

> [!NOTE]
> [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare invece [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).

Per eseguire il multitasking, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sposta talvolta thread tra processori diversi. Anche se in questo modo viene garantita una maggiore efficienza del sistema operativo, questa attività può comportare una riduzione delle prestazioni di SQL Server nel caso di carichi di lavoro elevati, poiché la cache di ogni processore viene ricaricata più volte con dati. L'assegnazione di processori a thread specifici può migliorare le prestazioni in base a queste condizioni eliminando il ricaricamento dei processori e riducendo la migrazione dei thread tra i processori, riducendo così il cambio di contesto. Tale associazione tra un thread e un processore è nota come affinità dei processori.

SQL Server supporta l'affinità dei processori tramite due opzioni di maschera di affinità: affinity mask (nota anche come **maschera di affinità della CPU**) e affinity I/O mask. Per altre informazioni sull'opzione affinity I/O mask, vedere [Opzione di configurazione del server affinity Input-Output mask](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md). Il supporto di Affinity CPU e I/O per server con 33 fino a 64 processori richiede rispettivamente l'uso aggiuntivo dell'[opzione di configurazione del server affinity64 mask](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) e dell'[opzione di configurazione del server affinity64 Input-Output mask](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md).

> [!NOTE]  
> Il supporto dell'affinità nei server dotati di un numero di processori compreso tra 33 e 64 è disponibile solo su sistemi operativi a 64 bit.

L'opzione affinity mask, già disponibile nelle versioni precedenti di SQL Server, controlla in modo dinamico l'affinità della CPU.

In SQL Server è possibile configurare l'opzione affinity mask senza che sia necessario riavviare l'istanza di SQL Server. Quando si usa sp_configure è necessario eseguire RECONFIGURE oppure RECONFIGURE WITH OVERRIDE dopo aver impostato un'opzione di configurazione. Se si usa [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], la modifica dell'opzione affinity mask non richiede il riavvio.

Le modifiche alle maschere di affinità vengono eseguite in modo dinamico, consentendo l'avvio e l'arresto su richiesta delle utilità di pianificazione della CPU che associano i thread dei processi all'interno di SQL Server. Questa situazione si può verificare quando le condizioni nel server vengono modificate. Ad esempio, se nel server viene aggiunta una nuova istanza di SQL Server, potrebbe essere necessario modificare l'opzione affinity mask per ridistribuire il carico dei processori.

Per le modifiche alle maschere di bit di affinità, è necessario che SQL Server abiliti una nuova utilità di pianificazione della CPU e disabiliti quella esistente. È quindi possibile elaborare nuovi batch nelle nuove utilità di pianificazione o in quelle rimanenti.

Per avviare una nuova utilità di pianificazione della CPU, SQL Server crea una nuova utilità di pianificazione e la aggiunge all'elenco di quelle standard. La nuova utilità di pianificazione viene presa in considerazione unicamente per i nuovi batch in entrata. L'esecuzione dei batch correnti continua nella stessa utilità di pianificazione. I thread di lavoro migrano alla nuova utilità di pianificazione man mano che si liberano o che ne vengono creati di nuovi.

Per chiudere un'utilità di pianificazione, è necessario che tutti i batch nell'utilità abbiano completato le relative attività e interrompano l'esecuzione. Un'utilità di pianificazione che è stata chiusa viene contrassegnata come offline, in modo che non venga pianificato alcun nuovo batch su di essa.

Se viene aggiunta o rimossa una nuova utilità di pianificazione, le attività di sistema permanenti quali monitoraggio dei blocchi, checkpoint, i thread delle attività di sistema (DTC di elaborazione) e il processo di segnalazione proseguono l'esecuzione mentre il server è operativo. Queste attività di sistema permanenti non eseguono la migrazione in modo dinamico. Per ridistribuire il carico del processore per queste attività tra le utilità di pianificazione, è necessario riavviare l'istanza di SQL Server. Se SQL Server tenta di chiudere un'utilità di pianificazione associata a un'attività di sistema permanente, l'esecuzione dell'attività continua nell'utilità di pianificazione offline (nessuna migrazione). L'utilità di pianificazione è associata ai processori nella maschera di affinità modificata e non dovrebbe applicare alcun carico al processore al quale è stata associata prima della modifica. La presenza di utilità di pianificazione offline aggiuntive non dovrebbe influire in modo significativo sul carico del sistema. In tal caso, è necessario riavviare il server di database per riconfigurare queste attività nelle utilità di pianificazione disponibili con la maschera di affinità modificata.

Non impostare i valori di configurazione 'affinity mask' è 'affinity I/O mask' di SQL Server per l'uso delle stesse CPU. Le prestazioni possono risentirne se si sceglie di associare un processore sia per la pianificazione dei thread di lavoro sia per l'elaborazione di I/O di SQL Server. Assicurarsi pertanto che i valori di configurazione non siano impostati per lo stesso processore. La stessa raccomandazione si applica alle opzioni "affinity64 mask" e "affinity64 I/O mask".  Per garantire che la nuova maschera di affinità non si sovrapponga alla maschera di affinità di I/O, il comando [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) verifica che le normali affinità di CPU e I/O si escludano a vicenda. In caso contrario, nella sessione del client e nel log degli errori di SQL Server viene visualizzato un messaggio di errore che indica che l'impostazione non è consigliata.

```sql
 Msg 5834, Level 16, State 1, Line 1
 The affinity mask specified conflicts with the IO affinity mask specified. Use the override option to force this configuration
```

Per consentire affinità di CPU e di I/O che si sovrappongono e non si escludono a vicenda, è possibile eseguire le opzioni RECONFIGURE WITH OVERRIDE.  

La maschera di affinità di I/O influisce direttamente sui processi di affinità di I/O, ad esempio i processi Lazywriter e i thread per la scrittura nel log. Se i processi Lazywriter e i thread per la scrittura nel log non sono associati, essi seguono le stesse regole definite per le attività permanenti, ad esempio monitoraggio dei blocchi o checkpoint.
Se si specifica una maschera di affinità che tenta di eseguire il mapping a una CPU non esistente, il comando RECONFIGURE visualizza un messaggio di errore nella sessione client e nel log degli errori di SQL Server. In questo caso, l'utilizzo dell'opzione RECONFIGURE WITH OVERRIDE non avrà alcun effetto e verrà visualizzato di nuovo lo stesso errore di configurazione.

È anche possibile escludere l'attività di SQL Server da assegnazioni di carichi di lavoro specifici del sistema operativo Windows. Se si imposta su 1 un bit corrispondente a un processore, il processore viene selezionato dal motore di database di SQL Server per l'assegnazione di thread. Se si imposta **affinity mask** su 0 (impostazione predefinita), l'affinità del thread viene impostata dagli algoritmi di pianificazione di Microsoft Windows. Se l'opzione della **affinity mask** viene impostata su un valore diverso da zero, l'affinità di SQL Server interpreta il valore come maschera di bit che indica che i processori sono selezionabili.  

L'esclusione dei thread di SQL Server da processori specifici consente a Microsoft Windows di valutare adeguatamente la gestione dei processi specifici di Windows. Ad esempio, per un server con 8 CPU nel quale sono in esecuzione due istanze di SQL Server (istanza A e B), l'amministratore di sistema può usare l'opzione affinity mask per assegnare il primo set di 4 CPU all'istanza A e il secondo set di 4 CPU all'istanza B. Per configurare più di 32 processori, impostare entrambe le opzioni affinity mask e affinity64 mask. I valori della **affinity mask** sono i seguenti:

- Un' **affinity mask** da un byte copre fino a 8 CPU in un computer multiprocessore.

- Un' **affinity mask** da due byte copre fino a 16 CPU in un computer multiprocessore.

- Un' **affinity mask** da tre byte copre fino a 24 CPU in un computer multiprocessore.

- Un' **affinity mask** da quattro byte copre fino a 32 CPU in un computer multiprocessore.

- Per coprire più di 32 CPU, configurare un valore affinity mask da 4 byte per le prime 32 CPU e un valore affinity64 mask da 4 byte per le CPU rimanenti.

L'impostazione dell'affinità processori di SQL Server è un'operazione estremamente complessa, pertanto è consigliabile eseguirla unicamente se è necessario. Nella maggior parte dei casi, l'affinità predefinita di Microsoft Windows offre le migliori prestazioni. Quando si impostano le maschere di affinità, tenere in considerazione i requisiti delle CPU delle altre applicazioni. Per ulteriori informazioni, consultare la documentazione di Windows.

> [!NOTE]
> Per visualizzare e analizzare l'utilizzo dei singoli processori, è possibile utilizzare Monitor di sistema di Windows.

Quando si specifica l'opzione affinity I/O mask, è necessario usarla insieme all'opzione di configurazione affinity mask. Come già accennato in precedenza, non abilitare la stessa CPU sia nell'opzione **affinity mask** che nell'opzione affinity I/O mask. Lo stato dei bit corrispondenti a ogni CPU deve essere uno dei tre seguenti:

- 0 in entrambe le opzioni affinity mask e affinity I/O mask.

- 1 nell'opzione affinity mask e 0 nell'opzione affinity I/O mask.

- 0 nell'opzione affinity mask e 1 nell'opzione affinity I/O mask.

> [!CAUTION]
> Non configurare l'affinità della CPU nel sistema operativo Windows e contemporaneamente l'opzione affinity mask in SQL Server. Le due impostazioni mirano a ottenere lo stesso risultato e, se le configurazioni sono incoerenti, potrebbero causare risultati imprevisti. La configurazione ottimale dell'affinità della CPU di SQL Server può essere ottenuta usando l'opzione sp_configure in SQL Server.

## <a name="example"></a>Esempio

Si supponga di configurare l'opzione affinity mask. Se, ad esempio, i processori 1, 2 e 5 sono selezionati come disponibili tramite l'impostazione dei bit 1, 2 e 5 su 1 e l'impostazione dei bit 0, 3, 4, 6 e 7 su 0, deve essere usato il valore esadecimale 0x26 oppure l'equivalente decimale di 38. Numerare le posizioni dei bit da destra a sinistra.

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'affinity mask', 38;
RECONFIGURE;
GO
```

Di seguito sono riportati i valori dell' **affinity mask** per un sistema con 8 CPU.  

|Valore decimale|Maschera di bit binaria|Numeri dei processori in cui vengono eseguiti i thread di SQL Server|  
|-------------------|---------------------|--------------------------------------------|  
|1|00000001|0|  
|3|00000011|0 e 1|  
|7|00000111|0, 1 e 2|  
|15|00001111|0, 1, 2 e 3|  
|31|00011111|0, 1, 2, 3 e 4|  
|63|00111111|0, 1, 2, 3, 4 e 5|  
|127|01111111|0, 1, 2, 3, 4, 5 e 6|  
|255|11111111|0, 1, 2, 3, 4, 5, 6 e 7|  

affinity mask è un'opzione avanzata. Se si usa la stored procedure di sistema sp_configure per modificare l'impostazione, è possibile modificare l'opzione **affinity mask** solo quando il valore di **show advanced options** è impostato su 1. Dopo aver eseguito il comando [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE, la nuova impostazione viene applicata immediatamente senza che sia necessario riavviare l'istanza di SQL Server.  

## <a name="non-uniform-memory-access-numa"></a>NUMA (Non-Uniform Memory Access)

Quando si usa hardware basato sulla configurazione NUMA ed è impostata l'opzione affinity mask, tutte le utilità di pianificazione di un nodo verranno associate alla rispettiva CPU. Quando l'opzione affinity mask non è impostata, ogni utilità di pianificazione viene associata al gruppo di CPU contenute nel nodo NUMA. Un'utilità di pianificazione di cui viene eseguito il mapping al nodo NUMA N1 potrà pianificare operazioni in qualsiasi CPU del nodo, ma non nelle CPU associate a un altro nodo.  

Le operazioni eseguite in un solo nodo NUMA possono utilizzare solo pagine del buffer di tale nodo. Quando un'operazione viene eseguita in parallelo sulle CPU di più nodi, è possibile utilizzare la memoria di tutti i nodi coinvolti.  
  
## <a name="licensing-issues"></a>Problemi relativi alle licenze

L'affinità dinamica è strettamente correlata alle licenze per le CPU. SQL Server non consente di configurare le opzioni affinity mask in modo da violare i criteri di licenza.  

### <a name="startup"></a>Avvio

Se un'opzione affinity mask specificata viola i criteri di licenza durante l'avvio di SQL Server o durante il collegamento di database, il livello del motore completerà il processo di avvio o l'operazione di collegamento o ripristino del database e successivamente reimposterà il valore di esecuzione di sp_configure per l'opzione affinity mask su zero, visualizzando un messaggio di errore nel log degli errori di SQL Server.  
  
### <a name="reconfigure"></a>Riconfigurare

Se un'opzione affinity mask specificata viola i criteri di licenza durante l'esecuzione del comando [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE, nella sessione client e nel log degli errori di SQL Server verrà visualizzato un messaggio di errore che richiede all'amministratore del database di riconfigurare l'opzione. In questo caso il comando RECONFIGURE WITH OVERRIDE non verrà accettato.  

## <a name="next-steps"></a>Passaggi successivi

- [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
- [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
- [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
- [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)
