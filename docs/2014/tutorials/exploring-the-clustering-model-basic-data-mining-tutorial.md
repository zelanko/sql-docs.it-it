---
title: Esplorazione del modello di Clustering (esercitazione di base di Data Mining) | Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280426"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>Esplorazione del modello di clustering (Esercitazione di base sul data mining)
  Il [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Clustering Raggruppa i case in cluster con caratteristiche simili. Tali raggruppamenti sono utili per l'esplorazione dei dati, l'identificazione delle relative anomalie e la creazione di stime.  
  
 Per l'esplorazione di modelli di data mining per il clustering, nel Visualizzatore [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering sono disponibili le schede seguenti:  
  

  
##  <a name="ClusterDiagramTab"></a> Scheda diagramma dei cluster  
 Nella scheda Diagramma dei cluster vengono visualizzati tutti i cluster di un modello di data mining. Le linee tra i cluster rappresentano la prossimità e appaiono ombreggiate in base al grado di analogia dei cluster. Il colore effettivo dei cluster rappresenta la frequenza della variabile e lo stato nel cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>Per esplorare il modello nella scheda Diagramma dei cluster  
  
1.  Usare la **modello di Data Mining** elenco nella parte superiore del **visualizzatore modello di Data Mining** tab per passare al `TM_Clustering` modello.  
  
2.  Nel **Viewer** elenco, selezionare **visualizzatore Microsoft Clustering**.  
  
3.  Nel **variabile ombreggiatura** , quindi selezionare **Bike Buyer**.  
  
     La variabile predefinita è **popolamento**, ma è possibile modificarlo in qualsiasi attributo del modello, per rilevare quali cluster contengono membri che hanno gli attributi desiderati.  
  
4.  Selezionare **1** nel **stato** finestra per esplorare i case in cui è stata acquistata una bicicletta.  
  
     Il **densità** legenda descrive la densità della coppia di stato dell'attributo selezionata in variabile ombreggiatura e stato. In questo esempio indica che il clusterwith l'ombreggiatura più scura contiene la percentuale più elevata di acquirenti di biciclette.  
  
5.  Posizionare il mouse sul cluster con l'ombreggiatura più scura.  
  
     Nella descrizione comando verrà visualizzata la percentuale di case che includono l'attributo `Bike Buyer = 1`.  
  
6.  Selezionare il cluster con la densità più elevata, il pulsante destro del cluster, selezionare **Rinomina Cluster** e digitare **Bike Buyers High** per identificarlo più avanti. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Individuare il cluster con l'ombreggiatura più leggera (e la densità più bassa). Il pulsante destro del cluster, selezionare **Rinomina Cluster** e digitare **Bike Buyers Low**. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Scegliere il **Bike Buyers High** del cluster e trascinarlo in un'area del riquadro che offre una visione chiara delle relative connessioni agli altri cluster.  
  
     Quando si seleziona un cluster, le linee che lo connettono agli altri cluster vengono evidenziate, in modo che sia possibile vedere facilmente tutte le relazioni del cluster. Quando il cluster non è selezionato, dal colore delle linee è possibile dedurre il livello di relazione tra tutti i cluster del diagramma. Se l'ombreggiatura è chiara o inesistente, il grado di somiglianza dei cluster è basso.  
  
9. Utilizzare il dispositivo di scorrimento nella parte sinistra della rete per escludere i collegamenti meno attendibili e individuare i cluster con le relazioni più strette. Il reparto marketing di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] potrebbe ad esempio raggruppare i cluster simili durante l'individuazione del metodo migliore per inviare i mailing diretti.  
  

  
##  <a name="ClusterProfilesTab"></a> Scheda Profili cluster  
 Il **profili Cluster** scheda fornisce una visualizzazione complessiva del `TM_Clustering` modello. Il **profili Cluster** scheda contiene una colonna per ogni cluster nel modello. Nella prima colonna sono elencati gli attributi associati ad almeno un cluster. La parte rimanente del visualizzatore contiene la distribuzione degli stati di un attributo per ogni cluster. La distribuzione di una variabile discreta viene visualizzata come una barra colorata e il numero massimo di barre è visualizzato nei **barre istogramma** elenco. Gli attributi continui sono visualizzati sotto forma di un grafico a rombi che rappresenta la deviazione media e standard in ogni cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>Per esplorare il modello nella scheda Profili cluster  
  
1.  Impostare **istogramma** devono le barre **5**.  
  
     Nel modello utilizzato in questo esempio 5 è il numero massimo di stati per ogni singola variabile.  
  
2.  Se il **legenda Data Mining** blocca la visualizzazione delle **profili dell'attributo**, spostarla dall'area di lavoro.  
  
3.  Selezionare il **Bike Buyers High** colonna e trascinarla a destra del **popolamento** colonna.  
  
4.  Selezionare il **Bike Buyers Low** colonna e trascinarla a destra del **Bike Buyers High** colonna.  
  
5.  Scegliere il **Bike Buyers High** colonna.  
  
     Il **variabili** colonna è ordinata in ordine di importanza per tale cluster. Scorrere la colonna e verificare le caratteristiche del cluster Bike Buyers High. È ad esempio più probabile che i clienti raggruppati in questo cluster abitino a breve distanza dal luogo di lavoro.  
  
6.  Fare doppio clic il **età** cella il **Bike Buyers High** colonna.  
  
     Il **legenda Data Mining** Visualizza modo più dettagliato Vista ed è possibile visualizzare l'intervallo di questi clienti, nonché l'età media età.  
  
7.  Fare doppio clic il **Bike Buyers Low** colonna e selezionare **Nascondi colonna**.  
  

  
##  <a name="ClusterCharacteristicsTab"></a> Scheda caratteristiche cluster  
 Con il **caratteristiche Cluster** scheda, è possibile esaminare in dettaglio le caratteristiche che costituiscono un cluster. Anziché confrontare le caratteristiche di tutti i cluster (come nella scheda Profili cluster), è possibile esplorare un cluster alla volta. Ad esempio, se si seleziona **Bike Buyers High** dalle **Cluster** elenco, è possibile visualizzare le caratteristiche dei clienti in questo cluster. Sebbene la visualizzazione sia diversa dalla scheda Profili cluster, i risultati sono gli stessi.  
  
> [!NOTE]  
>  A meno che non si imposta un valore iniziale per **holdoutseed**, risultati varieranno ogni volta che si elabora il modello. Per altre informazioni, vedere [elemento HoldoutSeed](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element)  
  

  
##  <a name="ClusterDiscriminationTab"></a> Scheda Analisi discriminante tra cluster  
 Con il **analisi discriminante tra Cluster** scheda, è possibile esplorare le caratteristiche che distinguono ogni cluster da un altro. Dopo aver selezionato due cluster, uno dal **Cluster 1** elenco e uno dalle **Cluster 2** elenco, il Visualizzatore calcola le differenze tra i cluster e visualizza un elenco degli attributi che distinguono maggiormente i cluster.  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>Per esplorare il modello nella scheda Analisi discriminante tra cluster  
  
1.  Nel **Cluster 1** , quindi selezionare **Bike Buyers High**.  
  
2.  Nel **Cluster 2** , quindi selezionare **Bike Buyers Low**.  
  
3.  Fare clic su **variabili** per ordinare in ordine alfabetico.  
  
     Alcune delle differenze più sostanziali fra i clienti nel **Bike Buyers Low** e **Bike Buyers High** cluster includono l'età, automobile, il numero di figli e l'area.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per esplorare gli altri modelli di data mining, vedere gli argomenti seguenti.  
  
-   [Esplorazione del modello di albero delle decisioni &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Esplorazione del modello Naive Bayes &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esplorazione del modello Naive Bayes &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Esplorazione del modello di albero delle decisioni &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare un modello usando il visualizzatore Microsoft Clustering](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [Scheda Analisi discriminante del cluster &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [Scheda profili di cluster &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [Scheda caratteristiche cluster &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [Scheda diagramma dei cluster &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
