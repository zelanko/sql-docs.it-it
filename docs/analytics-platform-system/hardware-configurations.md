---
title: Le configurazioni hardware, sistema di piattaforma Analitica | Microsoft Docs
description: L'hardware di appliance Analitica Platform System (APS) è stato progettato con unità scalabili in modo che si acquista la giusta quantità di elaborazione e archiviazione in base alle esigenze aziendali. L'appliance Ridimensiona archiviazione per Parallel Data Warehouse da pochi terabyte a più di 6 petabyte di dati.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2a252e5f2aebd8d51b9b0eb1f353ded504155c2e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283253"
---
# <a name="hardware-configurations---analytics-platform-system"></a>Configurazioni hardware, sistema di piattaforma Analitica
L'hardware del sistema di piattaforma Analitica (AP) è stato progettato con unità scalabili in modo che si acquista la giusta quantità di elaborazione e archiviazione in base alle esigenze aziendali. L'appliance scala di archiviazione per SQL Server Parallel Data Wareouse (PDW) da pochi terabyte a più di 6 petabyte di dati.  
  
## <a name="contents"></a>Sommario  
  
-   [Configurazioni di un Rack](#section1)  
  
-   [Configurazioni a più Rack](#section2)  

  
## <a name="section1"></a>Configurazioni di un Rack  
Il primo rack nell'appliance contiene i componenti necessari per l'esecuzione di PDW. La configurazione di appliance minimo è un Rack e rete oltre a un'unità di scala di Base. Questi diagrammi mostrano modi che possono essere configurate prima rack dell'appliance. È possibile avere tra 2 e 9 nodi di calcolo nel primo rack, a seconda del fornitore dell'hardware.  
  
### <a name="first-rack-configurations---dell"></a>Prima di tutto installare in Rack configurazioni - DELL  
La configurazione minima per un'appliance DELL ha 3 nodi di calcolo. È possibile aggiungere fino a 2 unità di scala di dati al primo rack per un totale di 9 nodi di calcolo.  
  
![Configurazioni del primo rack Dell](media/first-rack-configurations-dell.png "configurazioni Dell del primo rack")  
  
### <a name="first-rack-configurations---hpe"></a>Prima di tutto installare in Rack configurazioni - HPE  
La configurazione minima per un'appliance HPE con 2 nodi di calcolo. È possibile aggiungere fino a 3 unità di scala di dati al primo rack per un totale di 8 nodi di calcolo.  
  
![HPE rack prima di tutto le configurazioni per HPE](media/first-rack-configurations-hpe.png "HPE rack prima di tutto le configurazioni")  
  
## <a name="section2"></a>Configurazioni a più rack  
Per aggiungere capacità a PDW è possibile aggiungere unità di scala dei dati, insieme ai componenti aggiuntivi di Rack & rete in base alle esigenze per fornire la potenza di appropriata, rete e infrastruttura in rack. Ogni Rack & rete aggiuntivo richiede un host passivo.  
  
Ogni fornitore di hardware specifica il numero di unità di scala di dati che è possibile aggiungere ha la capacità dell'appliance. È consigliabile aggiungere sufficiente unità di scala di dati per visualizzare almeno una maggiorazione pari al 20% delle prestazioni. Ad esempio, l'aggiunta di una scala dei dati in un'applicazione che dispone già di 20 unità di scala di Data unit potrebbe comportare un guadagno trascurabile sulle prestazioni. Il guadagno netto non sarebbe opportuno i costi e impegno.  
  
### <a name="scale-out-example---hpe"></a>Scalare in orizzontale esempio - HPE  
Questo diagramma mostra un'appliance di 3 rack HP contiene 20 nodi di calcolo.  
  
![Appliance HPE con 20 nodi di calcolo](media/scale-out-hpe.png "appliance HPE con 20 nodi di calcolo")  
  
### <a name="scale-out-example---dell-quanta"></a>Scalabilità orizzontale di quantum esempio - DELL,  
Questo diagramma mostra un'appliance di DELL o Quanta 3 rack che contiene i nodi di calcolo 21.  
  
![Appliance Dell con nodi di calcolo 21](media/scale-out-dell.png "appliance Dell 21 nodi di calcolo")  
 
