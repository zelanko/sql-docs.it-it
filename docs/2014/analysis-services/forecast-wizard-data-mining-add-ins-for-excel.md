---
title: Procedura guidata previsione (componenti aggiuntivi Data mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0717d8a81cc89897de005144dd631d23da42137
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081029"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>Procedura guidata Previsione (componenti aggiuntivi Data mining per Excel)
  ![Procedura guidata Associazione sulla barra multifunzione Data mining](media/dmc-forecast.gif "Procedura guidata Associazione sulla barra multifunzione Data mining")  
  
 La procedura guidata Previsione consente di stimare i valori in una serie temporale e utilizza l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series, ovvero un algoritmo di regressione per la stima di colonne continue, ad esempio le vendite di prodotti.  
  
 Ogni modello di previsione deve contenere una serie del case, ossia la colonna che distingue i punti di una sequenza. Se ad esempio si utilizzano dati cronologici per prevedere le vendite in un periodo di diversi mesi, utilizzare una colonna contenente una serie di date come serie del case.  
  
 È possibile creare stime da un modello di previsione senza fornire i nuovi dati di input.  
  
 Lo strumento di [analisi delle tabelle &#40;per excel&#41;](forecast-table-analysis-tools-for-excel.md) , nella barra multifunzione **analizza** consente inoltre di creare modelli di previsione, ma è meno personalizzabile e può utilizzare solo i dati nelle tabelle di Excel.  
  
## <a name="using-the-forecast-wizard"></a>Utilizzo della procedura guidata Previsione  
  
1.  Sulla barra multifunzione **data mining** fare clic su **previsione**.  
  
2.  In **selezione dati di origine**scegliere la tabella di Excel, l'intervallo o l'origine dati esterna da utilizzare come input.  
  
     Se si utilizza un'origine dati esterna, è possibile definire viste o query personalizzate e salvarle come origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Nella pagina **previsione** , per **timestamp**, selezionare una colonna contenente un valore numerico univoco (inclusi i valori di data e ora) che può essere utilizzata come serie di casi. L'origine dati deve essere ordinata in ordine crescente in base a questa colonna.  
  
     Se i dati non includono colonne di questo tipo, è possibile usare l'opzione \<nessun timestamp>. Nella procedura guidata verrà aggiunta una colonna di ordinamento univoca per i dati di input; pertanto, è necessario assicurarsi che i dati vengano ordinati nel modo desiderato prima di eseguire la procedura guidata e di scegliere questa opzione.  
  
4.  Facoltativamente, è possibile fare clic su **parametri** e personalizzare il comportamento del modello di data mining.  
  
     I modelli di previsione supportano diversi algoritmi:  
  
    -   ARIMA  
  
    -   ARTXP (un tipo di modello di regressione)  
  
    -   ARTXP e ARIMA combinati  
  
     Per informazioni sulle differenze, vedere [riferimento tecnico per l'algoritmo Microsoft Time Series](data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
     È inoltre possibile aggiungere hint di periodicità, specificare le opzioni di anti-aliasing e personalizzare le opzioni di regressione per il modello.  
  
5.  Nella pagina **fine** specificare un nome descrittivo per il set di dati e il modello, quindi impostare le opzioni seguenti che consentono di controllare la modalità di utilizzo del modello finito:  
  
    -   **Esplora modello**. Quando questa opzione è selezionata, non appena viene completata l'elaborazione del modello da parte della procedura guidata, viene aperta una finestra **Esplora** che consente di esplorare i risultati. Il contenuto del visualizzatore dipende dal tipo di modello compilato. Per altre informazioni, vedere [esplorazione di un modello di previsione](browsing-a-forecasting-model.md).  
  
    -   **Abilitare il drill-through**. Selezionare questa opzione per visualizzare i dati sottostanti dal modello finito. Questa opzione è disponibile solo se si compila un modello Decision Trees.  
  
    -   **Usa modello temporaneo**. Se si seleziona questa opzione, il modello non verrà salvato nel server. I modelli temporanei vengono eliminati quando si chiude Excel.  
  
### <a name="requirements"></a>Requisiti  
 I dati devono includere almeno una colonna che può essere utilizzata come serie temporale. I valori in questa colonna devono essere univoci e continui, ovvero non devono essere presenti gap. Prima di eseguire la procedura guidata, ordinare i dati in base alle colonna della serie temporale in ordine crescente.  
  
 Se i dati non includono una colonna della data o dell'ora, è possibile assegnare una serie numerica arbitraria o crearne una mediante la procedura guidata. Se si crea la colonna di ordinamento della serie, verificare che le altre colonne vengano ordinate nell'ordine desiderato prima di avviare la procedura guidata.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)   
 [Strumenti di analisi tabelle di previsione &#40;per Excel&#41;](forecast-table-analysis-tools-for-excel.md)   
 [Esplorazione di un modello di previsione](browsing-a-forecasting-model.md)  
  
  
