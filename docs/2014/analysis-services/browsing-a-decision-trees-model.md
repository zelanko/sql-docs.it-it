---
title: Esplorazione di una decisione di modello di albero delle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
manager: craigg
ms.openlocfilehash: 257d193c84420a0c70ea99ef2a8cadfa9e11eec5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468760"
---
# <a name="browsing-a-decision-trees-model"></a>Esplorazione di un modello Decision Trees
  Quando si apre un modello di classificazione utilizzando **esplorare**, il modello viene visualizzato in un visualizzatore di struttura ad albero delle decisioni interattivo, simile al [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizzatore alberi delle decisioni in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Nell visualizzatore vengono visualizzati i risultati di classificazione come grafico progettato per evidenziare i criteri che differenziano un gruppo di dati da un altro. È inoltre possibile eseguire il drill-down in singoli subset dell'albero e recuperare i dati sottostanti.  
  
##  <a name="bkmk_Top"></a> Esplorare il modello  
 I modelli basati sull'algoritmo Decision Trees contengono molte informazioni interessanti da esplorare. Il **esplorare** finestra include le schede e riquadri che consentono di apprendere gli schemi e stimare i risultati utilizzando il grafico seguenti:  
  
-   [Albero delle decisioni](#BKMK_DecisionTree)  
  
-   [Rete di dipendenze](#BKMK_DNetwork)  
  
 Per provare un modello di albero delle decisioni, è possibile utilizzare i dati di esempio nella scheda Dati di training (o Origine dati) della cartella di lavoro dei dati di esempio e compilare un modello di albero delle decisioni utilizzando Bike Buyer come attributo stimabile.  
  
###  <a name="BKMK_DecisionTree"></a> Albero delle decisioni  
 Questa vista è stata progettata per comprendere ed esplorare i fattori che portano un risultato.  
  
 Il grafico dell'albero delle decisioni può essere letto da sinistra a destra nel modo seguente:  
  
-   I rettangoli, che sono detti *nodi*, contengono subset di dati. L'etichetta del nodo indica le caratteristiche di definizione di tale subset.  
  
-   Il nodo più a sinistra, con l'etichetta **tutti**, rappresenta il set di dati completo. Tutti i nodi successivi rappresentano i subset di dati.  
  
-   Un albero delle decisioni contiene molte *suddivide*, o posizioni in cui i dati divergono in più set basati sugli attributi.  
  
     Ad esempio, nella prima divisione nel modello di esempio il set di dati viene suddiviso in tre gruppi per età.  
  
-   La divisione subito dopo il **tutti** nodo è la più importante perché Mostra la condizione primaria che divide il set di dati.  
  
     Le altre divisioni si trovano a destra. Pertanto, analizzando differenti segmenti dell'albero, è possibile sapere quali attributi hanno influito maggiormente sul comportamento di acquisto.  
  
 ![Grafico della rete di dipendenze per un modello di associazione](media/dm13-dec-tree-split-definition.gif "grafico della rete di dipendenze per un modello di associazione")  
  
 Utilizzando queste informazioni, è possibile concentrare una campagna di marketing sui clienti che potrebbero semplicemente aver bisogno di incoraggiamento per eseguire un acquisto.  
  
##### <a name="explore-the-decision-tree"></a>Esplorazione dell'albero delle decisioni  
  
1.  Fare clic sui **tutte** nodo ed esaminare le **legenda Data Mining**.  
  
     Viene visualizzato il conteggio esatto di case nel training set e una descrizione dettagliata dei risultati.  
  
     È possibile visualizzare le stesse informazioni in una descrizione comando se si posiziona il mouse su un nodo.  
  
2.  Fare clic sui segni più e meno accanto a ogni nodo per espandere o comprimere l'albero.  
  
     È anche possibile usare la **Mostra il livello** dispositivo di scorrimento per espandere o comprimere l'albero.  
  
3.  Si noti che alcuni nodi sono più scuri di altri.  
  
     Per impostazione predefinita **popolamento** viene usato come variabile ombreggiatura, il che significa che l'intensità del colore Mostra quali nodi dispongono di maggiore supporto.  
  
     Pertanto il nodo più a sinistra è il più scuro perché contiene l'intero set di dati.  
  
4.  Modificare il valore per **sfondo** dalla **tutti i casi** al **Sì**.  
  
     ![Modifica grafico dell'albero delle decisioni per evidenziare gli acquirenti](media/dm13-dectreeshadedbuyer.gif "Modifica grafico dell'albero delle decisioni per evidenziare gli acquirenti")  
  
5.  Ora l'intensità del colore indica quanti clienti in ogni nodo hanno acquistato una bicicletta, che rappresenta il comportamento di interesse.  
  
     Si notino le barre colorate all'interno di ogni nodo. Si tratta di un istogramma in cui è illustrata la distribuzione dei risultati all'interno di questo subset di dati. Ad esempio, nell'albero delle decisioni Bike Buyer di esempio, la barra colorata indica la proporzione di clienti che hanno acquistato biciclette (valori Sì) e gli utenti che non è stato eseguito (nessun valore). Per ottenere i valori esatti, è possibile fare clic sul nodo e visualizzare il **legenda Data Mining**.  
  
6.  Seguendo il grafico, è possibile vedere come ogni subset di dati è ulteriormente scomposto in gruppi più piccoli e quali attributi sono più utili per la stima di un risultato.  
  
     Esaminando solo l'intensità dell'ombreggiatura, è possibile concentrarsi su un paio di gruppi di interesse e ottenere dati più dettagliati su di essi per il confronto. Ad esempio, questi gruppi hanno una probabilità piuttosto elevata di acquistare biciclette:  
  
    -   Età > = 32 e \< 53 e Yearly Income > = 26000 e gli elementi figlio = 0  
  
         Case totali: 1150  
  
         Probabilità acquirente di biciclette: 18%  
  
    -   Età > = 32 e \< 53 e Yearly Income > = 26000 e gli elementi figlio non = stato civile e 0 = 'Single'  
  
         Case totali: 402  
  
         Probabilità acquirente di biciclette: 16%  
  
7.  Modificare il valore per **sfondo** da **Yes** a **No** e vedere come cambia il grafico.  
  
     ![Grafico della rete di dipendenze per un modello di associazione](media/dm13-dec-tree-background-no.gif "grafico della rete di dipendenze per un modello di associazione")  
  
 **Suggerimenti**  
  
-   Se i dati possono essere suddivisi in più serie, viene compilato un modello diverso per ogni set di dati che si desidera modellare.  
  
-   Nel modello di dati di esempio, è presente un solo risultato stimabile, Bike Buyer, ma si supponga di informazioni sul fatto che il cliente acquista un piano di servizio e voleva stimare anche. In questo caso si disporrebbe di tali dati in una colonna separata e si includerebbero due attributi stimabili nel modello.  
  
     Scegliere il **istogramma** opzione, nell'angolo superiore sinistro del riquadro dell'albero delle decisioni per modificare il numero massimo di stati che possono essere visualizzati negli istogrammi dell'albero. Tale opzione è utile se l'attributo stimabile include molti stati. Gli stati vengono visualizzati in un istogramma in ordine di diffusione da sinistra a destra.  
  
-   È anche possibile usare le opzioni sul **albero delle decisioni** pressione di tab per influire sulla modalità di visualizzazione albero, lo zoom avanti o indietro o ridimensionando il grafico per adattarlo alla finestra.  
  
-   Per impostare il numero predefinito di livelli visualizzati per tutti gli alberi del modello, usare **Espansione predefinita** .  
  
-   Selezionare **Mostra nomi lunghi** per visualizzare il nome completo dell'attributo, inclusa l'origine dati. Il nome breve e il nome lungo coincidono a meno che i case non vengano recuperati da un'origine dati diversa da quella degli attributi per ogni case.  
  
 [Torna all'inizio](#bkmk_Top)  
  
###  <a name="BKMK_DNetwork"></a> Rete di dipendenze  
 Il **rete di dipendenze** Vista sono riportati i collegamenti tra gli attributi di input e gli attributi stimabili nel modello.  
  
1.  Fare clic e trascinare il dispositivo di scorrimento a sinistra del visualizzatore.  
  
     Nella posizione in alto vengono visualizzate tutte le connessioni. Quando si trascina il dispositivo di scorrimento verso il basso, nel visualizzatore vengono visualizzati solo i collegamenti più attendibili.  
  
2.  Fare quindi clic sul nodo Bike Buyer.  
  
     ![Vista della rete di dipendenze per gli alberi delle decisioni](media/dm13-dectree-depnet.gif "vista della rete di dipendenze per gli alberi delle decisioni")  
  
     Quando si seleziona un nodo, nel visualizzatore vengono evidenziate le dipendenze specifiche del nodo. In questo caso, nel visualizzatore viene evidenziato ogni nodo che consente di stimare il risultato.  
  
3.  Se il visualizzatore contiene numerosi nodi, è possibile cercare nodi specifici tramite il **Trova nodo** pulsante. Se si fa clic sul pulsante **Trova nodo** , verrà visualizzata la finestra di dialogo **Trova nodo** , che consente di cercare e selezionare nodi specifici mediante un filtro.  
  
4.  La legenda nella parte inferiore del visualizzatore consente di individuare le corrispondenze tra i colori e i tipi di dipendenza rappresentati nel grafico. Ad esempio, quando si seleziona un nodo stimabile, a quest'ultimo viene applicata un'ombreggiatura turchese mentre ai nodi utilizzati per la stima del nodo selezionato viene applicata un'ombreggiatura arancione.  
  
 [Torna all'inizio](#bkmk_Top)  
  
### <a name="drill-through-to-underlying-data"></a>Drill-through sui dati sottostanti  
 Diversi tipi di modelli supportano la possibilità *drill-through* dal modello ai dati del case sottostanti. Ciò può risultare molto utile se si desidera contattare i clienti in un segmento specifico o estrarre i dati per eseguire un'ulteriore analisi.  
  
##### <a name="get-case-data"></a>Recupero di dati dei case  
  
1.  Fare clic con il pulsante destro del mouse sul nodo dell'albero contenente i dati desiderati e selezionare una di queste opzioni:  
  
    -   **Drill-Through modello**. Questa opzione consente di ottenere i case che appartengono al nodo selezionato e di salvarli in una tabella in Excel. È possibile tornare solo alle colonne dei dati utilizzati effettivamente nella compilazione del modello.  
  
    -   **Drill-Through le colonne della struttura**. Questa opzione consente di ottenere i case che appartengono al nodo selezionato e di salvarli in una tabella in Excel. Si ottengono tutte le informazioni disponibili nell'oggetto sottostante dei dati durante la compilazione di esso, persino di una colonna non è stati utilizzati nel modello. Ad esempio, si potrebbe aver escluso l'indirizzo e il CAP del cliente in quanto tali campi non sono utili con l'analisi, ma sono stati lasciati nella struttura.  
  
     Tornare a Excel per visualizzare i dati. Nel visualizzatore Sfoglia viene eseguita una query, vengono salvati i dati in una tabella in un nuovo foglio di lavoro e vengono etichettati i risultati.  
  
     ![risultati del drill-through vengono salvati in Excel](media/dm13-dectree-drillthroughresults.gif "risultati del drill-through vengono salvati in Excel")  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione di modelli in Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
