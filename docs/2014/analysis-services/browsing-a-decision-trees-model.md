---
title: Esplorazione di un modello Decision Trees | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- tree viewer
- mining model, decision tree
- decision tree [data mining]
- dependency network
ms.assetid: 6b3dd1ae-caff-41c3-817b-802dc020ff88
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4a4f41e548746d443ff9cbed5eca17e557127240
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527747"
---
# <a name="browsing-a-decision-trees-model"></a>Esplorazione di un modello Decision Trees
  Quando si apre un modello di classificazione utilizzando **Sfoglia**, il modello viene visualizzato in un visualizzatore albero delle decisioni interattivo, simile al [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizzatore Decision Trees in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Nell visualizzatore vengono visualizzati i risultati di classificazione come grafico progettato per evidenziare i criteri che differenziano un gruppo di dati da un altro. È inoltre possibile eseguire il drill-down in singoli subset dell'albero e recuperare i dati sottostanti.  
  
##  <a name="explore-the-model"></a><a name="bkmk_Top"></a>Esplorare il modello  
 I modelli basati sull'algoritmo Decision Trees contengono molte informazioni interessanti da esplorare. La finestra **Esplora** include le schede e i riquadri seguenti che consentono di acquisire familiarità con i modelli e prevedere i risultati mediante il grafo:  
  
-   [Albero delle decisioni](#BKMK_DecisionTree)  
  
-   [Rete di dipendenze](#BKMK_DNetwork)  
  
 Per provare un modello di albero delle decisioni, è possibile utilizzare i dati di esempio nella scheda Dati di training (o Origine dati) della cartella di lavoro dei dati di esempio e compilare un modello di albero delle decisioni utilizzando Bike Buyer come attributo stimabile.  
  
###  <a name="decision-tree"></a><a name="BKMK_DecisionTree"></a>Albero delle decisioni  
 Questa vista è stata progettata per comprendere ed esplorare i fattori che portano un risultato.  
  
 Il grafico dell'albero delle decisioni può essere letto da sinistra a destra nel modo seguente:  
  
-   I rettangoli, denominati *nodi*, contengono subset dei dati. L'etichetta del nodo indica le caratteristiche di definizione di tale subset.  
  
-   Il nodo più a sinistra, denominato **All**, rappresenta il set di dati completo. Tutti i nodi successivi rappresentano i subset di dati.  
  
-   Un albero delle decisioni contiene molte *divisioni*o posizioni in cui i dati dipendono da più set in base agli attributi.  
  
     Ad esempio, nella prima divisione nel modello di esempio il set di dati viene suddiviso in tre gruppi per età.  
  
-   La divisione subito dopo il nodo **tutti** è la più importante perché mostra la condizione primaria che divide il set di dati.  
  
     Le altre divisioni si trovano a destra. Pertanto, analizzando differenti segmenti dell'albero, è possibile sapere quali attributi hanno influito maggiormente sul comportamento di acquisto.  
  
 ![Grafico della rete di dipendenze per un modello di associazione](media/dm13-dec-tree-split-definition.gif "Grafico della rete di dipendenze per un modello di associazione")  
  
 Utilizzando queste informazioni, è possibile concentrare una campagna di marketing sui clienti che potrebbero semplicemente aver bisogno di incoraggiamento per eseguire un acquisto.  
  
##### <a name="explore-the-decision-tree"></a>Esplorazione dell'albero delle decisioni  
  
1.  Fare clic sul nodo **tutti** ed esaminare **Legenda data mining**.  
  
     Viene visualizzato il conteggio esatto di case nel training set e una descrizione dettagliata dei risultati.  
  
     È possibile visualizzare le stesse informazioni in una descrizione comando se si posiziona il mouse su un nodo.  
  
2.  Fare clic sui segni più e meno accanto a ogni nodo per espandere o comprimere l'albero.  
  
     È anche possibile usare il dispositivo di scorrimento **Mostra livello** per espandere o ridurre l'albero.  
  
3.  Si noti che alcuni nodi sono più scuri di altri.  
  
     Per impostazione predefinita, la **popolazione** viene utilizzata come variabile ombreggiatura, il che significa che l'intensità del colore mostra quali nodi hanno il maggior supporto.  
  
     Pertanto il nodo più a sinistra è il più scuro perché contiene l'intero set di dati.  
  
4.  Modificare il valore di **background** da **tutti i case** in **Sì**.  
  
     ![modifica del grafico dell'albero delle decisioni per evidenziare gli acquirenti](media/dm13-dectreeshadedbuyer.gif "modifica del grafico dell'albero delle decisioni per evidenziare gli acquirenti")  
  
5.  Ora l'intensità del colore indica quanti clienti in ogni nodo hanno acquistato una bicicletta, che rappresenta il comportamento di interesse.  
  
     Si notino le barre colorate all'interno di ogni nodo. Si tratta di un istogramma in cui è illustrata la distribuzione dei risultati all'interno di questo subset di dati. Nell'albero delle decisioni di Sample Bike Buyer, ad esempio, la barra colorata Mostra la percentuale di clienti che hanno acquistato biciclette (sì valori) rispetto a quelli che non hanno (nessun valore). Per ottenere i valori esatti, è possibile fare clic sul nodo e visualizzare **Legenda data mining**.  
  
6.  Seguendo il grafico, è possibile vedere come ogni subset di dati è ulteriormente scomposto in gruppi più piccoli e quali attributi sono più utili per la stima di un risultato.  
  
     Esaminando solo l'intensità dell'ombreggiatura, è possibile concentrarsi su un paio di gruppi di interesse e ottenere dati più dettagliati su di essi per il confronto. Ad esempio, questi gruppi hanno una probabilità piuttosto elevata di acquistare biciclette:  
  
    -   Age >= 32 e \< 53 and Yearly Income > = 26000 e Children = 0  
  
         Case totali: 1150  
  
         Probabilità per gli acquirenti di biciclette: 18%  
  
    -   Age >= 32 e \< 53 and Yearly Income > = 26000 e Children not = 0 e coniuge status =' single '  
  
         Totale dei case: 402  
  
         Probabilità Bike Buyer: 16%  
  
7.  Modificare il valore di **background** da **Yes** a **No** e vedere come viene modificato il grafico.  
  
     ![Grafico della rete di dipendenze per un modello di associazione](media/dm13-dec-tree-background-no.gif "Grafico della rete di dipendenze per un modello di associazione")  
  
 **Suggerimenti**  
  
-   Se i dati possono essere suddivisi in più serie, viene compilato un modello diverso per ogni set di dati che si desidera modellare.  
  
-   Nel modello di dati di esempio, è presente un solo risultato stimabile-Bike Buyer, ma si supponga di avere informazioni sul fatto che il cliente abbia acquistato un piano di servizio e voglia prevedere anche questo. In questo caso si disporrebbe di tali dati in una colonna separata e si includerebbero due attributi stimabili nel modello.  
  
     Fare clic sull'opzione **istogramma** nell'angolo superiore sinistro del riquadro dell'albero delle decisioni per modificare il numero massimo di Stati che possono essere visualizzati negli istogrammi dell'albero. Tale opzione è utile se l'attributo stimabile include molti stati. Gli stati vengono visualizzati in un istogramma in ordine di diffusione da sinistra a destra.  
  
-   È inoltre possibile utilizzare le opzioni della scheda **albero delle decisioni** per influire sulla modalità di visualizzazione dell'albero, eseguendo lo zoom avanti o indietro o ridimensionando il grafico per adattarlo alla finestra.  
  
-   Per impostare il numero predefinito di livelli visualizzati per tutti gli alberi del modello, usare **Espansione predefinita** .  
  
-   Selezionare **Mostra nome lungo** per visualizzare il nome completo dell'attributo, inclusa l'origine dati. Il nome breve e il nome lungo coincidono a meno che i case non vengano recuperati da un'origine dati diversa da quella degli attributi per ogni case.  
  
 [Torna all'inizio](#bkmk_Top)  
  
###  <a name="dependency-network"></a><a name="BKMK_DNetwork"></a>Rete di dipendenze  
 Nella visualizzazione **rete di dipendenze** vengono visualizzate le connessioni tra gli attributi di input e gli attributi stimabili nel modello.  
  
1.  Fare clic e trascinare il dispositivo di scorrimento a sinistra del visualizzatore.  
  
     Nella posizione in alto vengono visualizzate tutte le connessioni. Quando si trascina il dispositivo di scorrimento verso il basso, nel visualizzatore vengono visualizzati solo i collegamenti più attendibili.  
  
2.  Fare quindi clic sul nodo Bike Buyer.  
  
     ![Vista della rete di dipendenze per gli alberi delle decisioni](media/dm13-dectree-depnet.gif "Vista della rete di dipendenze per gli alberi delle decisioni")  
  
     Quando si seleziona un nodo, nel visualizzatore vengono evidenziate le dipendenze specifiche del nodo. In questo caso, nel visualizzatore viene evidenziato ogni nodo che consente di stimare il risultato.  
  
3.  Se il visualizzatore contiene molti nodi, è possibile cercare nodi specifici tramite il pulsante **Trova nodo** . Se si fa clic sul pulsante **Trova nodo** , verrà visualizzata la finestra di dialogo **Trova nodo** , che consente di cercare e selezionare nodi specifici mediante un filtro.  
  
4.  La legenda nella parte inferiore del visualizzatore consente di individuare le corrispondenze tra i colori e i tipi di dipendenza rappresentati nel grafico. Ad esempio, quando si seleziona un nodo stimabile, a quest'ultimo viene applicata un'ombreggiatura turchese mentre ai nodi utilizzati per la stima del nodo selezionato viene applicata un'ombreggiatura arancione.  
  
 [Torna all'inizio](#bkmk_Top)  
  
### <a name="drill-through-to-underlying-data"></a>Drill-through sui dati sottostanti  
 Diversi tipi di modelli supportano la possibilità di *eseguire il drill-through* dal modello ai dati del case sottostanti. Ciò può risultare molto utile se si desidera contattare i clienti in un segmento specifico o estrarre i dati per eseguire un'ulteriore analisi.  
  
##### <a name="get-case-data"></a>Recupero di dati dei case  
  
1.  Fare clic con il pulsante destro del mouse sul nodo dell'albero contenente i dati desiderati e selezionare una di queste opzioni:  
  
    -   **Modello drill-through**. Questa opzione consente di ottenere i case che appartengono al nodo selezionato e di salvarli in una tabella in Excel. È possibile tornare solo alle colonne dei dati utilizzati effettivamente nella compilazione del modello.  
  
    -   **Colonne della struttura drill-through**. Questa opzione consente di ottenere i case che appartengono al nodo selezionato e di salvarli in una tabella in Excel. È possibile ottenere tutte le informazioni disponibili nei dati sottostanti al momento della compilazione, anche se nel modello non è stata usata una colonna. Ad esempio, si potrebbe aver escluso l'indirizzo e il CAP del cliente in quanto tali campi non sono utili con l'analisi, ma sono stati lasciati nella struttura.  
  
     Tornare a Excel per visualizzare i dati. Nel visualizzatore Sfoglia viene eseguita una query, vengono salvati i dati in una tabella in un nuovo foglio di lavoro e vengono etichettati i risultati.  
  
     ![risultati di drill-through salvati in Excel](media/dm13-dectree-drillthroughresults.gif "risultati di drill-through salvati in Excel")  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
