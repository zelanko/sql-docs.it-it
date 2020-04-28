---
title: Configurazioni hardware
description: L'hardware del dispositivo Analytics Platform System (APS) viene progettato con unità scalabili, in modo da acquistare la quantità corretta di elaborazione e archiviazione in base alle esigenze aziendali. Il dispositivo ridimensiona l'archiviazione per data warehouse parallele da pochi terabyte a oltre 6 petabyte di dati.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee16045931da345f06c141597ccd25d19a36dea7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401129"
---
# <a name="hardware-configurations---analytics-platform-system"></a>Configurazioni hardware-sistema di piattaforma di analisi
L'hardware del sistema di piattaforma di analisi (APS) viene progettato con unità scalabili, in modo da acquistare la quantità corretta di elaborazione e archiviazione in base alle esigenze aziendali. Il dispositivo ridimensiona l'archiviazione per SQL Server Parallel Data Wareouse (PDW) da pochi terabyte a oltre 6 petabyte di dati.  
  
## <a name="contents"></a>Sommario  
  
-   [Configurazioni a un rack](#section1)  
  
-   [Configurazioni a più rack](#section2)  

  
## <a name="one-rack-configurations"></a><a name="section1"></a>Configurazioni a un rack  
Il primo rack nell'appliance contiene i componenti necessari per eseguire PDW. La configurazione minima del dispositivo è un rack e una rete, oltre a un'unità di scala di base. Questi diagrammi mostrano i modi in cui è possibile configurare il primo rack dell'appliance. È possibile avere un nodo di calcolo compreso tra 2 e 9 nel primo rack, a seconda del fornitore dell'hardware.  
  
### <a name="first-rack-configurations---dell"></a>Configurazioni del primo rack-DELL  
La configurazione minima per un appliance DELL ha 3 nodi di calcolo. È possibile aggiungere fino a due unità di scala dei dati al primo rack per un totale di 9 nodi di calcolo.  
  
![Configurazioni di dell First rack](media/first-rack-configurations-dell.png "Configurazioni di dell First rack")  
  
### <a name="first-rack-configurations---hpe"></a>Configurazioni del primo rack-HPE  
La configurazione minima per un'appliance HPE è costituita da 2 nodi di calcolo. È possibile aggiungere fino a 3 unità di scala dati al primo rack per un totale di 8 nodi di calcolo.  
  
![HPE prime configurazioni di rack per HPE](media/first-rack-configurations-hpe.png "HPE prime configurazioni di rack")  
  
## <a name="multi-rack-configurations"></a><a name="section2"></a>Configurazioni a più rack  
Per aggiungere capacità a PDW è possibile aggiungere unità di scala dei dati, oltre a rack aggiuntivi & componenti di rete, in base alle esigenze, per fornire l'alimentazione, la rete e l'infrastruttura rack appropriati. Ogni rete & rack aggiuntiva richiede un host passivo.  
  
Ogni fornitore di hardware specifica il numero di unità di scala dei dati che è possibile aggiungere data la capacità dell'appliance. È consigliabile aggiungere unità di scala dei dati sufficienti per visualizzare almeno un incremento del 20% delle prestazioni. Ad esempio, l'aggiunta di un'unità di scala dati a un'appliance che dispone già di 20 unità di scala dati può comportare un miglioramento delle prestazioni trascurabile. Il guadagno netto non varrebbe il costo e il lavoro richiesto.  
  
### <a name="scale-out-example---hpe"></a>Esempio di scalabilità orizzontale-HPE  
Questo diagramma mostra un dispositivo HP con 3 rack che contiene 20 nodi di calcolo.  
  
![Appliance HPE con 20 nodi di calcolo](media/scale-out-hpe.png "Appliance HPE con 20 nodi di calcolo")  
  
### <a name="scale-out-example---dell-quanta"></a>Esempio di Scale Out-DELL, Quantum  
Questo diagramma mostra un'appliance DELL o di un contenitore di 3 rack che contiene 21 nodi di calcolo.  
  
![Appliance dell con 21 nodi di calcolo](media/scale-out-dell.png "Appliance dell con 21 nodi di calcolo")  
 
