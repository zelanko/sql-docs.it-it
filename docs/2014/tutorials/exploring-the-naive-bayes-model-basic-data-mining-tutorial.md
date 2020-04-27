---
title: Esplorazione del modello Naive Bayes (esercitazione di base sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62472885"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>Esplorazione del modello Naive Bayes (Esercitazione di base sul data mining)
  L' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Naive Bayes offre diversi metodi per la visualizzazione dell'interazione tra l'acquisto di biciclette e gli attributi di input.  
  
 Nel [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizzatore Naive Bayes sono disponibili le schede seguenti da utilizzare per l'esplorazione dei modelli di data mining Naive Bayes:  
  
 
  
##  <a name="dependency-network"></a><a name="DependencyNetwork"></a>Rete di dipendenze  
 La scheda **rete di dipendenze** funziona in modo analogo alla scheda **rete di dipendenze** per il [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizzatore albero. Ogni nodo nel visualizzatore rappresenta un attributo e le righe tra i nodi rappresentano le relazioni. Nel visualizzatore è possibile osservare tutti gli attributi che influiscono sullo stato dell'attributo stimabile, ovvero Bike Buyer.  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Per esplorare il modello nella scheda Rete di dipendenze  
  
1.  Utilizzare l'elenco **modello di data mining** nella parte superiore della scheda **Visualizzatore modello di data mining** per `TM_NaiveBayes` passare al modello.  
  
2.  Utilizzare l'elenco **Visualizzatore** per passare al **Visualizzatore Microsoft Naive Bayes**.  
  
3.  Fare clic `Bike Buyer` sul nodo per identificarne le dipendenze.  
  
     L'ombreggiatura rosa indica che tutti gli attributi influenzano l'acquisto di biciclette.  
  
4.  Regolare il dispositivo di scorrimento per identificare l'attributo più influente.  
  
     Spostando verso il basso il dispositivo di scorrimento rimangono visibili solo gli attributi che incidono maggiormente sulla colonna [Bike Buyer]. Se si sposta il dispositivo di scorrimento è possibile individuare che alcuni degli attributi più influenti sono il numero di automobili possedute, la distanza dal luogo di lavoro e il numero complessivo di figli.  
 
  
##  <a name="attribute-profiles"></a><a name="AttributeProfiles"></a> Profili attributo  
 Nella scheda **Profili attributo** viene descritto il modo in cui diversi stati degli attributi di input influiscono sul risultato dell'attributo stimabile.  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>Per esplorare il modello nella scheda Profili attributo  
  
1.  Nella casella **stimabile** verificare che `Bike Buyer` sia selezionato.  
  
2.  Se la **Legenda data mining** blocca la visualizzazione dei **Profili attributo**, spostarla all'esterno del percorso.  
  
3.  Nella casella barre **istogramma** selezionare **5**.  
  
     Nel modello utilizzato in questo esempio 5 è il numero massimo di stati per ogni singola variabile.  
  
     Gli attributi che influiscono sullo stato di questo attributo stimabile vengono elencati in combinazione con i valori di ogni stato degli attributi di input e la loro distribuzione in ogni stato dell'attributo stimabile.  
  
4.  Nella colonna **attributi** trovare il **numero di automobili possedute**.  Si notino le differenze negli istogrammi tra gli acquirenti di biciclette (la colonna con etichetta 1) e i non acquirenti (la colonna con etichetta 0). È molto più probabile che una bicicletta venga acquistata da una persona priva di automobili o che ne possiede una sola.  
  
5.  Fare doppio clic sulla cella **numero Cars di proprietà** nella colonna Bike Buyer (colonna con etichetta 1).  
  
     In **Legenda data mining** viene visualizzata una visualizzazione più dettagliata.  
  
  
##  <a name="attribute-characteristics"></a><a name="AttributeCharacteristics"></a>Caratteristiche degli attributi  
 Con la scheda **Caratteristiche attributo** è possibile selezionare un attributo e un valore per vedere la frequenza con cui vengono visualizzati i valori per gli altri attributi nei case del valore selezionato.  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>Per esplorare il modello nella scheda Caratteristiche attributo  
  
1.  Nell'elenco **attributo** verificare che `Bike Buyer` sia selezionato.  
  
2.  Impostare il **valore** su **1**.  
  
     Nel visualizzatore si osserverà che è più probabile che una bicicletta venga acquistata dai clienti senza figli, che abitano a breve distanza dal luogo di lavoro e che vivono nell'area dell'America del nord.  
  
  
##  <a name="attribute-discrimination"></a><a name="AttributeDiscrimination"></a>Discriminazione degli attributi  
 Con la scheda analisi **discriminante attributi** è possibile analizzare la relazione tra due valori discreti di acquisto di biciclette e altri valori di attributo. Poiché il `TM_NaiveBayes` modello dispone solo di due Stati, 1 e 0, non è necessario apportare alcuna modifica al visualizzatore.  
  
 Nel visualizzatore è possibile osservare che le persone che non possiedono un'automobile tendenzialmente acquistano biciclette, mentre le persone che possiedono due automobili in genere non ne acquistano.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per esplorare gli altri modelli di data mining, vedere gli argomenti seguenti.  
  
-   [Esplorazione del modello Decision Trees &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Esplorazione del modello di clustering &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 5: Testing models &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Esplorazione del modello di clustering &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Visualizzare un modello utilizzando il Visualizzatore Microsoft Naive Bayes](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [Scheda Analisi discriminante attributi &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [Scheda Profili attributo &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [Scheda Caratteristiche attributo &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [Scheda rete di dipendenze &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  
