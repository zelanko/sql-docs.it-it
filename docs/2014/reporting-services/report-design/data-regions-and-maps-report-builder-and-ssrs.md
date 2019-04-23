---
title: Aree dati e mappe (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data regions
ms.assetid: 3afb8874-b36c-4e44-a0d8-80d2f7135fb1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 590cbab5e2b4091c4d0112914631f57d6f7bc8ea
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59933907"
---
# <a name="data-regions-and-maps-report-builder-and-ssrs"></a>Aree dati e mappe (Generatore report e SSRS)
  Un'area dati è un oggetto in un report che consente di visualizzare dati da un set di dati del report. I dati del report possono essere visualizzati come numeri e testo in una tabella, una matrice o un elenco, graficamente in un grafico o un misuratore e su uno sfondo geografico in una mappa. Le tabelle, le matrici e gli elenchi sono tutti basati sull'area dati *Tablix* , che si espande in base alle necessità per visualizzare tutti i dati dal set di dati. Un'area dati Tablix supporta più gruppi di righe e colonne, nonché righe e colonne statiche e dinamiche. Un grafico consente di visualizzare più serie e gruppi di categorie in un'ampia gamma di formati di grafico. Un misuratore consente di visualizzare un singolo valore o un valore aggregato per un set di dati. Una mappa consente di visualizzare dati spaziali come elementi della mappa che possono variare nell'aspetto in base ai dati aggregati di un set di dati.  
  
 È possibile salvare un'area dati o eseguire il mapping come parte del report. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="table"></a>Tabella  
 Una tabella è un'area dati in cui i dati vengono presentati riga per riga. Le colonne della tabella sono statiche, ovvero il numero di colonne viene definito dall'utente durante la progettazione del report. Le righe della tabella sono dinamiche e si espandono verso il basso per includere tutti i dati. È possibile aggiungere gruppi alle tabelle, in modo da organizzare i dati in base ai campi selezionati o tramite espressioni. Per informazioni sull'aggiunta di una tabella a un report, vedere [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md).  
  
## <a name="matrix"></a>Matrice  
 Una matrice è nota anche come area dati a campi incrociati. Un'area dati della matrice contiene sia colonne che righe dinamiche che si espandono in modo da includere tutti i dati. Una matrice può includere colonne e righe dinamiche, nonché colonne e righe statiche. Le colonne e le righe possono contenere altre colonne o righe e possono essere usate per raggruppare i dati. Per informazioni sull'aggiunta di una matrice a un report, vedere [matrici &#40;Generatore Report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)  
  
## <a name="list"></a>List  
 Un elenco è un'area dati in cui i dati possono essere disposti liberamente. È possibile disporre gli elementi dei report in modo da creare un form, con caselle di testo, immagini e altre aree dati inserite in qualsiasi punto all'interno dell'elenco. Per informazioni sull'aggiunta di un elenco a un report, vedere [sono elencati &#40;Generatore Report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
## <a name="chart"></a>Grafico  
 Un grafico consente di rappresentare graficamente i dati. I grafici possono essere, ad esempio, a barre, a torta e a linee, ma sono supportati numerosi altri stili. Per informazioni sull'aggiunta di un grafico a un report, vedere [i grafici &#40;Generatore Report e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
## <a name="gauge"></a>Misuratore  
 Un misuratore presenta i dati sotto forma di intervallo con un indicatore che punta a un valore specifico all'interno dell'intervallo. I misuratori sono usati per visualizzare indicatori di prestazioni chiave (KPI) e altre metriche. Esempi di misuratori sono quelli lineari e circolari. Per altre informazioni sull'aggiunta di un misuratore a un report, vedere [misura &#40;Generatore Report e SSRS&#41;](gauges-report-builder-and-ssrs.md).  
  
## <a name="map"></a>Mappa  
 Una mappa consente di presentare dati su uno sfondo geografico. Tali dati possono essere dati spaziali ottenuti da una query di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , un file di forma ESRI o tessere mappa di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing. I dati spaziali sono costituiti da set di coordinate che definiscono poligoni che rappresentano forme o aree, linee che rappresentano itinerari o percorsi e punti rappresentati da marcatori. È possibile associare dati aggregati a elementi della mappa per variarne automaticamente colore e dimensione. È possibile, ad esempio, variare il tipo di marcatore per un archivio basato sugli importi delle vendite o il colore per una strada basata sul limite di velocità. Per altre informazioni, vedere [Mappe &#40;Generatore report e SSRS&#41;](maps-report-builder-and-ssrs.md).  
  
## <a name="data-regions-in-the-report-layout"></a>Aree dati nel layout del report  
 È possibile aggiungere più aree dati a un report. Le aree dati si espandono in base alla quantità di dati del set di dati del report a cui sono collegate. Una matrice in cui vengono visualizzate le vendite per ogni prodotto per anno, ad esempio, include un gruppo di righe basato sui nomi di prodotto e un gruppo di colonne basato sugli anni. Quando si esegue il report, la matrice si espande verso la parte inferiore della pagina per ogni prodotto e attraverso la pagina per ogni anno. Un grafico posizionato accanto alla matrice sull'area di progettazione del report viene visualizzato accanto alla matrice espansa nel report visualizzabile. La modalità di rendering delle aree dati in una pagina segue un set di regole basate sul formato di output di un report. Per semplificare il controllo del rendering di un grafico e una matrice in una pagina, ad esempio, è necessario usare un rettangolo come contenitore o annidare entrambe le aree dati in un elenco. Per altre informazioni, vedere [Layout e rendering della pagina &#40;Generatore report e SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md).  
  
## <a name="nested-data-regions"></a>Aree dati nidificate  
 È possibile annidare aree dati all'interno di altre aree dati. Se si desidera ad esempio creare un record delle vendite per ogni venditore in un database, è possibile creare un elenco con caselle di testo e un'immagine per visualizzare le informazioni sul dipendente, quindi aggiungere aree dati della tabella e del grafico all'elenco per visualizzare il record delle vendite del dipendente. Per altre informazioni, vedere [Aree dati annidate &#40;Generatore report e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md).  
  
## <a name="multiple-data-regions-linked-to-the-same-dataset"></a>Più aree dati collegate allo stesso set di dati  
 È possibile collegare più aree dati allo stesso set di dati per fornire viste diverse degli stessi dati. È ad esempio possibile mostrare gli stessi dati in una tabella e in un grafico. È possibile creare il report per fornire pulsanti di ordinamento interattivi nella tabella, in modo che quando si ordina la tabella, venga automaticamente ordinato anche il grafico. Per altre informazioni, vedere [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md).  
  
## <a name="data-for-a-data-region"></a>Dati per un'area dati  
 Ogni Tablix, grafico e misuratore è progettato per visualizzare dati da un singolo set di dati. Una mappa consente di visualizzare dati spaziali e dati analitici dagli stessi set di dati o da set di dati diversi. È inoltre possibile includere valori da set di dati non collegati all'area dati nei modi seguenti:  
  
-   Aggregare valori che non dipendono da un ordinamento o un raggruppamento il cui ambito è un set di dati diverso.  
  
-   Cercare valori da coppie nome-valore in un set di dati diverso.  
  
 Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla creazione di report &#40;Generatore report e SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [Report, parti del report e definizioni dei report &#40;Generatore report e SSRS&#41;](reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Layout e rendering della pagina &#40;Generatore report e SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md)   
 [Esercitazioni su &#40;Generatore Report&#41;](../report-builder-tutorials.md)   
 [Esercitazioni su Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
