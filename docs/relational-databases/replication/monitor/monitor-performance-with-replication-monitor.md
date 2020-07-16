---
title: Monitorare le prestazioni con Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Log Reader Agent, monitoring
- Replication Monitor, performance
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication]
ms.assetid: f212397d-1bfd-496b-a246-668952891d09
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: a2894c2b9919f3f270bad4407a70ef9aedda5223
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86159819"
---
# <a name="monitor-performance-with-replication-monitor"></a>Monitoraggio delle prestazioni con Monitoraggio replica
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
  Monitoraggio replica di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di monitorare le prestazioni della replica transazionale e della replica di tipo merge nei modi seguenti:  
  
-   Impostazione di avvisi e soglie  
  
-   Visualizzazione delle misurazioni delle prestazioni  
  
-   Determinazione della latenza con token di traccia (replica transazionale)  
  
-   Visualizzazione di statistiche dettagliate sulla sincronizzazione (replica di tipo merge)  
  
-   Visualizzazione di transazioni e tempi di recapito (replica transazionale)  
  
## <a name="set-warnings-and-thresholds"></a>Impostazione di avvisi e soglie  
 Monitoraggio replica consente di abilitare avvisi in relazione a varie condizioni delle prestazioni. Quando si attiva un avviso, si specifica una soglia. Quando tale soglia viene raggiunta o superata, viene visualizzato un avviso nella colonna **Stato** della sottoscrizione e della pubblicazione associate nella sincronizzazione (a meno che non sia necessario visualizzare un problema con una priorità più elevata). Oltre a visualizzare un avviso in Monitoraggio replica, il raggiungimento di un valore soglia può inoltre attivare un messaggio di avviso. È possibile attivare avvisi per le condizioni delle prestazioni seguenti:  
  
-   Superamento della latenza specificata (quantità di tempo trascorso tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore).  
  
     Si applica alla replica transazionale. Se la soglia specificata viene raggiunta o superata, viene visualizzato lo stato **Prestazioni critiche**.  
  
-   Superamento del tempo di sincronizzazione specificato.  
  
     Si applica alla replica di tipo merge. Se la soglia specificata viene raggiunta o superata, viene visualizzato lo stato **Merge con esecuzione prolungata**. È possibile specificare soglie diverse per connessioni remote e LAN.  
  
-   Impossibilità di elaborare il numero di righe specificato in un determinato intervallo di tempo.  
  
     Si applica alla replica di tipo merge. Se la soglia specificata viene raggiunta o superata, viene visualizzato lo stato **Prestazioni critiche**. È possibile specificare soglie diverse per connessioni remote e LAN.  
  
 Per altre informazioni, vedere [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
## <a name="view-performance-measurements"></a>Visualizzazione delle misurazioni delle prestazioni  
 In Monitoraggio replica vengono visualizzati i valori relativi alla qualità delle prestazioni per repliche transazionali e di tipo merge nelle colonne **Prestazioni medie correnti** e **Prestazioni peggiori correnti** per le pubblicazioni e nella colonna **Prestazioni** per le sottoscrizioni. I valori possibili sono:  
  
-   Eccellenti  
  
-   Buone  
  
-   Discrete  
  
-   Scarse  
  
-   Critiche (solo per la replica transazionale)  
  
 I valori vengono determinati nei modo seguenti:  
  
-   Per la replica transazionale la qualità delle prestazioni viene determinata dalla soglia di latenza. Se la soglia non viene impostata, non verrà visualizzato alcun valore. Nella tabella seguente viene illustrata la correlazione tra la soglia e il valore della qualità delle prestazioni. Ad esempio, se la soglia è impostata su 60 secondi e la latenza attuale è di 30 secondi, la latenza rappresenta il 50% della soglia, producendo quindi il valore Buone.  
  
    |Eccellenti|Buone|Discrete|Scarse|Critico|  
    |---------------|----------|----------|----------|--------------|  
    |0 – 34%|35 – 59%|60 – 84%|85 – 99%|100% +|  
  
-   Per la replica di tipo merge la qualità delle prestazioni è indipendente dalla soglia. La soglia di elaborazione delle righe determina in realtà se il valore **Prestazioni critiche** viene visualizzato nella colonna **Stato** . La qualità delle prestazioni è determinata dal confronto tra le prestazioni delle singole sottoscrizioni e le prestazioni medie cronologiche delle sottoscrizioni, che utilizzano lo stesso tipo di connessione (remota o LAN), rispetto alla pubblicazione. In Monitoraggio replica viene visualizzato un valore dopo cinque sincronizzazioni con 50 o più modifiche eseguite con lo stesso tipo di connessione. Se sono state eseguite meno di cinque sincronizzazioni con 50 o più modifiche oppure la sincronizzazione più recente include meno di 50 modifiche, in Monitoraggio replica non viene visualizzato alcun valore.  
  
     Nella tabella seguente viene illustrata la correlazione tra le prestazioni medie e il valore della qualità delle prestazioni. Ad esempio, se dieci Sottoscrittori hanno eseguito la sincronizzazione tramite una connessione LAN con una velocità media di elaborazione di 100 righe al secondo e successivamente una delle sottoscrizioni esegue la sincronizzazione con una velocità di 125 righe al secondo, le prestazioni di sincronizzazione di quel Sottoscrittore saranno del 125% rispetto alla media, producendo quindi il valore Buone.  
  
    |Eccellenti|Buone|Discrete|Scarse|  
    |---------------|----------|----------|----------|  
    |151+%|76 – 150%|26 – 75%|0 – 25%|  
  
 Per altre informazioni sulla visualizzazione delle informazioni relative alle sottoscrizioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="determine-latency-with-tracer-tokens"></a>Determinazione della latenza con token di traccia  
 La replica transazionale consente di misurare la latenza di un sistema inserendo un token (una piccola quantità di dati) nel log delle transazioni del database di pubblicazione e misurando il tempo impiegato dal token per arrivare al database di distribuzione e ai Sottoscrittori. Il token consente inoltre di rilevare se i dati non raggiungono il database di distribuzione o il Sottoscrittore. Per altre informazioni, vedere [Misurazione della latenza e convalida delle connessioni per la replica transazionale](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="view-detailed-synchronization-performance-for-merge-replication"></a>Visualizzazione di statistiche dettagliate sulle prestazioni di sincronizzazione per la replica di tipo merge  
 Per la replica di tipo merge in Monitoraggio replica vengono visualizzate statistiche dettagliate di ogni articolo elaborato durante la sincronizzazione, inclusa la quantità di tempo impiegato in ogni fase di elaborazione (caricamento delle modifiche, download delle modifiche e così via). Ciò può essere utile per individuare tabelle specifiche che determinano rallentamenti ed è l'opzione migliore per risolvere problemi relativi alle prestazioni delle sottoscrizioni di tipo merge. Per altre informazioni sulla visualizzazione di statistiche dettagliate, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="view-transactions-and-delivery-time-for-transactional-replication"></a>Visualizzazione delle transazioni e dei tempi di recapito della replica transazionale  
 Per la replica transazionale in Monitoraggio replica vengono visualizzate informazioni sul numero di transazioni nel database di distribuzione non ancora distribuite a un Sottoscrittore e il tempo stimato per la relativa distribuzione. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
