---
title: La disponibilità elevata nel sistema di piattaforma Analitica | Microsoft Docs
description: Informazioni su come sistema di piattaforma Analitica (AP) è progettato per la disponibilità elevata.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5c8a562ab105e1bc40b590916d0881757036aeff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280348"
---
# <a name="analytics-platform-system-high-availability"></a>Disponibilità elevata del sistema di piattaforma Analitica
Informazioni su come sistema di piattaforma Analitica (AP) è progettato per la disponibilità elevata.  
  
## <a name="high-availability-architecture"></a>Architettura a disponibilità elevata  
![Architettura dello strumento](media/appliance-architecture.png "architettura dello strumento")  
  
## <a name="network"></a>Rete  
Per la disponibilità di rete, l'appliance APS dispone di due reti InfiniBand. Se una delle reti InfiniBand diventa inattiva, l'altro è ancora disponibile. Inoltre, Active Directory ha replicato i controller di dominio per risolvere le richieste in ingresso alla rete InfiniBand corretta.  
  
Per altre informazioni, vedere [schede di rete InfiniBand configurare](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Archiviazione  
Per proteggere i dati, i punti di accesso utilizza RAID 1, il mirroring per mantenere due copie di tutti i dati utente. Quando un disco non riesce, il sistema hardware consente di ricompilare i dati in un disco di riserva e imposta un avviso che si verifica un errore di disco.  
  
Per mantenere i dati disponibili in linea, APS Usa spazi di archiviazione di Windows e volumi condivisi cluster per gestire l'archiviazione collegata direttamente i dischi dati utente. È presente un pool di archiviazione per unità di scala di dati organizzati in volumi condivisi del Cluster che sono disponibili per gli host del nodo di calcolo tramite punti di montaggio.  
  
Per verificare che il pool di archiviazione rimane online, ogni host nell'unità di scala di dati dispone di una macchina virtuale ISCSI che non esegue il failover. Questa architettura è importante perché se un host non riesce, i dati sono ancora accessibili tramite gli altri host nell'unità di scala di dati.  
  
## <a name="hosts"></a>Host  
Per la disponibilità dell'host, tutti gli host sono configurati in un Cluster di Failover di Windows. Ogni rack dispone di un host passivo. Facoltativamente, il primo rack, che controlla l'infrastruttura di appliance e SQL Server Parallel Data Warehouse (PDW), può avere un secondo host passivo. Se un host non riesce, le macchine virtuali che sono configurate per il failover, eseguirà il failover in un host passivo disponibile.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>I nodi PDW e dell'infrastruttura di appliance  
Per la disponibilità elevata dei nodi di PDW e dell'infrastruttura di appliance APS utilizza la virtualizzazione. Ognuno dei componenti di infrastruttura dell'appliance e PDW eseguiti in una macchina virtuale.  
  
Ogni macchina virtuale è definito come un ruolo del cluster di failover di Windows. Quando una macchina virtuale non riesce, il cluster viene riavviato in un host passivo disponibile. Le macchine virtuali distribuite tramite System Center Virtual Machine Manager. Quando si verifica un failover, la macchina virtuale in esecuzione nell'host passivo è ancora in grado di accedere ai dati utente tramite la rete InfiniBand.  
  
Il nodo di controllo e le macchine virtuali di nodo di calcolo vengono configurate come cluster a nodo singolo. Il cluster a nodo singolo gestisce le reti InfiniBand come risorsa cluster per verificare che il cluster Usa sempre l'IP InfiniBand active. Il cluster a nodo singolo gestisce i processi PDW in esecuzione all'interno della macchina virtuale. Ad esempio, il cluster a nodo singolo è SQL Server e Data Movement Service (DMS) come risorse in modo che è possibile avviarli nell'ordine corretto. Il nodo di controllo della macchina virtuale controlla anche l'ordine di avvio per le altre macchine virtuali eseguite in host di orchestrazione.  
  
