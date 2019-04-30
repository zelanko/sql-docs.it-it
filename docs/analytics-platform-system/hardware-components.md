---
title: Componenti hardware, sistema di piattaforma Analitica | Microsoft Docs
description: Analitica piattaforma di strumenti analitici Usa componenti scalabili in modo che è possibile acquistare la giusta quantità di elaborazione e archiviazione in base alle esigenze aziendali. Quando si ordinano i punti di accesso, è necessario una combinazione di questi componenti hardware di base.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8cf7fd100f72e14b09ea086a1ebff5140a9068a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157379"
---
# <a name="hardware-components-for-analytics-platform-system"></a>Componenti hardware per il sistema di piattaforma Analitica

Analitica piattaforma di strumenti analitici Usa componenti scalabili in modo che è possibile acquistare la giusta quantità di elaborazione e archiviazione in base alle esigenze aziendali. Quando si ordinano i punti di accesso, è necessario una combinazione di questi componenti hardware di base. I fornitori di hardware specifico potrebbero usare convenzioni di denominazione diverse o i componenti aggiuntivi.  
 
  
## <a name="rackandnetwork"></a>Rack e rete 
 
Tutti i componenti di punti di accesso vengono archiviati in uno o più rack che rientra nel proprio data center. Ogni rack viene fornito con unità di distribuzione dell'alimentazione (PDU), due commutatori InfiniBand e due commutatori Ethernet.  
  
![Rete e rack](media/rack-and-network.png "APS su rack e di rete")  
  
## <a name="datascaleunit"></a>Unità di scala di dati
 
Un'unità di scala di dati contiene l'host di dati e archiviazione diretta (DAS) per l'elaborazione e archiviazione dei dati utente. Per aggiungere capacità aggiungere unità di scala di dati in base alle configurazioni supportate dal fornitore dell'hardware. Man mano che aumenta il numero di unità di scala di dati, è necessario aggiungere ulteriori Rack & componenti di rete, in base alle esigenze, per fornire informazioni di alimentazione, rete e installare in rack dell'infrastruttura.  
  
### <a name="data-host"></a>Host di dati  

Un host di dati è un server dedicato all'elaborazione dei dati utente. Parallel Data Warehouse (PDW), un nodo di calcolo viene eseguito in ogni host di dati. Per le Appliance HPE, l'unità di scala di dati dispone di due host di dati. Per le Appliance Dell e quantum, l'unità di scala di dati ha tre dati host.  
  
### <a name="direct-attached-storage"></a>Archiviazione diretta
 
L'archiviazione diretta (DAS) è un pool di dischi connessi agli host dei dati. Tutti gli host dei dati può accedere a tutti i dischi. Come parte di senza condivisione architettura, i nodi di calcolo in esecuzione negli host i dati non condividono singoli dischi. Tuttavia, per la disponibilità elevata, viene condiviso l'accesso all'archiviazione e ognuno degli host dei dati può accedere a tutti i dischi.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Scalabilità unit architettura di dati - DELL e quantum
  
![Unità di scalabilità](media/scalability-unit-dell.png "unità di scalabilità di Dell")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Architettura di unità di scala Data - HPE 
 
![Unità di scalabilità di HPE](media/scalability-unit-hpe.png "unit HPE scalabilità")  
  
### <a name="data-scale-unit-description"></a>Descrizione unità di scala dei dati

Un'unità di scala di dati dispone di un server (host) per ogni nodo di calcolo e di una matrice di un disco collegato direttamente collegato con SAS Serial Attached SCSI (). Archiviazione file CAB, l'array di dischi è suddivisa in due metà ciascuno con un set di alimentazione ridondanti. Spazi di archiviazione di Windows Server gestisce i dati dell'utente, la duplicazione dei dati tra coppie di dischi con mirroring RAID 1. Nella metà diverse di array di dischi sono archiviati i dischi in ogni coppia di disco.  
  
L'array di dischi contiene anche dischi di riserva a caldo e un disco del sistema. Se un disco non riesce, spazi di archiviazione Usa la copia dei dati sul disco funzionano per ricompilare una copia duplicata dei dati in una riserva a caldo. Si tratta di un'importante funzionalità di riparazione automatica che consente di proteggere dalla perdita di dati.  
  
Il numero totale di dischi per i nodi di calcolo:  
  
-   DELL ha 96 dischi = (3 servers) * (16 dischi per ogni server) \* (2 per i dischi con ridondanza).  
  
-   HPE è 64 dischi = (2 Server) * (16 dischi per ogni server) \* (2 per i dischi con ridondanza).  
  
-   Inoltre, ogni array di dischi con dischi di riserva a caldo e un disco del sistema.  
  
**Per la disponibilità elevata**, quando un nodo di calcolo viene eseguito il failover, può continuano a funzionare e accedere ai dati utente tramite altri host nell'unità di scala di dati. Almeno uno degli host fisici collegati direttamente deve funzionare o accesso ai dati nella risorsa di archiviazione viene perso.  
  
**Per le dimensioni dei dischi**, delle risorse di archiviazione diretta può avere 1, 2 o 3 unità disco di Terabyte. Tutte le unità di scala di dati devono essere dischi della stessa dimensione.  
  
## <a name="basescaleunit"></a>Unità di scala di base 
 
L'unità di scala di Base contiene il numero minimo di brain power host, gli host di dati e archiviazione collegata direttamente che è necessario per l'appliance. Include i componenti seguenti. 
  
### <a name="orchestration-host"></a>Host di orchestrazione  
Il server esegue il cervello di PDW.
  
### <a name="passive-host"></a>Host passivo  
Questo server fornisce la disponibilità elevata. Sia online e pronto per l'esecuzione dei processi nel caso in cui si verifica un errore in un host di dati o l'orchestrazione. L'host di orchestrazione, passivo host e i server di unità di scala dei dati sono configurati come cluster di failover Windows. Ogni rack nell'appliance richiede un host passivo.  
  
### <a name="optional-passive-host"></a>Host passivo facoltativo  
Per aggiungere un'ulteriore ridondanza, è possibile aggiungere un secondo host passivo per l'unità di scala di Base.  
  
### <a name="data-scale-unit"></a>Unità di scala di dati  
L'unità di scala di Base include un'unità di scala di dati che viene posizionata nella parte inferiore del rack.  
  
Questo diagramma mostra l'unità di scala di Base oltre il Rack e la rete. Questa è la configurazione minima per un dispositivo di sistema di piattaforma Analitica.  
  
![Unità di scala di base](media/base-scale-unit.png "unità di scala di Base")  
 
