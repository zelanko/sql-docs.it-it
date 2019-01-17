---
title: Capacità di elaborazione e archiviazione - sistema di piattaforma Analitica | Microsoft Docs
description: I requisiti aziendali determinano il numero di unità di scala di dati e le dimensioni dei dischi di nodo di calcolo necessarie nell'appliance del sistema di piattaforma Analitica (AP).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f20de8ebc4e3b2970e439dbc413e588aa08b5324
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361571"
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Capacità di elaborazione e archiviazione nel sistema di piattaforma Analitica
I requisiti aziendali determinano il numero di unità di scala di dati e le dimensioni dei dischi di nodo di calcolo necessarie nell'appliance del sistema di piattaforma Analitica (AP). Utilizzare questi calcoli di elaborazione e archiviazione per la capacità di acquisto e decisioni relative alla pianificazione.  
  
  
## <a name="section1"></a>Pianificazione della capacità di elaborazione  
Le prestazioni delle query per SQL Server Parallel Data Warehouse (PDW) dipende molto il numero di core della CPU dedicati sui dati in parallelo. Entro i limiti, l'aumento del parallelismo migliora le prestazioni delle query di elaborazione parallela massiva (MPP). Anche se le dimensioni dei dati sono relativamente piccola, la potenza del motore di query MPP è stata migliorata con parallelismo maggiore.  
  
Ad esempio, un'appliance con 12 nodi di calcolo ha 192 core CPU che elaborano i dati in parallelo. È stata vie 192 parallelismo completata. Un'appliance con 56 nodi di calcolo con 896 core tutti operano in parallelo. In questo ordine di grandezza di parallelismo non è realizzabile senza elaborazione MPP.  
  
Man mano che aumenta il numero di nodi di calcolo, la scalabilità orizzontale dell'appliance richiede l'aggiunta di più di un nodo di calcolo in un momento per ottenere un vantaggio evidente. I fornitori di hardware supportano configurazioni specifiche solo dei dati di unità di scala per garantire che il vantaggio della scalabilità dell'appliance supera il costo della ridistribuzione dei dati tra più nodi di calcolo.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Esempi di configurazione di unità di scala dei dati - HPE  
Questi sono esempi di configurazioni HPE supportate per Uunits scala dei dati. Essi potrebbero variare rispetto alle configurazioni supportate più recenti, ma vengono forniti come esempio di come migliorare la capacità, circa il 20%.  
  
Maggiorazione è il miglioramento percentuale capacità aumentando Uunits la scalabilità dei dati da una riga a quella successiva. Ad esempio, aumentare le unità di scala di dati da 6 a 8 offre una maggiorazione 33% di memoria e core CPU.  Aumenta anche lo spazio su disco che non sia mostrato in questa tabella.  
  
|Unità di scala dei dati|Nodi di calcolo|Core CPU|Memoria (GB)|Maggiorazione|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|2|32|512|-|  
|2|4|64|1024|100%|  
|3|6|96|1536|50%|  
|4|8|128|2048|33%|  
|5|10|160|2560|25%|  
|6|12|192|3072|20%|  
|8|16|256|4096|33%|  
|10|20|320|5120|25%|  
|12|24|384|6144|20%|  
|16|32|512|8192|33%|  
|20|40|640|10240|25%|  
|24|48|768|12288|20%|  
|28|56|896|14336|17%|  
  
Spiegazione:  
  
-   **Unità di scala dati** per ogni dispositivo. Per altre informazioni sulle unità di scala dei dati, vedere [componenti Hardware del sistema di piattaforma Analitica](hardware-components.md).  
  
-   **Nodi di calcolo** per ogni dispositivo.  
  
-   **Core CPU** per ogni dispositivo. Sono presenti 16 core per nodo di calcolo, un solo core per ogni coppia di disco con mirroring. Per struttura disco nodo di calcolo, vedere [componenti Hardware del sistema di piattaforma Analitica](hardware-components.md).  
  
-   **Memoria** per ogni dispositivo. Ciascun core è 256 GB di memoria.  
  
### <a name="data-scale-unit-configuration-examples---dell-quanta"></a>I dati di scalabilità unit esempi di configurazione - Dell, quantum  
Questi sono esempi di configurazioni supportate Dell e quantum per Uunits scala dei dati. Essi potrebbero variare rispetto alle configurazioni supportate più recenti, ma vengono forniti come esempio di come migliorare la capacità, circa il 20%.  
  
Maggiorazione è il miglioramento percentuale capacità aumentando Uunits la scalabilità dei dati da una riga a quella successiva. Ad esempio, aumentare le unità di scala di dati da 6 a 8 offre una maggiorazione 33% di memoria e core CPU. Aumenta anche lo spazio su disco che non sia mostrato in questa tabella.  
  
|Unità di scala dei dati|Nodi di calcolo|Core CPU|Memoria (GB)|Maggiorazione|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|3|48|768|-|  
|2|6|96|1536|100%|  
|3|9|144|2,304|50%|  
|4|12|192|3,072|33%|  
|5|15|240|3,840|25%|  
|6|18|288|4,608|20%|  
|7|21|336|5,376|17%|  
|8|24|384|6,144|14%|  
|9|27|432|6,912|13%|  
|12|36|576|9,216|33%|  
|15|45|720|11,520|25%|  
|18|54|864|13,824|20%|  
  
## <a name="section2"></a>Pianificazione della capacità di archiviazione  
Questa tabella restituisce una stima che è possibile caricare e archiviare fino a 6 petabyte di dati non compressi in un'appliance di sistema di piattaforma Analitica completamente compilata. 
  
|fornitore|Dimensioni dell'unità|Nodo di calcolo per ogni archiviazione fisica dei dati|Numero massimo di nodi di calcolo per ogni rack|Archiviazione dati massimo fisica per rack|Stima di archiviazione dati massimo di utenti rack|Rack massimo|Stima di archiviazione dati massimo di utenti per dispositivo|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2,240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4,480 TB|  
|HPE|4 TB|64 TB|8|512 TB|1280 TB|7|8,960 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|2,160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4,320 TB|  
|DELL|4 TB|64 TB|9|576 TB|1440 TB|6|8,640 TB|   
  
Spiegazione:  
  
-   **Dimensioni dell'unità** è 1, 2 o 4 TB per ogni fornitore di Hardware.  
  
-   **Archiviazione fisica dei dati per ogni nodo di calcolo** = (dimensioni dell'unità) * (16 dischi per nodo di calcolo). I dischi con mirroring non sono inclusi poiché sono per la ridondanza.  
  
-   **Nodi di calcolo massima per ogni rack** è specifico per il fornitore dell'hardware.  
  
-   **Archiviazione fisica massima dei dati per ogni rack** = (archivio dati fisico per ogni nodo di calcolo) * (nodi di calcolo massima per ogni rack).  
  
-   **Stimato di archiviazione dati massimo di utenti rack** = (archiviazione fisica massima dei dati per ogni rack) * (5 per un rapporto di compressione 5:1) \* (50% per i log e tempDB). Si tratta di una stima conservativa per i dati utente non compressi che possono essere caricati e archiviati nell'appliance. Si tratta di una stima e non vengono applicata da software. L'archiviazione dei dati utente effettivo varia a seconda dei dati e la configurazione.  
  
-   **Rack massimo** è specifico per ogni fornitore di Hardware.  
  
-   **Appliance di archiviazione dati massimo stimato** (costo stimato sono archiviazione dati massimo per ogni rack) * (numero massimo dei rack). Si tratta di una stima delle dimensioni totali complessivi di dati dell'utente che è possibile caricare e archiviare in un dispositivo completamente compilato.  
  
