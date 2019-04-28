---
title: Visualizzatori dei modelli (Progettazione modelli di Data Mining) di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.viewers.f1
ms.assetid: 4ba391d5-c97b-4848-ba7c-7d096fa4b7dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7890360221f3adae73efef7a58ae1179e19760a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727937"
---
# <a name="mining-model-viewers-data-mining-model-designer"></a>Visualizzatori modello di data mining (Progettazione modelli di data mining)
  Usare la scheda **Visualizzatore modello di data mining** per l'esplorazione dei modelli di data mining contenuti in una struttura di data mining.  
  
 Prima si seleziona il modello di data mining, quindi si seleziona un visualizzatore. In ogni modello sono sempre presenti due visualizzatori: un visualizzatore personalizzato in cui possono essere incluse più schede e il visualizzatore generico.  
  
 Per una procedura dettagliata sull'utilizzo di ogni visualizzatore, vedere [Visualizzatori modello di Data Mining](data-mining/data-mining-model-viewers.md).  
  
## <a name="common-options"></a>Opzioni comuni  
 **Aggiorna contenuto visualizzatore**  
 Consente di ricaricare il modello di data mining nel visualizzatore.  
  
 **Modello di data mining**  
 Fare clic su un modello di data mining da visualizzare contenuto nella struttura di data mining corrente. Il modello di data mining verrà prima aperto nel visualizzatore personalizzato associato.  
  
 **Visualizzatore**  
 Consente di scegliere un visualizzatore da utilizzare per l'esplorazione del modello di data mining selezionato. Nell'elenco sono inclusi i visualizzatori forniti da [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] per ogni modello di data mining, il Visualizzatore contenuto di data mining [!INCLUDE[msCoName](../includes/msconame-md.md)] e gli eventuali visualizzatori plug-in.  
  
 Nel diagramma seguente vengono mostrati il visualizzatore personalizzato e quello generico per lo stesso modello.  
  
-   Nel diagramma superiore viene mostrato il visualizzatore per un modello di data mining basato sull'algoritmo Microsoft Time Series. Questo particolare visualizzatore personalizzato consente di creare automaticamente un grafico della serie temporale e fornisce cinque stime.  
  
-   L'immagine inferiore illustra lo stesso modello visualizzato usando **Microsoft Generic Content Tree Viewer**. In questo visualizzatore viene presentato il contenuto del modello di data mining in base a uno schema standardizzato. Per altre informazioni, vedere [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](microsoft-generic-content-tree-viewer-data-mining.md).  
  
 ![Panoramica di progettazione modelli di data mining](media/generic-mining-model-tab1.gif "Panoramica della progettazione di modelli di data mining")  
  
## <a name="viewers-and-their-components"></a>Visualizzatori e relativi componenti  
 A seconda del modello selezionato, verrà mostrato un visualizzatore diverso, adattato all'algoritmo utilizzato per creare il modello di data mining selezionato. In ogni visualizzatore personalizzato sono disponibili molti strumenti e finestre di dialogo che consentono di esplorare le statistiche e gli schemi del modello.  
  
 Nell'elenco seguente vengono descritte le opzioni di ogni visualizzatore personalizzato.  
  
### <a name="microsoft-association-rules-algorithm"></a>Algoritmo Microsoft Association Rules  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Association Rules](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
    -   [Scheda set di elementi &#40;visualizzatore modello di Data Mining&#41;](itemsets-tab-mining-model-viewer.md)  
  
    -   [Scheda regole &#40;visualizzatore modello di Data Mining&#41;](rules-tab-mining-model-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;visualizzatore modello di Data Mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
### <a name="microsoft-clustering-algorithm"></a>Algoritmo Microsoft Clustering  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Clustering](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
    -   [Scheda diagramma dei cluster &#40;visualizzatore modello di Data Mining&#41;](cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [Scheda profili di cluster &#40;visualizzatore modello di Data Mining&#41;](cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [Scheda caratteristiche cluster &#40;visualizzatore modello di Data Mining&#41;](cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [Scheda Analisi discriminante del cluster &#40;visualizzatore modello di Data Mining&#41;](cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [Finestra di dialogo legenda data mining &#40;visualizzatore modello di Data Mining&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-decision-tree-algorithm"></a>Algoritmo Microsoft Decision Trees  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Decision Trees](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
    -   [Scheda albero decisionale &#40;visualizzatore modello di Data Mining&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;visualizzatore modello di Data Mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Finestra di dialogo legenda data mining &#40;visualizzatore modello di Data Mining&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-linear-regression-algorithm"></a>Algoritmo Microsoft Linear Regression  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Neural Network](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [Scheda albero decisionale &#40;visualizzatore modello di Data Mining&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;visualizzatore modello di Data Mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Finestra di dialogo legenda data mining &#40;visualizzatore modello di Data Mining&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-logistic-regression-algorithm"></a>Algoritmo Microsoft Logistic Regression  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Neural Network](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
### <a name="microsoft-nave-bayes-algorithm"></a>Algoritmo Microsoft Naive Bayes  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Naive Bayes](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;visualizzatore modello di Data Mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Attributo definisce il profilo della scheda &#40;visualizzatore modello di Data Mining&#41;](attribute-profiles-tab-mining-model-viewer.md)  
  
    -   [Scheda Caratteristiche attributo &#40;visualizzatore modello di Data Mining&#41;](attribute-characteristics-tab-mining-model-viewer.md)  
  
    -   [Scheda Analisi discriminante dell'attributo &#40;visualizzatore modello di Data Mining&#41;](attribute-discrimination-tab-mining-model-viewer.md)  
  
### <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Neural Network](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;visualizzatore modello di Data Mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Rete neurale &#40;visualizzatore modello di Data Mining&#41;](neural-network-mining-model-viewer.md)  
  
    -   [Dialogo Trova nodo &#40;visualizzatore modello di Data Mining&#41;](find-node-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-sequence-clustering-algorithm"></a>Algoritmo Microsoft Sequence Clustering  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Sequence Clustering](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
    -   [Scheda diagramma dei Cluster di Clustering delle sequenze &#40;visualizzatore modello di Data Mining](sequence-clustering-cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [Sequence Clustering Cluster definisce il profilo della scheda &#40;visualizzatore modello di Data Mining](sequence-clustering-cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [Scheda caratteristiche Cluster di Clustering delle sequenze &#40;visualizzatore modello di Data Mining&#41;](sequence-clustering-cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [Scheda Analisi discriminante tra Cluster di Clustering delle sequenze &#40;visualizzatore modello di Data Mining&#41;](sequence-clustering-cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [Sequence Clustering scheda transizioni di stato &#40;visualizzatore modello di Data Mining&#41;](sequence-clustering-cluster-transition-tab-mining-model-viewer.md)  
  
### <a name="microsoft-time-series-algorithm"></a>Algoritmo Microsoft Time Series  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Times Series](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
    -   [Modello della scheda &#40;visualizzatori modello di Data Mining&#41;](model-tab-mining-model-viewers.md)  
  
    -   [Grafico della scheda &#40;visualizzatori modello di Data Mining&#41;](chart-tab-mining-model-viewers.md)  
  
    -   [Finestra di dialogo legenda data mining &#40;visualizzatore modello di Data Mining&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzazione di modelli di data mining &#40;Progettazione modelli di Data Mining&#41;](mining-models-view-data-mining-model-designer.md)   
 [Visualizzazione struttura di data mining &#40;Progettazione modelli di Data Mining&#41;](mining-structure-view-data-mining-model-designer.md)   
 [Finestra di progettazione grafico accuratezza di data mining &#40;Data Mining&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Generatore di Query di stima &#40;Data Mining&#41;](prediction-query-builder-data-mining.md)  
  
  
