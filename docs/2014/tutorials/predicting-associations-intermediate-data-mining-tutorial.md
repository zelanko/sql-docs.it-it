---
title: Stima delle associazioni (esercitazione intermedia di Data Mining) | Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022362"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>Stima delle associazioni (Esercitazione intermedia sul data mining)
  Dopo avere elaborato i modelli, è possibile utilizzare le informazioni sulle associazioni archiviate nei modelli per creare stime. Nell'attività finale di questa lezione verrà illustrato come compilare query di stima rispetto nei modelli di associazione creati. In questa lezione si presuppone che l'utente abbia familiarità con l'utilizzo del generatore delle query di stima e desideri apprendere come compilare query di stima mediante modelli di associazione. Per altre informazioni su come usare generatore Query di stima, vedere [interfacce di Data Mining Query](../../2014/analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="creating-a-singleton-prediction-query"></a>Creazione di una query di stima singleton  
 Le query di stima in un modello di associazione possono essere molto utili per:  
  
-   Consigliare articoli a un cliente, in base ad acquisti correlati o precedenti  
  
-   Trovare eventi correlati.  
  
-   Identificare relazioni nei set di transazioni.  
  
 Per compilare una query di stima, è innanzitutto necessario selezionare il modello di associazione che si desidera utilizzare, quindi specificare i dati di input. È possibile recuperare gli input da un'origine dati esterna, ad esempio un elenco di valori, oppure compilare una query singleton e fornire i valori.  
  
 Per questo scenario verranno dapprima create alcune query di stima singleton, per avere un'idea del funzionamento delle stime. Si creerà quindi una query per le stime batch che è possibile utilizzare per dare consigli a un cliente sulla base dei suoi acquisti correnti.  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>Per creare una query di stima basata su un modello di associazione  
  
1.  Scegliere il **stima modello di Data Mining** scheda della finestra di progettazione modelli di Data Mining.  
  
2.  Nel **modello di Data Mining** riquadro, fare clic su **Seleziona modello**. Se è già selezionato il modello corretto, ignorare questo passaggio e quello successivo.  
  
3.  Nel **Seleziona modello di Data Mining** finestra di dialogo espandere il nodo che rappresenta la struttura di data mining **Association**e selezionare il modello **associazione**. Fare clic su **OK**.  
  
     Ai fini di questa esercitazione, è possibile ignorare il riquadro di input.  
  
4.  Nella griglia, fare clic sulla cella vuota sotto **origine** e selezionare **funzione di stima.** Nella cella sotto **campo**, selezionare `PredictAssociation`.  
  
     È anche possibile usare la **Predict** funzione per stimare le associazioni. Se è necessario assicurarsi di scegliere la versione del **Predict** funzione che accetta una colonna di tabella come argomento.  
  
5.  Nel **modello di Data Mining** riquadro, selezionare la tabella nidificata `vAssocSeqLineItems`e trascinarla nella griglia al **criteri/argomento** casella per il `PredictAssociation` (funzione).  
  
     Il trascinamento dei nomi di tabella e colonna consente di compilare istruzioni complesse senza errori di sintassi. Tuttavia, sostituisce il contenuto corrente della cella, che include altri argomenti facoltativi per il `PredictAssociation` (funzione). Per visualizzare gli altri argomenti, è possibile aggiungere temporaneamente una seconda istanza della funzione alla griglia per riferimento.  
  
6.  Scegliere il **criteri/argomento** finestra e digitare il testo seguente dopo il nome di tabella: `,3`  
  
     Il testo completo la **criteri/argomento** finestra dovrebbe essere come segue:  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  Scegliere il **risultati** pulsante nell'angolo superiore del generatore di Query di stima.  
  
 I risultati previsti contengono una singola colonna con l'intestazione **espressione**. Il **espressione** colonna contiene una tabella nidificata con una singola colonna e le tre righe seguenti. Poiché non è stato specificato un valore di input, queste stime rappresentano le associazioni di prodotti più probabili per il modello nel suo complesso.  
  
|Modello|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 Successivamente, si userà il **Input Query Singleton** riquadro per specificare un prodotto come input per la query e visualizzare i prodotti che più probabilmente associato a tale elemento.  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>Per creare una query di stima singleton con gli input della tabella nidificata  
  
1.  Scegliere il **progettazione** pulsante nell'angolo del generatore di Query di stima per tornare alla griglia di compilazione query.  
  
2.  Nel **modello di Data Mining** dal menu **Query Singleton**.  
  
3.  Nel **modello di Data Mining** finestra di dialogo, seleziona la **Association** modello.  
  
4.  Nella griglia, fare clic sulla cella vuota sotto **origine** e selezionare **funzione di stima.** Nella cella sotto **campo**, selezionare `PredictAssociation`.  
  
5.  Nel **modello di Data Mining** riquadro, selezionare la tabella nidificata `vAssocSeqLineItems`e trascinarla nella griglia al **criteri/argomento** casella per il `PredictAssociation` (funzione). Tipo `,3` dopo il nome della tabella nidificata Analogamente nella procedura precedente.  
  
6.  Nel **Input Query Singleton** nella finestra di dialogo fare clic sul **valore** casella accanto a **vAssoc Seq Line Items**e quindi fare clic su di **(...)**  pulsante.  
  
7.  Nel **Input tabella nidificata** finestra di dialogo `Touring Tire` nel **colonna Key** riquadro e quindi fare clic su **Aggiungi**.  
  
8.  Scegliere il **risultati** pulsante.  
  
 I risultati mostrano ora le stime relative ai prodotti che sono con la massima probabilità associati a Touring Tire.  
  
|Modello|  
|-----------|  
|Touring Tire Tube|  
|Sport-100|  
|Water Bottle|  
  
 Dall'esplorazione del modello si è già appreso tuttavia che Touring Tire Tube viene frequentemente acquistato insieme a Touring Tire. Si è tuttavia maggiormente interessati a individuare i prodotti che è possibile consigliare ai clienti che acquistano questi articoli congiuntamente. Si modificherà quindi la query in modo da stimare i prodotti correlati in base ai due articoli inclusi tra gli acquisti, aggiungendovi inoltre la probabilità per ogni prodotto stimato.  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>Per aggiungere input e probabilità alla query di stima singleton  
  
1.  Scegliere il **progettazione** pulsante nell'angolo del generatore di Query di stima per tornare alla griglia di compilazione query.  
  
2.  Nel **Input Query Singleton** nella finestra di dialogo fare clic sul **valore** casella accanto a **vAssoc Seq Line Items**e quindi fare clic su di **(...)**  pulsante.  
  
3.  Nel **la colonna chiave** riquadro, selezionare `Touring Tire`, quindi fare clic su **Add**.  
  
4.  Nella griglia, fare clic sulla cella vuota sotto **origine** e selezionare **funzione di stima.** Nella cella sotto **campo**, selezionare `PredictAssociation`.  
  
5.  Nel **modello di Data Mining** riquadro, selezionare la tabella nidificata `vAssocSeqLineItems`e trascinarla nella griglia al **criteri/argomento** casella per il `PredictAssociation` (funzione). Tipo `,3` dopo il nome della tabella nidificata Analogamente nella procedura precedente.  
  
6.  Nel **Input tabella nidificata** finestra di dialogo `Touring Tire Tube` nel **colonna Key** riquadro e quindi fare clic su **Aggiungi**.  
  
7.  Nella griglia, nella riga per il `PredictAssociation` funzione, fare clic sui **criteri/argomento** casella e modificare gli argomenti per aggiungere l'argomento INCLUDE_STATISTICS.  
  
     Il testo completo la **criteri/argomento** finestra dovrebbe essere come segue:  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  Scegliere il **risultati** pulsante.  
  
 I risultati nella tabella nidificata mostrano ora le stime, insieme al supporto e alla probabilità. Per altre informazioni su come interpretare questi valori, vedere [modello di contenuto di Data Mining per i modelli di associazione &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291...|0.252...|  
|Water Bottle|2866|0.192...|0.175...|  
|Patch Kit|2113|0.142...|0.132|  
  
## <a name="working-with-results"></a>Utilizzo dei risultati  
 Quando nei risultati sono presenti molte tabelle nidificate, è possibile convertire i risultati in formato flat per semplificarne la visualizzazione. A tale scopo, è possibile modificare manualmente la query aggiungendovi la parola chiave `FLATTENED`.  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Per convertire in formato flat i set di righe nidificati in una query di stima  
  
1.  Scegliere il **SQL** pulsante nell'angolo del generatore di Query di stima.  
  
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
  
3.  Scegliere il **risultati** pulsante nell'angolo superiore del generatore di Query di stima.  
  
 Si noti che dopo avere modificato manualmente una query, non sarà possibile tornare alla visualizzazione Progettazione senza perdere le modifiche apportate. Per salvare la query, è possibile copiare in un file di testo l'istruzione DMX creata manualmente. Tornando alla visualizzazione Progettazione, verrà ripristinata l'ultima versione della query valida in tale visualizzazione.  
  
## <a name="creating-multiple-predictions"></a>Creazione di più stime  
 Si supponga di voler conoscere le stime migliori per i singoli clienti in base agli acquisti passati. È possibile utilizzare dati esterni come input per la query di stima, ad esempio tabelle contenenti l'ID cliente e gli acquisti di prodotti più recenti. I requisiti prevedono che le tabelle di dati siano già definite come una vista origine dati di Analysis Services e che i dati di input contengano tabelle del case e nidificate analoghe a quelle utilizzate nel modello. Non è necessario che abbiano gli stessi nomi, ma la struttura deve essere simile. Ai fini di questa esercitazione, verranno utilizzate le tabelle originali sulle quali è stato eseguito il training del modello.  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>Per modificare il metodo di input per la query di stima  
  
1.  Nel **modello di Data Mining** dal menu **Query Singleton** anche in questo caso, per cancellare il segno di spunta.  
  
2.  Verrà visualizzato un messaggio di errore per avvisare che la query singleton andrà persa. Scegliere **Sì**.  
  
     Il nome della finestra di dialogo input diventerà **Seleziona tabelle di Input**.  
  
 Poiché si è interessati alla creazione di una query di stima che fornisca l'ID cliente e un elenco di prodotti come input, si aggiungerà la tabella dei clienti come tabella del case e la tabella degli acquisti come tabella nidificata. Si aggiungeranno quindi funzioni di stima per creare consigli.  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Per creare una query di stima tramite input di tabelle nidificate  
  
1.  Nel riquadro Modello di data mining selezionare il modello Association Filtered.  
  
2.  Nel **Seleziona tabelle di Input** finestra di dialogo, fare clic su **Seleziona tabella del Case**.  
  
3.  Nel **Seleziona tabella del** della finestra di dialogo per **Zdroj dat**, selezionare AdventureWorksDW2008. Nel **nome tabella/vista** elencare, selezionare vAssocSeqOrders e quindi fare clic su **OK**.  
  
     La tabella vAssocSeqOrders verrà aggiunta al riquadro.  
  
4.  Nel **Seleziona tabelle di Input** finestra di dialogo, fare clic su **Seleziona tabella nidificata**.  
  
5.  Nel **Seleziona tabella del** della finestra di dialogo per **Zdroj dat**, selezionare AdventureWorksDW2008. Nel **nome tabella/vista** elencare, selezionare vAssocSeqLineItems e quindi fare clic su **OK**.  
  
     La tabella vAssocSeqLineItems verrà aggiunta al riquadro.  
  
6.  Nel **specifica Join nidificato** nella finestra di dialogo, trascinare il OrderNumber campo dalla tabella del case e rilasciarlo sul campo OrderNumber nella tabella nidificata.  
  
     È anche possibile fare clic su **Aggiungi relazione** e creare la relazione selezionando le colonne da un elenco.  
  
7.  Nel **specificare la relazione** finestra di dialogo, verificare che sui campi OrderNumber venga eseguito il mapping correttamente e quindi fare clic su **OK**.  
  
8.  Fare clic su **OK** per chiudere la **specifica Join nidificato** nella finestra di dialogo.  
  
     La tabella del case e la tabella nidificata verranno aggiornate nel riquadro di progettazione in modo da visualizzare i join che connettono le colonne dati esterne alle colonne del modello. Se le relazioni sono errate, è possibile fare doppio clic la linea di join e scegliere **Modifica connessioni** per modificare la colonna di mapping, oppure fare clic sulla linea di join e selezionare **eliminare** per rimuovere il relazione completamente.  
  
9. Aggiungere una nuova riga alla griglia. Per la **origine**, selezionare **tabella vAssocSeqOrders**. Per la **campo**, selezionare CustomerKey.  
  
10. Aggiungere una nuova riga alla griglia. Per la **origine**, selezionare **tabella vAssocSeqOrders**. Per la **campo**, selezionare l'area.  
  
11. Aggiungere una nuova riga alla griglia. Per la **origine**, selezionare **funzione di stima**e per **campo**, selezionare `PredictAssociation`.  
  
12. Trascinare vAssocSeqLineItems nella **criteri/argomento** finestra di `PredictAssociation` riga. Fare clic su Fine il **criteri/argomento** casella e quindi digitare il testo seguente: `INCLUDE_STATISTICS,3`  
  
     Il testo completo la **criteri/argomento** casella deve essere: `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. Scegliere il **risultato** pulsante per visualizzare le stime per ogni cliente.  
  
 È possibile provare a creare una query di stima simile in più modelli, per vedere se l'applicazione di filtri modifica i risultati della stima. Per altre informazioni sulla creazione di stime e altri tipi di query, vedere [Association Model Query Examples](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto dei modelli di data mining per i modelli di associazione &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)   
 [Creare una query di stima usando Generatore di query di stima](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
