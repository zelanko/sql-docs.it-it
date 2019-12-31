---
title: Componenti hardware
description: Analytics Platform System (APS) usa componenti scalabili che consentono di acquistare la quantità corretta di elaborazione e archiviazione in base ai requisiti aziendali. Quando si ordinano i punti di APS, sarà necessaria una combinazione di questi componenti hardware di base.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: db9966315d60fd4de1de7ae6805620d3f2144e6f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401139"
---
# <a name="hardware-components-for-analytics-platform-system"></a>Componenti hardware per il sistema di piattaforma Analytics

Analytics Platform System (APS) usa componenti scalabili che consentono di acquistare la quantità corretta di elaborazione e archiviazione in base ai requisiti aziendali. Quando si ordinano i punti di APS, sarà necessaria una combinazione di questi componenti hardware di base. I fornitori di hardware specifici potrebbero utilizzare convenzioni di denominazione diverse o avere componenti aggiuntivi.  
 
  
## <a name="rackandnetwork"></a>Rack e rete 
 
I componenti APS sono tutti archiviati in uno o più rack che rientrano nell'data center. Ogni rack è dotato di unità di distribuzione dell'alimentazione (PDU), due commutatori InfiniBand e due commutatori Ethernet.  
  
![Rack e rete](media/rack-and-network.png "Rack e rete APS")  
  
## <a name="datascaleunit"></a>Unità di scala dati
 
Un'unità di scala dati contiene gli host di dati e l'archiviazione diretta (DAS) per l'elaborazione e l'archiviazione dei dati utente. Per aggiungere capacità, è necessario aggiungere unità di scala dati in base alle configurazioni supportate dal fornitore dell'hardware. Con l'aumentare del numero di unità di scalabilità dei dati, è necessario aggiungere altri componenti di rete & rack, in base alle esigenze, per offrire più potenza, rete e infrastruttura rack.  
  
### <a name="data-host"></a>Host dati  

Un host di dati è un server dedicato all'elaborazione dei dati utente. Parallel data warehouse (PDW) esegue un nodo di calcolo in ogni host di dati. Per le appliance HPE, l'unità di scala dei dati dispone di due host di dati. Per le appliance dell e Quantity, l'unità di scala dati ha tre host di dati.  
  
### <a name="direct-attached-storage"></a>Archiviazione collegata direttamente
 
Il gruppo DAS (Direct Attached Storage) è un pool di dischi connessi agli host di dati. Tutti gli host di dati possono accedere a tutti i dischi. Come parte dell'architettura Shared Nothing, i nodi di calcolo in esecuzione negli host di dati non condividono singoli dischi. Per la disponibilità elevata, tuttavia, l'accesso alla risorsa di archiviazione è condiviso e ogni host di dati può accedere a qualsiasi disco.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Architettura di unità di scala dati-DELL e Quantum
  
![Unità di scalabilità](media/scalability-unit-dell.png "Unità di scalabilità dell")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Architettura dell'unità di scala dei dati-HPE 
 
![Unità di scalabilità HPE](media/scalability-unit-hpe.png "Unità di scalabilità HPE")  
  
### <a name="data-scale-unit-description"></a>Descrizione unità di scala dati

Un'unità di scala dati ha un solo server (host) per ogni nodo di calcolo e un array di dischi collegato direttamente collegato con SAS (Serial Attached SCSI). All'interno del cabinet di archiviazione, l'array di dischi è suddiviso in due metà, ognuna con alimentatori ridondanti. Spazi di archiviazione di Windows Server gestisce i dati degli utenti duplicando i dati tra coppie di dischi con mirroring RAID 1. I dischi in ogni coppia di dischi vengono archiviati in mezze diverse dell'array di dischi.  
  
L'array di dischi contiene anche dischi di riserva a caldo e un disco di sistema. Se si verifica un errore in un disco, spazi di archiviazione usa la copia corretta dei dati sul disco funzionante per ricompilare una copia duplicata dei dati in una riserva a caldo. Si tratta di un'importante funzionalità di correzione automatica che consente di evitare la perdita di dati.  
  
Il numero totale di dischi per i nodi di calcolo:  
  
-   DELL ha 96 dischi = (3 Server) * (16 dischi per Server) \* (2 per i dischi ridondanti).  
  
-   HPE ha 64 dischi = (2 Server) * (16 dischi per Server) \* (2 per i dischi ridondanti).  
  
-   Ogni array di dischi dispone inoltre di dischi di riserva a caldo e un disco di sistema.  
  
**Per la disponibilità elevata**, quando viene eseguito il failover di un nodo di calcolo, può comunque funzionare e accedere ai dati utente tramite l'altro host nell'unità di scala dati. Almeno uno degli host fisici collegati direttamente deve funzionare o l'accesso ai dati per l'archiviazione va perso.  
  
**Per le dimensioni dei dischi**, l'archiviazione collegata direttamente può avere unità disco da 1, 2 o 3 terabyte. Tutte le unità di scala dei dati devono avere dischi delle stesse dimensioni.  
  
## <a name="basescaleunit"></a>Unità di scala di base 
 
L'unità di scala di base contiene il numero minimo di host di sistema cerebrale, host di dati e archiviazione collegata direttamente necessaria per l'appliance. Include i componenti seguenti. 
  
### <a name="orchestration-host"></a>Host di orchestrazione  
Questo server esegue i cervelli di PDW.
  
### <a name="passive-host"></a>Host passivo  
Questo server garantisce un'elevata disponibilità. È online e pronto per l'esecuzione di processi in caso di errore nell'orchestrazione o nell'host di dati. L'host di orchestrazione, l'host passivo e i server di unità scala dati sono configurati come cluster di failover di Windows. Ogni rack nell'appliance richiede un host passivo.  
  
### <a name="optional-passive-host"></a>Host passivo facoltativo  
Per aggiungere ulteriore ridondanza, è possibile aggiungere un secondo host passivo all'unità di scala di base.  
  
### <a name="data-scale-unit"></a>Unità di scala dati  
L'unità di scala di base include un'unità di scala dei dati posizionata nella parte inferiore del rack.  
  
Questo diagramma mostra l'unità di scala di base più il rack e la rete. Questa è la configurazione minima per un'appliance del sistema della piattaforma di analisi.  
  
![Unità di scala di base](media/base-scale-unit.png "Unità di scala di base")  
 
