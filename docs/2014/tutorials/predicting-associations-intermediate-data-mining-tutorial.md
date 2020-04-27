---
title: Associazioni di stima (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9140c5f2-b340-45a6-9c27-d870d15aafea
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bee5ca4ded1b2fd5cbda0712cb766c825b9d0318
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62472846"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>Stima delle associazioni (Esercitazione intermedia sul data mining)
  Dopo avere elaborato i modelli, è possibile utilizzare le informazioni sulle associazioni archiviate nei modelli per creare stime. Nell'attività finale di questa lezione verrà illustrato come compilare query di stima rispetto nei modelli di associazione creati. In questa lezione si presuppone che l'utente abbia familiarità con l'utilizzo del generatore delle query di stima e desideri apprendere come compilare query di stima mediante modelli di associazione. Per ulteriori informazioni su come utilizzare Generatore di query di stima, vedere [interfacce di query di data mining](../../2014/analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="creating-a-singleton-prediction-query"></a>Creazione di una query di stima singleton  
 Le query di stima in un modello di associazione possono essere molto utili per:  
  
-   Consigliare articoli a un cliente, in base ad acquisti correlati o precedenti  
  
-   Trovare eventi correlati.  
  
-   Identificare relazioni nei set di transazioni.  
  
 Per compilare una query di stima, è innanzitutto necessario selezionare il modello di associazione che si desidera utilizzare, quindi specificare i dati di input. È possibile recuperare gli input da un'origine dati esterna, ad esempio un elenco di valori, oppure compilare una query singleton e fornire i valori.  
  
 Per questo scenario verranno dapprima create alcune query di stima singleton, per avere un'idea del funzionamento delle stime. Si creerà quindi una query per le stime batch che è possibile utilizzare per dare consigli a un cliente sulla base dei suoi acquisti correnti.  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>Per creare una query di stima basata su un modello di associazione  
  
1.  Fare clic sulla scheda **Stima modello** di data mining di progettazione modelli di data mining.  
  
2.  Nel riquadro **modello di data mining** fare clic su **Seleziona modello**. Se è già selezionato il modello corretto, ignorare questo passaggio e quello successivo.  
  
3.  Nella finestra di dialogo **Seleziona modello di data mining** espandere il nodo che rappresenta l' **associazione**della struttura di data mining e selezionare l' **associazione**del modello. Fare clic su **OK**.  
  
     Ai fini di questa esercitazione, è possibile ignorare il riquadro di input.  
  
4.  Nella griglia fare clic sulla cella vuota sotto **origine** e selezionare **funzione di stima.** Nella cella sotto **campo**selezionare `PredictAssociation`.  
  
     È anche possibile usare la funzione **Predict** per stimare le associazioni. In tal caso, assicurarsi di scegliere la versione della funzione **Predict** che accetta una colonna di tabella come argomento.  
  
5.  Nel riquadro **modello di data mining** selezionare la tabella `vAssocSeqLineItems`nidificata e trascinarla nella griglia alla casella **criteri/argomento** della `PredictAssociation` funzione.  
  
     Il trascinamento dei nomi di tabella e colonna consente di compilare istruzioni complesse senza errori di sintassi. Tuttavia, sostituisce il contenuto corrente della cella, che include altri argomenti facoltativi per la `PredictAssociation` funzione. Per visualizzare gli altri argomenti, è possibile aggiungere temporaneamente una seconda istanza della funzione alla griglia per riferimento.  
  
6.  Fare clic sulla casella **criteri/argomento** e digitare il testo seguente dopo il nome della tabella:`,3`  
  
     Il testo completo nella casella **criteri/argomento** dovrebbe essere il seguente:  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  Fare clic sul pulsante **risultati** nell'angolo superiore del generatore di query di stima.  
  
 I risultati previsti contengono una singola colonna con l' **espressione**di intestazione. La colonna **espressione** contiene una tabella nidificata con una singola colonna e le tre righe seguenti. Poiché non è stato specificato un valore di input, queste stime rappresentano le associazioni di prodotti più probabili per il modello nel suo complesso.  
  
|Modello|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 Successivamente, si utilizzerà il riquadro **input query singleton** per specificare un prodotto come input per la query e verranno visualizzati i prodotti più probabilmente associati a tale elemento.  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>Per creare una query di stima singleton con gli input della tabella nidificata  
  
1.  Fare clic sul pulsante **progettazione** nell'angolo della generatore di query di stima per tornare alla griglia di compilazione della query.  
  
2.  Scegliere **query singleton**dal menu **modello di data mining** .  
  
3.  Nella finestra di dialogo **modello di data mining** selezionare il modello **Association** .  
  
4.  Nella griglia fare clic sulla cella vuota sotto **origine** e selezionare **funzione di stima.** Nella cella sotto **campo**selezionare `PredictAssociation`.  
  
5.  Nel riquadro **modello di data mining** selezionare la tabella `vAssocSeqLineItems`nidificata e trascinarla nella griglia alla casella **criteri/argomento** della `PredictAssociation` funzione. Digitare `,3` dopo il nome della tabella nidificata come nella procedura precedente.  
  
6.  Nella finestra di dialogo **input query singleton** fare clic sulla casella **valore** accanto a **vAssoc Seq Line Items**, quindi fare clic sul pulsante **(...)** .  
  
7.  Nella finestra di dialogo **input tabella nidificata** selezionare `Touring Tire` nel riquadro **colonna chiave** , quindi fare clic su **Aggiungi**.  
  
8.  Fare clic sul pulsante **risultati** .  
  
 I risultati mostrano ora le stime relative ai prodotti che sono con la massima probabilità associati a Touring Tire.  
  
|Modello|  
|-----------|  
|Touring Tire Tube|  
|Sport-100|  
|Water Bottle|  
  
 Dall'esplorazione del modello si è già appreso tuttavia che Touring Tire Tube viene frequentemente acquistato insieme a Touring Tire. Si è tuttavia maggiormente interessati a individuare i prodotti che è possibile consigliare ai clienti che acquistano questi articoli congiuntamente. Si modificherà quindi la query in modo da stimare i prodotti correlati in base ai due articoli inclusi tra gli acquisti, aggiungendovi inoltre la probabilità per ogni prodotto stimato.  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>Per aggiungere input e probabilità alla query di stima singleton  
  
1.  Fare clic sul pulsante **progettazione** nell'angolo della generatore di query di stima per tornare alla griglia di compilazione della query.  
  
2.  Nella finestra di dialogo **input query singleton** fare clic sulla casella **valore** accanto a **vAssoc Seq Line Items**, quindi fare clic sul pulsante **(...)** .  
  
3.  Nel riquadro **colonna chiave** selezionare `Touring Tire`e quindi fare clic su **Aggiungi**.  
  
4.  Nella griglia fare clic sulla cella vuota sotto **origine** e selezionare **funzione di stima.** Nella cella sotto **campo**selezionare `PredictAssociation`.  
  
5.  Nel riquadro **modello di data mining** selezionare la tabella `vAssocSeqLineItems`nidificata e trascinarla nella griglia alla casella **criteri/argomento** della `PredictAssociation` funzione. Digitare `,3` dopo il nome della tabella nidificata come nella procedura precedente.  
  
6.  Nella finestra di dialogo **input tabella nidificata** selezionare `Touring Tire Tube` nel riquadro **colonna chiave** , quindi fare clic su **Aggiungi**.  
  
7.  Nella griglia, nella riga per la `PredictAssociation` funzione, fare clic sulla casella **criteri/argomento** e modificare gli argomenti per aggiungere l'argomento INCLUDE_STATISTICS.  
  
     Il testo completo nella casella **criteri/argomento** dovrebbe essere il seguente:  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  Fare clic sul pulsante **risultati** .  
  
 I risultati nella tabella nidificata mostrano ora le stime, insieme al supporto e alla probabilità. Per ulteriori informazioni su come interpretare questi valori, vedere il [contenuto del modello di data mining per i modelli di associazione &#40;Analysis Services-Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,291...|0,252...|  
|Water Bottle|2866|0,192...|0,175...|  
|Patch Kit|2113|0,142...|0,132|  
  
## <a name="working-with-results"></a>Utilizzo dei risultati  
 Quando nei risultati sono presenti molte tabelle nidificate, è possibile convertire i risultati in formato flat per semplificarne la visualizzazione. A tale scopo, è possibile modificare manualmente la query aggiungendovi la parola chiave `FLATTENED`.  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Per convertire in formato flat i set di righe nidificati in una query di stima  
  
1.  Fare clic sul pulsante **SQL** nell'angolo del generatore di query di stima.  
  
     La griglia viene sostituita da un riquadro aperto in cui è possibile visualizzare e modificare l'istruzione DMX creata dal generatore delle query di stima.  
  
2.  Dopo la parola chiave `SELECT` digitare `FLATTENED`.  
  
     Il testo completo della query dovrebbe risultare analogo al seguente:  
  
    ```  
    SELECT FLATTENED  
      PredictAssociation([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,3)  
    FROM  
      [Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Touring Tire' AS [Model]  
      UNION SELECT 'Touring Tire Tube' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
    ```  
  
3.  Fare clic sul pulsante **risultati** nell'angolo superiore del generatore di query di stima.  
  
 Si noti che dopo avere modificato manualmente una query, non sarà possibile tornare alla visualizzazione Progettazione senza perdere le modifiche apportate. Per salvare la query, è possibile copiare in un file di testo l'istruzione DMX creata manualmente. Tornando alla visualizzazione Progettazione, verrà ripristinata l'ultima versione della query valida in tale visualizzazione.  
  
## <a name="creating-multiple-predictions"></a>Creazione di più stime  
 Si supponga di voler conoscere le stime migliori per i singoli clienti in base agli acquisti passati. È possibile utilizzare dati esterni come input per la query di stima, ad esempio tabelle contenenti l'ID cliente e gli acquisti di prodotti più recenti. I requisiti prevedono che le tabelle di dati siano già definite come una vista origine dati di Analysis Services e che i dati di input contengano tabelle del case e nidificate analoghe a quelle utilizzate nel modello. Non è necessario che abbiano gli stessi nomi, ma la struttura deve essere simile. Ai fini di questa esercitazione, verranno utilizzate le tabelle originali sulle quali è stato eseguito il training del modello.  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>Per modificare il metodo di input per la query di stima  
  
1.  Nel menu **modello di data mining** selezionare di nuovo **query singleton** per cancellare il segno di spunta.  
  
2.  Verrà visualizzato un messaggio di errore per avvisare che la query singleton andrà persa. Fare clic su **Sì**.  
  
     Il nome della finestra di dialogo di input viene modificato in **Seleziona tabella**/e di input.  
  
 Poiché si è interessati alla creazione di una query di stima che fornisca l'ID cliente e un elenco di prodotti come input, si aggiungerà la tabella dei clienti come tabella del case e la tabella degli acquisti come tabella nidificata. Si aggiungeranno quindi funzioni di stima per creare consigli.  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Per creare una query di stima tramite input di tabelle nidificate  
  
1.  Nel riquadro Modello di data mining selezionare il modello Association Filtered.  
  
2.  Nella finestra di dialogo **Seleziona tabella/** e di input fare clic su **Seleziona tabella del case**.  
  
3.  Nella finestra di dialogo **Seleziona tabella** selezionare AdventureWorksDW2008 per **origine dati**. Nell'elenco **nome tabella/vista** selezionare vAssocSeqOrders e quindi fare clic su **OK**.  
  
     La tabella vAssocSeqOrders verrà aggiunta al riquadro.  
  
4.  Nella finestra di dialogo **Seleziona tabella/** e di input fare clic su **Seleziona tabella nidificata**.  
  
5.  Nella finestra di dialogo **Seleziona tabella** selezionare AdventureWorksDW2008 per **origine dati**. Nell'elenco **nome tabella/vista** selezionare vAssocSeqLineItems e quindi fare clic su **OK**.  
  
     La tabella vAssocSeqLineItems verrà aggiunta al riquadro.  
  
6.  Nella finestra di dialogo **Specifica join annidato** trascinare il campo OrderNumber dalla tabella del case e rilasciarlo sul campo OrderNumber nella tabella nidificata.  
  
     È anche possibile fare clic su **Aggiungi relazione** e creare la relazione selezionando le colonne da un elenco.  
  
7.  Nella finestra di dialogo **specifica relazione** verificare che i campi OrderNumber siano mappati correttamente, quindi fare clic su **OK**.  
  
8.  Fare clic su **OK** per chiudere la finestra di dialogo **Specifica join annidato** .  
  
     La tabella del case e la tabella nidificata verranno aggiornate nel riquadro di progettazione in modo da visualizzare i join che connettono le colonne dati esterne alle colonne del modello. Se le relazioni sono errate, è possibile fare clic con il pulsante destro del mouse sulla linea di join e scegliere **modifica connessioni** per modificare il mapping delle colonne. in alternativa, è possibile fare clic con il pulsante destro del mouse sulla linea di join e scegliere **Elimina** per rimuovere completamente la relazione.  
  
9. Aggiungere una nuova riga alla griglia. Per **origine**selezionare **tabella vAssocSeqOrders**. In **campo**selezionare CustomerKey.  
  
10. Aggiungere una nuova riga alla griglia. Per **origine**selezionare **tabella vAssocSeqOrders**. Per **campo**selezionare Region (area).  
  
11. Aggiungere una nuova riga alla griglia. Per **origine**selezionare **funzione di stima**e in **campo**selezionare `PredictAssociation`.  
  
12. Trascinare vAssocSeqLineItems nella casella **criteri/argomento** della `PredictAssociation` riga. Fare clic alla fine della casella **criteri/argomento** , quindi digitare il testo seguente:`INCLUDE_STATISTICS,3`  
  
     Il testo completo nella casella **criteri/argomento** deve essere:`[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. Fare clic sul pulsante **risultato** per visualizzare le stime per ogni cliente.  
  
 È possibile provare a creare una query di stima simile in più modelli, per vedere se l'applicazione di filtri modifica i risultati della stima. Per ulteriori informazioni sulla creazione di stime e altri tipi di query, vedere [esempi di query sul modello di associazione](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Contenuto del modello di data mining per i modelli di associazione &#40;Analysis Services-Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)   
 [Creare una query di stima utilizzando Generatore query di stima](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
