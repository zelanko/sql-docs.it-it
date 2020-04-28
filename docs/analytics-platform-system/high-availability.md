---
title: Disponibilità elevata
description: Informazioni sul modo in cui il sistema di piattaforma di analisi (APS) è progettato per la disponibilità elevata.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6246ed25909a2e366d8bbafcd912a4fd923cc84a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401106"
---
# <a name="analytics-platform-system-high-availability"></a>Disponibilità elevata del sistema della piattaforma Analytics
Informazioni sul modo in cui il sistema di piattaforma di analisi (APS) è progettato per la disponibilità elevata.  
  
## <a name="high-availability-architecture"></a>Architettura a disponibilità elevata  
![Architettura del dispositivo](media/appliance-architecture.png "Architettura del dispositivo")  
  
## <a name="network"></a>Rete  
Per la disponibilità di rete, il dispositivo APS dispone di due reti InfiniBand. Se una delle reti InfiniBand diventa inattiva, l'altra è ancora disponibile. Inoltre, Active Directory ha replicato i controller di dominio per risolvere le richieste in ingresso alla rete InfiniBand corretta.  
  
Per ulteriori informazioni, vedere [configurare le schede di rete InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Archiviazione  
Per mantenere il livello di sicurezza dei dati, APS usa il mirroring RAID 1 per mantenere due copie di tutti i dati utente. Quando si verifica un errore in un disco, il sistema hardware ricompila i dati su un disco di riserva e imposta un avviso in caso di errore del disco.  
  
Per rendere disponibili i dati online, APS USA spazi di archiviazione di Windows e volumi condivisi cluster per gestire i dischi dati utente nell'archiviazione collegata direttamente. Un pool di archiviazione per ogni unità di scala dei dati è organizzato in volumi condivisi del cluster, che sono disponibili per gli host del nodo di calcolo tramite punti di montaggio.  
  
Per assicurarsi che il pool di archiviazione rimanga online, ogni host nell'unità di scala dati dispone di una macchina virtuale ISCSI che non esegue il failover. Questa architettura è importante perché in caso di errore di un host, i dati sono ancora accessibili tramite gli altri host nell'unità di scala dati.  
  
## <a name="hosts"></a>Hosts  
Per la disponibilità dell'host, tutti gli host sono configurati in un cluster di failover di Windows. Ogni rack dispone di un host passivo. Facoltativamente, il primo rack, che controlla SQL Server Parallel data warehouse (PDW) e l'infrastruttura dell'appliance, può avere un secondo host passivo. Se si verifica un errore in un host, le macchine virtuali configurate per il failover eseguiranno il failover su un host passivo disponibile.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>Nodi PDW e infrastruttura Appliance  
Per la disponibilità elevata dei nodi PDW e dell'infrastruttura dell'appliance, APS usa la virtualizzazione. Ognuno dei componenti di infrastruttura PDW e Appliance viene eseguito in una macchina virtuale.  
  
Ogni macchina virtuale è definita come un ruolo nel cluster di failover di Windows. Quando si verifica un errore in una macchina virtuale, il cluster lo riavvia in un host passivo disponibile. Le macchine virtuali vengono distribuite con System Center Virtual Machine Manager. Quando si verifica un failover, la macchina virtuale in esecuzione nell'host passivo è ancora in grado di accedere ai dati utente tramite la rete InfiniBand.  
  
Le macchine virtuali del nodo di controllo e del nodo di calcolo sono configurate come cluster a nodo singolo. Il cluster a nodo singolo gestisce le reti InfiniBand come risorsa cluster per garantire che il cluster usi sempre l'IP InfiniBand attivo. Il cluster a nodo singolo gestisce i processi PDW eseguiti all'interno della macchina virtuale. Ad esempio, il cluster a nodo singolo ha SQL Server e il servizio di spostamento dei dati (DMS) come risorse in modo che possano avviarle nell'ordine corretto. La VM del nodo di controllo Controlla anche l'ordine di avvio per le altre macchine virtuali in esecuzione nell'host di orchestrazione.  
  
