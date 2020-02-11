---
title: Visualizzatori modello di data mining (Progettazione modelli di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.viewers.f1
ms.assetid: 4ba391d5-c97b-4848-ba7c-7d096fa4b7dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67cd89f4cf857f11f08f69769ff54a22fd83760f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077724"
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
 Consente di scegliere un visualizzatore da utilizzare per l'esplorazione del modello di data mining selezionato. In questo elenco sono inclusi i [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] visualizzatori forniti da per ogni modello [!INCLUDE[msCoName](../includes/msconame-md.md)] di data mining, il Visualizzatore contenuto di data mining e gli eventuali visualizzatori plug-in.  
  
 Nel diagramma seguente vengono mostrati il visualizzatore personalizzato e quello generico per lo stesso modello.  
  
-   Nel diagramma superiore viene mostrato il visualizzatore per un modello di data mining basato sull'algoritmo Microsoft Time Series. Questo particolare visualizzatore personalizzato consente di creare automaticamente un grafico della serie temporale e fornisce cinque stime.  
  
-   L'immagine inferiore illustra lo stesso modello visualizzato usando **Microsoft Generic Content Tree Viewer**. In questo visualizzatore viene presentato il contenuto del modello di data mining in base a uno schema standardizzato. Per altre informazioni, vedere [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](microsoft-generic-content-tree-viewer-data-mining.md).  
  
 ![Panoramica di Progettazione modelli di data mining](media/generic-mining-model-tab1.gif "Panoramica di Progettazione modelli di data mining")  
  
## <a name="viewers-and-their-components"></a>Visualizzatori e relativi componenti  
 A seconda del modello selezionato, verrà mostrato un visualizzatore diverso, adattato all'algoritmo utilizzato per creare il modello di data mining selezionato. In ogni visualizzatore personalizzato sono disponibili molti strumenti e finestre di dialogo che consentono di esplorare le statistiche e gli schemi del modello.  
  
 Nell'elenco seguente vengono descritte le opzioni di ogni visualizzatore personalizzato.  
  
### <a name="microsoft-association-rules-algorithm"></a>Algoritmo Microsoft Association Rules  
  
-   [Visualizzare un modello utilizzando il Visualizzatore Microsoft Association Rules](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
    -   [Scheda set di elementi &#40;Visualizzatore modello di data mining&#41;](itemsets-tab-mining-model-viewer.md)  
  
    -   [Scheda regole &#40;Visualizzatore modello di data mining&#41;](rules-tab-mining-model-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;Visualizzatore modello di data mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
### <a name="microsoft-clustering-algorithm"></a>Algoritmo Microsoft Clustering  
  
-   [Visualizzare un modello utilizzando il Visualizzatore Microsoft Clustering](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
    -   [Scheda Diagramma cluster &#40;Visualizzatore modello di data mining&#41;](cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [Scheda Profili cluster &#40;Visualizzatore modello di data mining&#41;](cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [Scheda Caratteristiche cluster &#40;Visualizzatore modello di data mining&#41;](cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [Scheda Analisi discriminante tra cluster &#40;Visualizzatore modello di data mining&#41;](cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [Finestra di dialogo Legenda data mining &#40;Visualizzatore modello di data mining&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-decision-tree-algorithm"></a>Algoritmo Microsoft Decision Trees  
  
-   [Visualizzare un modello utilizzando il Visualizzatore Microsoft Decision Trees](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
    -   [Scheda albero delle decisioni &#40;Visualizzatore modello di data mining&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;Visualizzatore modello di data mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Finestra di dialogo Legenda data mining &#40;Visualizzatore modello di data mining&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-linear-regression-algorithm"></a>Algoritmo Microsoft Linear Regression  
  
-   [Visualizzare un modello utilizzando il Visualizzatore Microsoft Neural Network](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [Scheda albero delle decisioni &#40;Visualizzatore modello di data mining&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;Visualizzatore modello di data mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Finestra di dialogo Legenda data mining &#40;Visualizzatore modello di data mining&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-logistic-regression-algorithm"></a>Algoritmo Microsoft Logistic Regression  
  
-   [Visualizzare un modello utilizzando il Visualizzatore Microsoft Neural Network](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
### <a name="microsoft-nave-bayes-algorithm"></a>Algoritmo Microsoft Naive Bayes  
  
-   [Visualizzare un modello utilizzando il Visualizzatore Microsoft Naive Bayes](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;Visualizzatore modello di data mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Scheda Profili attributo &#40;Visualizzatore modello di data mining&#41;](attribute-profiles-tab-mining-model-viewer.md)  
  
    -   [Scheda Caratteristiche attributo &#40;Visualizzatore modello di data mining&#41;](attribute-characteristics-tab-mining-model-viewer.md)  
  
    -   [Scheda Analisi discriminante attributi &#40;Visualizzatore modello di data mining&#41;](attribute-discrimination-tab-mining-model-viewer.md)  
  
### <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm  
  
-   [Visualizzare un modello utilizzando il Visualizzatore Microsoft Neural Network](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [Scheda rete di dipendenze &#40;Visualizzatore modello di data mining&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Visualizzatore modello di data mining &#40;di rete neurale&#41;](neural-network-mining-model-viewer.md)  
  
    -   [Finestra di dialogo Trova nodo &#40;Visualizzatore modello di data mining&#41;](find-node-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-sequence-clustering-algorithm"></a>Algoritmo Microsoft Sequence Clustering  
  
-   [Visualizzare un modello usando il Visualizzatore Microsoft Sequence Clustering](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
    -   [Scheda Diagramma cluster Sequence Clustering &#40;Visualizzatore modello di data mining](sequence-clustering-cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [Scheda Profili cluster Sequence Clustering &#40;Visualizzatore modello di data mining](sequence-clustering-cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [Scheda Caratteristiche cluster Sequence Clustering &#40;Visualizzatore modello di data mining&#41;](sequence-clustering-cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [Scheda Analisi discriminante cluster Sequence Clustering &#40;Visualizzatore modello di data mining&#41;](sequence-clustering-cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [Scheda transizione cluster Sequence Clustering &#40;Visualizzatore modello di data mining&#41;](sequence-clustering-cluster-transition-tab-mining-model-viewer.md)  
  
### <a name="microsoft-time-series-algorithm"></a>Algoritmo Microsoft Time Series  
  
-   [Visualizzare un modello utilizzando il Visualizzatore Microsoft Times Series](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
    -   [Scheda modello &#40;visualizzatori modello di data mining&#41;](model-tab-mining-model-viewers.md)  
  
    -   [Scheda grafico &#40;visualizzatori modello di data mining&#41;](chart-tab-mining-model-viewers.md)  
  
    -   [Finestra di dialogo Legenda data mining &#40;Visualizzatore modello di data mining&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzazione modelli di data mining &#40;Progettazione modelli di data mining&#41;](mining-models-view-data-mining-model-designer.md)   
 [Visualizzazione struttura di data mining &#40;Progettazione modelli di data mining&#41;](mining-structure-view-data-mining-model-designer.md)   
 [Progettazione Grafico accuratezza modello di data mining &#40;&#41;di data mining](mining-accuracy-chart-designer-data-mining.md)   
 [Generatore di query di stima &#40;&#41;di data mining](prediction-query-builder-data-mining.md)  
  
  
