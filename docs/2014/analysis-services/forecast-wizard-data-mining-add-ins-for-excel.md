---
title: Prevedere la procedura guidata (dati componenti aggiuntivi Data Mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ba2f28e4f2e66fd642273d06409eb128d219d8b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543696"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>Procedura guidata Previsione (componenti aggiuntivi Data mining per Excel)
  ![Procedura guidata associazione sulla barra multifunzione Data Mining](media/dmc-forecast.gif "procedura guidata nella barra multifunzione Data Mining di associazione")  
  
 La procedura guidata Previsione consente di stimare i valori in una serie temporale e utilizza l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series, ovvero un algoritmo di regressione per la stima di colonne continue, ad esempio le vendite di prodotti.  
  
 Ogni modello di previsione deve contenere una serie del case, ossia la colonna che distingue i punti di una sequenza. Se ad esempio si utilizzano dati cronologici per prevedere le vendite in un periodo di diversi mesi, utilizzare una colonna contenente una serie di date come serie del case.  
  
 È possibile creare stime da un modello di previsione senza fornire i nuovi dati di input.  
  
 Il [previsione &#40;strumenti di analisi tabelle per Excel&#41; ](forecast-table-analysis-tools-for-excel.md) strumento il **Analizza** sulla barra multifunzione, inoltre consente di creare modelli di previsione, ma è meno personalizzabile e può usare solo i dati nelle tabelle di Excel.  
  
## <a name="using-the-forecast-wizard"></a>Utilizzo della procedura guidata Previsione  
  
1.  Nel **Data Mining** sulla barra multifunzione, fare clic su **previsione**.  
  
2.  Nel **selezione dati di origine**, scegliere la tabella di Excel, intervallo o origine dati esterna da utilizzare come input.  
  
     Se si utilizza un'origine dati esterna, è possibile definire viste o query personalizzate e salvarle come origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Nel **Forecasting** pagina, per **timestamp**, selezionare una colonna contenente i valore di numerico univoco (che include i valori di data e ora) che può essere utilizzato come serie del case. L'origine dati deve essere ordinata in ordine crescente in base a questa colonna.  
  
     Se i dati non dispone di una colonna di questo tipo, è possibile usare l'opzione \<Nessun timestamp >. Nella procedura guidata verrà aggiunta una colonna di ordinamento univoca per i dati di input; pertanto, è necessario assicurarsi che i dati vengano ordinati nel modo desiderato prima di eseguire la procedura guidata e di scegliere questa opzione.  
  
4.  Facoltativamente, è possibile fare clic su **parametri** e personalizzare il comportamento del modello di data mining.  
  
     I modelli di previsione supportano diversi algoritmi:  
  
    -   ARIMA  
  
    -   ARTXP (un tipo di modello di regressione)  
  
    -   ARTXP e ARIMA combinati  
  
     Per informazioni sulle differenze, vedere [riferimento tecnico algoritmo Microsoft Time Series](data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
     È inoltre possibile aggiungere hint di periodicità, specificare le opzioni di anti-aliasing e personalizzare le opzioni di regressione per il modello.  
  
5.  Nel **fine** pagina, fornire un nome descrittivo per il set di dati e il modello e impostare le opzioni seguenti che consentono di controllare l'utilizzo del modello finito:  
  
    -   **Esplora modello**. Quando questa opzione è selezionata, il più presto la procedura guidata al termine dell'elaborazione del modello, viene aperto un **esplorare** finestra per semplificare l'esplorazione dei risultati. Il contenuto del visualizzatore dipende dal tipo di modello compilato. Per altre informazioni, vedere [esplorazione di un modello di previsione](browsing-a-forecasting-model.md).  
  
    -   **Consenti drill-through**. Selezionare questa opzione per visualizzare i dati sottostanti dal modello finito. Questa opzione è disponibile solo se si compila un modello Decision Trees.  
  
    -   **Usa modello temporaneo**. Se si seleziona questa opzione, il modello non verrà salvato nel server. I modelli temporanei vengono eliminati quando si chiude Excel.  
  
### <a name="requirements"></a>Requisiti  
 I dati devono includere almeno una colonna che può essere utilizzata come serie temporale. I valori in questa colonna devono essere univoci e continui, vale a dire, devono contenere gap. Prima di eseguire la procedura guidata, ordinare i dati in base alle colonna della serie temporale in ordine crescente.  
  
 Se i dati non includono una colonna della data o dell'ora, è possibile assegnare una serie numerica arbitraria o crearne una mediante la procedura guidata. Se si crea la colonna di ordinamento della serie, verificare che le altre colonne vengano ordinate nell'ordine desiderato prima di avviare la procedura guidata.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di Data Mining](creating-a-data-mining-model.md)   
 [Prevedere la &#40;strumenti di analisi tabelle per Excel&#41;](forecast-table-analysis-tools-for-excel.md)   
 [Esplorazione di un modello di previsione](browsing-a-forecasting-model.md)  
  
  
