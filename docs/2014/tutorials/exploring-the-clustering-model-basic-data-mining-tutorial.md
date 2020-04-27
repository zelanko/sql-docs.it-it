---
title: Esplorazione del modello di clustering (esercitazione di base sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9bb2c6457122a5ea49824ca178b6950d88f75563
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63280426"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>Esplorazione del modello di clustering (Esercitazione di base sul data mining)
  L' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo di Clustering raggruppa i case in cluster che contengono caratteristiche simili. Tali raggruppamenti sono utili per l'esplorazione dei dati, l'identificazione delle relative anomalie e la creazione di stime.  
  
 Per l'esplorazione di modelli di data mining per il clustering, nel Visualizzatore [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering sono disponibili le schede seguenti:  
  

  
##  <a name="cluster-diagram-tab"></a><a name="ClusterDiagramTab"></a>Scheda Diagramma cluster  
 Nella scheda Diagramma dei cluster vengono visualizzati tutti i cluster di un modello di data mining. Le linee tra i cluster rappresentano la prossimità e appaiono ombreggiate in base al grado di analogia dei cluster. Il colore effettivo dei cluster rappresenta la frequenza della variabile e lo stato nel cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>Per esplorare il modello nella scheda Diagramma dei cluster  
  
1.  Utilizzare l'elenco **modello di data mining** nella parte superiore della scheda **Visualizzatore modello di data mining** per `TM_Clustering` passare al modello.  
  
2.  Nell'elenco **Visualizzatore** selezionare **Microsoft cluster Viewer**.  
  
3.  Nella casella **Variabile ombreggiatura** selezionare **Bike Buyer**.  
  
     La variabile predefinita è **population**, ma è possibile modificarla in qualsiasi attributo del modello, per individuare i cluster che contengono membri che hanno gli attributi desiderati.  
  
4.  Selezionare **1** nella casella **stato** per esplorare i casi in cui è stata acquistata una bicicletta.  
  
     La legenda **densità** descrive la densità della coppia di stati degli attributi selezionata nella variabile ombreggiatura e nello stato. In questo esempio viene indicato che clusterwith l'ombreggiatura più scura ha la percentuale più alta di acquirenti di biciclette.  
  
5.  Posizionare il mouse sul cluster con l'ombreggiatura più scura.  
  
     Nella descrizione comando verrà visualizzata la percentuale di case che includono l'attributo `Bike Buyer = 1`.  
  
6.  Selezionare il cluster con la densità più elevata, fare clic con il pulsante destro del mouse sul cluster, scegliere **Rinomina cluster** e digitare **Bike Buyers High** per identificarlo in seguito. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Individuare il cluster con l'ombreggiatura più leggera (e la densità più bassa). Fare clic con il pulsante destro del mouse sul cluster, scegliere **Rinomina cluster** e digitare **Bike Buyers Low**. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Fare clic sul cluster **Bike Buyers High** e trascinarlo in un'area del riquadro che fornirà una visualizzazione chiara delle connessioni agli altri cluster.  
  
     Quando si seleziona un cluster, le linee che lo connettono agli altri cluster vengono evidenziate, in modo che sia possibile vedere facilmente tutte le relazioni del cluster. Quando il cluster non è selezionato, dal colore delle linee è possibile dedurre il livello di relazione tra tutti i cluster del diagramma. Se l'ombreggiatura è chiara o inesistente, il grado di somiglianza dei cluster è basso.  
  
9. Utilizzare il dispositivo di scorrimento nella parte sinistra della rete per escludere i collegamenti meno attendibili e individuare i cluster con le relazioni più strette. Il reparto marketing di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] potrebbe ad esempio raggruppare i cluster simili durante l'individuazione del metodo migliore per inviare i mailing diretti.  
  

  
##  <a name="cluster-profiles-tab"></a><a name="ClusterProfilesTab"></a>Scheda Profili cluster  
 La scheda **Profili cluster** fornisce una visualizzazione complessiva del `TM_Clustering` modello. La scheda **Profili cluster** contiene una colonna per ogni cluster nel modello. Nella prima colonna sono elencati gli attributi associati ad almeno un cluster. La parte rimanente del visualizzatore contiene la distribuzione degli stati di un attributo per ogni cluster. La distribuzione di una variabile discreta viene visualizzata come una barra colorata con il numero massimo di barre visualizzate nell'elenco **Barre istogramma** . Gli attributi continui sono visualizzati sotto forma di un grafico a rombi che rappresenta la deviazione media e standard in ogni cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>Per esplorare il modello nella scheda Profili cluster  
  
1.  Impostare le barre **istogramma** su **5**.  
  
     Nel modello utilizzato in questo esempio 5 è il numero massimo di stati per ogni singola variabile.  
  
2.  Se la **Legenda data mining** blocca la visualizzazione dei **Profili attributo**, spostarla all'esterno del percorso.  
  
3.  Selezionare la colonna **Bike Buyers High** e trascinarla a destra della colonna **popolazione** .  
  
4.  Selezionare la colonna **Bike Buyers Low** e trascinarla a destra della colonna **Bike Buyers High** .  
  
5.  Fare clic sulla colonna **Bike Buyers High** .  
  
     La colonna **variables** è ordinata in ordine di importanza per il cluster. Scorrere la colonna e verificare le caratteristiche del cluster Bike Buyers High. È ad esempio più probabile che i clienti raggruppati in questo cluster abitino a breve distanza dal luogo di lavoro.  
  
6.  Fare doppio clic sulla cella **Age** nella colonna **Bike Buyers High** .  
  
     In **Legenda data mining** viene visualizzata una visualizzazione più dettagliata ed è possibile visualizzare l'intervallo di tempo di questi clienti, oltre alla durata media.  
  
7.  Fare clic con il pulsante destro del mouse sulla colonna **Bike Buyers Low** e selezionare **Nascondi colonna**.  
  

  
##  <a name="cluster-characteristics-tab"></a><a name="ClusterCharacteristicsTab"></a>Scheda Caratteristiche cluster  
 Con la scheda **Caratteristiche cluster** è possibile esaminare più in dettaglio le caratteristiche che costituiscono un cluster. Anziché confrontare le caratteristiche di tutti i cluster (come nella scheda Profili cluster), è possibile esplorare un cluster alla volta. Ad esempio, se si seleziona **Bike Buyers High** dall'elenco **cluster** , è possibile visualizzare le caratteristiche dei clienti in questo cluster. Sebbene la visualizzazione sia diversa dalla scheda Profili cluster, i risultati sono gli stessi.  
  
> [!NOTE]  
>  A meno che non si imposti un valore iniziale per **HoldoutSeed**, i risultati variano ogni volta che si elabora il modello. Per altre informazioni, vedere [elemento HoldoutSeed](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element)  
  

  
##  <a name="cluster-discrimination-tab"></a><a name="ClusterDiscriminationTab"></a>Scheda Analisi discriminante tra cluster  
 Con la scheda analisi **discriminante tra cluster** è possibile esplorare le caratteristiche che distinguono un cluster da un altro. Dopo aver selezionato due cluster, uno dall'elenco **cluster 1** e uno dall'elenco **cluster 2** , il Visualizzatore calcola le differenze tra i cluster e visualizza un elenco degli attributi che distinguono maggiormente i cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>Per esplorare il modello nella scheda Analisi discriminante tra cluster  
  
1.  Nella casella **cluster 1** selezionare **Bike Buyers High**.  
  
2.  Nella casella **cluster 2** selezionare **Bike Buyers Low**.  
  
3.  Fare clic su **variabili** per ordinare alfabeticamente.  
  
     Alcune delle differenze più sostanziali tra i clienti nei cluster **Bike Buyers Low** e Bike Buyers **High** includono Age, auto ownership, Number of Children e Region.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per esplorare gli altri modelli di data mining, vedere gli argomenti seguenti.  
  
-   [Esplorazione del modello Decision Trees &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Esplorazione del modello Naive Bayes &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esplorazione del modello Naive Bayes &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Esplorazione del modello Decision Trees &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Visualizzare un modello utilizzando il Visualizzatore Microsoft Clustering](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [Scheda Analisi discriminante tra cluster &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [Scheda Profili cluster &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [Scheda Caratteristiche cluster &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [Scheda Diagramma cluster &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
