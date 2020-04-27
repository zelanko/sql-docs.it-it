---
title: Visualizzare un modello utilizzando il Visualizzatore Microsoft Naive Bayes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discrimination [Analysis Services]
- naive bayes model [Analysis Services]
- Bayesian classifiers
- mining model content, viewing
- predictive modeling [Analysis Services]
- Naive Bayes Viewer [Analysis Services]
- data mining [Analysis Services], predictive modeling
- Microsoft Naive Bayes Viewer
- histograms [Analysis Services]
- mining models [Analysis Services], predictive modeling
- dependencies [Analysis Services]
ms.assetid: 19743095-63c1-4486-8c1d-2efc143243be
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 668ca4cfae7b660ff9e44de06c8523d8f9324cc9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086025"
---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>Visualizzare un modello utilizzando il Visualizzatore Microsoft Naive Bayes
  Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] visualizzatore Naive Bayes in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di visualizzare i modelli di data mining [!INCLUDE[msCoName](../../includes/msconame-md.md)] compilati con l'algoritmo Naive Bayes. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes è un algoritmo di classificazione altamente adattabile alle attività di modellazione predittiva. Per altre informazioni su questo algoritmo, vedere [Algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm.md).  
  
 Poiché uno degli scopi principali di un modello Naive Bayes consiste nell'esplorare rapidamente i dati di un set, il Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes include diversi metodi per la visualizzazione dell'interazione tra gli attributi stimabili e gli attributi di input per una tabella del case.  
  
> [!NOTE]  
>  Per visualizzare informazioni dettagliate sulle equazioni utilizzate nel modello e sugli schemi individuati, utilizzare il [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer. Per altre informazioni, vedere [Visualizzare un modello usando Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Microsoft Generic Content Tree Viewer &#40;Data mining&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>Schede del Visualizzatore  
 Per la visualizzazione di un modello di data mining in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]viene utilizzato il visualizzatore appropriato nella scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining. Per l'esplorazione dei dati, nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes sono disponibili le schede seguenti:  
  
-   [Rete di dipendenze](#BKMK_Dependency)  
  
-   [Profili attributo](#BKMK_Profiles)  
  
-   [Caratteristiche attributo](#BKMK_Characteristics)  
  
-   [Analisi discriminante attributi](#BKMK_Discrimination)  
  
##  <a name="dependency-network"></a><a name="BKMK_Dependency"></a>Rete di dipendenze  
 Nella scheda **Rete di dipendenze** vengono visualizzate le dipendenze tra gli attributi di input e gli attributi stimabili di un modello. Il dispositivo di scorrimento a sinistra del visualizzatore svolge la funzione di filtro correlato ai livelli di attendibilità delle dipendenze. Se si sposta il dispositivo di scorrimento verso il basso, vengono visualizzati solo i collegamenti più attendibili.  
  
 Quando si seleziona un nodo, nel visualizzatore vengono evidenziate le dipendenze specifiche del nodo. Se ad esempio si sceglie un nodo stimabile, nel visualizzatore verrà inoltre evidenziato ogni nodo che contribuisce alla stima del nodo stimabile.  
  
 La legenda nella parte inferiore del visualizzatore consente di individuare le corrispondenze tra i colori e i tipi di dipendenza rappresentati nel grafico. Ad esempio, quando si seleziona un nodo stimabile, a quest'ultimo viene applicata un'ombreggiatura turchese mentre ai nodi utilizzati per la stima del nodo selezionato viene applicata un'ombreggiatura arancione.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
##  <a name="attribute-profiles"></a><a name="BKMK_Profiles"></a> Profili attributo  
 Nella scheda **Profili attributo** viene visualizzata una griglia con istogrammi. Tale griglia consente di confrontare l'attributo stimabile selezionato nella casella **Stimabile** con tutti gli altri attributi del modello. Ogni colonna della scheda rappresenta uno stato dell'attributo stimabile. Se l'attributo stimabile include molti stati, è possibile modificare il numero di stati visualizzati nell'istogramma regolando le **Barre istogramma**. Se il numero scelto è inferiore al numero totale di stati dell'attributo, gli stati saranno elencati nell'ordine in cui vengono supportati, con gli stati rimanenti raccolti in un singolo bucket grigio.  
  
 Fare clic sulla casella di controllo **Mostra legenda** per visualizzare una legenda di data mining che consente di individuare le corrispondenze tra i colori dell'istogramma e gli stati di un attributo. Nella legenda di data mining viene visualizzata anche la distribuzione di case per ogni coppia attributo-valore selezionata.  
  
 Per copiare il contenuto della griglia negli Appunti in formato tabella HTML, fare clic con il pulsante destro del mouse sulla scheda **Profili attributo** e scegliere **Copia**.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
##  <a name="attribute-characteristics"></a><a name="BKMK_Characteristics"></a>Caratteristiche degli attributi  
 Per usare la scheda **Caratteristiche attributo** , è necessario selezionare un attributo stimabile dall'elenco **Attributo** e uno degli stati corrispondenti dall'elenco **Valore** . Quando si impostano tali variabili, nella scheda **Caratteristiche attributo** vengono visualizzati gli stati degli attributi associati al case dell'attributo selezionato. Gli attributi vengono ordinati in base alla priorità.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
##  <a name="attribute-discrimination"></a><a name="BKMK_Discrimination"></a>Discriminazione degli attributi  
 Per usare la scheda **Analisi discriminante attributi** , è necessario selezionare un attributo stimabile e due degli stati corrispondenti dagli elenchi **Attributo**, **Valore 1**e **Valore 2** . Nella griglia della scheda **Analisi discriminante attributi** verranno visualizzate colonne con le informazioni seguenti:  
  
 **Attributo**  
 Elenca altri attributi nel set di dati contenente uno stato che predilige in modo significativo uno stato dell'attributo stimabile.  
  
 **Valori**  
 Mostra il valore dell'attributo nella colonna **Attributo**.  
  
 **Predilige \<il valore 1>**  
 Mostra una barra colorata che indica in quale misura il valore dell'attributo predilige il valore dell'attributo stimabile mostrato in **Valore 1**.  
  
 **Predilige \<il valore 2>**  
 Mostra una barra colorata che indica in quale misura il valore dell'attributo predilige il valore dell'attributo stimabile mostrato in **Valore 2**.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vedi anche  
 [Algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm.md)   
 [Attività e procedure relative al Visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Strumenti di data mining](data-mining-tools.md)   
 [Visualizzatori modello di data mining](data-mining-model-viewers.md)  
  
  
