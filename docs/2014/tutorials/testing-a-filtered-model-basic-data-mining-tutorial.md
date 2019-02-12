---
title: Test di un modello filtrato (esercitazione di base di Data Mining) | Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011142"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>Test di un modello filtrato (Esercitazione di base sul data mining)
  Ora che è stato possibile determinare che il `TM_Decision_Tree` modello è il più accurato, sarà necessario personalizzare il modello per meglio soddisfare le esigenze del [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] campagna di mailing. In particolare, il reparto marketing desidera sapere se esistono differenze tra i clienti di sesso maschile e femminile. Le informazioni possono aiutarli a decidere quali riviste utilizzare per la pubblicità e quali prodotti includere nei mailing.  
  
## <a name="using-filters"></a>Utilizzo dei filtri  
 I filtri consentono di creare facilmente modelli compilati in base a subset dei dati. Il filtro viene applicato solo al modello e non modifica l'origine dati sottostante.  
  
 In questa lezione verrà creato un modello filtrato in base al genere per determinare le caratteristiche che influiscono maggiormente sul comportamento di acquisto di persone di sesso maschile e femminile.  
  
 Prima di tutto si apporterà una copia del `TM_Decision_Tree` modello.  
  
#### <a name="to-copy-the-decision-tree-model"></a>Per copiare il modello Decision Trees  
  
1.  Nelle [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], in Esplora soluzioni, scegliere **BasicDataMining**.  
  
2.  Fare clic sulla scheda **Modelli di data mining** .  
  
3.  Fare clic il `TM_Decision_Tree` del modello e selezionare **nuovo modello di Data Mining.**  
  
4.  Nel **nome modello** digitare `TM_Decision_Tree_Male`.  
  
5.  Fare clic su **OK**.  
  
 Creare quindi un filtro per selezionare i clienti per il modello in base al sesso.  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>Per creare un filtro di case su un modello di data mining  
  
1.  Fare doppio clic il `TM_Decision_Tree_Male` modello di data mining per aprire il menu di scelta rapida.  
  
     -oppure-  
  
     Selezionare il modello. Scegliere **Imposta filtro modello** dal menu **Modello di data mining**.  
  
2.  Nella finestra di dialogo **Filtro modello** fare clic sulla riga superiore nella griglia della casella di testo **Colonna struttura di data mining** .  
  
     Nell'elenco a discesa verranno visualizzati solo i nomi delle colonne della tabella.  
  
3.  Nella casella di testo colonna struttura di Data Mining, selezionare **Gender**.  
  
     L'icona a sinistra della casella di testo cambierà per indicare che l'elemento selezionato è una tabella o una colonna.  
  
4.  Scegliere il **operatore** casella di testo e selezionare l'operatore di uguaglianza (=) dall'elenco.  
  
5.  Scegliere il **valore** casella di testo e digitare **M**.  
  
6.  Fare clic sulla riga successiva nella griglia.  
  
7.  Fare clic su **OK** per chiudere la **filtro modello** nella finestra di dialogo.  
  
     Il filtro viene visualizzato nei **proprietà** finestra. In alternativa, è possibile avviare il **filtro modello** della finestra di dialogo il **proprietà** finestra.  
  
8.  Ripetere i passaggi precedenti, ma questa volta il modello di nome `TM_Decision_Tree_Female` e digitare **F** nel **valore** casella di testo.  
  
## <a name="process-the-filtered-models"></a>Elaborazione dei modelli filtrati  
 Per utilizzare i modelli, è innanzitutto necessario distribuirli ed elaborarli. Per altre informazioni sull'elaborazione dei modelli, vedere [elaborazione di modelli nella struttura di Mailing destinata &#40;Basic Data Mining Tutorial&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md).  
  
#### <a name="to-process-the-filtered-model"></a>Per elaborare i modello filtrati  
  
1.  Fare doppio clic il `TM_Decision_Tree_Male` del modello e selezionare **Elabora struttura di Data Mining e tutti i modelli**s  
  
2.  Fare clic su **eseguiti** per elaborare i nuovi modelli.  
  
3.  Al termine dell'elaborazione, fare clic su **Chiudi** in entrambe le finestre di elaborazione.  
  
     Sono ora visualizzati due nuovi modelli le **modelli di Data Mining** scheda.  
  
## <a name="evaluate-the-results"></a>Valutazione dei risultati  
 Visualizzare i risultati e stimare l'accuratezza dei modelli filtrati seguendo gli stessi passaggi effettuati per i tre modelli precedenti. Per altre informazioni, vedere:  
  
 [Esplorazione del modello di albero delle decisioni &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [Test dell'accuratezza con i grafici di accuratezza &#40;Esercitazione di base sul data mining&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>Per esplorare i modelli filtrati  
  
1.  Selezionare il **visualizzatore modello di Data Mining** scheda **progettazione Data Mining**.  
  
2.  Nella casella di modello di Data Mining, selezionare `TM_Decision_Tree_Male`.  
  
3.  Diapositiva **Mostra il livello** a `3`.  
  
4.  Modifica il **sfondo** valore `1`.  
  
5.  Posizionare il cursore sul nodo con l'etichetta **tutti** per visualizzare il numero di acquirenti di biciclette rispetto a non-bike Buyer.  
  
6.  Ripetere i passaggi da 1 a 5 per `TM_Decision_Tree_Female`.  
  
7.  Esplorare i risultati per il `TM_Decision_Tree` e i modelli filtrati in base al sesso. Dal confronto fra tutti gli acquirenti di biciclette risulta che gli acquirenti di biciclette di sesso maschile e femminile condividono alcune caratteristiche con gli acquirenti di biciclette non filtrati, ma con alcune differenze interessanti. Si tratta di informazioni utili che [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] possono usare per sviluppare la campagna di marketing.  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>Per testare l'accuratezza dei modelli filtrati  
  
1.  Passare al **grafico di accuratezza Data Mining** Progettazione modelli di Data Mining nella scheda [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e selezionare il **selezione Input** scheda.  
  
2.  Nel **Seleziona set di dati da utilizzare per il grafico di accuratezza** casella di gruppo, selezionare **utilizzare test case della struttura di data mining**.  
  
3.  Nel **selezione Input** scheda della finestra di progettazione modelli di Data Mining, in **selezionare le colonne modello di data mining stimabile da visualizzare nel grafico di accuratezza**, selezionare la casella di controllo **Sincronizza colonne stimabili e I valori**.  
  
4.  Nel **nome colonna stimabile** colonna, verificare che **Bike Buyer** è selezionato per ogni modello.  
  
5.  Nel **mostrare** colonna, selezionare i modelli.  
  
6.  Nel **valore stima** colonna, selezionare `1`.  
  
7.  Selezionare il **grafico di accuratezza** pressione di tab per visualizzare il grafico di accuratezza.  
  
     Si noterà ora che tutti e tre i modelli Decision Trees offrono un livello di accuratezza considerevole rispetto al modello di ipotesi casuale e prestazioni superiori rispetto ai modelli di clustering e Naive Bayes.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni sui filtri, vedere [i filtri per i modelli di Data Mining &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Per un esempio di come applicare filtri a tabelle nidificate, vedere [esercitazione intermedia sul Data Mining dei dati &#40;Analysis Services - Data Mining&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md).  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Test dell'accuratezza con i grafici di accuratezza &#40;Esercitazione di base sul data mining&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 6: Creazione e utilizzo di stime &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazione intermedia sul Data Mining &#40;Analysis Services - Data Mining&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Attività e procedure relative al modello di data mining](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Eliminare un filtro da un modello di Data Mining](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [Filtri per i modelli di data mining &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
