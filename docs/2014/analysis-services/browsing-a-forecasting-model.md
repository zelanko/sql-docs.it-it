---
title: Esplorazione di un modello di previsione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- forecasting [data mining]
- mining models, viewing
- mining model, time series
- time series [data mining]
ms.assetid: ad35a528-1949-4048-8678-3b9760c1c88c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5176d4e40f0f99810a14ad5ce4298e3a7167d770
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640298"
---
# <a name="browsing-a-forecasting-model"></a>Esplorazione di un modello di previsione
  Quando si apre un modello di previsione utilizzando **esplorare**, il modello viene visualizzato in un visualizzatore interattivo, simile al visualizzatore modello time series in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Il visualizzatore consente di esplorare le tendenze, confrontare le serie, creare stime e ottenere informazioni sul modello e sui dati sottostanti.  
  
##  <a name="bkmk_Top"></a> Esplorare il modello  
 Il **esplorare** visualizzatore per i modelli di previsione fornisce una visualizzazione del grafico che mostra le tendenze nel tempo e consente di creare stime e una visualizzazione del modello che rappresenta la serie temporale come albero delle decisioni o albero di regressione.  
  
-   [Visualizzazione grafico](#bkmk_charts)  
  
-   [Visualizzazione del modello](#bkmk_Model)  
  
 Per provare un modello di previsione, è possibile usare i dati di esempio nella scheda previsione della cartella di lavoro di dati di esempio e compilare un modello di serie ora utilizzando il [prevedere la procedura guidata &#40;aggiuntivi di Data Mining per Excel&#41; ](forecast-wizard-data-mining-add-ins-for-excel.md) nel  **Data Mining** della barra multifunzione, oppure [previsione &#40;strumenti di analisi tabelle per Excel&#41; ](forecast-table-analysis-tools-for-excel.md) nel **Analizza** della barra multifunzione.  
  
###  <a name="bkmk_charts"></a> Grafico  
 Il **grafico** scheda viene visualizzata la tendenza nella serie di dati nel corso del tempo, insieme ai valori stimati. L'asse verticale del grafico rappresenta i valori della serie, mentre l'asse orizzontale rappresenta il tempo.  
  
##### <a name="explore-the-forecasting-chart"></a>Esplorare il grafico di previsione  
  
1.  Questo modello contiene più serie temporali, ma per semplificare il grafico, è possibile visualizzare una singola serie o solo alcune serie correlate.  
  
     ![stime cronologiche in un modello di previsione](media/dm13-forecast-chart-historicpredictions.gif "stime cronologiche in un modello di previsione")  
  
     Utilizzare le caselle di controllo per selezionare la previsione solo per l'America del nord e solo per l'importo delle vendite.  
  
2.  Fare clic su **stime** e digitare un nuovo valore per controllare i valori di ora futuri quanti si desidera visualizzare nel grafico.  
  
     Il valore predefinito è 5.  
  
3.  Fare clic su qualsiasi punto della linea, cronologica o futura, per visualizzare i valori esatti per quel punto nel tempo, visualizzato nei **legenda Data Mining**.  
  
4.  Nel grafico vengono visualizzati sia i dati cronologici che i dati futuri. Si noti la linea punteggiata con uno sfondo ombreggiato. Questi valori sono stime future, basate sul modello.  
  
     I dati cronologici (utilizzati per compilare il modello) vengono mostrati sul lato sinistro del grafico.  
  
5.  Selezionare il **Mostra stime cronologiche** possibilità di farsi un'idea per la stabilità della serie temporale.  
  
     ![per una singola serie nel modello di previsioni](media/dm13-forecast-chart-singleseries.gif "previsioni per una singola serie nel modello")  
  
     Le stime cronologiche sono valori stimati basati sulla serie a quel determinato punto che vengono confrontati con i valori cronologici effettivi. Se la linea punteggiata (contenente i valori stimati) si differenzia dalla linea continua (i valori effettivi), significa che la prima parte della serie forse non rappresenta una stima accurata dei valori successivi. Potrebbero essere necessari più dati o potrebbe semplicemente essere un indicatore di volatilità nel ciclo.  
  
6.  Selezionare il **Mostra deviazioni** opzione per visualizzare le barre di errore nel grafico.  
  
     Le barre di errore consentono di valutare visivamente la variabilità delle stime. La qualità delle stime varia a seconda dei dati di origine, ma quando si aumenta il numero di intervalli per la stima, dovrebbe essere visualizzato un aumento costante delle deviazioni.  
  
 **Suggerimenti**  
  
-   Per attivare/disattivare visualizzazione delle **legenda Data Mining**, fare doppio clic su qualsiasi punto nel grafico.  
  
     È possibile visualizzare un intervallo di tempo specifico facendo clic sul grafico, trascinando una selezione temporale all'interno del grafico, quindi facendo di nuovo clic per ingrandire l'intervallo selezionato.  
  
-   Per ottenere una copia del grafico corrente, fare clic su **copia in Excel**, quindi fare clic su un foglio di lavoro di Excel. Viene inserito un elemento grafico nel foglio tramite tutte le opzioni che erano state impostate, inclusa una legenda.  
  
     Tuttavia, questo grafico è statico e pertanto non è possibile modificare la legenda o visualizzare i dati sottostanti; Se occorre una vista del grafico più interattiva, usare il [visualizzatori di Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
-   Fare clic su **Abs** nella barra dei menu del visualizzatore per alternare le curve relative e assolute.  
  
     Questa opzione è utile se il grafico contiene più modelli, ma la scala dei dati di ogni modello è molto diversa.  
  
     Ad esempio, se gli archivi dell'area Pacifico sono nuovi e le vendite sono basse e se vengono utilizzati valori assoluti, la linea che mostra le vendite dell'area Pacifico potrebbe risultare piatta, rendendo difficile la visualizzazione delle modifiche effettive, mentre gli altri modelli vengono visualizzati in una scala più normale.  
  
     Passando alla vista in cui vengono utilizzati valori relativi, è possibile normalizzare la scala di modelli diversi e visualizzare le differenze come percentuale delle modifiche. Quando le modifiche sono relative a ogni modello, possono essere visualizzate nello stesso grafico senza una distorsione significativa.  
  
 [Esplorare il modello](#bkmk_Top)  
  
###  <a name="bkmk_Model"></a> Modello  
 Un modello di previsione può anche essere rappresentato come albero delle decisioni o, se la serie è principalmente lineare, modello di regressione.  
  
 Ad esempio, in questo modello esiste una differenza nella formula di regressione basata su una determinata condizione, pertanto l'albero si divide in due rami, ognuno con una formula di regressione diversa.  
  
 ![Filtrare singola serie nel modello di previsione](media/dm13-forecast-model-northamerica.gif "filtrare singola serie nel modello di previsione")  
  
##### <a name="explore-the-forecasting-model-as-a-tree"></a>Esplorare il modello di previsione come un albero  
  
1.  Fare clic sui **albero** elenco a discesa elenco e scegliere un modello da visualizzare.  
  
     Per ogni attributo stimabile viene visualizzato un nodo di regressione o un albero separato. Ad esempio, se i dati contengono le vendite per l'Europa, l'America del nord e il Pacifico, sono presenti tre modelli diversi, uno per ogni serie di dati.  
  
2.  Trascinare il **Mostra il livello** dispositivo di scorrimento per filtrare i livelli inferiori dell'albero e concentrare le divisioni più importanti.  
  
3.  Fare clic su ogni nodo per visualizzare alcune statistiche descrittive nella **legenda Data Mining**.  
  
     Quando si posiziona il mouse su un nodo, vengono visualizzate anche le stesse statistiche nella descrizione comando e la formula completa che descrive tale nodo.  
  
4.  Se si desidera copiare le informazioni contenute nel **legenda Data Mining**, fare doppio clic il **legenda Data Mining**, selezionare **copia**e fare clic all'interno del foglio di lavoro di Excel. Il **copia in Excel** opzione consente di copiare il grafico, non le statistiche.  
  
 [Esplorare il modello](#bkmk_Top)  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione di modelli in Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
