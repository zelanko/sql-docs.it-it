---
title: Esplorazione dei modelli Market Basket (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: da1c9cb7-6c32-4b9b-96ec-ecea772aeb77
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8a7b2f97cbda0594698c6cbaa68019a6493f1e74
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63224604"
---
# <a name="exploring-the-market-basket-models-intermediate-data-mining-tutorial"></a>Esplorazione dei modelli Market Basket (Esercitazione intermedia sul data mining)
  Ora che è stato compilato il `Association` modello, è possibile esplorarlo utilizzando il [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizzatore associazione nella scheda **Visualizzatore modello** di data mining di progettazione modelli di data mining. In questa esercitazione viene descritto l'utilizzo del visualizzatore per esplorare le relazioni tra elementi. Il visualizzatore consente di visualizzare immediatamente i prodotti che tendono a comparire insieme e di ottenere un'idea generale degli schemi risultanti.  
  
 Il [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizzatore associazione contiene tre schede: **regole**, **set**di elementi e **rete di dipendenze**. Poiché ogni scheda rivela una vista leggermente diversa dei dati, quando si esplora un modello, in genere si passa diverse volte da un riquadro all'altro man mano che si ottengono le informazioni.  
  
-   [Scheda rete di dipendenze](#bkmk_DepNet)  
  
-   [Scheda set di elementi](#bkmk_Itemsets)  
  
-   [Scheda regole](#bkmk_Rules)  
  
-   [Generic Content Tree Viewer](#bkmk_ContentViewer)  
  
 Per questa esercitazione, si inizierà dalla scheda **rete di dipendenze** , quindi si utilizzeranno la scheda **regole** e la scheda **set** di elementi per approfondire la comprensione delle relazioni rivelate nel visualizzatore. Si utilizzerà inoltre **Microsoft Generic Content Tree Viewer** per recuperare statistiche dettagliate per singole regole o set di elementi.  
  
##  <a name="dependency-network-tab"></a><a name="bkmk_DepNet"></a>Scheda rete di dipendenze  
 Con la scheda **rete di dipendenze** è possibile esaminare l'interazione dei diversi elementi nel modello. Ogni nodo nel visualizzatore rappresenta un elemento, mentre le linee tra i nodi rappresentano regole. Selezionando un nodo, è possibile visualizzare gli altri nodi che stimano l'elemento selezionato oppure gli elementi stimati dall'elemento corrente. In alcuni casi, è presente un'associazione bidirezionale tra gli elementi, ovvero che compaiono spesso nella stessa transazione. È possibile fare riferimento alla legenda dei colori nella parte inferiore della scheda per determinare la direzione dell'associazione.  
  
 Una linea che collega due elementi indica che è probabile che questi elementi compaiano insieme in una transazione. In altre parole, è probabile che i clienti acquistino insieme questi elementi. Il dispositivo di scorrimento è associato alla probabilità della regola. Spostare il dispositivo di scorrimento verso l'alto o verso il basso per escludere le associazioni deboli, ovvero le regole con una bassa probabilità.  
  
 Il grafico della rete di dipendenze Mostra le regole pairwise, che possono essere rappresentate logicamente come A->B, ovvero se viene acquistato il prodotto A, il prodotto B è probabilmente. Il grafico non può visualizzare le regole del tipo AB->C. Se si sposta il dispositivo di scorrimento per mostrare tutte le regole ma non è comunque visibile alcuna linea nel grafico, ciò significa che non vi sono coppie di regole che soddisfano i criteri dei parametri dell'algoritmo.  
  
 È anche possibile trovare i nodi in base al nome, digitando le prime lettere del nome di attributo. Per altre informazioni, vedere [Finestra di dialogo Trova nodo &#40;Visualizzatore modello di data mining&#41;](../../2014/analysis-services/find-node-dialog-box-mining-model-viewer.md).  
  
#### <a name="to-open-the-association-mode-in-the-microsoft-assocaition-rules-viewer"></a>Per aprire il modello Association nel Visualizzatore Microsoft Association Rules  
  
1.  In **Esplora soluzioni**fare doppio clic sulla struttura di associazione.  
  
2.  In Progettazione modelli di data mining fare clic sulla scheda **Visualizzatore modello di data mining** .  
  
3.  Selezionare associazione nell'elenco dei modelli di data mining nell'elenco a discesa **modello di data mining** .  
  
#### <a name="to-navigate-the-dependency-graph-and-locate-specific-nodes"></a>Per navigare nel grafico delle dipendenze e individuare nodi specifici  
  
1.  Nella scheda **Visualizzatore modello di data mining** fare clic sulla scheda **rete di dipendenze** .  
  
2.  Fare clic su **Zoom** più volte, fino a quando non è possibile visualizzare facilmente le etichette per ogni nodo.  
  
     Per impostazione predefinita, il grafico viene visualizzato con tutti i nodi visibili. In un modello complesso possono esservi molti nodi, ognuno dei quali risulta piuttosto piccolo.  
  
3.  Fare clic **+** sul segno nell'angolo in basso a destra del visualizzatore e tenendo premuto il pulsante del mouse per eseguire il panning intorno al grafico.  
  
4.  Sul lato sinistro del visualizzatore trascinare il dispositivo di scorrimento verso il basso, spostandolo da **tutti i collegamenti** (impostazione predefinita) nella parte inferiore del controllo dispositivo di scorrimento.  
  
5.  Il visualizzatore aggiornerà il grafico in modo da mostrare solo l'associazione più forte, tra gli elementi Touring Tire e Touring Tire Tube.  
  
6.  Fare clic sul nodo con etichetta **Touring Tire Tube = existing**.  
  
     Il grafico viene aggiornato in modo da evidenziare solo gli elementi che sono fortemente correlati a questo elemento. Si noti la direzione della freccia tra i due elementi.  
  
7.  Sul lato sinistro del visualizzatore trascinare nuovamente il dispositivo di scorrimento verso l'alto, spostandolo dalla parte inferiore fino alla parte centrale.  
  
     Si notino le modifiche nella freccia che connette i due elementi.  
  
8.  Selezionare **Mostra solo nome attributo** dall'elenco a discesa nella parte superiore del riquadro rete di dipendenze.  
  
     Le etichette di testo nel grafico verranno aggiornate per mostrare solo il nome del modello.  
  
 [Torna all'inizio](#bkmk_DepNet)  
  
##  <a name="itemsets-tab"></a><a name="bkmk_Itemsets"></a>Scheda set di elementi  
 Il passaggio successivo consiste nell'ottenere maggiori informazioni sulle regole e sui set di elementi generati dal modello per i prodotti Touring Tire e Touring Tire Tube. Nella scheda **set** di elementi vengono visualizzate tre importanti informazioni correlate ai set di elementi individuati dall' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo di associazione:  
  
-   **Supporto:** Numero di transazioni in cui si verifica il set di elementi.  
  
-   **Dimensioni:** Numero di elementi nel set di elementi.  
  
-   **Elementi:** Elenco degli elementi inclusi in ogni set di elementi.  
  
 L'algoritmo consente di generare molti set di elementi a seconda della modalità di impostazione dei parametri. Ciascun set di elementi visualizzato rappresenta transazioni relative alla vendita dell'elemento. Utilizzando i controlli nella parte superiore della scheda **set** di elementi, è possibile filtrare il visualizzatore in modo da visualizzare solo i set di elementi che contengono un supporto minimo specificato e le dimensioni del set di elementi.  
  
 Se si utilizza un diverso modello di data mining e non vengono elencati set di elementi, questo avviene perché nessun set di elementi soddisfa il criterio dei parametri dell'algoritmo. In tale scenario, è possibile modificare i parametri dell'algoritmo per consentire set di elementi che dispongono di un supporto inferiore.  
  
#### <a name="to-filter-the-itemsets-that-are-shown-in-the-viewer-by-name"></a>Per filtrare i set di elementi mostrati nel visualizzatore per nome  
  
1.  Fare clic sulla scheda **set** di elementi del visualizzatore.  
  
2.  Nella casella **Filtra set di elementi** Digitare `Touring Tire`, quindi fare clic all'esterno della casella.  
  
     Il filtro restituirà tutti gli elementi che contengono questa stringa.  
  
3.  Nell'elenco **Mostra** selezionare **Mostra solo il nome dell'attributo**.  
  
4.  Selezionare la casella di controllo **Mostra nomi lunghi** .  
  
     L'elenco dei set di elementi verrà aggiornato per mostrare solo i set di elementi che contengono la stringa Touring Tire. Il nome lungo del set di elementi include il nome della tabella che contiene l'attributo e il valore per ogni elemento.  
  
5.  Deselezionare la casella di controllo **Mostra nomi lunghi** .  
  
     L'elenco dei set di elementi verrà aggiornato per mostrare solo il nome breve.  
  
 I valori nella colonna **supporto** indicano il numero di transazioni per ogni set di elementi. Una transazione per un set di elementi indica un acquisto in cui erano inclusi tutti gli elementi nel set di elementi.  
  
 Per impostazione predefinita, il visualizzatore elenca i set di elementi per supporto in ordine decrescente. È possibile fare clic sulle intestazioni di colonna per eseguire l'ordinamento in base a una colonna diversa, ad esempio il nome o la dimensione del set di elementi. Se si è interessati a ottenere maggiori informazioni sulle singole transazioni incluse in un set di elementi, è possibile eseguire il drill-through dai set di elementi ai singoli case. Le colonne della struttura nei risultati del drill-through sono il livello di reddito del cliente e l'ID cliente, che non sono stati utilizzati nel modello.  
  
#### <a name="to-view-details-for-an-itemset"></a>Per visualizzare i dettagli per un set di elementi  
  
1.  Nell'elenco dei set di elementi fare clic sull'intestazione di colonna **set di elementi** per eseguire l'ordinamento in base al nome.  
  
2.  Individuare l'elemento, `Touring Tire` (senza un secondo elemento).  
  
3.  Fare clic con il pulsante destro `Touring Tire`del mouse sull'elemento, selezionare **drill-through**, quindi selezionare **colonne struttura e modello**.  
  
     Nella finestra di dialogo **drill-through** vengono visualizzate le singole transazioni utilizzate come supporto per il set di elementi.  
  
4.  Espandere la tabella nidificata vAssocSeqLineItems per visualizzare l'elenco effettivo di acquisti nella transazione.  
  
#### <a name="to-filter-itemsets-by-support-or-size"></a>Per filtrare i set di elementi per supporto o per dimensione  
  
1.  Cancellare il testo eventualmente presente nella casella **Filtra set di elementi** . Non è possibile utilizzare un filtro basato su testo insieme con un filtro numerico.  
  
2.  Nella casella **supporto minimo** Digitare 100, quindi fare clic sullo sfondo del visualizzatore.  
  
     L'elenco dei set di elementi verrà aggiornato in modo da mostrare solo i set di elementi con supporto di almeno 100.  
  
 [Torna all'inizio](#bkmk_DepNet)  
  
##  <a name="rules-tab"></a><a name="bkmk_Rules"></a>Scheda regole  
 Nella scheda **regole** vengono visualizzate le informazioni seguenti relative alle regole individuate dall'algoritmo.  
  
-   **Probabilità:** *Probabilità* di una regola, definita come la probabilità dell'elemento a destra in base alla parte sinistra.  
  
-   **Importanza:** Misura dell'utilità di una regola. Un valore superiore indica una regola migliore.  
  
     L'importanza viene fornita per aiutare a misurare l'utilità di una regola, perché la probabilità da sola può essere fuorviante. Ad esempio, se ogni transazione contenesse una bottiglia d'acqua (si supponga che la bottiglia d'acqua venga aggiunta automaticamente agli acquisti di ogni cliente nell'ambito di una promozione), il modello creerebbe una regola che stima che la bottiglia di acqua dispone di una probabilità pari a 1. Sulla base della sola probabilità, questa regola è molto accurata, ma non fornisce informazioni utili.  
  
-   **Regola:** Definizione della regola. Per un modello Market Basket, una regola descrive una specifica combinazione di elementi.  
  
 Ogni regola può essere utilizzata per fare previsioni sulla presenza di un elemento in una transazione in base alla presenza di altri elementi. Analogamente alla scheda **set** di elementi, è possibile filtrare le regole in modo da visualizzare solo le regole più interessanti. Se si utilizza un modello di data mining che non dispone di regole, potrebbe essere necessario modificare i parametri dell'algoritmo per abbassare la soglia di probabilità per le regole.  
  
#### <a name="to-see-only-rules-that-include-the-mountain-200-bicycle"></a>Per visualizzare solo le regole che includono la bicicletta Mountain-200  
  
1.  Nella scheda **Visualizzatore modello di data mining** fare clic sulla scheda **regole** .  
  
2.  Nella casella **Filter Rule (regola filtro** ) immettere `Mountain-200`.  
  
     Deselezionare la casella di controllo **Mostra nomi lunghi** .  
  
3.  Nell'elenco **Mostra** selezionare **Mostra solo il nome dell'attributo**.  
  
     Il Visualizzatore visualizzerà quindi solo le regole che contengono le parole "`Mountain-200`". La probabilità della regola indica con quale probabilità è possibile che un utente acquisti una `Mountain-200` bicicletta, che acquista anche l'altro prodotto elencato.  
  
 Le regole vengono ordinate per probabilità in ordine decrescente, ma è possibile fare clic sulle intestazioni di colonna per modificare l'ordinamento. Se si è interessati a ottenere maggiori dettagli su una particolare regola, è possibile utilizzare il drill-through per visualizzare i case di supporto.  
  
#### <a name="to-view-cases-that-support-a-particular-rule"></a>Per visualizzare i case che supportano una particolare regola  
  
1.  Nella scheda **regole** fare clic con il pulsante destro del mouse sulla regola che si desidera visualizzare.  
  
2.  Selezionare **drill-through**, quindi selezionare **solo colonne modello**o **colonne struttura e modello**.  
  
     La finestra di dialogo **drill-through** fornisce un riepilogo della regola nella parte superiore del riquadro e un elenco di tutti i case utilizzati come dati di supporto per la regola.  
  
 [Torna all'inizio](#bkmk_DepNet)  
  
##  <a name="generic-content-tree-viewer"></a><a name="bkmk_ContentViewer"></a>Generic Content Tree Viewer  
 Questo visualizzatore può essere utilizzato per tutti i modelli, indipendentemente dall'algoritmo o dal tipo di modello. **Microsoft Generic Content Tree Viewer** è disponibile nell'elenco a discesa **Visualizzatore** .  
  
 Un albero del contenuto è una rappresentazione di un modello di data mining sotto forma di una serie di nodi, dove ogni nodo rappresenta le informazioni relative a un subset di dati. Il nodo può contenere un modello, un set di regole, un cluster o la definizione di un intervallo di date che condividono le stesse caratteristiche. Il contenuto esatto del nodo differisce a seconda dell'algoritmo e del tipo di attributo stimabile, ma la rappresentazione generale del contenuto è la stessa. È possibile espandere ogni nodo per aumentare il livello di dettaglio e copiare il contenuto di qualsiasi nodo negli Appunti.  
  
#### <a name="to-view-details-about-the-rule-by-using-the-content-viewer"></a>Per visualizzare i dettagli sulla regola tramite Generic Content Tree Viewer  
  
1.  Nella scheda **Visualizzatore modello di data mining** selezionare **Microsoft Generic Content Tree Viewer** dall'elenco **Visualizzatore** .  
  
2.  Nel riquadro Didascalia nodo scorrere fino alla fine dell'elenco, quindi fare clic sull'ultimo nodo.  
  
     Il visualizzatore mostra prima i set di elementi e quindi le regole, ma non li raggruppa. Il modo più semplice per individuare un nodo specifico è creare una query contenuto. Per altre informazioni, vedere [Esempi di query sul modello di associazione](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
3.  Nel riquadro Dettagli nodo esaminare il valore di NODE_TYPE e NODE_DESCRIPTION.  
  
     Un tipo di nodo 8 è una regola e un tipo di nodo 7 è un set di elementi. Per una regola, il valore di NODE_DESCRIPTION indica le condizioni che costituiscono la regola. Per un set di elementi, il valore di NODE_DESCRIPTION indica gli elementi inclusi nel set di elementi.  
  
 È anche possibile creare una query contenuto per ottenere statistiche dettagliate sulle regole. Per ulteriori informazioni sul contenuto dei modelli di data mining e su come interpretarlo, vedere contenuto dei modelli [di data mining per i modelli di associazione &#40;Analysis Services-&#41;di data mining ](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
 [Torna all'inizio](#bkmk_DepNet)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Applicazione di filtri a una tabella nidificata in un modello di data mining &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Lezione 3: creazione di uno scenario Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)   
 [Lezione 4: compilazione di uno scenario di clustering delle sequenze &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)   
 [Algoritmo Microsoft Association](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Association Rules](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)  
  
  
