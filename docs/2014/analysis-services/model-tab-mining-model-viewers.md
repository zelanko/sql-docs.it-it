---
title: Scheda modello (Visualizzatori modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.timeseries.decisiontree.f1
ms.assetid: 50570bb4-fcac-411e-b530-0398437efda7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05c0a25ceded07264e4dbe10467e9dc6f093f6c0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077614"
---
# <a name="model-tab-mining-model-viewers"></a>Scheda Modello (Visualizzatori modello di data mining)
  Nella scheda **Modello** del Visualizzatore Microsoft Time Series viene visualizzata una rappresentazione di una serie temporale come nodo in un grafico, simile a quella usata nei modelli di albero delle decisioni.  
  
 Utilizzare questa vista di un modello Time Series per estrarre informazioni utili sull'analisi della serie temporale, inclusi l'equazione per il grafico e i termini e i coefficienti ARIMA.  
  
 **Per altre informazioni:** [Algoritmo Microsoft Time Series](data-mining/microsoft-time-series-algorithm.md)e [Visualizzare un modello usando il Visualizzatore Microsoft Time Series](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)e [Algoritmo Microsoft Time Series](data-mining/microsoft-time-series-algorithm.md)  
  
## <a name="options"></a>Opzioni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Scegliere un modello di data mining da visualizzare. Il modello di data mining verrà aperto nel visualizzatore associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per l'esplorazione del modello di data mining selezionato. È possibile usare il visualizzatore personalizzato per questo tipo di modello o **Microsoft Generic Content Tree Viewer** . Se disponibili, è anche possibile utilizzare i visualizzatori plug-in.  
  
 **Zoom avanti**  
 Consente di eseguire lo zoom avanti del diagramma.  
  
 **Zoom indietro**  
 Consente di eseguire lo zoom indietro del diagramma.  
  
 **Copia parte visibile del grafico**  
 Consente di copiare la sezione visibile del diagramma negli Appunti.  
  
 **Copia grafico intero**  
 Consente di copiare tutto il diagramma negli Appunti.  
  
 **Ridimensiona e adatta il diagramma alla finestra**  
 Consente di eseguire lo zoom indietro del diagramma finché l'intero diagramma non si adatta alla schermata.  
  
 **Albero**  
 Consente di selezionare un albero nell'elenco a discesa da mostrare nel visualizzatore  
  
 Se nel modello Time Series sono incluse più serie, ognuna di esse viene rappresentata come albero separato. Ad esempio, se nel tempo sono state create stime sia per [Quantity] sia per [Sales Amount], viene creata una serie separata per ogni attributo stimabile.  
  
 La lunghezza dell'evidenziazione colorata nell'elenco indica il numero di livelli nell'albero. Ovvero, un modello Time Series che può essere rappresentato da un singolo nodo disporrebbe di una sola equazione per descrivere la tendenza e la barra colorata sarebbe molto corta. Naturalmente, se il modello è di tipo MIXED, nel nodo saranno contenute sia un'equazione ARIMA sia ARTxp.  
  
 Se l'albero mostrato nell'elenco a discesa dispone di una barra colorata più lunga significa che il modello dispone di molti rami nell'albero. In caso di diramazione la regressione è più complessa e il modello deve essere suddiviso in più segmenti con un'equazione diversa (o coppia di equazioni) in ogni nodo.  
  
 **Background**  
 Utilizzare questo controllo per selezionare lo stato rappresentato dal colore di sfondo in ogni nodo.  
  
 **Espansione predefinita**  
 Consente di impostare il numero predefinito di livelli visualizzati per tutti gli alberi nel modello.  
  
 **Mostra livello**  
 Consente di modificare il numero di livelli visualizzati nell'albero.  
  
## <a name="see-also"></a>Vedi anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visualizzatori modello di data mining](data-mining/data-mining-model-viewers.md)  
  
  
