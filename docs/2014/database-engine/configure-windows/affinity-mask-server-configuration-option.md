---
title: Opzione di configurazione del server affinity mask | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a041171d9639429196b09b7a1f9254a30907ab2e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62814035"
---
# <a name="affinity-mask-server-configuration-option"></a>Opzione di configurazione del server affinity mask
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare invece [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql).  
  
 Per eseguire il multitasking, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sposta talvolta thread tra processori diversi. Sebbene in questo modo venga garantita una maggiore efficienza del sistema operativo, questa attività può comportare una riduzione delle prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel caso di carichi di lavoro elevati, poiché la cache di ogni processore viene ricaricata più volte con dati. In tali casi, l'assegnazione dei processori a thread specifici consente di aumentare le prestazioni, in quanto le operazioni di ricaricamento dei processori vengono eliminate e si riduce la migrazione dei thread tra i processori, limitando lo scambio di contesto. Questo tipo di associazione tra un thread e un processore è definito "affinità processori".  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'affinità processori tramite due opzioni Affinity mask: Affinity mask (nota anche come **Affinity CPU mask**) e Affinity I/O mask. Per altre informazioni sull'opzione Affinity I/O mask, vedere [Opzione di configurazione del server Affinity Input-Output](affinity-input-output-mask-server-configuration-option.md). Il supporto di Affinity CPU e I/O per server con 33 fino a 64 processori richiede rispettivamente l'uso aggiuntivo dell'[opzione di configurazione del server affinity64 mask](affinity64-mask-server-configuration-option.md) e dell'[opzione di configurazione del server affinity64 Input-Output mask](affinity64-input-output-mask-server-configuration-option.md).  
  
> [!NOTE]  
>  Il supporto dell'affinità nei server dotati di un numero di processori compreso tra 33 e 64 è disponibile solo su sistemi operativi a 64 bit.  
  
 L'opzione affinity mask, disponibile nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], controlla in modo dinamico l'affinità di CPU.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile configurare l'opzione affinity mask senza che sia necessario riavviare l'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando si utilizza sp_configure è necessario eseguire RECONFIGURE oppure RECONFIGURE WITH OVERRIDE dopo aver impostato un'opzione di configurazione. Se si utilizza [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], la modifica dell'opzione affinity mask non richiede il riavvio.  
  
 Le modifiche alle maschere di affinità vengono eseguite in modo dinamico, consentendo l'avvio e l'arresto a richiesta delle utilità di pianificazione della CPU che associano i thread dei processi all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa situazione si può verificare quando le condizioni nel server vengono modificate. Ad esempio, se nel server viene aggiunta una nuova istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], potrebbe essere necessario modificare l'opzione affinity mask per ridistribuire il carico dei processori.  
  
 Per le modifiche alle maschere di bit di affinità, è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abiliti una nuova utilità di pianificazione della CPU e disabiliti quella esistente. È quindi possibile elaborare nuovi batch nelle nuove utilità di pianificazione o in quelle rimanenti.  
  
 Per avviare una nuova utilità di pianificazione della CPU, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una nuova utilità di pianificazione e la aggiunge all'elenco di quelle standard. La nuova utilità di pianificazione viene presa in considerazione unicamente per i nuovi batch in entrata. L'esecuzione dei batch correnti continua nella stessa utilità di pianificazione. I thread di lavoro migrano alla nuova utilità di pianificazione man mano che si liberano o che ne vengono creati di nuovi.  
  
 Per chiudere un'utilità di pianificazione, è necessario che tutti i batch nell'utilità abbiano completato le relative attività e interrompano l'esecuzione. Un'utilità di pianificazione che è stata chiusa viene contrassegnata come offline, in modo che non venga pianificato alcun nuovo batch su di essa.  
  
 Se viene aggiunta o rimossa una nuova utilità di pianificazione, le attività di sistema permanenti quali lockmonitor, checkpoint, i thread delle attività di sistema (elaborazione DTC) e signal process proseguono l'esecuzione mentre il server è operativo. Queste attività di sistema permanenti non eseguono la migrazione in modo dinamico. Per ridistribuire il carico del processore di queste attività nelle utilità di pianificazione, è necessario riavviare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta di chiudere un'utilità di pianificazione associata a un'attività di sistema permanente, l'esecuzione dell'attività continua nell'utilità di pianificazione offline (nessuna migrazione). L'utilità di pianificazione è associata ai processori nella maschera di affinità modificata e non dovrebbe applicare alcun carico al processore con il quale è stata creata l'affinità prima della modifica. La presenza di utilità di pianificazione offline aggiuntive non dovrebbe influire in modo significativo sul carico del sistema. In caso contrario, per riconfigurare queste attività è necessario riavviare il server di database.  
  
 La maschera di affinità di I/O influisce direttamente sui processi di affinità di I/O, ad esempio i processi Lazywriter e i thread per la scrittura nel log. Se per i processi Lazywriter e i thread per la scrittura nel log non viene creata un'affinità, essi seguono le stesse regole definite per le attività permanenti, ad esempio lockmonitor o checkpoint.  
  
 Per garantire che la nuova maschera di affinità sia valida, il comando RECONFIGURE verifica che le affinità di CPU e I/O si escludano a vicenda. In caso contrario, nella sessione del client e nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene visualizzato un messaggio di errore che indica che l'impostazione non è corretta. Per consentire affinità di CPU e di I/O che non si escludono a vicenda, è possibile eseguire le opzioni RECONFIGURE WITH OVERRIDE.  
  
 Se si specifica una maschera di affinità che tenta di eseguire il mapping a una CPU non esistente, il comando RECONFIGURE visualizza un messaggio di errore nella sessione client e nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questo caso, l'utilizzo dell'opzione RECONFIGURE WITH OVERRIDE non avrà alcun effetto e verrà visualizzato di nuovo lo stesso errore di configurazione.  
  
 È inoltre possibile escludere l'attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da processori ai quali sono stati assegnati carichi di lavoro specifici nei sistemi operativi Windows 2000 o Windows Server 2003. Se si imposta su 1 un bit corrispondente a un processore, il processore viene selezionato dal Motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'assegnazione di thread. Quando si imposta `affinity mask` su 0 (impostazione predefinita), l'affinità del thread viene impostata dagli algoritmi di pianificazione di Microsoft Windows 2000 o windows Server 2003. Se l'opzione `affinity mask` viene impostata su un valore diverso da zero, l'affinità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta il valore come maschera di bit indicante i processori selezionabili.  
  
 L'esclusione dei thread [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da processori specifici consente a Microsoft Windows 2000 o Windows Server 2003 di valutare adeguatamente la gestione dei processi specifici di Windows. Ad esempio, per un server con 8 CPU nel quale sono in esecuzione due istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (istanza A e B), l'amministratore di sistema può utilizzare l'opzione affinity mask per assegnare il primo set di 4 CPU all'istanza A e il secondo set di 4 CPU all'istanza B. Per configurare più di 32 processori, impostare entrambe le opzioni affinity mask e affinity64 mask. I valori per l'opzione `affinity mask` sono i seguenti:  
  
-   Un valore `affinity mask` da 1 byte comprende fino a 8 CPU in un computer multiprocessore.  
  
-   Un valore `affinity mask` da 2 byte consente di coprire fino a 16 CPU in un computer multiprocessore.  
  
-   Un valore `affinity mask` da 3 byte consente di coprire fino a 24 CPU in un computer multiprocessore.  
  
-   Un valore `affinity mask` da 4 byte consente di coprire fino a 32 CPU in un computer multiprocessore.  
  
-   Per coprire più di 32 CPU, configurare un valore affinity mask da 4 byte per le prime 32 CPU e un valore affinity64 mask da 4 byte per le CPU rimanenti.  
  
 L'impostazione dell'affinità processori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un'operazione estremamente complessa, pertanto è consigliabile eseguirla unicamente se è necessario. Nella maggior parte dei casi, l'affinità predefinita di Microsoft Windows 2000 o Windows Server 2003 offre le migliori prestazioni. Quando si impostano le maschere di affinità, è inoltre consigliabile tenere in considerazione i requisiti delle CPU delle altre applicazioni. Per ulteriori informazioni, consultare la documentazione di Windows.  
  
> [!NOTE]  
>  Per visualizzare e analizzare l'utilizzo dei singoli processori, è possibile utilizzare Monitor di sistema di Windows.  
  
 Quando si specifica l'opzione affinity I/O mask, essa deve essere utilizzata insieme all'opzione di configurazione affinity mask. Non abilitare la stessa CPU in entrambe le opzioni `affinity mask` e affinity I/O mask. Lo stato dei bit corrispondenti a ogni CPU deve essere uno dei tre seguenti:  
  
-   0 in entrambe le opzioni affinity mask e affinity I/O mask.  
  
-   1 nell'opzione affinity mask e 0 nell'opzione affinity I/O mask.  
  
-   0 nell'opzione affinity mask e 1 nell'opzione affinity I/O mask.  
  
> [!CAUTION]  
>  Non configurare l'affinità di CPU nel sistema operativo Windows e contemporaneamente l'opzione affinity mask in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le due impostazioni mirano a ottenere lo stesso risultato e, se le configurazioni sono incoerenti, potrebbero causare risultati imprevisti. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La configurazione ottimale dell'affinità di CPU in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere ottenuta usando l'opzione sp_configure.  
  
## <a name="example"></a>Esempio  
 Si supponga di configurare l'opzione affinity mask. Se, ad esempio, i processori 1, 2 e 5 sono selezionati come disponibili tramite l'impostazione dei bit 1, 2 e 5 su 1 e l'impostazione dei bit 0, 3, 4, 6 e 7 su 0, viene specificato il valore esadecimale 0x26 oppure l'equivalente decimale `38` . Numerare i bit da destra a sinistra. L'opzione affinity mask inizia a contare i processori da 0 a 31. Nell'esempio seguente il contatore `1` rappresenta il secondo processore nel server.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'affinity mask', 38;  
RECONFIGURE;  
GO  
```  
  
 Di seguito sono riportati i valori `affinity mask` per un sistema con 8 CPU.  
  
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
  
 affinity mask è un'opzione avanzata. Se si utilizza il sistema sp_configure stored procedure per modificare l'impostazione, è possibile modificare `affinity mask` solo quando il valore di **Show Advanced Options** è impostato su 1. Dopo aver eseguito il comando [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE, la nuova impostazione viene applicata immediatamente senza che sia necessario riavviare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="non-uniform-memory-access-numa"></a>Configurazione NUMA (Non-Uniform Memory Access)  
 Quando si utilizza hardware basato sulla configurazione NUMA ed è impostata l'opzione affinity mask, verrà creata un'affinità fra tutte le utilità di pianificazione di un nodo e la rispettiva CPU. Quando l'opzione affinity mask non è impostata, viene creata un'affinità tra le utilità di pianificazione e il gruppo di CPU contenute nel nodo NUMA. Un'utilità di pianificazione di cui viene eseguito il mapping al nodo NUMA N1 potrà pianificare operazioni in qualsiasi CPU del nodo, ma non nelle CPU associate a un altro nodo.  
  
 Le operazioni eseguite in un solo nodo NUMA possono utilizzare solo pagine del buffer di tale nodo. Quando un'operazione viene eseguita in parallelo sulle CPU di più nodi, è possibile utilizzare la memoria di tutti i nodi coinvolti.  
  
## <a name="licensing-issues"></a>Problemi relativi alle licenze  
 L'affinità dinamica è strettamente correlata alle licenze per le CPU. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente di configurare le opzioni affinity mask in modo da violare i criteri di licenza.  
  
### <a name="startup"></a>Avvio  
 Se un'opzione affinity mask specificata viola i criteri di licenza durante l'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o durante il collegamento di database, il livello del motore completerà il processo di avvio o l'operazione di collegamento o ripristino del database e successivamente reimposterà il valore di esecuzione di sp_configure per l'opzione affinity mask su zero, visualizzando un messaggio di errore nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="reconfigure"></a>Riconfigurare  
 Se un'opzione affinity mask specificata viola i criteri di licenza durante l'esecuzione del comando [!INCLUDE[tsql](../../includes/tsql-md.md)] RECONFIGURE, nella sessione client e nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà visualizzato un messaggio di errore che richiede all'amministratore del database di riconfigurare l'opzione. In questo caso il comando RECONFIGURE WITH OVERRIDE non verrà accettato.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
