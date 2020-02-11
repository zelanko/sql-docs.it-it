---
title: Esplorazione del modello Sequence Clustering (Esercitazione intermedia sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63164051"
---
# <a name="exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Esplorazione del modello Sequence Clustering (Esercitazione intermedia sul data mining)
  Ora che è stato compilato il modello **Sequence Clustering with Region** , è possibile esplorarlo utilizzando [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering Viewer nella scheda **Visualizzatore modello** di data mining di progettazione modelli di data mining. Il [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizzatore Sequence Clustering contiene cinque schede **: diagramma dei cluster**, **Profili cluster**, **caratteristiche del cluster**, **ClusterDiscrimination**e **transizioni di stato**. Per ulteriori informazioni sull'utilizzo di questo visualizzatore, vedere visualizzare [un modello utilizzando il Visualizzatore Microsoft Sequence Clustering](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
-   [Scheda Diagramma cluster](#bkmk_CDiagram)  
  
-   [Scheda Profili cluster](#bkmk_CProfiles)  
  
-   [Scheda Caratteristiche cluster](#bkmk_CChars)  
  
-   [Scheda Analisi discriminante tra cluster](#bkmk_CDiscrim2)  
  
-   [Scheda transizioni di stato](#bkmk_StateTran)  
  
-   [Generic Content Tree Viewer](#bkmk_Generic)  
  
##  <a name="bkmk_CDiagram"></a>Scheda Diagramma cluster  
 Nella scheda **diagramma dei cluster** vengono visualizzati graficamente i cluster individuati dall'algoritmo nel database. Il layout del diagramma rappresenta la relazione tra i cluster, con i cluster simili raggruppati. Per impostazione predefinita, l'ombreggiatura di ogni nodo rappresenta la densità di tutti i case nel cluster: quanto più scura appare l'ombreggiatura del nodo, maggiore sarà il numero di case contenuti. È possibile modificare il significato dell'ombreggiatura dei nodi in modo da rappresentare il supporto, all'interno di ogni cluster, di un attributo e uno stato.  
  
 È inoltre possibile rinominare i cluster per facilitare l'identificazione e l'utilizzo dei cluster di destinazione. In questa esercitazione verranno rinominati il cluster con la percentuale più elevata di clienti dell'area del Pacifico e il cluster che contiene il maggior numero di case.  
  
> [!NOTE]  
>  I case assegnati a cluster specifici potrebbero cambiare quando si rielabora il modello, a seconda dei dati e dei parametri del modello stesso. Inoltre, se i cluster vengono rinominati, i nomi andranno persi quando si rielabora il modello di data mining.  
  
#### <a name="to-change-the-attribute-used-for-highlighting-clusters"></a>Per cambiare l'attributo utilizzato per evidenziare i cluster  
  
1.  Nell'elenco **Variabile ombreggiatura** selezionare **modello**.  
  
2.  Selezionare **Cycling Cap** nell'elenco **stato** .  
  
     Il diagramma verrà aggiornato per visualizzare la concentrazione del prodotto selezionato in ognuno dei cluster. Il cluster caratterizzato dall'ombreggiatura più scura contiene la densità maggiore di berretti da ciclista (Cycling Cap). È possibile modificare la variabile ombreggiatura per utilizzare qualsiasi stato di qualsiasi colonna di input.  
  
3.  Nell'elenco **Variabile ombreggiatura** selezionare **popolazione**.  
  
     Impostando la variabile ombreggiatura su Popolazione, il diagramma viene aggiornato per confrontare i cluster in base alla dimensione. Il cluster con l'ombreggiatura più scura contiene più case rispetto agli altri cluster.  
  
#### <a name="to-rename-nodes-in-the-model"></a>Per rinominare i nodi del modello  
  
1.  Modificare la **Variabile ombreggiatura** in `Region`e impostare **lo stato** su **Pacific**.  
  
2.  Evidenziare il nodo più scuro del grafico.  
  
3.  Fare clic con il pulsante destro del mouse sul cluster e scegliere **Rinomina cluster.**  
  
4.  Digitare il nome**cluster Pacific.**  
  
5.  Modificare il valore della **Variabile ombreggiatura** in **popolamento**.  
  
6.  Nel grafico aggiornato individuare il cluster più scuro, che dovrebbe corrispondere al cluster più grande. Se non si è in grado di individuare il cluster più grande in base all'ombreggiatura, posizionare il mouse su ogni cluster e visualizzare la descrizione comando, quindi scegliere il cluster che contiene il maggior numero di case.  
  
7.  Fare clic con il pulsante destro del mouse sul cluster e scegliere **Rinomina cluster**. Digitare il nuovo nome `Largest Cluster`.  
  
 È possibile eseguire il drill-through dal nodo che rappresenta il cluster per visualizzare i dettagli dei case contenuti in ogni cluster. Questa operazione può essere utile se si desidera intraprendere determinate azioni sulla base dei risultati dell'analisi, ad esempio inviare un messaggio di posta elettronica a un cliente. È inoltre possibile esplorare gli altri attributi dei case inclusi nella struttura ma non utilizzati nel modello, ad esempio Region e IncomeGroup. Per ulteriori informazioni sul drill-through dai modelli di data mining ai casi sottostanti, vedere [query drill-through &#40;&#41;di data mining ](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-drill-through-to-details-from-the-cluster-diagram"></a>Per eseguire il drill-through nei dettagli dal diagramma dei cluster  
  
1.  Fare clic con `Pacific Cluster`il pulsante destro del mouse, scegliere **drill-through**, quindi **colonne struttura e modello**.  
  
     Verrà visualizzata la finestra di dialogo **drill-through** . Le colonne non utilizzate nel modello, ma disponibili per l'esecuzione di query, sono precedute dalla **struttura**.  
  
     È possibile notare che questo cluster contiene prevalentemente clienti dell'area del Pacifico e solo alcuni clienti residenti in altre aree geografiche.  
  
2.  Fare clic sul segno più nella colonna nidificata v Assoc Seq Line Items per visualizzare la sequenza di articoli in un determinato ordine cliente.  
  
3.  Chiudere la finestra di dialogo **drill-through** .  
  
    > [!NOTE]  
    >  Il pulsante **Riproduci** consente di eseguire una query sui dati. Tuttavia, la riesecuzione di una query non comporta la modifica dei dati visualizzati, a meno che il modello non sia stato aggiornato in modo dinamico in background da un altro processo.  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CProfiles"></a>Scheda Profili cluster  
 Nella scheda **Profili cluster** vengono visualizzate le sequenze presenti in ogni cluster. I cluster sono elencati in singole colonne a destra della colonna **Stati** .  
  
 Nel visualizzatore la riga del **modello** descrive la distribuzione complessiva degli elementi in un cluster e la riga **Model. Samples** contiene le sequenze degli elementi. Ogni riga delle sequenze di colori in ogni cella della riga **Model. Samples** rappresenta il comportamento di un utente selezionato in modo casuale nel cluster.  
  
 Ogni colore in ogni singolo istogramma di sequenza rappresenta un modello di prodotto. In Legenda data mining vengono indicate le sequenze di prodotti utilizzando la codifica con colori e i nomi dei modelli dei prodotti. Se sono state aggiunte altre colonne al modello per il clustering, ad esempio Region o IncomeGroup, il visualizzatore conterrà una riga aggiuntiva per ogni colonna, in cui viene visualizzata la distribuzione di questi valori all'interno di ogni cluster.  
  
#### <a name="to-view-the-sequences-that-are-most-common-in-a-cluster"></a>Per visualizzare le sequenze più comuni in un cluster  
  
1.  Fare clic con il **** pulsante destro del mouse sulla riga del modello `Largest Cluster`nella colonna per il cluster e selezionare **Mostra legenda**.  
  
     La colonna **color** contiene una barra ombreggiata che indica la frequenza degli elementi trovati nelle sequenze. Ogni articolo è rappresentato da un colore diverso. Nella colonna **significato** sono elencati i nomi dei modelli di prodotto per ogni colore. La colonna **Distribution** indica la percentuale di case che contengono questo elemento in una sequenza.  
  
2.  Chiudere **Legenda data mining**.  
  
3.  Fare clic con il pulsante destro del mouse sulla riga **Model. Samples** nella colonna con l'intestazione **popolamento** e selezionare **Mostra legenda**.  
  
4.  Analizza l'elenco di sequenze nel modello generale`.`  
  
     In Legenda data mining sono elencate per prime le sequenze più comuni, pertanto è possibile notare che Mountain Tire Tube è il primo articolo in molte sequenze. Ciò indica che è molto probabile che un cliente includa per primo tra gli acquisti l'articolo Mountain Tire Tube.  
  
#### <a name="to-drill-through-to-cases-from-the-cluster-viewer"></a>Per eseguire il drill-through nei case dal visualizzatore cluster  
  
1.  Scorrere verso il basso nel riquadro attributo fino a trovare la riga per `Region` l'attributo.  
  
     La riga contiene un istogramma per ogni cluster nel modello, oltre a un istogramma aggiuntivo per la **popolazione**, che indica l'intero set di case utilizzato nel modello. Un istogramma è una barra contenente diversi colori, ognuno dei quali rappresenta un attributo, mentre la dimensione della sezione colorata relativa all'attributo rappresenta la percentuale di case caratterizzati da tale attributo.  
  
2.  Confrontare gli istogrammi per i cluster rinominati `Pacific Cluster` e. `Largest Cluster` Ogni cluster viene visualizzato in una colonna diversa.  
  
     Entrambi sono identificati da un colore in tinta unita, ma i colori sono diversi.  
  
3.  Nella `Region` riga, posizionare il puntatore del mouse sull'istogramma colorato `Largest Cluster`per.  
  
     I valori visualizzati nella descrizione comando indicano le percentuali effettive dei case di ogni area.  
  
4.  Fare clic con il pulsante destro del mouse `Region` sull'istogramma colorato nella riga per `Pacific Cluster`, selezionare **drill-through**, quindi selezionare **solo colonne modello**.  
  
5.  Spostare la barra di scorrimento per rivedere tutti i clienti contenuti in questo cluster.  
  
     Eseguendo il drill-through nei dettagli è possibile notare anche questa volta che il cluster contiene prevalentemente ordini provenienti dall'area del Pacifico, oltre ad alcuni ordini provenienti dal Nord America e dall'Europa.  
  
6.  Chiudere la finestra di dialogo **drill-through** .  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CChars"></a>Scheda Caratteristiche cluster  
 La scheda **Caratteristiche cluster** riepiloga le transizioni tra gli stati in un cluster visualizzando le barre che rappresentano visivamente l'importanza del valore dell'attributo per il cluster selezionato. La colonna **variabili** indica il modo in cui il modello è importante per il cluster o il popolamento selezionato, ovvero un particolare valore o la relazione tra i valori, nota come *transizione*. Nella colonna **valori** sono disponibili maggiori dettagli sul valore o la transizione, mentre la colonna **probabilità** rappresenta visivamente il peso dell'attributo o della transizione.  
  
#### <a name="to-view-the-important-attributes-for-a-cluster"></a>Per visualizzare gli attributi importanti per un cluster  
  
1.  Nell'elenco a discesa **cluster** selezionare `Pacific Cluster`.  
  
     L'elenco viene aggiornato per mostrare le caratteristiche del cluster rinominato `Pacific Cluster`. In questo cluster la caratteristica più importante è `Region`.  
  
2.  Posizionare il mouse sulla barra ombreggiata nella riga per `Region`.  
  
     La probabilità che il valore corrisponda a Pacific è molto elevata. Per ulteriori informazioni su come interpretare questi valori, vedere [riferimento tecnico per l'algoritmo Microsoft Sequence Clustering](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
3.  Esaminare l'elenco delle caratteristiche del cluster fino a individuare la prima riga di transizione.  
  
4.  Una riga di transizione contiene la transizione del testo nella colonna **variabili** e una combinazione di valori di attributo sequenziali nella colonna **valore** . La sequenza può inoltre contenere punti iniziali e valori mancanti.  
  
     Si supponga, ad esempio, che la transizione includa il valore [Start]-> Road Tire Tube. Ciò significa che i clienti contenuti in questo cluster includono frequentemente l'articolo Road Tire Tube per primo tra gli acquisti. Questo comportamento potrebbe indicare che il prodotto è un articolo popolare molto ricercato dai clienti oppure semplicemente che il prodotto è facile da reperire sul sito riservato agli acquisti.  
  
5.  Scorrere l'elenco fino a individuare la prima transizione che non contiene **[Start]** o **mancante** .  
  
     Si supponga, ad esempio, di trovare la transizione **Touring Tire, Touring Tire Tube**. Ciò significa che i clienti inclusi in questo cluster hanno frequentemente acquistato questi articoli in combinazione, esattamente nell'ordine indicato.  
  
6.  Posizionare il mouse sulla barra ombreggiata relativa a questa transizione.  
  
     La probabilità della transizione verrà visualizzata come percentuale.  
  
7.  Nell'elenco a discesa **cluster** selezionare **popolamento (tutti)**.  
  
     L'elenco degli attributi verrà aggiornato per visualizzare le caratteristiche di tutti gli ordini utilizzati per creare il modello. In questo modello di data mining, la caratteristica più importante per distinguere i cluster è `Region`, con il valore **America del Nord**.  
  
 Dall'analisi di queste attività emergono due aspetti. In primo luogo, per ottenere un numero significativo di combinazioni è necessario disporre di una quantità elevata di dati. Ad esempio, è probabile che le sequenze con probabilità più elevata includano uno stato **[Start]** o **Missing** .  
  
 Il secondo è costituito da un forte impatto sul clustering sugli attributi `Region`per, che rende più difficile la visualizzazione dei gruppi di sequenze. Si decide pertanto di creare un altro modello che utilizza solo le sequenze e non include le colonne relative a area o reddito.  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_CDiscrim2"></a>Scheda Analisi discriminante tra cluster  
 La scheda analisi **discriminante tra cluster** consente di confrontare due cluster, per determinare gli attributi che distinguono un determinato cluster da un altro cluster. La scheda contiene quattro colonne: **variabili**, **valori**, **cluster 1**e **cluster 2**.  È possibile scegliere qualsiasi cluster da usare come **cluster 1** e **cluster 2**.  
  
 La colonna **variabili** indica il nome dell'attributo, che può essere un nome di colonna o una combinazione di nome di colonna e **transizione**di parola. Nella colonna **valori** viene visualizzato il valore esatto dell'attributo o della transizione. Le barre ombreggiate nelle colonne per **cluster 1** e **cluster 2** indicano il livello di attendibilità dell'attributo nei cluster da confrontare. Più lunga è la barra, maggiore è la probabilità che il cluster includa case con tale attributo.  
  
#### <a name="to-compare-two-clusters-by-using-the-cluster-discrimination-tab"></a>Per confrontare due cluster tramite la scheda Analisi discriminante tra cluster  
  
1.  Nella scheda analisi **discriminante tra cluster** per **cluster 1**Selezionare `Pacific Cluster`.  
  
     Per impostazione predefinita, la selezione per il **cluster 2** viene modificata in **complemento al cluster Pacifico**.  
  
     L'attributo top che distingue `Pacific Cluster` da tutti gli altri casi è l'area. L'influenza dell'attributo Region sul clustering nasconde gli altri attributi. Per evitare questo effetto, provare a eseguire il confronto tra alcuni dei cluster più piccoli. Questa operazione modifica l'elenco degli attributi, che potrebbe ora includere più transizioni tra modelli.  
  
2.  Individuare una riga di transizione e posizionare il mouse sulla barra ombreggiata.  
  
     Gli elementi nella colonna **valori** possono includere sia gli Stati sia le transizioni. L'ombreggiatura di ogni elemento indica il punteggio dell'analisi discriminante. Per ulteriori informazioni sul significato di punteggi diversi, vedere il [contenuto dei modelli di data mining per i modelli Sequence clustering &#40;Analysis Services-&#41;di data mining ](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_StateTran"></a>Scheda transizioni di stato  
 Nella scheda **transizioni di stato** è possibile selezionare un cluster ed esplorare le transizioni di stato. Se si seleziona **popolamento (tutti)** nell'elenco a discesa cluster, il diagramma mostra la distribuzione degli Stati per l'intero modello di data mining.  
  
 Ogni nodo del grafico rappresenta uno stato o un possibile valore delle sequenze che si sta tentando di analizzare. Il colore di sfondo dei nodi rappresenta la frequenza di tale stato. Alcuni stati sono collegati da linee che indicano la presenza di una transizione tra tali stati. È possibile spostare il dispositivo di scorrimento verso l'alto o verso il basso per modificare la soglia di probabilità delle transizioni. Ad alcuni nodi sono associati numeri che indicano la probabilità dello stato.  
  
#### <a name="to-explore-the-relationships-in-the-state-transition-tab"></a>Per esplorare le relazioni nella scheda Transizioni di stato  
  
1.  Nella scheda **transizioni di stato** del Visualizzatore modello di data mining selezionare `Pacific Cluster` dall'elenco dei cluster. Verificare che l'opzione **Mostra etichette perimetrali** sia selezionata.  
  
     Il grafico verrà aggiornato per visualizzare le transizioni più comuni in questo cluster.  
  
2.  Fare clic su un nodo collegato da una linea a un altro nodo.  
  
     Il grafico verrà aggiornato per evidenziare i nodi correlati. Il valore numerico accanto alla linea indica la probabilità della transizione.  
  
3.  Aumentare il dispositivo di scorrimento fino a **tutti i collegamenti**per aumentare il numero di transizioni incluse nel grafico.  
  
4.  Selezionare **popolamento (tutti)** dal **cluster**.  
  
     Si noti che quando si carica un cluster diverso, vengono ripristinate le impostazioni di visualizzazione predefinite del grafico, pertanto il dispositivo di scorrimento viene ricollocato in posizione centrale.  
  
5.  Fare clic sul nodo più scuro del grafico, che dovrebbe essere **Sport-100**.  
  
     Si noti che questo prodotto non è collegato da alcuna linea ad altri prodotti.  
  
6.  Spostare il dispositivo di scorrimento verso l'alto di uno spazio, per aumentare il numero di transizioni incluse nel grafico. Non andare fino a **tutti i collegamenti** .  
  
     Il grafico verrà aggiornato con l'aggiunta di diverse transizioni, nessuna delle quali include tuttavia il modello Sport-100.  
  
7.  Spostare il controllo Slider fino a tutti i **collegamenti**. Fare clic sul nodo Sport-100, se non è già selezionato.  
  
     Il grafico verrà aggiornato con l'aggiunta di numerose transizioni che includono il prodotto Sport-100. La direzione della freccia della linea di connessione indica se l'articolo Sport-100 è stato selezionato come primo o secondo articolo nella coppia.  
  
8.  Fare clic sul nodo relativo a Touring Tire e riposizionare il dispositivo di scorrimento al centro.  
  
     Inizialmente, esistono molte linee di transizione che connettono Touring Tire ad altri prodotti, ma quando si aumenta la soglia di probabilità, le transizioni meno probabili vengono eliminate dal grafo, lasciando solo la transizione, Touring Tire > Touring Tire Tube. Questa transizione indica che se un cliente include un articolo Touring Tire tra gli acquisti, esiste una forte probabilità che il cliente inserisca successivamente un articolo Touring Tire Tube.  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
##  <a name="bkmk_Generic"></a>Generic Content Tree Viewer  
 Questo visualizzatore può essere utilizzato per tutti i modelli, indipendentemente dall'algoritmo o dal tipo di modello. **MicrosoftGeneric Content Tree Viewer** è disponibile nell'elenco a discesa **Visualizzatore** .  
  
 Un albero dei contenuti è una rappresentazione di un modello di data mining sotto forma di una serie di nodi, in cui ogni nodo rappresenta le informazioni relative ai dati di training. Il nodo può contenere un modello, un set di regole, un cluster o la definizione di un intervallo di date che condividono alcuni attributi. Il contenuto esatto del nodo differisce a seconda dell'algoritmo e dell'attributo stimabile, ma la rappresentazione generale del contenuto è la stessa.  
  
 È possibile espandere ogni nodo per aumentare il livello di dettaglio e copiare il contenuto di qualsiasi nodo negli Appunti. Per altre informazioni, vedere [Visualizzare un modello utilizzando Microsoft Generic Content Tree Viewer](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
#### <a name="to-view-details-for-a-sequence-clustering-model-by-using-the-generic-content-tree-viewer"></a>Per visualizzare i dettagli di un modello Sequence Clustering tramite Generic Content Tree Viewer  
  
1.  Nella scheda **Visualizzatore modello di data mining** fare clic sull'elenco **Visualizzatore** e selezionare **Microsoft Generic Content Tree Viewer**.  
  
2.  Nel riquadro **Didascalia nodo** fare clic `Pacific Cluster (1)`su.  
  
     Il nome di questo nodo è composto dal nome descrittivo assegnato al cluster e dall'ID nodo sottostante. È possibile utilizzare gli ID nodo per eseguire il drill-down in ulteriori dettagli relativi al modello.  
  
3.  Espandere il primo nodo figlio, denominato **livello sequenza per cluster 1**.  
  
     Il nodo del livello di sequenza relativo a un cluster contiene dettagli sugli stati e le transizioni inclusi in tale cluster. È possibile utilizzare questi dettagli, disponibili nella colonna NODE_DISTRIBUTION, per esplorare le sequenze e gli stati di ogni cluster o dell'intero modello.  
  
4.  Continuare a espandere i nodi e a visualizzare i dettagli nel visualizzatore HTML.  
  
 Per ulteriori informazioni sul contenuto del modello di data mining e su come utilizzare i dettagli nel Visualizzatore, vedere [contenuto dei modelli di data mining per i modelli Sequence clustering &#40;Analysis Services-Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
 [Torna all'inizio](#bkmk_CDiagram)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di un modello Sequence Clustering correlato &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Sequence Clustering](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Sequence Clustering Model Query Examples](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)  
  
  
