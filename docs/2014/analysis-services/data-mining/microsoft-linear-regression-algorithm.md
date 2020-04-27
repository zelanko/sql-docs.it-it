---
title: Algoritmo Microsoft Linear regressione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 50a4abb8-c0b0-4380-ba5e-c49b305b9d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a855df4440f2c023380a97aa37e35047db27ebb9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174420"
---
# <a name="microsoft-linear-regression-algorithm"></a>Algoritmo Microsoft Linear Regression
  L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression è una variante dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees che consente di calcolare una relazione lineare tra una variabile dipendente e indipendente e quindi di usare tale relazione per la stima.

 La relazione assume la forma di un'equazione relativa alla linea che rappresenta meglio una serie di dati. Ad esempio, la linea contenuta nel diagramma seguente è la migliore rappresentazione lineare possibile dei dati.

 ![Retta di modellazione di un set di dati](../media/linear-regression.gif "Retta di modellazione di un set di dati")

 A ogni punto dati del diagramma corrisponde un errore associato alla relativa distanza dalla retta di regressione. I coefficienti a e b dell'equazione di regressione regolano l'angolo e la posizione della retta di regressione. È possibile ottenere l'equazione di regressione modificando i coefficienti a e b fino a quando la somma degli errori associati a tutti i punti raggiunge il minimo.

 Sono disponibili altri tipi di regressione che utilizzano più variabili, nonché metodi di regressione non lineari, tuttavia la regressione lineare è un metodo utile e noto per la modellazione della risposta a una modifica in alcuni fattori sottostanti.

## <a name="example"></a>Esempio
 Tale tipo di regressione consente di determinare una relazione tra due colonne continue. È possibile ad esempio utilizzare la regressione lineare per calcolare una linea di tendenza da dati di produzione o di vendita. La regressione lineare può inoltre essere utilizzata come precursore dello sviluppo di modelli di data mining più complessi, per valutare le relazioni tra colonne di dati.

 Sebbene diversi metodi disponibili per calcolare la regressione lineare non richiedano strumenti di data mining, il vantaggio garantito dall'uso dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression per questa attività è rappresentato dal fatto che tutte le possibili relazioni tra le variabili vengono calcolate e testate automaticamente. Non è necessario selezionare un metodo di calcolo, ad esempio la risoluzione per i minimi quadrati. La regressione lineare potrebbe tuttavia semplificare eccessivamente le relazioni in scenari in cui sul risultato influiscono più fattori.

## <a name="how-the-algorithm-works"></a>Funzionamento dell'algoritmo
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression è una variante dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees. Quando si seleziona l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression, viene richiamato un tipo di algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees speciale, con parametri che vincolano il comportamento dell'algoritmo e richiedono determinati tipi di dati di input. In un modello di regressione lineare, inoltre, per calcolare le relazioni nella sessione iniziale viene utilizzato tutto il set di dati, mentre con un modello di albero delle decisioni standard i dati vengono suddivisi ripetutamente in subset o alberi minori.

## <a name="data-required-for-linear-regression-models"></a>Dati necessari per i modelli di regressione lineare
 Per preparare i dati da utilizzare in un modello di regressione lineare è necessario comprendere i requisiti dell'algoritmo, tra cui la quantità di dati necessaria e la modalità di utilizzo dei dati. I requisiti di questo tipo di modello sono i seguenti:

-   **Una colonna a chiave singola** Ogni modello deve contenere una colonna numerica o di testo che identifichi in modo univoco ogni record. Le chiavi composte non sono consentite.

-   **Una colonna stimabile** Richiede almeno una colonna stimabile. È possibile includere più attributi stimabili in un modello, ma tali attributi devono essere tipi di dati numerici continui. Non è possibile utilizzare un tipo di dati datetime come attributo stimabile anche se l'archiviazione nativa dei dati è numerica.

-   **Colonne di input** Le colonne di input devono contenere dati numerici continui ed essere associate al tipo di dati appropriato.

 Per altre informazioni, vedere la sezione Requisiti in [Riferimento tecnico per l'algoritmo Microsoft Linear Regression](microsoft-linear-regression-algorithm-technical-reference.md).

## <a name="viewing-a-linear-regression-model"></a>Visualizzazione di un modello di regressione lineare
 Per esplorare il modello, è possibile usare il **Visualizzatore Microsoft Decision Trees**. La struttura ad albero per un modello di regressione lineare è molto semplice, in quanto tutte le informazioni sull'equazione di regressione sono contenute in un solo nodo. Per altre informazioni, vedere [Visualizzare un modello usando il Visualizzatore Microsoft Decision Trees](browse-a-model-using-the-microsoft-tree-viewer.md).

 Per ulteriori dettagli sull'equazione, è anche possibile visualizzare i coefficienti e altri dettagli tramite [Microsoft Generic Content Tree Viewer](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).

 Per un modello di regressione lineare, il contenuto del modello include metadati, la formula di regressione e statistiche sulla distribuzione dei valori di input. Per altre informazioni, vedere [Contenuto dei modelli di data mining per i modelli di regressione lineare &#40;Analysis Services - Data mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).

## <a name="creating-predictions"></a>Creazione di stime
 Dopo l'elaborazione del modello, i risultati vengono archiviati come set di statistiche con la formula di regressione lineare che è possibile utilizzare per calcolare tendenze future. Per esempi di query da usare con un modello di regressione lineare, vedere [Esempi di query sul modello di regressione lineare](linear-regression-model-query-examples.md).

 Per informazioni generali sulla creazione di query in base ai modelli di data mining, vedere [Query di data mining](data-mining-queries.md).

 Selezionando l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Linear Regression, se l'attributo stimabile è un tipo di dati numerico continuo, oltre a creare un modello di regressione lineare, è possibile creare un modello di albero delle decisioni che contenga regressioni. In questo caso, l'algoritmo suddividerà i dati quando rileverà punti di separazione appropriati, ma per alcune aree di dati creerà una formula di regressione. Per altre informazioni sugli alberi di regressione con un modello di albero delle decisioni, vedere [Contenuto dei modelli di data mining per i modelli di albero delle decisioni &#40;Analysis Services - Data mining&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).

## <a name="remarks"></a>Osservazioni

-   Non supporta l'utilizzo del linguaggio PMML (Predictive Model Markup Language) per la creazione di modelli di data mining.

-   Non supporta la creazione di dimensioni di data mining.

-   Supporta il drill-through.

-   Supporta l'utilizzo di modelli di data mining OLAP.

## <a name="see-also"></a>Vedi anche
 [Algoritmi di data mining &#40;Analysis Services-Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md) [esempio di query sul modello](linear-regression-model-query-examples.md) di regressione lineare dell' [algoritmo Microsoft Linear](microsoft-linear-regression-algorithm-technical-reference.md) regressione, [contenuto del modello di data mining per i modelli di regressione lineare &#40;Analysis Services-Data mining&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)


