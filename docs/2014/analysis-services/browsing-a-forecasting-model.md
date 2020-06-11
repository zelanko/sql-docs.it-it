---
title: Esplorazione di un modello di previsione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: acf5d2f16271cf525194c1df48ac02c4c4241467
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527707"
---
# <a name="browsing-a-forecasting-model"></a>Esplorazione di un modello di previsione
  Quando si apre un modello di previsione utilizzando **Sfoglia**, il modello viene visualizzato in un visualizzatore interattivo, simile al Visualizzatore modello Time Series in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Il visualizzatore consente di esplorare le tendenze, confrontare le serie, creare stime e ottenere informazioni sul modello e sui dati sottostanti.  
  
##  <a name="explore-the-model"></a><a name="bkmk_Top"></a>Esplorare il modello  
 Il visualizzatore **Browse** per i modelli di previsione fornisce una visualizzazione del grafico che mostra le tendenze nel tempo e consente di creare stime e una vista modello, che rappresenta le serie temporali come albero delle decisioni o albero di regressione.  
  
-   [Visualizzazione grafico](#bkmk_charts)  
  
-   [Visualizzazione modello](#bkmk_Model)  
  
 Per sperimentare un modello di previsione, è possibile utilizzare i dati di esempio nella scheda previsioni della cartella di lavoro dei dati di esempio e compilare un modello Time Series utilizzando la [procedura guidata previsione &#40;componenti aggiuntivi Data mining per excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md) sulla barra multifunzione **Data** mining o gli [strumenti di analisi tabelle &#40;per Excel&#41;](forecast-table-analysis-tools-for-excel.md) nella barra multifunzione **analizza** .  
  
###  <a name="chart"></a><a name="bkmk_charts"></a>Grafico  
 Nella scheda **grafico** viene visualizzata la tendenza nella serie di dati nel corso del tempo, insieme ai valori stimati. L'asse verticale del grafico rappresenta i valori della serie, mentre l'asse orizzontale rappresenta il tempo.  
  
##### <a name="explore-the-forecasting-chart"></a>Esplorare il grafico di previsione  
  
1.  Questo modello contiene più serie temporali, ma per semplificare il grafico, è possibile visualizzare una singola serie o solo alcune serie correlate.  
  
     ![stime cronologiche in un modello di previsione](media/dm13-forecast-chart-historicpredictions.gif "stime cronologiche in un modello di previsione")  
  
     Utilizzare le caselle di controllo per selezionare la previsione solo per l'America del nord e solo per l'importo delle vendite.  
  
2.  Fare clic su **passaggi stima** e digitare un nuovo valore per controllare il numero di valori temporali futuri che si desidera visualizzare nel grafico.  
  
     Il valore predefinito è 5.  
  
3.  Fare clic su un punto qualsiasi della riga, cronologica o futura, per visualizzare i valori esatti per quel punto nel tempo, visualizzati in **Legenda data mining**.  
  
4.  Nel grafico vengono visualizzati sia i dati cronologici che i dati futuri. Si noti la linea punteggiata con uno sfondo ombreggiato. Questi valori sono stime future, basate sul modello.  
  
     I dati cronologici (utilizzati per compilare il modello) vengono mostrati sul lato sinistro del grafico.  
  
5.  Selezionare l'opzione **Mostra stime cronologiche** per ottenere un senso per la stabilità della serie temporale.  
  
     ![previsione per una singola serie nel modello](media/dm13-forecast-chart-singleseries.gif "previsione per una singola serie nel modello")  
  
     Le stime cronologiche sono valori stimati basati sulla serie a quel determinato punto che vengono confrontati con i valori cronologici effettivi. Se la linea punteggiata (contenente i valori stimati) si differenzia dalla linea continua (i valori effettivi), significa che la prima parte della serie forse non rappresenta una stima accurata dei valori successivi. Potrebbero essere necessari più dati o potrebbe semplicemente essere un indicatore di volatilità nel ciclo.  
  
6.  Selezionare l'opzione **Mostra deviazioni** per visualizzare le barre di errore nel grafico.  
  
     Le barre di errore consentono di valutare visivamente la variabilità delle stime. La qualità delle stime varia a seconda dei dati di origine, ma quando si aumenta il numero di intervalli per la stima, dovrebbe essere visualizzato un aumento costante delle deviazioni.  
  
 **Suggerimenti**  
  
-   Per abilitare o disabilitare la visualizzazione di **Legenda data mining**, fare clic con il pulsante destro del mouse su qualsiasi punto del grafico.  
  
     È possibile visualizzare un intervallo di tempo specifico facendo clic sul grafico, trascinando una selezione temporale all'interno del grafico, quindi facendo di nuovo clic per ingrandire l'intervallo selezionato.  
  
-   Per ottenere una copia del grafico corrente, fare clic su **copia in Excel**, quindi fare clic su un foglio di lavoro in Excel. Viene inserito un elemento grafico nel foglio tramite tutte le opzioni che erano state impostate, inclusa una legenda.  
  
     Tuttavia, questo grafico è statico, pertanto non è possibile modificare la legenda né visualizzare i dati sottostanti; Se è necessaria una visualizzazione grafico più interattiva, usare i [visualizzatori di Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
-   Fare clic su **ABS** nella barra dei menu del visualizzatore per passare tra le curve assolute e relative.  
  
     Questa opzione è utile se il grafico contiene più modelli, ma la scala dei dati di ogni modello è molto diversa.  
  
     Ad esempio, se gli archivi dell'area Pacifico sono nuovi e le vendite sono basse e se vengono utilizzati valori assoluti, la linea che mostra le vendite dell'area Pacifico potrebbe risultare piatta, rendendo difficile la visualizzazione delle modifiche effettive, mentre gli altri modelli vengono visualizzati in una scala più normale.  
  
     Passando alla vista in cui vengono utilizzati valori relativi, è possibile normalizzare la scala di modelli diversi e visualizzare le differenze come percentuale delle modifiche. Quando le modifiche sono relative a ogni modello, possono essere visualizzate nello stesso grafico senza una distorsione significativa.  
  
 [Esplorazione del modello](#bkmk_Top)  
  
###  <a name="model"></a><a name="bkmk_Model"></a>Modello  
 Un modello di previsione può anche essere rappresentato come albero delle decisioni o, se la serie è principalmente lineare, modello di regressione.  
  
 Ad esempio, in questo modello esiste una differenza nella formula di regressione basata su una determinata condizione, pertanto l'albero si divide in due rami, ognuno con una formula di regressione diversa.  
  
 ![Filtro di una singola serie nel modello di previsione](media/dm13-forecast-model-northamerica.gif "Filtro di una singola serie nel modello di previsione")  
  
##### <a name="explore-the-forecasting-model-as-a-tree"></a>Esplorare il modello di previsione come un albero  
  
1.  Fare clic sull'elenco a discesa **albero** e scegliere un modello da visualizzare.  
  
     Per ogni attributo stimabile viene visualizzato un nodo di regressione o un albero separato. Ad esempio, se i dati contengono le vendite per l'Europa, l'America del nord e il Pacifico, sono presenti tre modelli diversi, uno per ogni serie di dati.  
  
2.  Trascinare il dispositivo di scorrimento **Mostra livello** per filtrare i livelli inferiori dell'albero e concentrarsi sulle divisioni più importanti.  
  
3.  Fare clic su ogni nodo per visualizzare alcune statistiche descrittive in **Legenda data mining**.  
  
     Quando si posiziona il mouse su un nodo, vengono visualizzate anche le stesse statistiche nella descrizione comando e la formula completa che descrive tale nodo.  
  
4.  Se si desidera copiare le informazioni in **Legenda data mining**, fare clic con il pulsante destro del mouse su **Legenda data mining**, selezionare **copia**, quindi fare clic all'interno del foglio di lavoro di Excel. L'opzione **copia in Excel** copia il grafo, non le statistiche.  
  
 [Esplorazione del modello](#bkmk_Top)  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
