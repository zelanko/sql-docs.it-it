---
title: Procedura guidata classificazione (componenti aggiuntivi Data mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- classification [data mining]
ms.assetid: 409c5076-c4c3-4f09-8f30-d3297df45f13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a62d937a733ea41b85a83224a043ff4ad7ecdd29
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087925"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>Procedura guidata Classificazione (componenti aggiuntivi Data mining per Excel)
  ![Procedura guidata Classificazione sulla barra multifunzione Data mining](media/dmc-classify.gif "Procedura guidata Classificazione sulla barra multifunzione Data mining")  
  
 La procedura guidata **Classificazione** consente di generare un modello di classificazione in base a dati esistenti di una tabella di Excel, un intervallo di Excel o un'origine dati esterna.  
  
 Un modello di classificazione consente di estrarre modelli dai dati che indicano somiglianze e di eseguire stime basate su raggruppamenti di valori. È possibile utilizzare un modello di classificazione, ad esempio, per stimare i rischi in base ai modelli di ricavo o costi.  
  
## <a name="using-the-classify-wizard"></a>Utilizzo della procedura guidata Classificazione  
  
1.  Sulla barra multifunzione **data mining** fare clic su **classificazione**, quindi su **Avanti**.  
  
2.  Nella pagina **selezione dati di origine** scegliere i dati da analizzare.  
  
     Questa procedura guidata supporta più tipi di dati: tabelle di Excel, intervalli di Excel e origini dati esterne. Con i dati esterni, è possibile aggiungerli in Excel oppure scegliere un set di tabelle o viste in un'origine dati di Analysis Services. È inoltre possibile aggiungere tabelle e modificare le colonne per creare origini dati ad hoc.  
  
3.  Nella pagina **classificazione** scegliere la colonna che si desidera classificare.  
  
     Esaminare le colonne dell'elenco, le **colonne di input**e deselezionare tutte le colonne con valori univoci e pertanto non sono utili per la creazione di modelli, ad esempio numeri ID, nomi di clienti e così via. È inoltre necessario rimuovere le colonne che essenzialmente duplicano la colonna classificabile.  
  
     Ad esempio, se si esegue la classificazione tramite la stima della categoria di un prodotto, è necessario escludere il campo della sottocategoria se esiste una regola business nota. In caso contrario, l'attendibilità di tale regola potrebbe impedire di individuare altre correlazioni.  
  
4.  Facoltativamente, fare clic su **parametri** per modificare i parametri dell'algoritmo e personalizzare il comportamento del modello di clustering.  
  
5.  Nella pagina **suddivisione dei dati in set di training e di testing** specificare la quantità di dati da mantenere per il test. Il resto viene sempre utilizzato per il training del modello.  
  
     L'impostazione predefinita è il 30% dei dati di testing e il 70% dei dati di training.  
  
6.  Nella pagina **fine** specificare un nome descrittivo per il set di dati e il modello, quindi impostare le opzioni seguenti che consentono di controllare la modalità di utilizzo del modello finito:  
  
    -   **Esplora modello**. Quando questa opzione è selezionata, non appena viene completata l'elaborazione del modello da parte della procedura guidata, viene aperta una finestra **Esplora** che consente di esplorare i risultati. Il contenuto del visualizzatore dipende dal tipo di modello compilato. Per ulteriori informazioni, vedere [esplorazione di un modello Decision Trees](browsing-a-decision-trees-model.md) ed [esplorazione di un modello di rete neurale](browsing-a-neural-network-model.md).  
  
    -   **Abilitare il drill-through**. Selezionare questa opzione per visualizzare i dati sottostanti dal modello finito. Questa opzione è disponibile solo se si compila un modello Decision Trees.  
  
    -   **Usa modello temporaneo**. Se si seleziona questa opzione, il modello non verrà salvato nel server. I modelli temporanei vengono eliminati quando si chiude Excel.  
  
## <a name="more-about-classification-models"></a>Ulteriori informazioni sui modelli di classificazione  
 Nella finestra di dialogo **parametri algoritmo** è inoltre possibile scegliere il metodo di classificazione tra gli algoritmi disponibili in Analysis Services:  
  
-   Microsoft Decision Trees  
  
-   Microsoft Logistic Regression  
  
-   Microsoft Naive Bayes  
  
-   Microsoft Neural Network  
  
 Sebbene gli algoritmi possano restituire risultati simili, analizzano i dati in modo diverso, pertanto è consigliabile provare diversi algoritmi e confrontare i risultati. Il metodo predefinito è Microsoft Decision Trees.  
  
 Nell'elenco **Parameters** è possibile modificare le opzioni avanzate, che dipendono dal tipo di algoritmo scelto. I parametri per ogni algoritmo vengono descritti in modo più dettagliato nella documentazione online di SQL Server.  
  
 [Guida di riferimento tecnico per l'algoritmo Microsoft Decision Trees](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Riferimento tecnico per l'algoritmo Microsoft Naive Bayes](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Microsoft Neural Network Algorithm Technical Reference](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisiti  
 Per utilizzare la procedura guidata **classificazione** , è necessario essere connessi a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] un database di. Per informazioni su come creare una connessione, vedere [connettersi ai dati di origine &#40;client di data mining per&#41;Excel ](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)  
  
  
