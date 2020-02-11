---
title: Esplorazione del modello di previsione (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0a00f409-050f-4b92-9763-ba31a6aa3052
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 607f300fbf2138796bb02c66c62386fcc93e6a45
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62992263"
---
# <a name="exploring-the-forecasting-model-intermediate-data-mining-tutorial"></a>Esplorazione del modello di previsione (Esercitazione intermedia sul data mining)
  Ora che è stato compilato il modello di data mining Forecasting, è possibile esplorare i risultati utilizzando la scheda **Visualizzatore modello** di data mining di progettazione modelli di data mining. Il [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizzatore Time Series contiene due schede: **grafici** e **modello**.  
  
 È inoltre possibile utilizzare Microsoft Generic Content Tree Viewer con tutti i modelli. Ogni vista presenta un'immagine leggermente diversa delle informazioni nel modello Time Series.  
  
-   [Scheda grafici](#bkmk_Charts)  
  
-   [Scheda Modello](#bkmk_Model)  
  
-   [Microsoft Generic Content Tree Viewer](#bkmk_Content)  
  
##  <a name="bkmk_Charts"></a>Scheda grafici  
 La scheda **grafici** del visualizzatore [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series Mostra graficamente ogni serie, inclusi i dati cronologici e le stime. Ogni linea del grafico della serie temporale rappresenta una combinazione univoca di prodotto, area e attributo stimabile.  
  
 Nella legenda a destra del visualizzatore vengono elencate le serie temporali disponibili, in base alle selezioni nell'elenco a discesa. È possibile scegliere le serie temporali da visualizzare nel grafico selezionando o deselezionando le caselle di controllo.  
  
 È inoltre possibile modificare le opzioni di visualizzazione, ad esempio i colori utilizzati per ogni serie temporale, o decidere se visualizzare i valori in qualsiasi punto del grafico.  
  
#### <a name="to-select-a-time-series"></a>Per selezionare una serie temporale  
  
1.  Se non è visibile, fare clic sulla scheda **grafici** della scheda **Visualizzatore modello di data mining** .  
  
2.  Fare clic sull'elenco a discesa a destra della vista del grafico e selezionare tutte le caselle di controllo. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     A questo punto il grafico dovrebbe contenere 24 linee delle serie.  
  
3.  Nelle caselle di controllo a destra del grafico deselezionare le caselle per nascondere temporaneamente le linee per tutte le serie basate sull'importo.  
  
     A questo punto deselezionare le caselle di controllo relative alle biciclette R750 e R250.  
  
     Il grafico conterrà solo le sei linee delle serie seguenti, in modo da consentire di confrontare più facilmente le tendenze per le biciclette M200 e T1000.  
  
    -   **M200 Europe: Quantity**  
  
    -   **M200 North America: Quantity**  
  
    -   **M200 Pacific: Quantity**  
  
    -   **T1000 Europe: Quantity**  
  
    -   **T1000 North America: Quantity**  
  
    -   **T1000 Pacific: Quantity**  
  
 ![Serie per la stima delle quantità M200 e T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "Serie per la stima delle quantità M200 e T1000")  
  
 Nel grafico riprodotto in questo visualizzatore sono inclusi sia i dati cronologici che quelli stimati. Ai dati stimati viene applicata un'ombreggiatura per distinguerli dai dati cronologici. Per rendere più semplice il confronto tra serie diverse, è inoltre possibile modificare i colori associati a ogni linea nel grafico. Per altre informazioni, vedere [Modificare i colori usati nei visualizzatori data mining](../../2014/analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md).  
  
 Dalle linee di tendenza è possibile vedere che in genere le vendite totali per tutte le aree sono in aumento e raggiungono il periodo di picco ogni anno nel mese di dicembre. Dal grafico è inoltre possibile vedere che i dati per la bicicletta T1000 hanno inizio molto più tardi dei dati per le altre serie di prodotti. Ciò è dovuto al fatto che si tratta di un prodotto più nuovo, ma essendo questa serie basata su una quantità di dati molto inferiore, è possibile che le stime non siano accurate.  
  
 Per impostazione predefinita, vengono visualizzati cinque intervalli per la stima per ogni serie temporale, sotto forma di linea punteggiata. È possibile modificare questo valore in modo da visualizzare un numero maggiore o minore di stime. È inoltre possibile visualizzare graficamente la deviazione standard per le stime aggiungendo barre di errore al grafico.  
  
#### <a name="to-change-prediction-and-display-options-in-the-chart-view"></a>Per modificare le opzioni relative a stima e visualizzazione nella vista del grafico  
  
1.  Provare a modificare il valore per i **passaggi di stima** gradualmente, aumentando da **5** a **10**e quindi tornando a **6**.  
  
     Nel caso di ampie fluttuazioni dei dati cronologici, tali fluttuazioni tendono a essere ripetute o addirittura amplificate man mano che si aumenta il numero di stime. A questo punto è probabilmente necessario effettuare una ricerca per comprendere la causa dell'eccessivo aumento di dati cronologici e decidere quindi se accettare i risultati, cercare di trovare un tipo di correzione nei dati di origine o applicare l'anti-aliasing al modello.  
  
2.  Selezionare la casella di controllo **Mostra deviazioni** .  
  
     Questa opzione consente di visualizzare l'errore stimato per ogni valore stimato.  
  
3.  Osservare la scala dell'asse X. Le modifiche dei dati cronologici e stimati vengono sempre espresse come una percentuale, ma i valori effettivi vengono modificati automaticamente in base a tutti i valori nel grafico. In caso di confronto dei modelli, è pertanto opportuno evitare di basarsi solo sugli elementi visivi. Per ottenere il valore esatto o l'incremento percentuale e il valore per le stime, posizionare il mouse sulla linea tratteggiata o sulle linee continue oppure fare clic sulle linee per visualizzare i valori in **Legenda data mining**.  
  
     **Suggerimento**: se **Legenda data mining** non è visibile, passare alla visualizzazione **modello** , fare clic con il pulsante destro del mouse su un nodo e scegliere Mostra **Legenda**.  
  
 Analizzando queste tendenze si nota la mancanza di dati per alcune serie e si desidera ottenere stime più affidabili facendo la media delle vendite per modello o eventualmente per area. Si esaminerà questo approccio in una lezione successiva di questa esercitazione.  
  
 [Torna all'inizio](#bkmk_Charts)  
  
##  <a name="bkmk_Model"></a>Scheda modello  
 La scheda **modello** del visualizzatore [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series in Progettazione modelli di data mining consente di visualizzare il modello di previsione sotto forma di grafico ad albero.  
  
 Notare innanzitutto che poiché i dati descrivono due misure diverse (Amount e Quantity) per vendite di più linee di prodotti (T1000 e così via) in tre aree diverse (Europa, Nord America e Pacific), il modello compilato contiene in effetti 24 alberi diversi, ognuno dei quali rappresenta un modello dei modelli di vendita per una combinazione diversa di area, prodotto e attributo stimabile.  
  
 È possibile scegliere la combinazione di linea prodotto, area e metrica vendite che si desidera visualizzare selezionando una serie dall'elenco a discesa **albero** nella scheda **modello** .  
  
 Nozioni che è possibile apprendere visualizzando il modello come un albero Si confronti, ad esempio, due modelli, uno con diversi livelli nell'albero e uno con un solo nodo.  
  
-   Quando un grafico dell'albero contiene un singolo nodo, significa che la tendenza individuata nel modello è per lo più omogenea nel tempo. È possibile utilizzare questo singolo nodo, denominato **All**, per visualizzare la formula che descrive la relazione tra le variabili di input e il risultato.  
  
-   Se un grafico dell'albero per una serie temporale dispone di più rami, significa che la serie temporale rilevata è troppo complessa per essere rappresentata come una singola equazione. Il grafico ad albero può invece contenere più rami, ogni ramo etichettato con le condizioni che hanno causato la *suddivisione*dell'albero. Quando l'albero viene diviso, ogni ramo rappresenta un segmento temporale diverso, all'interno del quale la tendenza può essere descritta come una singola equazione.  
  
     Se, ad esempio, si osserva il grafico grafico e si verifica un improvviso salto nel volume di vendita che inizia a settembre e si continua fino a un giorno festivo, è possibile passare alla visualizzazione **modello** per visualizzare la data esatta in cui la tendenza è cambiata. I rami nell'albero che rappresentano "prima di settembre" e "dopo settembre" contengono formule diverse: una formula che descrive matematicamente le tendenze di vendita fino alla divisione e un'altra formula che descrive le tendenze di vendita per il settembre fino a festività di fine anno.  
  
#### <a name="to-explore-the-decision-tree-for-a-time-series-model"></a>Per esplorare l'albero delle decisioni per un modello Time Series  
  
1.  Nell'elenco **albero** nella scheda **modello** del Visualizzatore selezionare la serie **T1000 Europe: amount** .  
  
     Fare clic sul nodo con l'etichetta **tutti**.  
  
     Per un nodo **tutti** , la descrizione comando visualizzata include informazioni quali, il numero di case nell'intera serie e le equazioni della serie temporale derivate dall'analisi dei dati.  
  
2.  Se **Legenda data mining** non è visibile, fare clic con il pulsante destro del mouse sul nodo e scegliere **Mostra legenda**.  
  
     La **Legenda data mining** fornisce le stesse informazioni presenti nella descrizione comando. Se una delle variabili indipendenti è discreta, verrà inoltre visualizzato un istogramma che illustra la distribuzione delle variabili nel nodo.  
  
3.  A questo punto selezionare una serie temporale diversa da visualizzare. Utilizzando l'elenco **ad albero** nella scheda **modello** del visualizzatore, selezionare la serie **M200 America del Nord: amount** .  
  
     Il grafico ad albero contiene ora un nodo **tutti** e due nodi figlio. Osservando le etichette dei nodi figlio, è possibile identificare il punto in cui la linea di tendenza è stata modificata.  
  
     Per ogni nodo figlio, la descrizione in **Legenda data mining** include anche il numero di case in ogni ramo dell'albero.  
  
 Nell'elenco seguente vengono descritte alcune funzionalità aggiuntive del visualizzatore alberi:  
  
-   È possibile modificare la variabile rappresentata nel grafico utilizzando il controllo in **background** . Per impostazione predefinita, i nodi più scuri contengono più casi, perché il valore di **background** è impostato su **population**. Per visualizzare solo il numero di case presenti in un nodo, posizionare il puntatore del mouse su un nodo e visualizzare la descrizione comando visualizzata oppure fare clic sul nodo e visualizzare i numeri nella finestra **legenda del nodo** .  
  
-   Nella descrizione comando o facendo clic sul nodo è inoltre possibile visualizzare la formula di regressione del nodo. Se è stato creato un modello misto, è possibile visualizzare due formule, una per ARTXP (nei nodi foglia) e uno per ARIMA (nel nodo radice dell'albero).  
  
-   Nei nodi che rappresentano numeri continui vengono utilizzati piccoli rombi. L'intervallo degli attributi viene visualizzato nella barra su cui è presente il rombo. Il rombo è centrato sulla media del nodo e il relativo spessore rappresenta la varianza dell'attributo in tale nodo.  
  
 [Torna all'inizio](#bkmk_Charts)  
  
##  <a name="bkmk_Content"></a>Opzionale Generic Content Tree Viewer  
 Oltre al visualizzatore personalizzato per la serie temporale, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornisce **MicrosoftGeneric Content Tree Viewer** per l'uso con tutti i modelli di data mining. Questo visualizzatore fornisce alcuni vantaggi:  
  
-   **Visualizzatore Microsoft Time Series**: questa visualizzazione unisce i risultati dei due algoritmi. Anche se è possibile visualizzare ogni serie separatamente, non è possibile determinare come sono stati combinati i risultati di ogni algoritmo. Inoltre in questa vista le descrizioni comando e Legenda data mining mostrano solo le statistiche più importanti.  
  
-   **Generic Content Tree Viewer**: consente di esplorare e visualizzare in una sola volta tutte le serie di dati utilizzate nel modello e, se è stato creato un modello misto, gli alberi ARIMA e ARTxp vengono visualizzati nello stesso grafico.  
  
     È possibile utilizzare questo visualizzatore per ottenere tutte le statistiche da entrambi gli algoritmi, oltre alle distribuzioni dei valori.  
  
     Consigliato per gli utenti esperti di data mining chi desiderano ottenere maggiori informazioni sulle analisi ARIMA e ARTXP.  
  
#### <a name="to-view-details-for-a-particular-data-series-in-the-generic-content-viewer"></a>Per visualizzare i dettagli per una particolare serie di dati in Generic Content Tree Viewer  
  
1.  Nella scheda **Visualizzatore modello di data mining** selezionare **Microsoft Generic Content Tree Viewer** dall'elenco a discesa **Visualizzatore** .  
  
2.  Nel riquadro **Didascalia nodo** fare clic sul nodo in primo piano (tutti).  
  
3.  Nel riquadro **Dettagli nodo** visualizzare il valore per ATTRIBUTE_NAME.  
  
     Questo valore indica quale serie, o combinazione di prodotto e area, è contenuta nel nodo. Nell'esempio di AdventureWorks il nodo superiore è relativo alla serie M200 Europe.  
  
4.  Nel riquadro **Didascalia nodo** individuare il primo nodo con nodi figlio.  
  
     Se un nodo della serie dispone di elementi figlio, la visualizzazione albero visualizzata nella scheda **modello** del Visualizzatore Microsoft Time Series avrà anche una struttura di branching.  
  
5.  Espandere il nodo e fare clic su uno dei nodi figlio.  
  
     La colonna NODE_DESCRIPTION dello schema contiene la condizione che ha causato la suddivisione dell'albero.  
  
6.  Nel riquadro **Didascalia nodo** fare clic sul nodo ARIMA superiore ed espandere il nodo fino a quando non sono visibili tutti i nodi figlio.  
  
7.  Nel riquadro **Dettagli nodo** visualizzare il valore per ATTRIBUTE_NAME.  
  
     Questo valore indica quale serie temporale è contenuta nel nodo. Il nodo superiore nella sezione ARIMA deve corrispondere al nodo superiore nella sezione (Tutti). Nell'esempio di AdventureWorks questo nodo contiene l'analisi ARIMA relativa alla serie M200 Europe.  
  
 Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli Time Series &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
 [Torna all'inizio](#bkmk_Charts)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di stime basate su serie temporali &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di query sul modello Time Series](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
