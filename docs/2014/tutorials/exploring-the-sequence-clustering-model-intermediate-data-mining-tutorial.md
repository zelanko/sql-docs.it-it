---
title: Esplorare il modello Sequence Clustering (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f8a485d5-47ed-4dd5-bb66-ef4d6d463845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e0904239933361b80727700c94b03e379751251f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164051"
---
# <a name="exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Esplorazione del modello Sequence Clustering (Esercitazione intermedia sul data mining)
  Ora che è stata compilata la **Sequence Clustering with Region** modello, è possibile esaminarlo utilizzando il [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizzatore Sequence Clustering nel **visualizzatore modello di Data Mining** scheda della finestra di progettazione modelli di Data Mining. Il [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizzatore Sequence Clustering include cinque schede: **Diagramma dei cluster**, **profili Cluster**, **caratteristiche del Cluster**, **ClusterDiscrimination**, e **transizionidistato**. Per altre informazioni su come utilizzare questo visualizzatore, vedere [esplorare un modello usando il visualizzatore Microsoft Sequence Clustering](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
-   [Scheda diagramma dei cluster](#bkmk_CDiagram)  
  
-   [Scheda Profili cluster](#bkmk_CProfiles)  
  
-   [Scheda caratteristiche cluster](#bkmk_CChars)  
  
-   [Scheda Analisi discriminante tra cluster](#bkmk_CDiscrim2)  
  
-   [Scheda transizioni di stato](#bkmk_StateTran)  
  
-   [Generic Content Tree Viewer](#bkmk_Generic)  
  
##  <a name="bkmk_CDiagram"></a> Scheda diagramma dei cluster  
 Il **diagramma dei Cluster** scheda Visualizza graficamente i cluster individuati dall'algoritmo nel database. Il layout del diagramma rappresenta la relazione tra i cluster, con i cluster simili raggruppati. Per impostazione predefinita, l'ombreggiatura di ogni nodo rappresenta la densità di tutti i case nel cluster: quanto più scura appare l'ombreggiatura del nodo, maggiore sarà il numero di case contenuti. È possibile modificare il significato dell'ombreggiatura dei nodi in modo da rappresentare il supporto, all'interno di ogni cluster, di un attributo e uno stato.  
  
 È inoltre possibile rinominare i cluster per facilitare l'identificazione e l'utilizzo dei cluster di destinazione. In questa esercitazione verranno rinominati il cluster con la percentuale più elevata di clienti dell'area del Pacifico e il cluster che contiene il maggior numero di case.  
  
> [!NOTE]  
>  I case assegnati a cluster specifici potrebbero cambiare quando si rielabora il modello, a seconda dei dati e dei parametri del modello stesso. Inoltre, se i cluster vengono rinominati, i nomi andranno persi quando si rielabora il modello di data mining.  
  
#### <a name="to-change-the-attribute-used-for-highlighting-clusters"></a>Per cambiare l'attributo utilizzato per evidenziare i cluster  
  
1.  Nel **variabile ombreggiatura** elenco, selezionare **modello**.  
  
2.  Selezionare **Cycling Cap** nel **stato** elenco.  
  
     Il diagramma verrà aggiornato per visualizzare la concentrazione del prodotto selezionato in ognuno dei cluster. Il cluster caratterizzato dall'ombreggiatura più scura contiene la densità maggiore di berretti da ciclista (Cycling Cap). È possibile modificare la variabile ombreggiatura per utilizzare qualsiasi stato di qualsiasi colonna di input.  
  
3.  Nel **variabile ombreggiatura** elenco, selezionare **popolamento**.  
  
     Impostando la variabile ombreggiatura su Popolazione, il diagramma viene aggiornato per confrontare i cluster in base alla dimensione. Il cluster con l'ombreggiatura più scura contiene più case rispetto agli altri cluster.  
  
#### <a name="to-rename-nodes-in-the-model"></a>Per rinominare i nodi del modello  
  
1.  Change **variabile ombreggiatura** a `Region`e impostare **stato** alla **Pacifico**.  
  
2.  Evidenziare il nodo più scuro del grafico.  
  
3.  Fare doppio clic su questo cluster e selezionare **Rinomina Cluster.**  
  
4.  Digitare il nome**Cluster Pacifico.**  
  
5.  Modificare il valore della **variabile ombreggiatura** al **popolamento**.  
  
6.  Nel grafico aggiornato individuare il cluster più scuro, che dovrebbe corrispondere al cluster più grande. Se non si è in grado di individuare il cluster più grande in base all'ombreggiatura, posizionare il mouse su ogni cluster e visualizzare la descrizione comando, quindi scegliere il cluster che contiene il maggior numero di case.  
  
7.  Fare doppio clic su questo cluster e selezionare **Rinomina Cluster**. Digitare il nuovo nome, `Largest Cluster`.  
  
 È possibile eseguire il drill-through dal nodo che rappresenta il cluster per visualizzare i dettagli dei case contenuti in ogni cluster. Questa operazione può essere utile se si desidera intraprendere determinate azioni sulla base dei risultati dell'analisi, ad esempio inviare un messaggio di posta elettronica a un cliente. È inoltre possibile esplorare gli altri attributi dei case inclusi nella struttura ma non utilizzati nel modello, ad esempio Region e IncomeGroup. Per altre informazioni sul drill-through dai modelli di data mining ai case sottostanti, vedere [query drill-through &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-drill-through-to-details-from-the-cluster-diagram"></a>Per eseguire il drill-through nei dettagli dal diagramma dei cluster  
  
1.  Fare doppio clic su `Pacific Cluster`, selezionare **drill-Through**, quindi selezionare **colonne struttura e modello**.  
  
     Il **drill-Through** verrà visualizzata la finestra di dialogo. Le colonne che non vengono utilizzati nel modello, ma che sono disponibili per l'esecuzione di query sono precedute **struttura**.  
  
     È possibile notare che questo cluster contiene prevalentemente clienti dell'area del Pacifico e solo alcuni clienti residenti in altre aree geografiche.  
  
2.  Fare clic sul segno più nella colonna nidificata v Assoc Seq Line Items per visualizzare la sequenza di articoli in un determinato ordine cliente.  
  
3.  Chiudi il **drill-Through** nella finestra di dialogo.  
  
    > [!NOTE]  
    >  Il **riprodurre** pulsante consente di rieseguire una query dei dati; tuttavia, rieseguendo la query non vengono modificati i dati visualizzati, a meno che il modello è stato aggiornato dinamicamente in background da un altro processo.  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CProfiles"></a> Scheda Profili cluster  
 Il **profili Cluster** scheda vengono visualizzate le sequenze in ogni cluster. I cluster sono elencati in singole colonne a destra del **stati** colonna.  
  
 Nel visualizzatore, il **Model** riga descrive la distribuzione complessiva degli elementi in un cluster e il **Model. Samples** riga contiene le sequenze di elementi. Ogni riga delle sequenze di colore in ogni cella della **Model. Samples** riga rappresenta il comportamento di un utente selezionato in modo casuale nel cluster.  
  
 Ogni colore in ogni singolo istogramma di sequenza rappresenta un modello di prodotto. In Legenda data mining vengono indicate le sequenze di prodotti utilizzando la codifica con colori e i nomi dei modelli dei prodotti. Se sono state aggiunte altre colonne al modello per il clustering, ad esempio Region o IncomeGroup, il visualizzatore conterrà una riga aggiuntiva per ogni colonna, in cui viene visualizzata la distribuzione di questi valori all'interno di ogni cluster.  
  
#### <a name="to-view-the-sequences-that-are-most-common-in-a-cluster"></a>Per visualizzare le sequenze più comuni in un cluster  
  
1.  Fare doppio clic il **Model** riga della colonna per il cluster `Largest Cluster`e selezionare **Mostra legenda**.  
  
     Il **colore** colonna contiene una barra ombreggiata che indica la frequenza degli articoli individuati nelle sequenze. Ogni articolo è rappresentato da un colore diverso. Il **significato** colonna elenca i nomi dei modelli di prodotto per ogni colore. Il **distribuzione** colonna indica la percentuale di case che contengono questo elemento in una sequenza.  
  
2.  Chiudi il **legenda Data Mining**.  
  
3.  Fare doppio clic il **Model. Samples** riga della colonna con intestazione **popolamento, ovvero** e selezionare **Mostra legenda**.  
  
4.  Analizzare l'elenco delle sequenze nel modello generale`.`  
  
     In Legenda data mining sono elencate per prime le sequenze più comuni, pertanto è possibile notare che Mountain Tire Tube è il primo articolo in molte sequenze. Ciò indica che è molto probabile che un cliente includa per primo tra gli acquisti l'articolo Mountain Tire Tube.  
  
#### <a name="to-drill-through-to-cases-from-the-cluster-viewer"></a>Per eseguire il drill-through nei case dal visualizzatore cluster  
  
1.  Scorrere verso il basso il riquadro attributi fino a individuare la riga per il `Region` attributo.  
  
     La riga contiene un istogramma per ogni cluster nel modello, oltre a un istogramma aggiuntivo per **popolamento**, vale a dire l'intero set di case utilizzati nel modello. Un istogramma è una barra contenente diversi colori, ognuno dei quali rappresenta un attributo, mentre la dimensione della sezione colorata relativa all'attributo rappresenta la percentuale di case caratterizzati da tale attributo.  
  
2.  Confrontare gli istogrammi dei cluster rinominati `Pacific Cluster` e `Largest Cluster`. Ogni cluster viene visualizzato in una colonna diversa.  
  
     Entrambi sono identificati da un colore in tinta unita, ma i colori sono diversi.  
  
3.  Nel `Region` di righe, posizionare il mouse sull'istogramma colorato relativo `Largest Cluster`.  
  
     I valori visualizzati nella descrizione comando indicano le percentuali effettive dei case di ogni area.  
  
4.  Fare doppio clic su istogramma colorato nella `Region` riga per `Pacific Cluster`, selezionare **drill-Through**, quindi selezionare **solo colonne modello**.  
  
5.  Spostare la barra di scorrimento per rivedere tutti i clienti contenuti in questo cluster.  
  
     Eseguendo il drill-through nei dettagli è possibile notare anche questa volta che il cluster contiene prevalentemente ordini provenienti dall'area del Pacifico, oltre ad alcuni ordini provenienti dal Nord America e dall'Europa.  
  
6.  Chiudi il **drill-Through** nella finestra di dialogo.  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CChars"></a> Scheda caratteristiche cluster  
 Il **caratteristiche Cluster** scheda sono riepilogate le transizioni tra stati in un cluster mediante la visualizzazione di barre che rappresentano graficamente l'importanza del valore dell'attributo per il cluster selezionato. Il **variabili** colonna indica rilevata dal modello come elemento importante per il cluster selezionato o la popolazione: un determinato valore o la relazione tra valori, detti *transizione*. Il **i valori** colonna fornisce informazioni dettagliate sul valore o la transizione e il **probabilità** colonna rappresenta graficamente il peso dell'attributo o della transizione.  
  
#### <a name="to-view-the-important-attributes-for-a-cluster"></a>Per visualizzare gli attributi importanti per un cluster  
  
1.  Nel **Cluster** elenco a discesa, seleziona `Pacific Cluster`.  
  
     L'elenco verrà aggiornato per mostrare le caratteristiche del cluster in cui è stato rinominato `Pacific Cluster`. In questo cluster la caratteristica più importante è `Region`.  
  
2.  Posizionare il mouse sulla barra ombreggiata nella riga relativa `Region`.  
  
     La probabilità che il valore corrisponda a Pacific è molto elevata. Per altre informazioni su come interpretare questi valori, vedere [riferimento Microsoft Sequence Clustering algoritmo tecniche](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
3.  Esaminare l'elenco delle caratteristiche del cluster fino a individuare la prima riga di transizione.  
  
4.  Una riga di transizione contiene il testo transizione nella **variabili** colonna e una combinazione di valori degli attributi sequenziali nella **valore** colonna. La sequenza può inoltre contenere punti iniziali e valori mancanti.  
  
     Ad esempio, si supponga che la transizione includa il valore [avvio] -> Road Tire Tube. Ciò significa che i clienti contenuti in questo cluster includono frequentemente l'articolo Road Tire Tube per primo tra gli acquisti. Questo comportamento potrebbe indicare che il prodotto è un articolo popolare molto ricercato dai clienti oppure semplicemente che il prodotto è facile da reperire sul sito riservato agli acquisti.  
  
5.  Scorrere l'elenco fino a individuare la prima transizione che non dispone **[avvio]** oppure **mancante** in esso.  
  
     Ad esempio, si supponga che si trova la transizione **Touring Tire, Touring Tire Tube**. Ciò significa che i clienti inclusi in questo cluster hanno frequentemente acquistato questi articoli in combinazione, esattamente nell'ordine indicato.  
  
6.  Posizionare il mouse sulla barra ombreggiata relativa a questa transizione.  
  
     La probabilità della transizione verrà visualizzata come percentuale.  
  
7.  Nel **Cluster** elenco a discesa, seleziona **popolazione (tutto)**.  
  
     L'elenco degli attributi verrà aggiornato per visualizzare le caratteristiche di tutti gli ordini utilizzati per creare il modello. In questo modello di data mining, è la caratteristica più importante per distinguere tra cluster `Region`, con il valore **America del Nord**.  
  
 Dall'analisi di queste attività emergono due aspetti. In primo luogo, per ottenere un numero significativo di combinazioni è necessario disporre di una quantità elevata di dati. Ad esempio, le sequenze con la probabilità più potranno che includono un **[avvio]** oppure **Missing** dello stato.  
  
 Il secondo è che esiste una forte impatto del clustering sugli attributi di `Region`, che rende più difficile visualizzare i gruppi di sequenze. Si decide pertanto di creare un altro modello che utilizza solo le sequenze e non include le colonne relative a area o reddito.  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CDiscrim2"></a> Scheda Analisi discriminante tra cluster  
 Il **analisi discriminante tra Cluster** scheda consente di confrontare due cluster, per determinare gli attributi che distinguono un particolare cluster da un altro cluster. La scheda contiene quattro colonne: **Le variabili**, **valori**, **Cluster 1**, e **Cluster 2**.  È possibile scegliere qualsiasi cluster da utilizzare come **Cluster 1** e **Cluster 2**.  
  
 Il **variabili** colonna indica il nome dell'attributo, che può essere un nome di colonna o combinazione di nome di colonna e la parola **transizione**. Il **valori** colonna Mostra il valore esatto dell'attributo o della transizione. Le barre ombreggiate nelle colonne relative **Cluster 1** e **Cluster 2** indicano la forza dell'attributo nei cluster che si desidera confrontare. Più lunga è la barra, maggiore è la probabilità che il cluster includa case con tale attributo.  
  
#### <a name="to-compare-two-clusters-by-using-the-cluster-discrimination-tab"></a>Per confrontare due cluster tramite la scheda Analisi discriminante tra cluster  
  
1.  Nel **analisi discriminante tra Cluster** scheda, per **Cluster 1**, selezionare `Pacific Cluster`.  
  
     Per impostazione predefinita, la selezione per **Cluster 2** diventa **complemento del Cluster Pacifico**.  
  
     L'attributo principale che distingue `Pacific Cluster` da tutti gli altri casi è l'area. L'influenza dell'attributo Region sul clustering nasconde gli altri attributi. Per evitare questo effetto, provare a eseguire il confronto tra alcuni dei cluster più piccoli. Questa operazione modifica l'elenco degli attributi, che potrebbe ora includere più transizioni tra modelli.  
  
2.  Individuare una riga di transizione e posizionare il mouse sulla barra ombreggiata.  
  
     Gli elementi di **valori** colonna può includere stati e transizioni. L'ombreggiatura di ogni elemento indica il punteggio dell'analisi discriminante. Per altre informazioni sul significato dei diversi punteggi, vedere [modello di contenuto di Data Mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_StateTran"></a> Scheda transizioni di stato  
 Nel **transizioni di stato** scheda, è possibile selezionare un cluster e visualizzare le transizioni di stato. Se si seleziona **popolazione (tutto)** dall'elenco a discesa del cluster, il diagramma mostra la distribuzione degli stati per il modello di data mining intero.  
  
 Ogni nodo del grafico rappresenta uno stato o un possibile valore delle sequenze che si sta tentando di analizzare. Il colore di sfondo dei nodi rappresenta la frequenza di tale stato. Alcuni stati sono collegati da linee che indicano la presenza di una transizione tra tali stati. È possibile spostare il dispositivo di scorrimento verso l'alto o verso il basso per modificare la soglia di probabilità delle transizioni. Ad alcuni nodi sono associati numeri che indicano la probabilità dello stato.  
  
#### <a name="to-explore-the-relationships-in-the-state-transition-tab"></a>Per esplorare le relazioni nella scheda Transizioni di stato  
  
1.  Nel **transizioni di stato** scheda visualizzatore modello di Data Mining selezionare `Pacific Cluster` dall'elenco dei cluster. Verificare che il **Mostra etichette sui bordi** opzione è selezionata.  
  
     Il grafico verrà aggiornato per visualizzare le transizioni più comuni in questo cluster.  
  
2.  Fare clic su un nodo collegato da una linea a un altro nodo.  
  
     Il grafico verrà aggiornato per evidenziare i nodi correlati. Il valore numerico accanto alla linea indica la probabilità della transizione.  
  
3.  Generare il dispositivo di scorrimento fino a **tutti i collegamenti**, per aumentare il numero di transizioni incluse nel grafico.  
  
4.  Selezionare **popolazione (tutto)** dalla **Cluster**.  
  
     Si noti che quando si carica un cluster diverso, vengono ripristinate le impostazioni di visualizzazione predefinite del grafico, pertanto il dispositivo di scorrimento viene ricollocato in posizione centrale.  
  
5.  Fare clic sul nodo più scuro del grafico, che deve essere **Sport-100**.  
  
     Si noti che questo prodotto non è collegato da alcuna linea ad altri prodotti.  
  
6.  Spostare il dispositivo di scorrimento verso l'alto di uno spazio, per aumentare il numero di transizioni incluse nel grafico. Non passare completamente alla **tutti i collegamenti** ancora.  
  
     Il grafico verrà aggiornato con l'aggiunta di diverse transizioni, nessuna delle quali include tuttavia il modello Sport-100.  
  
7.  Spostare il dispositivo di scorrimento fino alla **tutti i collegamenti**. Fare clic sul nodo Sport-100, se non è già selezionato.  
  
     Il grafico verrà aggiornato con l'aggiunta di numerose transizioni che includono il prodotto Sport-100. La direzione della freccia della linea di connessione indica se l'articolo Sport-100 è stato selezionato come primo o secondo articolo nella coppia.  
  
8.  Fare clic sul nodo relativo a Touring Tire e riposizionare il dispositivo di scorrimento al centro.  
  
     Inizialmente, sono presenti numerose linee di transizione che collegano Touring Tire agli altri prodotti, ma quando si aumenta la soglia di probabilità, le transizioni meno probabili vengono eliminate dal grafico, lasciando solo la transizione Touring Tire > Touring Tire Tube. Questa transizione indica che se un cliente include un articolo Touring Tire tra gli acquisti, esiste una forte probabilità che il cliente inserisca successivamente un articolo Touring Tire Tube.  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_Generic"></a> Generic Content Tree Viewer  
 Questo visualizzatore può essere utilizzato per tutti i modelli, indipendentemente dall'algoritmo o dal tipo di modello. Il **MicrosoftGeneric Content Tree Viewer** è disponibile il **Visualizzatore** elenco a discesa.  
  
 Un albero dei contenuti è una rappresentazione di un modello di data mining sotto forma di una serie di nodi, in cui ogni nodo rappresenta le informazioni relative ai dati di training. Il nodo può contenere un modello, un set di regole, un cluster o la definizione di un intervallo di date che condividono alcuni attributi. Il contenuto esatto del nodo differisce a seconda dell'algoritmo e dell'attributo stimabile, ma la rappresentazione generale del contenuto è la stessa.  
  
 È possibile espandere ogni nodo per aumentare il livello di dettaglio e copiare il contenuto di qualsiasi nodo negli Appunti. Per altre informazioni, vedere [Visualizzare un modello utilizzando Microsoft Generic Content Tree Viewer](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
#### <a name="to-view-details-for-a-sequence-clustering-model-by-using-the-generic-content-tree-viewer"></a>Per visualizzare i dettagli di un modello Sequence Clustering tramite Generic Content Tree Viewer  
  
1.  Nel **visualizzatore modello di Data Mining** scheda, fare clic sui **Visualizzatore** elencare e selezionare **Microsoft Generic Content Tree viewer**.  
  
2.  Nel **didascalia del nodo** riquadro, fare clic su `Pacific Cluster (1)`.  
  
     Il nome di questo nodo è composto dal nome descrittivo assegnato al cluster e dall'ID nodo sottostante. È possibile utilizzare gli ID nodo per eseguire il drill-down in ulteriori dettagli relativi al modello.  
  
3.  Espandere il primo nodo figlio denominato **livello sequenza per cluster 1**.  
  
     Il nodo del livello di sequenza relativo a un cluster contiene dettagli sugli stati e le transizioni inclusi in tale cluster. È possibile utilizzare questi dettagli, disponibili nella colonna NODE_DISTRIBUTION, per esplorare le sequenze e gli stati di ogni cluster o dell'intero modello.  
  
4.  Continuare a espandere i nodi e a visualizzare i dettagli nel visualizzatore HTML.  
  
 Per altre informazioni sul contenuto del modello di data mining e su come usare i dettagli nel visualizzatore, vedere [contenuto del modello di Data Mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di un modello Sequence Clustering correlato &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Sequence Clustering Algorithm](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Esempi di query sul modello di cluster di sequenza](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)  
  
  
