---
title: Verifica dell'accuratezza con i grafici di accuratezza (esercitazione di base sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 822d414b-4a39-473f-80c3-53476e30655a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 06cefcdac192b715fe843f842088456f769cdd24
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63042659"
---
# <a name="testing-accuracy-with-lift-charts-basic-data-mining-tutorial"></a>Test dell'accuratezza con i grafici di accuratezza (Esercitazione di base sul data mining)
  Nella scheda **Grafico accuratezza** modello di data mining di progettazione modelli di data mining è possibile calcolare il modo in cui ognuno dei modelli esegue stime e confrontare i risultati di ogni modello direttamente con i risultati degli altri modelli. Questo metodo di confronto viene definito *grafico di accuratezza*. In genere, l'accuratezza predittiva di un modello di data mining è misurata dall'accuratezza stessa del modello o dall'accuratezza della classificazione. Per questa esercitazione si utilizzerà solo il grafico di accuratezza.  
  
 In questo argomento verranno eseguite le attività seguenti:  
  
-   [Scegliere i dati di input](#BKMK_InputData)  
  
-   [Configurare i parametri del grafico di accuratezza](#BKMK_Selecting)  
  
##  <a name="BKMK_InputData"></a>Scelta dei dati di input  
 Il primo passaggio per verificare l'accuratezza dei modelli di data mining consiste nel selezionare l'origine dati che verrà utilizzata per il testing. Si testerà l'accuratezza dei modelli rispetto ai dati di testing, quindi li si utilizzerà con dati esterni.  
  
#### <a name="to-select-the-data-set"></a>Per selezionare il set di dati  
  
1.  Passare alla scheda **Grafico accuratezza** modello di data mining in progettazione [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] modelli di data mining in e selezionare la scheda **Selezione input** .  
  
2.  Nella casella **di gruppo Seleziona set di dati da utilizzare per il grafico di accuratezza** selezionare **utilizza test case della struttura di data mining**. Si tratta dei dati di testing che sono stati riservati al momento della creazione della struttura di data mining.  
  
     Per ulteriori informazioni sulle altre opzioni, vedere [scegliere un tipo di grafico di accuratezza e impostare le opzioni del grafico](../../2014/analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md).  
  
##  <a name="BKMK_Selecting"></a>Impostazione dei parametri del grafico di accuratezza  
 Per creare un grafico di accuratezza, è necessario definire tre elementi:  
  
-   I modelli da includere nel grafico di accuratezza  
  
-   L'attributo stimabile da misurare In alcuni modelli potrebbero essere presenti più destinazioni, ma ogni grafico può misurare un solo risultato alla volta.  
  
     Per utilizzare una colonna come **nome di colonna stimabile** in un grafico di accuratezza, è necessario che il tipo di `Predict` utilizzo `Predict Only`delle colonne sia o. Inoltre, il tipo di contenuto della colonna di destinazione deve essere `Discrete` o `Discretized`. In altre parole, non è possibile utilizzare grafici di accuratezza per misurare l'accuratezza su risultati numerici continui.  
  
-   Si desidera misurare l'accuratezza generale del modello o la relativa accuratezza nella stima di un particolare valore (ad esempio [Bike Buyer] =' Sì')  
  
#### <a name="to-generate-the-lift-chart"></a>Per generare il grafico di accuratezza  
  
1.  Nella scheda **Selezione input** di progettazione modelli di data mining, in **selezionare le colonne stimabili del modello di data mining da visualizzare nel grafico di accuratezza**, selezionare la casella di controllo **Sincronizza colonne e valori di stima**.  
  
2.  Nella colonna **nome colonna stimabile** verificare che **Bike Buyer** sia selezionato per ogni modello.  
  
3.  Nella colonna **Mostra** selezionare ogni modello.  
  
     Per impostazione predefinita, nella struttura di data mining sono selezionati tutti i modelli. È possibile decidere di non includere un modello. Tuttavia in questa esercitazione verranno lasciati selezionati tutti i modelli.  
  
4.  Nella colonna **valore stima** selezionare **1**. Lo stesso valore viene inserito automaticamente per ciascun modello che ha la stessa colonna stimabile.  
  
5.  Selezionare la scheda **grafico di accuratezza** .  
  
     Quando si fa clic sulla scheda, viene eseguita una query di stima per ottenere le stime per i dati di test e i risultati vengono confrontati con valori noti. I risultati vengono tracciati sul grafico.  
  
     Se è stato specificato un determinato risultato di destinazione utilizzando l'opzione **stima valore** , il grafico di accuratezza traccia i risultati delle ipotesi casuali e i risultati di un modello ideale.  
  
    -   La riga relativa alle ipotesi casuali mostra l'accuratezza presentata dal modello senza l'utilizzo di dati informativi per il calcolo delle stime, ovvero una divisione 50-50 tra due risultati. Il grafico di accuratezza consente di visualizzare le migliori prestazioni registrate dal modello rispetto a un'ipotesi casuale.  
  
    -   La linea del modello ideale rappresenta il limite superiore di accuratezza. Mostra il massimo vantaggio che è possibile ottenere se le stime del modello fossero sempre accurate.  
  
     I modelli di data mining creati ricadranno in genere tra questi due estremi. Qualsiasi miglioramento dall'ipotesi casuale viene considerato *Lift*.  
  
6.  Utilizzare la legenda per individuare le linee colorate che rappresentano il modello ideale e il modello di ipotesi casuale.  
  
     Si noterà che il `TM_Decision_Tree` modello fornisce il massimo livello di accuratezza, superando i modelli di clustering e Naive Bayes.  
  
 Per una spiegazione approfondita di un grafico di accuratezza simile a quello creato in questa lezione, vedere [grafico di accuratezza &#40;Analysis Services-&#41;di data mining ](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md).  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Test di un modello filtrato &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Grafico di accuratezza &#40;Analysis Services-&#41;di data mining](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [Scheda grafico di accuratezza &#40;vista Grafico accuratezza modello di data mining&#41;](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)  
  
  
