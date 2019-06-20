---
title: Creazione di stime su un modello Sequence Clustering (esercitazione intermedia di Data Mining) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63217746"
---
# <a name="creating-predictions-on-a-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Creazione di stime su un modello Sequence Clustering (Esercitazione intermedia sul data mining)
  Dopo aver compreso il modello sequence clustering esplorandolo nel visualizzatore, è possibile creare query di stima utilizzando Generatore Query di stima nel **stima modello di Data Mining** scheda della finestra di progettazione modelli di Data Mining. Per creare una stima, occorre selezionare innanzitutto il modello Sequence Clustering, quindi i dati di input. Per gli input, è possibile utilizzare un'origine dati esterna o compilare una query singleton e fornire valori in una finestra di dialogo.  
  
 In questa lezione si presuppone che l'utente abbia già familiarità con l'utilizzo del generatore delle query di stima e desideri apprendere come compilare query specifiche per un modello Sequence Clustering. Per informazioni generali su come usare generatore Query di stima, vedere [nuove interfacce Query Data Mining](../../2014/analysis-services/data-mining/data-mining-query-tools.md) o nella sezione dell'esercitazione base sul Data Mining [creazione di stime &#40;Basic Data Mining Tutorial&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md).  
  
## <a name="creating-predictions-on-the-regional-model"></a>Creazione di stime sul modello regionale  
 Per questo scenario verranno dapprima create alcune query di stima singleton, per avere un'idea di come le stime potrebbero variare a seconda dell'area.  
  
#### <a name="to-create-a-singleton-query-on-a-sequence-clustering-model"></a>Per creare una query singleton in un modello Sequence Clustering  
  
1.  Scegliere il **stima modello di Data Mining** scheda della finestra di progettazione modelli di Data Mining.  
  
2.  Nel **modello di Data Mining** colonna dal menu **Query Singleton**.  
  
     Il **modello di Data Mining** riquadro e **Input Query Singleton** riquadro visualizzato.  
  
3.  Nel **modello di Data Mining** riquadro, fare clic su **Seleziona modello**. Se il modello Sequence Clustering è già stato selezionato, ignorare questo passaggio.  
  
     Il **modello di Data Mining selezionare** verrà visualizzata la finestra di dialogo.  
  
4.  Espandere il nodo che rappresenta la struttura di data mining **Sequence Clustering with Region**, quindi selezionare il modello **Sequence Clustering with Region**. Fare clic su **OK**. Per il momento, ignorare il riquadro di input. Gli input verranno specificati dopo avere configurato le funzioni di stima.  
  
5.  Nella griglia, fare clic sulla cella vuota sotto **origine** e selezionare **funzione di stima.** Nella cella sotto **campo**, selezionare **PredictSequence**.  
  
    > [!NOTE]  
    >  È anche possibile usare la **Predict** (funzione). Se è necessario assicurarsi di scegliere la versione del **Predict** funzione che accetta una colonna di tabella come argomento...  
  
6.  Nel **modello di Data Mining** riquadro, selezionare la tabella nidificata `v Assoc Seq Line Items`e trascinarla nella griglia, al **criteri/argomento** casella per i **PredictSequence** (funzione).  
  
     Il trascinamento dei nomi di tabella e colonna consente di compilare istruzioni complesse senza errori di sintassi. Tuttavia, sostituisce il contenuto corrente della cella, che include altri argomenti facoltativi per il **PredictSequence** (funzione). Per visualizzare gli altri argomenti, è possibile aggiungere temporaneamente una seconda istanza della funzione alla griglia per riferimento.  
  
7.  Scegliere il **risultato** pulsante nell'angolo superiore del generatore di Query di stima.  
  
 I risultati previsti contengono una singola colonna con l'intestazione **espressione**. Il **espressione** colonna contiene una tabella nidificata con tre colonne come indicato di seguito:  
  
|$SEQUENCE|Line Number|Modello|  
|---------------|-----------------|-----------|  
|1||Mountain-200|  
  
 Che cosa indicano questi risultati? Si tenga presente che non è stato specificato alcun input. La stima pertanto viene eseguita rispetto all'intera popolazione dei case e Analysis Services restituisce la stima più probabile a livello complessivo.  
  
### <a name="adding-inputs-to-a-singleton-prediction-query"></a>Aggiunta di input a una query di stima singleton  
 Finora non è stato specificato alcun input. Nell'attività successiva, si userà il **Input Query Singleton** riquadro specificare alcuni input per la query. Innanzitutto, si utilizzerà [Region] come input per il modello Sequence Clustering regionale, per determinare se le sequenze stimate sono le stesse per tutte le aree. Verrà quindi descritto come modificare la query per aggiungere la probabilità per ogni stima e convertire i risultati in formato flat per renderne più semplice la visualizzazione.  
  
##### <a name="to-generate-predictions-for-a-specific-customer-group"></a>Per generare stime per uno specifico gruppo di clienti  
  
1.  Scegliere il **progettazione** pulsante nell'angolo superiore sinistro del generatore di Query di stima per tornare alla griglia di compilazione query.  
  
2.  Nel **Input Query Singleton** finestra di dialogo, fare clic sul **valore** casella per `Region`e selezionare **Europa**.  
  
3.  Scegliere il **risultato** pulsante per visualizzare le stime per i clienti in Europa.  
  
4.  Scegliere il **progettazione** pulsante nell'angolo superiore sinistro del generatore di Query di stima per tornare alla griglia di compilazione query.  
  
5.  Nel **Input Query Singleton** finestra di dialogo, fare clic sul **valore** casella per `Region`e selezionare **America del Nord**.  
  
6.  Scegliere il **risultato** pulsante per visualizzare le stime per i clienti in America del Nord.  
  
### <a name="adding-probabilities-by-using-a-custom-expression"></a>Aggiunta di probabilità tramite un'espressione personalizzata  
 Restituire la probabilità per ogni stima è leggermente più complicato, perché la probabilità è un attributo della stima e viene restituita come una tabella nidificata. Se si ha familiarità con DMX (Data Mining Extensions), è possibile modificare facilmente la query per aggiungere un'istruzione sub-SELECT sulla tabella nidificata. Tuttavia, è anche possibile creare un'istruzione sub-SELECT nel generatore delle query di stima aggiungendo un'espressione personalizzata.  
  
##### <a name="to-output-probabilities-for-a-predicted-sequence-by-using-a-custom-expression"></a>Per restituire le probabilità per una sequenza stimata tramite un'espressione personalizzata  
  
1.  Scegliere il **progettazione** pulsante nell'angolo superiore sinistro del generatore di Query di stima per tornare alla griglia di compilazione query.  
  
2.  Nella griglia sotto **origine**, fare clic su una nuova riga e selezionare **espressione personalizzata**.  
  
3.  Lasciare la casella sotto **campo** vuoto.  
  
4.  Per la **Alias**, tipo `t`.  
  
5.  Nel **criteri/argomento** , digitare l'istruzione Sub-select completa come mostrato nell'esempio di codice seguente. Assicurarsi di includere le parentesi iniziale e finale.  
  
    ```  
    (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))  
    ```  
  
6.  Scegliere il **risultato** pulsante per visualizzare le stime per i clienti in Europa.  
  
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
  
1.  Scegliere il **Query** pulsante nell'angolo del generatore di Query di stima.  
  
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
  
3.  Scegliere il **risultati** pulsante nell'angolo superiore del generatore di Query di stima.  
  
 Dopo avere modificato manualmente una query, non sarà possibile tornare alla visualizzazione della struttura senza perdere le modifiche apportate. È tuttavia possibile salvare l'istruzione DMX creata manualmente in un file di testo, quindi tornare alla visualizzazione della struttura. Eseguendo tale operazione, verrà ripristinata l'ultima versione della query valida nella visualizzazione della struttura.  
  
## <a name="creating-predictions-on-the-related-model"></a>Creazione di stime sul modello correlato  
 Negli esempi precedenti è stata utilizzata una colonna della tabella del case, Region, come input per la query di stima singleton perché si era interessati a sapere se il modello aveva individuato eventuali differenze tra le aree. Tuttavia, dopo avere esplorato il modello, si è deciso che le differenze non sono abbastanza marcate da giustificare una personalizzazione dei consigli sui prodotti in base all'area. Ciò che si è realmente interessati a stimare sono gli articoli che i clienti selezionano. Nelle query che seguono, pertanto, si utilizzerà il modello Sequence Clustering che non include Region per generare consigli per tutti i clienti.  
  
### <a name="using-nested-table-columns-as-input"></a>Utilizzo di colonne di tabelle nidificate come input  
 Innanzitutto verrà creata una query di stima singleton che accetta un solo articolo come input e restituisce l'articolo successivo più probabile. Per ottenere una stima di questo tipo, è necessario utilizzare una colonna di tabella nidificata come valore di input. Questo avviene perché l'attributo stimato, Model, fa parte di una tabella nidificata. Analysis Services fornisce le **Input tabella nidificata** per semplificare la creazione di query di stima nella finestra di dialogo attributi di tabelle nidificate tramite il generatore di Query di stima.  
  
##### <a name="to-use-a-nested-table-as-input-to-a-prediction"></a>Per utilizzare una tabella nidificata come input per una stima  
  
1.  Scegliere il **progettazione** pulsante nell'angolo superiore sinistro del generatore di Query di stima per tornare alla griglia di compilazione query.  
  
2.  Nel **Input Query Singleton** finestra di dialogo, fare clic sul **valore** casella per `Region`e selezionare la riga vuota per cancellare l'input per questo campo.  
  
3.  Nel **Input Query Singleton** finestra di dialogo, fare clic sul **valore** casella per `vAssocSeqLineItems`e quindi fare clic sul pulsante (...).  
  
4.  Nel **Input tabella nidificata** finestra di dialogo, fare clic su **Add**.  
  
5.  Nella nuova riga, fare clic sulla casella sotto `Model`e selezionare Touring Tire dall'elenco. Fare clic su **OK**.  
  
6.  Scegliere il **risultato** pulsante per visualizzare le stime.  
  
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
  
1.  Nel **modello di Data Mining** riquadro, selezionare il modello Sequence Clustering, se non è già selezionato.  
  
2.  Nel **Seleziona tabelle di Input** finestra di dialogo, fare clic su **Seleziona tabella del Case**.  
  
3.  Nel **Seleziona tabella** nella finestra di dialogo per l'origine dati, selezionare Orders. Nel **nome tabella/vista** elencare, selezionare vAssocSeqOrders e quindi fare clic su **OK**.  
  
4.  Nel **Seleziona tabelle di Input** finestra di dialogo, fare clic su **Seleziona tabella nidificata**.  
  
5.  Nel **Seleziona tabella del** della finestra di dialogo per **Zdroj dat**, selezionare Orders. Nel **nome tabella/vista** elencare, selezionare vAssocSeqLineItems e quindi fare clic su **OK**.  
  
     Analysis Services tenterà di rilevare le relazioni e di crearle automaticamente se i tipi di dati corrispondono e i nomi delle colonne sono simili. Se le relazioni create sono errate, è possibile fare doppio clic la linea di join e scegliere **Modifica connessioni** per modificare la colonna di mapping, oppure fare clic sulla linea di join e selezionare **eliminare** a rimuovere completamente la relazione. In questo caso, poiché le tabelle erano già unite in join nella vista origine dati, tali relazioni vengono aggiunte automaticamente al riquadro di progettazione.  
  
6.  Aggiungere una nuova riga alla griglia. Per la **origine**, selezionare vAssocSeqOrders e per **campo**, selezionare CustomerKey.  
  
7.  Aggiungere una nuova riga alla griglia. Per la **origine**, selezionare **funzione di stima**e per **campo**, selezionare **PredictSequence**.  
  
8.  Trascinare vAssocSeqLineItems nella **criteri/argomento** casella. Fare clic su Fine il **criteri/argomento** e quindi digitare gli argomenti seguenti: `2`.  
  
     Il testo completo la **criteri/argomento** casella deve essere: `[Sequence Clustering].[v Assoc Seq Line Items],2`  
  
9. Scegliere il **risultato** pulsante per visualizzare le stime per ogni cliente.  
  
 Questo passaggio conclude l'esercitazione relativa ai modelli Sequence Clustering.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Se si sono concluse tutte le sezioni di [esercitazione intermedia sul Data Mining dei dati &#40;Analysis Services - Data Mining&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md), il passaggio successivo potrebbe essere imparare a utilizzare le istruzioni di Data Mining Extensions (DMX) per compilare modelli e generare stime. Per altre informazioni, vedere [creazione e l'esecuzione di query modelli di Data Mining con DMX: Esercitazioni su &#40;Analysis Services - Data Mining&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md).  
  
 Se si ha familiarità con i concetti relativi alla programmazione, è anche possibile utilizzare AMO (Analysis Management Objects) per gestire a livello di codice gli oggetti di data mining. Per altre informazioni, vedere [Classi di data mining AMO](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes).  
  
## <a name="see-also"></a>Vedere anche  
 [Sequence Clustering Model Query Examples](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Contenuto dei modelli di data mining per i modelli Sequence Clustering &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
