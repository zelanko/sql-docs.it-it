---
title: Test di un modello filtrato (esercitazione di base sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa4910b2849c4eb2dd04c6d0115c83683ee8bea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044096"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>Test di un modello filtrato (Esercitazione di base sul data mining)
  Ora che è stato stabilito che il `TM_Decision_Tree` modello è il più accurato, sarà possibile personalizzare il modello in base alle esigenze della campagna [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] di mailing diretto. In particolare, il reparto marketing desidera sapere se esistono differenze tra i clienti di sesso maschile e femminile. Queste informazioni possono aiutarli a decidere quali riviste utilizzare per la pubblicità e quali prodotti includere nei mailing.  
  
## <a name="using-filters"></a>Utilizzo dei filtri  
 I filtri consentono di creare facilmente modelli compilati in base a subset dei dati. Il filtro viene applicato solo al modello e non modifica l'origine dati sottostante.  
  
 In questa lezione verrà creato un modello filtrato in base al genere per determinare le caratteristiche che influiscono maggiormente sul comportamento di acquisto di persone di sesso maschile e femminile.  
  
 Prima di tutto si effettuerà una copia `TM_Decision_Tree` del modello.  
  
#### <a name="to-copy-the-decision-tree-model"></a>Per copiare il modello Decision Trees  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]Esplora soluzioni selezionare **BasicDataMining**.  
  
2.  Fare clic sulla scheda **Modelli di data mining** .  
  
3.  Fare clic con `TM_Decision_Tree` il pulsante destro del mouse sul modello e scegliere **nuovo modello di data mining.**  
  
4.  Nel campo **nome modello** Digitare `TM_Decision_Tree_Male`.  
  
5.  Fare clic su **OK**.  
  
 Creare quindi un filtro per selezionare i clienti per il modello in base al sesso.  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>Per creare un filtro di case su un modello di data mining  
  
1.  Per aprire il menu `TM_Decision_Tree_Male` di scelta rapida, fare clic con il pulsante destro del mouse sul modello.  
  
     -- o --  
  
     Selezionare il modello. Scegliere **Imposta filtro modello** dal menu **Modello di data mining**.  
  
2.  Nella finestra di dialogo **Filtro modello** fare clic sulla riga superiore nella griglia della casella di testo **Colonna struttura di data mining** .  
  
     Nell'elenco a discesa verranno visualizzati solo i nomi delle colonne della tabella.  
  
3.  Nella casella di testo colonna struttura di data mining selezionare **Gender**.  
  
     L'icona a sinistra della casella di testo cambierà per indicare che l'elemento selezionato è una tabella o una colonna.  
  
4.  Fare clic sulla casella di testo **operatore** e selezionare l'operatore di uguaglianza (=) nell'elenco.  
  
5.  Fare clic sulla casella di testo **valore** e digitare **M**.  
  
6.  Fare clic sulla riga successiva nella griglia.  
  
7.  Fare clic su **OK** per chiudere la finestra di dialogo **filtro modello** .  
  
     Il filtro viene visualizzato nella finestra **Proprietà** . In alternativa, è possibile avviare la finestra di dialogo **filtro modello** dalla finestra **Proprietà** .  
  
8.  Ripetere i passaggi precedenti, ma questa volta denominare `TM_Decision_Tree_Female` il modello e digitare **F** nella casella di testo **valore** .  
  
## <a name="process-the-filtered-models"></a>Elaborazione dei modelli filtrati  
 Per utilizzare i modelli, è innanzitutto necessario distribuirli ed elaborarli. Per ulteriori informazioni sull'elaborazione dei modelli, vedere [elaborazione di modelli nella struttura Targeted mailing &#40;esercitazione di base sul Data Mining&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md).  
  
#### <a name="to-process-the-filtered-model"></a>Per elaborare i modello filtrati  
  
1.  Fare clic con il `TM_Decision_Tree_Male` pulsante destro del mouse sul modello e scegliere **Elabora struttura di data mining e tutti i modelli**  
  
2.  Fare clic su **Esegui** per elaborare i nuovi modelli.  
  
3.  Al termine dell'elaborazione, fare clic su **Chiudi** in entrambe le finestre di elaborazione.  
  
     Sono ora disponibili due nuovi modelli nella scheda **modelli di data mining** .  
  
## <a name="evaluate-the-results"></a>Valutazione dei risultati  
 Visualizzare i risultati e stimare l'accuratezza dei modelli filtrati seguendo gli stessi passaggi effettuati per i tre modelli precedenti. Per altre informazioni, vedere:  
  
 [Esplorazione del modello Decision Trees &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [Test dell'accuratezza con i grafici di accuratezza &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>Per esplorare i modelli filtrati  
  
1.  Selezionare la scheda **Visualizzatore modello di data mining** in Progettazione modelli di **data mining**.  
  
2.  Nella casella modello di data mining selezionare `TM_Decision_Tree_Male`.  
  
3.  Diapositiva **Mostra livello** a `3`.  
  
4.  Modificare il **** valore di sfondo `1`in.  
  
5.  Posizionare il cursore sul nodo con l'etichetta **tutti** per visualizzare il numero di acquirenti di biciclette rispetto agli acquirenti non bike.  
  
6.  Ripetere i passaggi 1-5 `TM_Decision_Tree_Female`per.  
  
7.  Esplorare i risultati per `TM_Decision_Tree` e i modelli filtrati per sesso. Dal confronto fra tutti gli acquirenti di biciclette risulta che gli acquirenti di biciclette di sesso maschile e femminile condividono alcune caratteristiche con gli acquirenti di biciclette non filtrati, ma con alcune differenze interessanti. Si tratta di informazioni utili [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] che possono essere usate per sviluppare la campagna di marketing.  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>Per testare l'accuratezza dei modelli filtrati  
  
1.  Passare alla scheda **Grafico accuratezza** modello di data mining in progettazione [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] modelli di data mining in e selezionare la scheda **Selezione input** .  
  
2.  Nella casella **di gruppo Seleziona set di dati da utilizzare per il grafico di accuratezza** selezionare **utilizza test case della struttura di data mining**.  
  
3.  Nella scheda **Selezione input** di progettazione modelli di data mining, in **selezionare le colonne stimabili del modello di data mining da visualizzare nel grafico di accuratezza**, selezionare la casella di controllo **Sincronizza colonne e valori di stima**.  
  
4.  Nella colonna **nome colonna stimabile** verificare che **Bike Buyer** sia selezionato per ogni modello.  
  
5.  Nella colonna **Mostra** selezionare ogni modello.  
  
6.  Nella colonna **stima valore** selezionare `1`.  
  
7.  Selezionare la scheda **grafico di accuratezza** per visualizzare il grafico di accuratezza.  
  
     Si noterà ora che tutti e tre i modelli Decision Trees offrono un livello di accuratezza considerevole rispetto al modello di ipotesi casuale e prestazioni superiori rispetto ai modelli di clustering e Naive Bayes.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per ulteriori informazioni sui filtri, vedere [filtri per i modelli di data mining &#40;Analysis Services-&#41;di data mining ](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Per un esempio di applicazione di filtri alle tabelle nidificate, vedere [esercitazione intermedia sul data mining &#40;Analysis Services-&#41;di data mining ](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md).  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Test dell'accuratezza con i grafici di accuratezza &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 6: creazione e utilizzo di stime &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione intermedia sul data mining &#40;Analysis Services-&#41;di data mining](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Attività e procedure relative al modello di data mining](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Eliminare un filtro da un modello di data mining](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [Filtri per i modelli di data mining &#40;Analysis Services-&#41;di data mining](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
