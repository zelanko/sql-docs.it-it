---
title: Memorizzazione nella cache, aggiornamento e prestazioni di Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- cache [SQL Server], replication
- Replication Monitor, caching
- refreshing data
- Replication Monitor, refreshing
ms.assetid: a2d8b666-ed41-4f86-b2b8-c8e118416ab7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: afa70f42c2ea5602bf549a4d5596bff2c8bbff66
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54123881"
---
# <a name="caching-refresh-and-replication-monitor-performance"></a>Memorizzazione nella cache, aggiornamento e prestazioni di Monitoraggio replica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Monitoraggio replica di[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è progettato per monitorare in modo efficiente un numero elevato di computer all'interno di un sistema di produzione. Le query utilizzate in Monitoraggio replica per eseguire calcoli e raccogliere dati vengono memorizzate nella cache e aggiornate con frequenza periodica. La memorizzazione nella cache riduce il numero di query e di calcoli necessari durante la visualizzazione di pagine diverse in Monitoraggio replica e consente di monitorare più utenti in modo efficiente.  
  
 L'aggiornamento della cache è gestito da un processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent denominato **Aggiornamento monitoraggio replica per distribuzione**. Il processo è impostato per l'esecuzione continua, ma la pianificazione dell'aggiornamento della cache è basata sull'attesa di una certa quantità di tempo dall'aggiornamento precedente:  
  
-   Se dopo l'ultima creazione della cache la cronologia dell'agente ha subito modifiche, il tempo di attesa sarà il valore minimo tra 4 secondi e la quantità di tempo impiegata per creare la cache precedente.  
  
-   Se dopo l'ultima creazione della cache la cronologia dell'agente non ha subito modifiche (ma possono essersi verificate modifiche di altro tipo), il tempo di attesa sarà il valore massimo tra 30 secondi e la quantità di tempo impiegata per creare la cache precedente.  
  
## <a name="refreshing-the-replication-monitor-user-interface"></a>Aggiornamento dell'interfaccia utente di Monitoraggio replica  
 L'interfaccia utente di Monitoraggio replica può essere aggiornata nei modi seguenti:  
  
-   La finestra principale di Monitoraggio replica, comprese tutte le schede, viene aggiornata automaticamente ogni cinque secondi per impostazione predefinita. Gli aggiornamenti automatici non forzano un aggiornamento della cache. Nell'interfaccia utente viene visualizzata la versione più recente dei dati della cache. È possibile personalizzare la frequenza di aggiornamento utilizzata per tutte le finestre associate a un server di pubblicazione modificando le impostazioni di quest'ultimo. È inoltre possibile disabilitare gli aggiornamenti automatici per un server di pubblicazione.  
  
-   Le finestre dei dettagli che vengono avviate da Monitoraggio replica non vengono aggiornate automaticamente per impostazione predefinita, ad eccezione delle finestre relative alle sottoscrizioni di tipo merge di cui viene eseguita la sincronizzazione. Se si specifica che le finestre dei dettagli devono essere aggiornate automaticamente, l'aggiornamento seguirà la stessa pianificazione della finestra principale di Monitoraggio replica.  
  
-   Tutte le finestre possono essere aggiornate manualmente premendo F5 o facendo clic con il pulsante destro del mouse su un nodo dell'albero di Monitoraggio replica e quindi scegliendo **Aggiorna**. Gli aggiornamenti manuali forzano un aggiornamento della cache.  
  
 Per altre informazioni, vedere [Aggiornare i dati in Monitoraggio replica](../../../relational-databases/replication/monitor/refresh-data-in-replication-monitor.md).  
  
## <a name="performance-considerations"></a>Considerazioni sulle prestazioni  
 Sebbene Monitoraggio replica sia progettato per un funzionamento efficiente, considerare gli aspetti seguenti:  
  
-   Se si dispone di una quantità elevata di pubblicazioni o sottoscrizioni, è consigliabile pianificare aggiornamenti automatici meno frequenti per l'interfaccia utente.  
  
-   Evitare di eseguire simultaneamente più istanze di Monitoraggio replica.  
  
-   Evitare di registrare una quantità elevata di server di distribuzione e di configurare Monitoraggio replica affinché si connetta automaticamente a tutti.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire processi di manutenzione della replica &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [Monitoraggio della replica](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
