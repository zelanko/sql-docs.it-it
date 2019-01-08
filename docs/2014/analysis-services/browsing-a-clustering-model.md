---
title: Esplorazione di un modello di Clustering | Microsoft Docs
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
- clustering [data mining]
- mining model, clustering
ms.assetid: 7f3f0949-d791-403a-88e2-54cb1a803dae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a0fd00201f782bba8b06ddde8753a86aeb89046
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535714"
---
# <a name="browsing-a-clustering-model"></a>Esplorazione di un modello di clustering
  Quando si apre un modello di clustering utilizzando **esplorare**, il modello viene visualizzato in un visualizzatore interattivo, simile al Visualizzatore di clustering in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Il visualizzatore consente di esplorare i cluster creati e comprenderne le caratteristiche. È inoltre possibile confrontare e contrapporre singoli segmenti con altri segmenti o con la popolazione.  
  
##  <a name="BKMK_Tabs"></a> Esplorare il modello  
 Il **esplorare** finestra include i seguenti strumenti che consentono di comprendere il modello di clustering ed esplorare gli attributi di gruppi di dati sottostanti:  
  
-   [Diagramma dei cluster](#BKMK_ClusterDiagram)  
  
-   [Profili cluster](#BKMK_ClusterProfiles)  
  
-   [Caratteristiche cluster](#BKMK_ClusterCharacteristics)  
  
-   [Analisi discriminante tra cluster](#BKMK_ClusterDiscrimination)  
  
 Per provare un modello di clustering, è possibile usare i dati di esempio nella scheda Training della cartella di lavoro di dati di esempio e compilare un modello di clustering utilizzando [Creazione guidata Cluster &#40;aggiuntivi di Data Mining per Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) e tutte le impostazioni predefinite .  
  
###  <a name="BKMK_ClusterDiagram"></a> Diagramma dei cluster  
 Il **diagramma dei Cluster** scheda Visualizza tutti i cluster che si trovano in un modello di data mining. Di seguito è possibile visualizzare il numero di raggruppamenti differenti trovati nel set di dati e la posizione che occupano gli uni rispetto agli altri.  
  
##### <a name="explore-the-cluster-diagram"></a>Esplorazione del diagramma dei cluster  
  
1.  Fare clic su Cluster 1 nel diagramma.  
  
     Si noti come le linee grigie che collegano tutti i cluster cambiano in modo che le linee che conducono al cluster selezionato vengano evidenziate in blu luminoso.  
  
     ![Introduzione al diagramma dei cluster](media/dm13-cluster-diagram-intro.gif "Introduzione al diagramma dei cluster")  
  
     L'intensità della linea che collega un cluster all'altro rappresenta il grado di somiglianza dei cluster. Se l'ombreggiatura è chiara o inesistente, il grado di somiglianza dei cluster è basso. Man mano che la linea diventa più scura, il grado di somiglianza tra i due cluster aumenta.  
  
2.  Fare clic e trascinare il dispositivo di scorrimento a sinistra del diagramma dei cluster per modificare il numero di linee visualizzate nel visualizzatore.  
  
     Quando si trascina il dispositivo di scorrimento verso il basso, vengono visualizzati solo i collegamenti più attendibili tra i cluster. Ciò consente di concentrarsi sui gruppi correlati.  
  
3.  Si noti che il **variabile ombreggiatura** controllo nell'angolo superiore destro delle **diagramma dei Cluster** finestra.  
  
     Per impostazione predefinita, viene impostata su **popolamento**. Ciò significa che i cluster più scuri dispongono di maggiore supporto.  
  
4.  Posizionare il cursore del mouse su qualsiasi cluster.  
  
     Viene visualizzata una descrizione comando contenente la popolazione di tale cluster.  
  
5.  A questo punto, fare clic sui **variabile ombreggiatura** elenco a discesa elenco e scegliere il **Age** variabile. Come in questo caso, viene visualizzato un elenco di valori nel **stato** casella di testo.  
  
     Nella colonna Age utilizzata come input per questo modello sono contenuti valori numerici continui, ma ai fini del clustering, tramite l'algoritmo vengono sempre discretizzati i numeri. Qui è possibile visualizzare i contenitori o gruppi che ha creato l'algoritmo, ad esempio "molto bassa (\<lt;=27)" e "molto elevato (> = 63)".  
  
6.  Dal **lo stato** negli elenchi a discesa, selezionare **molto elevato** e vedere come cambia il diagramma.  
  
     Modificando la variabile ombreggiatura, è possibile vedere immediatamente quali cluster contengono più clienti di questa fascia di età di destinazione e quali cluster contengono meno clienti in questa fascia di età.  
  
     ![Modificare il diagramma dei cluster per mostrare l'età](media/dm13-cluster-diagramshadebyage.gif "modificare il diagramma dei cluster per mostrare l'età")  
  
     Più scura è l'ombreggiatura, maggiore è la proporzione dell'attributo di destinazione e della distribuzione dei valori di tale cluster.  
  
7.  Individuare il cluster ombreggiatura più scura quando la **variabile ombreggiatura** è impostata su Age > 65.  
  
     Posizionare il mouse sul cluster.  
  
     Il valore visualizzato nella descrizione comando ora mostra la popolazione di clienti contenuti in questo cluster maggiori di 65 anni.  
  
8.  Il cluster e scegliere **Rinomina Cluster**. Digitare un nuovo nome descrittivo, ad esempio **oltre 65**. Il nuovo nome viene salvato con il modello nel server e può essere utilizzato per l'identificazione del cluster nelle altre viste di clustering.  
  
 [Torna all'inizio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterProfiles"></a> Profili cluster  
 Il **profili Cluster** scheda consente di confrontare la composizione di tutti i cluster in modo immediato. In questa scheda è possibile iniziare quando si sta acquisendo familiarità con il modello. Questa vista è anche utile successivamente, se, dopo aver esplorato un cluster specifico, si stabilisce che è necessario trovare quelli correlati.  
  
 **Profili cluster** offre anche un'utile Panoramica del modo in cui i cluster sono diversi tra loro. Di conseguenza, potrebbe risultare comodo utilizzare questa vista per assegnare a ogni cluster un nome descrittivo.  
  
##### <a name="explore-the-cluster-profiles"></a>Esplorazione del profili dei cluster  
  
1.  Fare clic sulla cella Occupation nella **stati** colonna, per visualizzare l'elenco di tutti i valori di Occupation.  
  
2.  Ora spostare il cursore su Occupation nei profili dei cluster.  
  
     Nella descrizione comando viene visualizzata la distribuzione di occupazioni in quel cluster.  
  
     ![Visualizzare i valori dettagliati nelle descrizioni comandi o nella legenda](media/dm13-cluster-profile-age-tooltip.gif "visualizzare i valori dettagliati nelle descrizioni comandi o nella legenda")  
  
     Si noti che, in alcuni cluster (ad esempio quello nell'immagine), l'elenco di occupazioni non sono completo e alcune occupazioni vengono sostituite con l'etichetta **altri**.  
  
     Ciò avviene per motivi strutturali poiché può essere difficile capire la differenza tra molte piccole barre in un istogramma. Per impostazione predefinita solo le barre di importanza più alta vengono mantenute e le barre rimanenti vengono raggruppate in un grigio **altri** bucket.  
  
     Per modificare il numero di barre visibili in qualsiasi istogramma, utilizzare l'opzione **barre istogramma**.  
  
3.  Si noti che il **età** colonna ha un aspetto diversa dagli altri. Fare clic sul rombo nel grafico utilizzato per rappresentare Age.  
  
     Nella colonna Age originalmente erano contenuti solo numeri continui. Per l'algoritmo di clustering sono richiesti valori discreti, pertanto vengono raggruppati i valori numerici nella colonna Age in un numero limitato di fasce di età, in base alla distribuzione di valori.  
  
4.  Fare clic su uno dei grafici a rombo in un profilo di cluster.  
  
     Questi grafici a rombi vengono visualizzati solo quando nei dati di origine si utilizzano valori numerici continui. Nei grafici a rombi vengono fornite alcune statistiche descrittive utili, inclusa la deviazione media e standard per tale valore in ogni cluster:  
  
    -   La linea nel grafico a rombi rappresenta l'intervallo di valori per l'attributo. I valori vengono anche mostrati nel **stati** colonna a sinistra del **profili** grafico.  
  
    -   Il centro del rombo è posizionato in corrispondenza della media del nodo.  
  
    -   La larghezza del rombo rappresenta la varianza dell'attributo in corrispondenza di quel nodo. Pertanto, un rombo con spessore minore indica che il nodo può creare una stima più accurata.  
  
5.  Per creare più spazio nel grafico, fare doppio clic su un cluster non è necessario visualizzare immediatamente e selezionare **Nascondi colonna**. Questo non viene eliminato dal modello; viene solo compressa temporaneamente la colonna.  
  
     Per visualizzare i cluster nascosti, è possibile fare clic e trascinare il bordo della colonna o selezionare il nome del cluster dall'elenco, **altri cluster**.  
  
6.  Scorrere verso il basso l'elenco di attributi fino a visualizzare Bike Buyer, quindi individuare il cluster con la percentuale più elevata di valori Sì.  
  
     Fare doppio clic sull'intestazione di colonna per il cluster che si desidera rinominare, selezionare **Rinomina cluster**e il tipo **acquirenti di biciclette**.  
  
     Il nuovo nome del cluster è persistente in tutte le viste e nel server, fino a quando non si rielabora il modello.  
  
     ![Rinominare i cluster per semplificare l'utilizzo del grafico](media/dm13-cluster-rename.gif "rinominare i cluster per semplificare l'utilizzo del grafico")  
  
 **Suggerimenti**  
  
-   Fare clic su un'intestazione di colonna per disporre gli attributi in ordine di importanza per il cluster.  
  
-   Trascinare le colonne per riordinarle nel visualizzatore.  
  
-   Fare clic su qualsiasi cella nel grafico dei profili per visualizzare statistiche dettagliate nel **legenda Data Mining**.  
  
-   Fare doppio clic su una cella qualsiasi e selezionare **colonne del modello di drill-through** per restituire i dati sottostanti per un nuovo foglio di lavoro di Excel.  
  
-   Fare clic sulla colonna del cluster sull'intestazione e seleziona **drill-through ai dati della struttura** per ottenere informazioni dettagliate sui membri del cluster che non sono state incluse nel modello.  
  
     Ad esempio, se si siano analizzando i clienti, si potrebbe lasciare le informazioni di contatto nei dati sottostanti (la struttura di data mining) ma non includerlo nel modello, perché non è utile per l'analisi. Tuttavia, dopo che i clienti sono stati assegnati ai cluster, è possibile visualizzare i dati dettagliati tramite il drill-through.  
  
 [Torna all'inizio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterCharacteristics"></a> Caratteristiche cluster  
 La vista Caratteristiche cluster consente di esplorare realmente un singolo cluster per trovare gli attributi che caratterizzano più fortemente questo gruppo di dati.  
  
##### <a name="explore-the-cluster-characteristics"></a>Esplorazione delle caratteristiche del cluster  
  
1.  Selezionare il **oltre 65** cluster sostituendo il **Cluster** elenco.  
  
     Dopo aver selezionato un cluster, è possibile visualizzare nel dettaglio le caratteristiche del cluster specifico.  
  
     Gli attributi contenuti nel cluster sono elencati nelle colonne **Variabili** , mentre lo stato di ogni attributo è elencato nella colonna **Valori** .  
  
     Gli stati degli attributi sono elencati in ordine di importanza, accompagnato dalla relativa probabilità in questo cluster, rappresentato come una barra colorata nella **probabilità** colonna.  
  
     ![Caratteristiche di un modello di clustering](media/dm13-cluster-characteristics.gif "caratteristiche di un modello di clustering")  
  
2.  Scegliere il **variabili** colonna per ordinare dall'attributo.  
  
     Modificando la variabile di ordinamento, è possibile vedere più facilmente come i valori per le variabili, ad esempio il reddito o la proprietà di un'automobile, vengono distribuiti nel gruppo.  
  
3.  Fare clic su **copia in Excel**.  
  
     Un nuovo foglio di lavoro viene aggiunto alla cartella di lavoro contenente le caratteristiche del cluster selezionato.  
  
4.  Scegliere ora un cluster diverso nell'elenco **acquirenti di biciclette**.  
  
5.  Fare clic su **copia in Excel**.  
  
     Si noti che il grafico delle caratteristiche del nuovo cluster viene aggiunto al relativo foglio di lavoro. È possibile spostarlo nello stesso foglio di lavoro di altro profilo per renderne più semplice per confrontarli, che verrà effettuato nel passaggio successivo.  
  
 **Suggerimenti**  
  
-   Si noti che la caratteristica primaria del cliente nel cluster oltre 65 è che non acquista il prodotto. Se si desidera saperne il motivo, è possibile esplorare i cluster e confrontare i gruppi o si potrebbe creare un modello correlato utilizzando un algoritmo che sia in grado di esplorare cause e risultati, ad esempio un modello di albero delle decisioni o un modello Naïve Bayes.  
  
-   Se si desidera ottenere un elenco completo di attributi e probabilità per questo cluster (o tutti i cluster), è possibile creare una query. Per esempi di query sui modelli di clustering, vedere [Clustering Model Query Examples](data-mining/clustering-model-query-examples.md).  
  
 [Torna all'inizio](#BKMK_Tabs)  
  
###  <a name="BKMK_ClusterDiscrimination"></a> Analisi discriminante tra cluster  
 Si utilizza il **analisi discriminante tra Cluster** pressione di tab per confrontare gli attributi tra due cluster o tra un cluster e tutti gli altri casi nel set di dati.  
  
 Per evidenziare le funzionalità di questo visualizzatore, lo confronteremo con alle tabelle side-by-side di Excel che è stato creato sulla base di **caratteristiche Cluster** visualizzazione.  
  
##### <a name="explore-cluster-discrimination"></a>Esplorazione dell'analisi discriminante del cluster  
  
1.  Per selezionare i cluster da confrontare, usare gli elenchi **Cluster 1** e **Cluster 2** .  
  
    -   Per Cluster 1, selezionare Oltre 65.  
  
    -   Per Cluster 2, selezionare Bike Buyer.  
  
     Il confronto dovrebbe essere simile a quello riportato nell'immagine seguente.  
  
     ![confronto tra cluster in un modello](media/dm13-cluster-compareclusters.gif "confronto tra cluster in un modello")  
  
     Si noti che, dietro le quinte, il **analisi discriminante tra Cluster** Visualizzatore inviate query complesse al server di data mining, per estrarre gli attributi più importanti nella distinzione tra i due gruppi, rendendo più semplice da confrontare due set di clienti.  
  
2.  Fare clic su uno del **predilige...**  colonne.  
  
     Nella barra a destra dell'elenco di valori e di attributi vengono visualizzati quali valori e funzionalità sono più importanti come caratteristica del cluster selezionato.  
  
3.  Confrontare quindi gli elenchi in Excel.  
  
     ![Grafico della rete di dipendenze per un modello di associazione](media/dm13-comparing-profiles-in-excel.gif "grafico della rete di dipendenze per un modello di associazione")  
  
     Poiché le statistiche sottostanti utilizzate per la compilazione dell'immagine nel visualizzatore vengono salvate in Excel come tabelle, è possibile filtrare, ordinare e visualizzare i valori effettivi di probabilità.  
  
     Oltre a utilizzare Excel, è consigliabile provare il visualizzatore cluster per Visio, che consente non solo di visualizzare i punti dati ma anche di modificare e migliorare ampiamente il grafico. Per altre informazioni, vedere [descrizione dettagliata del diagramma Cluster &#40;componenti aggiuntivi Data Mining&#41;](cluster-diagram-walkthrough-data-mining-add-ins.md).  
  
 **Suggerimenti**  
  
 Dopo aver ottenuto alcune informazioni sui gruppi di clienti, provare a usare il [Scenario di simulazione &#40;strumenti di analisi tabelle per Excel&#41; ](what-if-scenario-table-analysis-tools-for-excel.md) oppure [dello Scenario ricerca obiettivo &#40;strumenti di analisi tabelle per Excel&#41; ](goal-seek-scenario-table-analysis-tools-for-excel.md) strumenti per esplorare i fattori nel modello che potrebbero essere modificate per influire sul risultato.  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione di modelli in Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)   
 [Creazione guidata del cluster &#40;dati di componenti aggiuntivi Data Mining per Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
  
