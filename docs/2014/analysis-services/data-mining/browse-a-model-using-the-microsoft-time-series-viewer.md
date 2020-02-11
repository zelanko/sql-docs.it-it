---
title: Visualizzare un modello utilizzando il Visualizzatore Microsoft Time Series | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], continuous columns
- mining model content, viewing
- Microsoft Time Series Viewer
- charts [Analysis Services]
- Time Series Viewer [Analysis Services]
- continuous columns
- regression algorithms [Analysis Services]
ms.assetid: a77c16cd-1cd0-4fc5-afeb-d1dab30d1e25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85767ce54991950e75b39bf909d6d0ff3cb2cd8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085975"
---
# <a name="browse-a-model-using-the-microsoft-time-series-viewer"></a>Visualizzare un modello utilizzando il Visualizzatore Microsoft Times Series
  Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visualizzatore Time Series in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente di visualizzare i modelli di data mining [!INCLUDE[msCoName](../../includes/msconame-md.md)] compilati con l'algoritmo Time Series. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series è un algoritmo di regressione che consente di creare modelli di data mining per la stima di colonne continue, relative ad esempio alle vendite di un prodotto, in uno scenario di previsione. Questi modelli Time Series possono includere informazioni in base ad algoritmi diversi:  
  
-   Algoritmo ARTxp, ottimizzato per le stime a breve termine.  
  
-   Algoritmo ARIMA, ottimizzato per le stime a lungo termine.  
  
-   Combinazione di algoritmi ARTxp e ARIMA.  
  
 Per altre informazioni su questi algoritmi, vedere [Algoritmo Microsoft Time Series](microsoft-time-series-algorithm.md) e [Riferimento tecnico per l'algoritmo Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md).  
  
> [!NOTE]  
>  Per visualizzare informazioni dettagliate sulle equazioni utilizzate nel modello e sui modelli individuati, utilizzare il visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Generic Content Tree Viewer. Per altre informazioni, vedere [Visualizzare un modello usando Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Microsoft Generic Content Tree Viewer &#40;Data mining&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="BKMK_ViewerTabs"></a>Schede del Visualizzatore  
 Per la visualizzazione di un modello di data mining in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]viene utilizzato il visualizzatore appropriato nella scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining. Il Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series include le schede seguenti:  
  
-   [Modello](#BKMK_Tree)  
  
-   [Grafici](#BKMK_Charts)  
  
 **Nota** Le informazioni visualizzate per il contenuto del modello e nella legenda data mining dipendono dall'algoritmo utilizzato dal modello. Tuttavia, le schede **Modello** e **Grafici** sono identiche indipendentemente dalla combinazione di algoritmi.  
  
###  <a name="BKMK_Tree"></a>Modello  
 Quando si compila un modello Time Series, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] il modello completato viene presentato come un albero. Se i dati contengono più serie di case, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene compilato un albero distinto per ognuna di esse. Si supponga ad esempio di elaborare stime di vendita per le aree Pacifico, Nord America ed Europa. Le stime per ognuna di queste aree sono serie di casi. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] compila un albero separato per ogni serie. Per visualizzare una determinata serie, selezionarla nell'elenco **Albero** .  
  
 Per ogni albero, il modello Time Series contiene un nodo **Tutti** e quindi si divide in una serie di nodi che rappresentano le strutture periodiche individuate dall'algoritmo. È possibile fare clic su ogni nodo per visualizzare statistiche, ad esempio il numero di case e l'equazione.  
  
 Se il modello è stato creato usando solo ARTxp, l'opzione **Legenda data mining** relativa al nodo radice contiene soltanto il numero totale di case. Per ogni nodo non radice, **Legenda data mining** contiene informazioni più dettagliate sulla divisione dell'albero, ad esempio è possibile che visualizzi l'equazione per il nodo e il numero di case. La *regola* nella legenda contiene informazioni che identificano la serie e l'intervallo di tempo al quale si applica la regola. Il testo della legenda `M200 Europe Amount -2` indica ad esempio che il nodo rappresenta il modello per la serie M200 Europe, in un periodo che risale a due intervalli di tempo prima.  
  
 Se il modello è stato creato usando solo ARIMA, la scheda **Modello** contiene un singolo nodo con la didascalia **Tutti**. L'opzione **Legenda data mining** per il nodo radice contiene l'equazione ARIMA.  
  
 Se si crea un modello misto, il nodo radice contiene soltanto il numero di case e l'equazione ARIMA. Dopo il nodo radice, l'albero si divide in nodi distinti per ogni struttura periodica. Per ogni nodo non radice, la Legenda data mining contiene entrambi gli algoritmi ARTxp e ARIMA, l'equazione per il nodo e il numero di case nel nodo. La prima voce dell'elenco è l'equazione ARTxp, etichettata come equazione del nodo dell'albero, seguita dall'equazione ARIMA. Per altre informazioni su come interpretare queste informazioni, vedere [Riferimento tecnico per l'algoritmo Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md).  
  
 In generale, il grafico dell'albero delle decisioni mostra la divisione più importante, ovvero il nodo **Tutti** , a sinistra del visualizzatore. Negli alberi delle decisioni la divisione dopo il nodo **Tutti** è la più importante perché contiene la condizione che separa in modo più netto i case presenti nei dati di training. In un modello Time Series la diramazione principale indica il ciclo stagionale più probabile. Le divisioni dopo il nodo **Tutti** vengono visualizzate a destra del ramo.  
  
 È possibile espandere o comprimere singoli nodi dell'albero per visualizzare o nascondere le divisioni che ricorrono dopo ogni nodo. È anche possibile usare le opzioni della scheda **Albero delle decisioni** per determinare la modalità di visualizzazione dell'albero. Per modificare il numero di livelli visualizzati nell'albero, usare il dispositivo di scorrimento **Mostra livello** . Per impostare il numero predefinito di livelli visualizzati per tutti gli alberi del modello, usare **Espansione predefinita** .  
  
 L'ombreggiatura del colore di sfondo di ogni nodo indica il numero di case esistenti nel nodo. Per determinare il numero esatto di case in un nodo, posizionare il puntatore sul nodo in modo da visualizzare una finestra popup corrispondente.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a>Grafici  
 Nella scheda **Grafici** viene visualizzato un grafico che indica il comportamento dell'attributo stimato nel corso del tempo, oltre a 5 valori futuri stimati. L'asse verticale del grafico rappresenta il valore della serie, mentre l'asse orizzontale rappresenta il tempo.  
  
> [!NOTE]  
>  Gli intervalli di tempo utilizzati sull'asse dell'ora dipendono dalle unità utilizzate nei dati: possono rappresentare giorni, mesi o anche secondi.  
  
 Usare il pulsante **Abs** per passare dalle curve assolute alle curve relative e viceversa. Se il grafico contiene più modelli, la scala dei dati di ogni modello può essere notevolmente diversa. Se si utilizza una curva assoluta, un modello può essere rappresentato da una retta, mentre un altro può indicare modifiche significative. Ciò si verifica perché la scala di un modello è maggiore di quella dell'altro. Passando a una curva relativa, la scala indica la percentuale di modifica anziché valori assoluti. In questo modo risulta più agevole confrontare modelli basati su scale diverse.  
  
 Se il modello di data mining contiene più serie temporali, è possibile selezionare una o più serie da visualizzare nel grafico. Fare clic sull'elenco a destra del visualizzatore e selezionare la serie desiderata. Se il grafico diventa troppo complesso, è possibile filtrare le serie visualizzate selezionando o deselezionando le caselle di controllo corrispondenti nella legenda.  
  
 Nel grafico vengono visualizzati sia i dati cronologici che i dati futuri. Ai dati futuri viene applicata un'ombreggiatura per distinguerli dai dati cronologici. I valori dei dati vengono visualizzati come linee continue per i dati cronologici e come linee punteggiate per le stime. È possibile modificare il colore delle linee utilizzate per ciascuna serie impostando le proprietà [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] or [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Modificare i colori usati nei visualizzatori data mining](change-the-colors-used-in-the-data-mining-viewer.md).  
  
 È possibile modificare l'intervallo di tempo visualizzato tramite le opzioni di zoom. È inoltre possibile visualizzare un intervallo di tempo specifico facendo clic sul grafico, trascinando una selezione temporale all'interno del grafico, quindi facendo di nuovo clic per ingrandire l'intervallo selezionato.  
  
 Per selezionare il numero di **intervalli** temporali da visualizzare nel modello, usare **Intervalli per la stima**. Se si seleziona la casella di controllo **Mostra deviazioni** , il visualizzatore fornisce barre di errore in cui viene indicata l'accuratezza del valore stimato.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al Visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Algoritmo Microsoft Time Series](microsoft-time-series-algorithm.md)   
 [Esempi di query sul modello Time Series](time-series-model-query-examples.md)   
 [Visualizzatori modello di data mining](data-mining-model-viewers.md)  
  
  
