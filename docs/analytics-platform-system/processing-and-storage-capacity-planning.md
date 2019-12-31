---
title: Capacità di elaborazione e archiviazione
description: I requisiti aziendali determinano il numero di unità di scala dei dati e le dimensioni dei dischi del nodo di calcolo necessari nell'appliance del sistema di piattaforma di analisi (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 143c37b6b55b96f8a0225c98db2212f07b2cd3a5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400538"
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Capacità di elaborazione e archiviazione nel sistema della piattaforma Analytics
I requisiti aziendali determinano il numero di unità di scala dei dati e le dimensioni dei dischi del nodo di calcolo necessari nell'appliance del sistema di piattaforma di analisi (APS). Usare questi calcoli di elaborazione e archiviazione per guidare le decisioni di acquisto e pianificazione della capacità.  
  
  
## <a name="section1"></a>Pianificazione della capacità di elaborazione  
Le prestazioni delle query per SQL Server Parallel data warehouse (PDW) dipendono in modo considerevole dal numero di core CPU che lavorano sui dati in parallelo. All'interno dei limiti, l'aumento del parallelismo migliora le prestazioni delle query di elaborazione parallela massiva (MPP). Anche se le dimensioni dei dati sono relativamente ridotte, la potenza del motore di query MPP viene migliorata con un maggiore parallelismo.  
  
Ad esempio, un appliance con 12 nodi di calcolo ha 192 core CPU che elaborano i dati in parallelo. Questo è il parallelismo a 192 vie! Un appliance con nodi di calcolo 56 ha 896 core che lavorano in parallelo. Questa grandezza del parallelismo non è raggiungibile senza MPP computing.  
  
Con l'aumentare del numero di nodi di calcolo, la scalabilità orizzontale del dispositivo richiede l'aggiunta di più di un nodo di calcolo alla volta per ottenere un vantaggio evidente. I fornitori di hardware supportano solo configurazioni specifiche di unità di scala dati, in modo da garantire che il vantaggio della scalabilità dell'appliance superi il costo della ridistribuzione dei dati tra più nodi di calcolo.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Esempi di configurazione di unità di scala dati-HPE  
Di seguito sono riportati alcuni esempi delle configurazioni HPE supportate per la scalabilità dei dati Uunits. Potrebbero variare rispetto alle configurazioni supportate più recenti, ma sono fornite come esempio per aumentare la capacità di circa il 20%.  
  
Il sollevamento è il miglioramento della capacità di percentuale aumentando il numero di Uunits di scalabilità dei dati da una riga a quella successiva. Ad esempio, l'aumento delle unità di scala dei dati da 6 a 8 garantisce un incremento del 33% nei core CPU e nella memoria.  Aumenta anche lo spazio su disco non visualizzato in questa tabella.  
  
|Unità di scala dei dati|Nodi di calcolo|Core CPU|Memoria (GB)|Leggermente più alto|  
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
  
-   **Unità di scala dei dati** per dispositivo. Per informazioni sulle unità di scala dei dati, vedere [componenti hardware del sistema della piattaforma di analisi](hardware-components.md).  
  
-   **Nodi di calcolo** per ogni appliance.  
  
-   **Core CPU** per Appliance. Sono disponibili 16 core per ogni nodo di calcolo, un core per ogni coppia di dischi con mirroring. Per la struttura del disco del nodo di calcolo, vedere [componenti hardware del sistema della piattaforma di analisi](hardware-components.md).  
  
-   **Memoria** per Appliance. Ogni core ha 256 GB di memoria.  
  
### <a name="data-scale-unit-configuration-examples---dell-quanta"></a>Esempi di configurazione di unità di scala dati-dell, Quantum  
Di seguito sono riportati esempi delle configurazioni dell e Quantum supportate per la scalabilità dei dati Uunits. Potrebbero variare rispetto alle configurazioni supportate più recenti, ma sono fornite come esempio per aumentare la capacità di circa il 20%.  
  
Il sollevamento è il miglioramento della capacità di percentuale aumentando il numero di Uunits di scalabilità dei dati da una riga a quella successiva. Ad esempio, l'aumento delle unità di scala dei dati da 6 a 8 garantisce un incremento del 33% nei core CPU e nella memoria. Aumenta anche lo spazio su disco non visualizzato in questa tabella.  
  
|Unità di scala dei dati|Nodi di calcolo|Core CPU|Memoria (GB)|Leggermente più alto|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|3|48|768|-|  
|2|6|96|1536|100%|  
|3|9|144|2.304|50%|  
|4|12|192|3.072|33%|  
|5|15|240|3.840|25%|  
|6|18|288|4.608|20%|  
|7|21|336|5.376|17%|  
|8|24|384|6.144|14%|  
|9|27|432|6.912|13%|  
|12|36|576|9.216|33%|  
|15|45|720|11.520|25%|  
|18|54|864|13.824|20%|  
  
## <a name="section2"></a>Pianificazione della capacità di archiviazione  
Questa tabella stima che è possibile caricare e archiviare fino a 6 petabyte di dati non compressi in un'appliance del sistema di piattaforma di analisi completamente compilata. 
  
|Console|Dimensioni dell'unità|Archiviazione dati fisica per nodo di calcolo|Numero massimo di nodi di calcolo per rack|Archiviazione dati massima fisica per rack|Spazio di archiviazione dati massimo stimato per rack|Numero massimo di rack|Archiviazione dati massima stimata per dispositivo|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2.240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4.480 TB|  
|HPE|4 TB|64 TB|8|512 TB|1280 TB|7|8.960 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|2.160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4.320 TB|  
|DELL|4 TB|64 TB|9|576 TB|1440 TB|6|8.640 TB|   
  
Spiegazione:  
  
-   Le **dimensioni dell'unità** sono pari a 1, 2 o 4 TB per ogni fornitore di hardware.  
  
-   **Archiviazione dati fisica per nodo di calcolo** = (dimensione unità) * (16 dischi per nodo di calcolo). I dischi con mirroring non sono inclusi perché sono per la ridondanza.  
  
-   Il **numero massimo di nodi di calcolo per rack** è specifico del fornitore dell'hardware.  
  
-   **Archiviazione dati massima fisica per rack** = (archiviazione dati fisica per nodo di calcolo) * (numero massimo di nodi di calcolo per rack).  
  
-   **Spazio di archiviazione dati massimo stimato per rack** = (archiviazione dati massima fisica per rack) * (5 per un rapporto di \* compressione 5:1) (50% per log e tempdb). Si tratta di una stima conservativa per i dati utente non compressi che possono essere caricati e archiviati nel dispositivo. Si tratta di una stima e non viene applicata dal software. L'archiviazione dei dati utente effettiva dipende dai dati e dalla configurazione.  
  
-   Il **numero massimo di rack** è specifico per ogni fornitore di hardware.  
  
-   **Spazio di archiviazione dati massimo stimato per appliance** = (spazio di archiviazione dati massimo stimato per rack) * (numero massimo di rack). Si tratta di una stima conservativa delle dimensioni totali complessive dei dati utente che è possibile caricare e archiviare in un'appliance completamente compilata.  
  
