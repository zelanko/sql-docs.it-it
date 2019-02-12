---
title: Esplorazione del modello Naive Bayes (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: eb35c829b798335a27a37629711acf299ac2c7c9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023532"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>Esplorazione del modello Naive Bayes (Esercitazione di base sul data mining)
  Il [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Naive Bayes fornisce diversi metodi per la visualizzazione dell'interazione tra l'acquisto di biciclette e gli attributi di input.  
  
 Il [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizzatore Naive Bayes sono disponibili le schede seguenti per l'esplorazione dei modelli di data mining Naive Bayes:  
  
 
  
##  <a name="DependencyNetwork"></a> Rete di dipendenze  
 Il **rete di dipendenze** pressione di tab funziona esattamente come le **rete di dipendenze** per la scheda di [!INCLUDE[msCoName](../includes/msconame-md.md)] Tree Viewer. Ogni nodo nel visualizzatore rappresenta un attributo e le righe tra i nodi rappresentano le relazioni. Nel visualizzatore è possibile osservare tutti gli attributi che influiscono sullo stato dell'attributo stimabile, ovvero Bike Buyer.  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Per esplorare il modello nella scheda Rete di dipendenze  
  
1.  Usare la **modello di Data Mining** elenco nella parte superiore del **visualizzatore modello di Data Mining** tab per passare al `TM_NaiveBayes` modello.  
  
2.  Usare la **Viewer** elenco per aprirlo **visualizzatore Microsoft Naive Bayes**.  
  
3.  Fare clic su di `Bike Buyer` nodo per identificarne le dipendenze.  
  
     L'ombreggiatura rosa indica che tutti gli attributi influenzano l'acquisto di biciclette.  
  
4.  Regolare il dispositivo di scorrimento per identificare l'attributo più influente.  
  
     Spostando verso il basso il dispositivo di scorrimento rimangono visibili solo gli attributi che incidono maggiormente sulla colonna [Bike Buyer]. Se si sposta il dispositivo di scorrimento è possibile individuare che alcuni degli attributi più influenti sono il numero di automobili possedute, la distanza dal luogo di lavoro e il numero complessivo di figli.  
 
  
##  <a name="AttributeProfiles"></a> Profili attributo  
 Il **profili attributo** scheda descrive come i diversi stati dell'effetto di attributi di input, il risultato dell'attributo stimabile.  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>Per esplorare il modello nella scheda Profili attributo  
  
1.  Nel **stimabile** verificare che `Bike Buyer` sia selezionata.  
  
2.  Se il **legenda Data Mining** blocca la visualizzazione delle **profili dell'attributo**, spostarla dall'area di lavoro.  
  
3.  Nel **istogramma** barre, quindi selezionare **5**.  
  
     Nel modello utilizzato in questo esempio 5 è il numero massimo di stati per ogni singola variabile.  
  
     Gli attributi che influiscono sullo stato di questo attributo stimabile vengono elencati in combinazione con i valori di ogni stato degli attributi di input e la loro distribuzione in ogni stato dell'attributo stimabile.  
  
4.  Nel **attributi** colonna, trovare **Number Cars Owned**.  Si notino le differenze negli istogrammi tra gli acquirenti di biciclette (la colonna con etichetta 1) e i non acquirenti (la colonna con etichetta 0). È molto più probabile che una bicicletta venga acquistata da una persona priva di automobili o che ne possiede una sola.  
  
5.  Fare doppio clic il **Number Cars Owned** cella degli acquirenti di biciclette colonna (colonna con etichettata 1).  
  
     Il **legenda Data Mining** consente di visualizzare una visualizzazione più dettagliata.  
  
  
##  <a name="AttributeCharacteristics"></a> Caratteristiche attributo  
 Con il **caratteristiche attributo** scheda, è possibile selezionare un attributo e valore da vedere con quale frequenza i valori per gli altri attributi vengono visualizzati nei casi valore selezionato.  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>Per esplorare il modello nella scheda Caratteristiche attributo  
  
1.  Nel **attributo** elenco, verificare che `Bike Buyer` sia selezionata.  
  
2.  Impostare il **valore** al **1**.  
  
     Nel visualizzatore si osserverà che è più probabile che una bicicletta venga acquistata dai clienti senza figli, che abitano a breve distanza dal luogo di lavoro e che vivono nell'area dell'America del nord.  
  
  
##  <a name="AttributeDiscrimination"></a> Analisi discriminante attributi  
 Con il **analisi discriminante attributi** scheda, è possibile esaminare la relazione tra due valori discreti dell'acquisto di biciclette e altri valori di attributo. Poiché il `TM_NaiveBayes` modello ha solo due stati, 1 e 0, non è necessario apportare modifiche al visualizzatore.  
  
 Nel visualizzatore è possibile osservare che le persone che non possiedono un'automobile tendenzialmente acquistano biciclette, mentre le persone che possiedono due automobili in genere non ne acquistano.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per esplorare gli altri modelli di data mining, vedere gli argomenti seguenti.  
  
-   [Esplorazione del modello di albero delle decisioni &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Esplorazione del modello di Clustering &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 5: Testare i modelli &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Esplorazione del modello di Clustering &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare un modello usando il visualizzatore Microsoft Naive Bayes](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [Scheda Analisi discriminante dell'attributo &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [Attributo definisce il profilo della scheda &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [Scheda Caratteristiche attributo &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [Scheda rete di dipendenze &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  
