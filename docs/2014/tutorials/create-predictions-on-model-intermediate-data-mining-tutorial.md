---
title: Creazione di stime in un modello Sequence Clustering (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 94a8d4f9-a76a-49c5-9785-917010359511
author: minewiskan
ms.author: owend
manager: kfilee
ms.openlocfilehash: 893067e234d868ae6dde2f93d93bfd50458bfeb2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63217746"
---
# <a name="creating-predictions-on-a-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Creazione di stime su un modello Sequence Clustering (Esercitazione intermedia sul data mining)
  Dopo aver compreso meglio il modello Sequence Clustering, esplorarlo nel Visualizzatore, è possibile creare query di stima utilizzando la stima Generatore di query nella scheda **Stima modello** di data mining di progettazione modelli di data mining. Per creare una stima, occorre selezionare innanzitutto il modello Sequence Clustering, quindi i dati di input. Per gli input, è possibile utilizzare un'origine dati esterna o compilare una query singleton e fornire valori in una finestra di dialogo.  
  
 In questa lezione si presuppone che l'utente abbia già familiarità con l'utilizzo del generatore delle query di stima e desideri apprendere come compilare query specifiche per un modello Sequence Clustering. Per informazioni generali sull'utilizzo di Generatore di query di stima, vedere [interfacce di query di data mining](../../2014/analysis-services/data-mining/data-mining-query-tools.md) o la sezione dell'esercitazione di base sul data mining, [creazione di stime &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md).  
  
## <a name="creating-predictions-on-the-regional-model"></a>Creazione di stime sul modello regionale  
 Per questo scenario verranno dapprima create alcune query di stima singleton, per avere un'idea di come le stime potrebbero variare a seconda dell'area.  
  
#### <a name="to-create-a-singleton-query-on-a-sequence-clustering-model"></a>Per creare una query singleton in un modello Sequence Clustering  
  
1.  Fare clic sulla scheda **Stima modello** di data mining di progettazione modelli di data mining.  
  
2.  Scegliere **query singleton**dal menu colonna **modello di data mining** .  
  
     Verranno visualizzati il riquadro **modello di data mining** e il riquadro **input query singleton** .  
  
3.  Nel riquadro **modello di data mining** fare clic su **Seleziona modello**. Se il modello Sequence Clustering è già stato selezionato, ignorare questo passaggio.  
  
     Verrà visualizzata la finestra di dialogo **Seleziona modello di data mining** .  
  
4.  Espandere il nodo che rappresenta la struttura di data mining **Sequence Clustering con Region**e selezionare il modello **Sequence Clustering with Region**. Fare clic su **OK**. Per il momento, ignorare il riquadro di input. Gli input verranno specificati dopo avere configurato le funzioni di stima.  
  
5.  Nella griglia fare clic sulla cella vuota sotto **origine** e selezionare **funzione di stima.** Nella cella sotto **campo**selezionare **PredictSequence**.  
  
    > [!NOTE]  
    >  È anche possibile usare la funzione **Predict** . In tal caso, assicurarsi di scegliere la versione della funzione **Predict** che accetta una colonna di tabella come argomento.  
  
6.  Nel riquadro **modello di data mining** selezionare la tabella `v Assoc Seq Line Items`nidificata e trascinarla nella griglia nella casella **criteri/argomento** della funzione **PredictSequence** .  
  
     Il trascinamento dei nomi di tabella e colonna consente di compilare istruzioni complesse senza errori di sintassi. Tuttavia, sostituisce il contenuto corrente della cella, che include altri argomenti facoltativi per la funzione **PredictSequence** . Per visualizzare gli altri argomenti, è possibile aggiungere temporaneamente una seconda istanza della funzione alla griglia per riferimento.  
  
7.  Fare clic sul pulsante **result** nell'angolo superiore del generatore di query di stima.  
  
 I risultati previsti contengono una singola colonna con l' **espressione**di intestazione. La colonna **espressione** contiene una tabella nidificata con tre colonne, come indicato di seguito:  
  
|$SEQUENCE|Line Number|Modello|  
|---------------|-----------------|-----------|  
|1||Mountain-200|  
  
 Che cosa indicano questi risultati? Si tenga presente che non è stato specificato alcun input. La stima pertanto viene eseguita rispetto all'intera popolazione dei case e Analysis Services restituisce la stima più probabile a livello complessivo.  
  
### <a name="adding-inputs-to-a-singleton-prediction-query"></a>Aggiunta di input a una query di stima singleton  
 Finora non è stato specificato alcun input. Nell'attività successiva verrà utilizzato il riquadro **input query singleton** per specificare alcuni input per la query. Innanzitutto, si utilizzerà [Region] come input per il modello Sequence Clustering regionale, per determinare se le sequenze stimate sono le stesse per tutte le aree. Verrà quindi descritto come modificare la query per aggiungere la probabilità per ogni stima e convertire i risultati in formato flat per renderne più semplice la visualizzazione.  
  
##### <a name="to-generate-predictions-for-a-specific-customer-group"></a>Per generare stime per uno specifico gruppo di clienti  
  
1.  Fare clic sul pulsante **progettazione** nell'angolo superiore sinistro del generatore di query di stima per tornare alla griglia di compilazione della query.  
  
2.  Nella finestra di dialogo **input query singleton** fare clic sulla casella **valore** per `Region`e selezionare **Europa**.  
  
3.  Fare clic sul pulsante **risultato** per visualizzare le stime per i clienti in Europa.  
  
4.  Fare clic sul pulsante **progettazione** nell'angolo superiore sinistro del generatore di query di stima per tornare alla griglia di compilazione della query.  
  
5.  Nella finestra di dialogo **input query singleton** fare clic sulla casella **valore** per `Region`e selezionare **America del Nord**.  
  
6.  Fare clic sul pulsante **risultato** per visualizzare le stime per i clienti in America del Nord.  
  
### <a name="adding-probabilities-by-using-a-custom-expression"></a>Aggiunta di probabilità tramite un'espressione personalizzata  
 Restituire la probabilità per ogni stima è leggermente più complicato, perché la probabilità è un attributo della stima e viene restituita come una tabella nidificata. Se si ha familiarità con DMX (Data Mining Extensions), è possibile modificare facilmente la query per aggiungere un'istruzione sub-SELECT sulla tabella nidificata. Tuttavia, è anche possibile creare un'istruzione sub-SELECT nel generatore delle query di stima aggiungendo un'espressione personalizzata.  
  
##### <a name="to-output-probabilities-for-a-predicted-sequence-by-using-a-custom-expression"></a>Per restituire le probabilità per una sequenza stimata tramite un'espressione personalizzata  
  
1.  Fare clic sul pulsante **progettazione** nell'angolo superiore sinistro del generatore di query di stima per tornare alla griglia di compilazione della query.  
  
2.  Nella griglia, in **origine**, fare clic su una nuova riga e selezionare **espressione personalizzata**.  
  
3.  Lasciare vuota la casella sotto **campo** .  
  
4.  Per **alias**Digitare `t`.  
  
5.  Nella casella **criteri/argomento** Digitare l'istruzione sub-SELECT completa, come illustrato nell'esempio di codice seguente. Assicurarsi di includere le parentesi iniziale e finale.  
  
    ```  
    (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))  
    ```  
  
6.  Fare clic sul pulsante **risultato** per visualizzare le stime per i clienti in Europa.  
  
 I risultati ora contengono due tabelle nidificate, una con la stima e una con la probabilità per la stima. Se la query non funziona, è possibile passare alla visualizzazione Progettazione query ed esaminare l'istruzione della query completa, che dovrebbe avere l'aspetto seguente:  
  
```  
SELECT  
  PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
  ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
FROM  
  [Sequence Clustering with Region]  
NATURAL PREDICTION JOIN  
(SELECT 'Europe' AS [Region]) AS t  
```  
  
### <a name="working-with-results"></a>Utilizzo dei risultati  
 Quando nei risultati sono presenti molte tabelle nidificate, è possibile convertire i risultati in formato flat per semplificarne la visualizzazione. A tale scopo, è possibile modificare manualmente la query aggiungendovi la parola chiave `FLATTENED`.  
  
##### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Per convertire in formato flat i set di righe nidificati in una query di stima  
  
1.  Fare clic sul pulsante **query** nell'angolo del generatore di query di stima.  
  
     La griglia viene sostituita da un riquadro aperto in cui è possibile visualizzare e modificare l'istruzione DMX creata dal generatore delle query di stima.  
  
2.  Dopo la parola chiave `SELECT` digitare `FLATTENED`.  
  
     Il testo completo della query dovrebbe risultare analogo al seguente:  
  
    ```  
    SELECT FLATTENED  
      PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
      ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
    FROM  
      [Sequence Clustering with Region]  
    NATURAL PREDICTION JOIN  
    (SELECT 'Europe' AS [Region]) AS t  
    ```  
  
3.  Fare clic sul pulsante **risultati** nell'angolo superiore del generatore di query di stima.  
  
 Dopo avere modificato manualmente una query, non sarà possibile tornare alla visualizzazione della struttura senza perdere le modifiche apportate. È tuttavia possibile salvare l'istruzione DMX creata manualmente in un file di testo, quindi tornare alla visualizzazione della struttura. Eseguendo tale operazione, verrà ripristinata l'ultima versione della query valida nella visualizzazione della struttura.  
  
## <a name="creating-predictions-on-the-related-model"></a>Creazione di stime sul modello correlato  
 Negli esempi precedenti è stata utilizzata una colonna della tabella del case, Region, come input per la query di stima singleton perché si era interessati a sapere se il modello aveva individuato eventuali differenze tra le aree. Tuttavia, dopo avere esplorato il modello, si è deciso che le differenze non sono abbastanza marcate da giustificare una personalizzazione dei consigli sui prodotti in base all'area. Ciò che si è realmente interessati a stimare sono gli articoli che i clienti selezionano. Nelle query che seguono, pertanto, si utilizzerà il modello Sequence Clustering che non include Region per generare consigli per tutti i clienti.  
  
### <a name="using-nested-table-columns-as-input"></a>Utilizzo di colonne di tabelle nidificate come input  
 Innanzitutto verrà creata una query di stima singleton che accetta un solo articolo come input e restituisce l'articolo successivo più probabile. Per ottenere una stima di questo tipo, è necessario utilizzare una colonna di tabella nidificata come valore di input. Questo avviene perché l'attributo stimato, Model, fa parte di una tabella nidificata. Analysis Services fornisce la finestra di dialogo **input tabella nidificata** che consente di creare facilmente query di stima sugli attributi di una tabella nidificata utilizzando l'generatore di query di stima.  
  
##### <a name="to-use-a-nested-table-as-input-to-a-prediction"></a>Per utilizzare una tabella nidificata come input per una stima  
  
1.  Fare clic sul pulsante **progettazione** nell'angolo superiore sinistro del generatore di query di stima per tornare alla griglia di compilazione della query.  
  
2.  Nella finestra di dialogo **input query singleton** fare clic sulla casella **valore** per `Region`e selezionare la riga vuota per cancellare l'input per questo campo.  
  
3.  Nella finestra di dialogo **input query singleton** fare clic sulla casella **valore** per `vAssocSeqLineItems`, quindi fare clic sul pulsante (...).  
  
4.  Nella finestra di dialogo **input tabella nidificata** fare clic su **Aggiungi**.  
  
5.  Nella nuova riga fare clic sulla casella in `Model`e selezionare Touring Tire nell'elenco. Fare clic su **OK**.  
  
6.  Fare clic sul pulsante **risultato** per visualizzare le stime.  
  
 Il modello consiglia gli articoli successivi per tutti i clienti che scelgono Touring Tire come primo articolo. Si sa già dall'esplorazione del modello che di frequente i clienti acquistano insieme i prodotti Touring Tire e Touring Tire Tube, pertanto questi consigli sembrano validi.  
  
|$SEQUENCE|Line Number|Modello|  
|---------------|-----------------|-----------|  
|1||Touring Tire Tube|  
|2||Sport-100|  
|3||Long-Sleeve Logo Jersey|  
  
### <a name="creating-a-bulk-prediction-query-using-nested-table-inputs"></a>Creazione di una query di stima bulk tramite input di tabelle nidificate  
 Una volta verificato che il modello crea il tipo di stime che è possibile utilizzare per la creazione di consigli, verrà creata una query di stima associata a un'origine dati esterna. Tale origine dati fornirà valori che rappresentano i prodotti correnti. Poiché si è interessati alla creazione di una query di stima che fornisca l'ID cliente e un elenco di prodotti come input, si aggiungerà la tabella dei clienti come tabella del case e la tabella degli acquisti come tabella nidificata. Si aggiungeranno quindi funzioni di stima per creare consigli, come in precedenza.  
  
 Si tratta della stessa procedura utilizzata per creare stime per lo scenario di analisi degli acquisti nella lezione 3, tuttavia in un modello Sequence Clustering le stime necessitano anche dell'ordine come input.  
  
##### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Per creare una query di stima tramite input di tabelle nidificate  
  
1.  Nel riquadro **modello di data mining** selezionare il modello Sequence Clustering, se non è già selezionato.  
  
2.  Nella finestra di dialogo **Seleziona tabella/** e di input fare clic su **Seleziona tabella del case**.  
  
3.  Nella finestra di dialogo **Seleziona tabella** selezionare Orders in origine dati. Nell'elenco **nome tabella/vista** selezionare vAssocSeqOrders e quindi fare clic su **OK**.  
  
4.  Nella finestra di dialogo **Seleziona tabella/** e di input fare clic su **Seleziona tabella nidificata**.  
  
5.  Nella finestra di dialogo **Seleziona tabella** selezionare Orders in **origine dati**. Nell'elenco **nome tabella/vista** selezionare vAssocSeqLineItems e quindi fare clic su **OK**.  
  
     Analysis Services tenterà di rilevare le relazioni e di crearle automaticamente se i tipi di dati corrispondono e i nomi delle colonne sono simili. Se le relazioni create non sono corrette, è possibile fare clic con il pulsante destro del mouse sulla linea di join e scegliere **modifica connessioni** per modificare il mapping delle colonne. in alternativa, è possibile fare clic con il pulsante destro del mouse sulla linea di join e scegliere **Elimina** per rimuovere completamente la relazione. In questo caso, poiché le tabelle erano già unite in join nella vista origine dati, tali relazioni vengono aggiunte automaticamente al riquadro di progettazione.  
  
6.  Aggiungere una nuova riga alla griglia. In **origine**selezionare vAssocSeqOrders e per **campo**selezionare CustomerKey.  
  
7.  Aggiungere una nuova riga alla griglia. Per **origine**selezionare **funzione di stima**e in **campo**selezionare **PredictSequence**.  
  
8.  Trascinare vAssocSeqLineItems nella casella **criteri/argomento** . Fare clic alla fine della casella **criteri/argomento** , quindi digitare gli argomenti seguenti: `2`.  
  
     Il testo completo nella casella **criteri/argomento** deve essere:`[Sequence Clustering].[v Assoc Seq Line Items],2`  
  
9. Fare clic sul pulsante **risultato** per visualizzare le stime per ogni cliente.  
  
 Questo passaggio conclude l'esercitazione relativa ai modelli Sequence Clustering.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Se sono state completate tutte le sezioni dell' [esercitazione intermedia sul data mining &#40;Analysis Services-Data mining&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md), il passaggio successivo potrebbe essere quello di imparare a utilizzare le istruzioni DMX (Data Mining Extensions) per compilare modelli e generare stime. Per ulteriori informazioni, vedere [creazione ed esecuzione di query sui modelli di data mining con DMX: esercitazioni &#40;Analysis Services-&#41;di data mining ](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md).  
  
 Se si ha familiarità con i concetti relativi alla programmazione, è anche possibile utilizzare AMO (Analysis Management Objects) per gestire a livello di codice gli oggetti di data mining. Per altre informazioni, vedere [Classi di data mining AMO](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes).  
  
## <a name="see-also"></a>Vedi anche  
 [Esempi di query sul modello Sequence Clustering](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
