---
title: Test dell'accuratezza con i grafici di accuratezza (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 822d414b-4a39-473f-80c3-53476e30655a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d5311f08e9ec6b31fd0eabc1395baa31319eff64
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52412208"
---
# <a name="testing-accuracy-with-lift-charts-basic-data-mining-tutorial"></a>Test dell'accuratezza con i grafici di accuratezza (Esercitazione di base sul data mining)
  Nel **Mining grafico di accuratezza** scheda Progettazione modelli di Data Mining, è possibile calcolare come ognuno dei modelli di esegue le stime e confrontare i risultati di ogni modello direttamente con i risultati degli altri modelli. Questo metodo di confronto è noto come un *grafico di accuratezza*. In genere, l'accuratezza predittiva di un modello di data mining è misurata dall'accuratezza stessa del modello o dall'accuratezza della classificazione. Per questa esercitazione si utilizzerà solo il grafico di accuratezza.  
  
 In questo argomento verranno eseguite le attività seguenti:  
  
-   [Scegliere i dati di Input](#BKMK_InputData)  
  
-   [Configurare i parametri del grafico di accuratezza](#BKMK_Selecting)  
  
##  <a name="BKMK_InputData"></a> Scelta dei dati di Input  
 Il primo passaggio per verificare l'accuratezza dei modelli di data mining consiste nel selezionare l'origine dati che verrà utilizzata per il testing. Si testerà l'accuratezza dei modelli rispetto ai dati di testing, quindi li si utilizzerà con dati esterni.  
  
#### <a name="to-select-the-data-set"></a>Per selezionare il set di dati  
  
1.  Passare al **grafico di accuratezza Data Mining** Progettazione modelli di Data Mining nella scheda [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e selezionare il **selezione Input** scheda.  
  
2.  Nel **Seleziona set di dati da utilizzare per il grafico di accuratezza** casella di gruppo, selezionare **utilizzare test case della struttura di data mining**. Si tratta dei dati di testing che sono stati riservati al momento della creazione della struttura di data mining.  
  
     Per altre informazioni sulle altre opzioni, vedere [scegliere un tipo di grafico di accuratezza e impostare le opzioni del grafico](../../2014/analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md).  
  
##  <a name="BKMK_Selecting"></a> Impostazione parametri grafico di accuratezza  
 Per creare un grafico di accuratezza, è necessario definire tre elementi:  
  
-   I modelli da includere nel grafico di accuratezza  
  
-   L'attributo stimabile da misurare In alcuni modelli potrebbero essere presenti più destinazioni, ma ogni grafico può misurare un solo risultato alla volta.  
  
     Per utilizzare una colonna come le **nome colonna stimabile** in un grafico di accuratezza, le colonne devono avere il tipo di utilizzo `Predict` o `Predict Only`. Inoltre, il tipo di contenuto della colonna di destinazione deve essere `Discrete` o `Discretized`. In altre parole, non è possibile utilizzare grafici di accuratezza per misurare l'accuratezza su risultati numerici continui.  
  
-   Si desidera misurare l'accuratezza del modello generale, o l'accuratezza alla stima di un determinato valore (ad esempio [Bike Buyer] = "Sì")  
  
#### <a name="to-generate-the-lift-chart"></a>Per generare il grafico di accuratezza  
  
1.  Nel **selezione Input** scheda della finestra di progettazione modelli di Data Mining, in **selezionare le colonne modello di data mining stimabile da visualizzare nel grafico di accuratezza**, selezionare la casella di controllo **Sincronizza colonne stimabili e I valori**.  
  
2.  Nel **nome colonna stimabile** colonna, verificare che **Bike Buyer** è selezionato per ogni modello.  
  
3.  Nel **mostrare** colonna, selezionare i modelli.  
  
     Per impostazione predefinita, nella struttura di data mining sono selezionati tutti i modelli. È possibile decidere di non includere un modello. Tuttavia in questa esercitazione verranno lasciati selezionati tutti i modelli.  
  
4.  Nel **valore stima** colonna, selezionare **1**. Lo stesso valore viene inserito automaticamente per ciascun modello che ha la stessa colonna stimabile.  
  
5.  Selezionare il **grafico di accuratezza** scheda.  
  
     Quando si fa clic sulla scheda, viene eseguita una query di stima per ottenere le stime per i dati di test e i risultati vengono confrontati con valori noti. I risultati vengono tracciati sul grafico.  
  
     Se si specifica un risultato di destinazione specifico utilizzando il **valore stima** opzione, il grafico di accuratezza traccia i risultati di ipotesi casuali e i risultati di un modello ideale.  
  
    -   La riga relativa alle ipotesi casuali mostra l'accuratezza presentata dal modello senza l'utilizzo di dati informativi per il calcolo delle stime, ovvero una divisione 50-50 tra due risultati. Il grafico di accuratezza consente di visualizzare le migliori prestazioni registrate dal modello rispetto a un'ipotesi casuale.  
  
    -   La linea del modello ideale rappresenta il limite superiore di accuratezza. Mostra il massimo vantaggio che è possibile ottenere se le stime del modello fossero sempre accurate.  
  
     I modelli di data mining creati ricadranno in genere tra questi due estremi. Qualsiasi miglioramento dell'ipotesi casuale viene considerato *accuratezza*.  
  
6.  Utilizzare la legenda per individuare le linee colorate che rappresentano il modello ideale e il modello di ipotesi casuale.  
  
     Si noterà che il `TM_Decision_Tree` modello fornisce il maggiore livello di accuratezza, prestazioni superiori rispetto ai modelli sia il Clustering e Naive Bayes.  
  
 Per una spiegazione dettagliata di un grafico di accuratezza simile a quello creato in questa lezione, vedere [grafico di accuratezza &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md).  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Test di un modello filtrato &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Grafico di accuratezza &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [Scheda grafico di accuratezza &#40;visualizzazione Grafico accuratezza di Data Mining&#41;](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)  
  
  
