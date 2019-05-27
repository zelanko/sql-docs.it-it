---
title: Algoritmo Microsoft Logistic Regression | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logical regression algorithms [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 3dd54d07-1c3b-4b87-b7f0-b962ed8cf844
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 14e86ac2dd32f2a3e1384e08aca597794ee4bc71
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083961"
---
# <a name="microsoft-logistic-regression-algorithm"></a>Algoritmo Microsoft Logistic Regression
  La regressione logistica è una nota tecnica statistica utilizzata per modellare i risultati binari.  
  
 Sono disponibili varie implementazioni della regressione logistica nella ricerca statistica, utilizzando tecniche di apprendimento diverse. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Logistic Regression è stato implementato utilizzando una variazione dell'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Neural Network. Questo algoritmo consente di condividere molte delle qualità delle reti neurale ma è più facile per eseguire il training.  
  
 Un vantaggio della regressione logistica è rappresentato dal fatto che l'algoritmo, considerando qualsiasi tipo di input, è estremamente flessibile e supporta diverse attività analitiche differenti:  
  
-   Utilizzo di dati demografici per fare stime sui risultati, ad esempio il livello di rischio per una determinata malattia.  
  
-   Esplorazione e ponderazione dei fattori che contribuiscono a un risultato. Ad esempio, il rilevamento dei fattori che influenzano i clienti a visitare ripetutamente un negozio.  
  
-   Classificazione di documenti, messaggi di posta elettronica o altri oggetti che dispongono di molti attributi.  
  
## <a name="example"></a>Esempio  
 Si consideri un gruppo di persone con informazioni demografiche simili che acquistano prodotti dall'azienda Adventure Works. Modellando i dati per correlarli a un risultato specifico, ad esempio l'acquisto di un prodotto di destinazione, è possibile rilevare come le informazioni demografiche contribuiscono alla probabilità che queste persone acquistino il prodotto di destinazione.  
  
## <a name="how-the-algorithm-works"></a>Funzionamento dell'algoritmo  
 La regressione logistica è un noto metodo statistico per la determinazione del contributo di più fattori a una coppia di risultati. L'implementazione Microsoft utilizza una rete neurale modificata per modellare le relazioni tra input e output. Viene misurato l'effetto di ciascun input sull'output e i vari input vengono ponderati nel modello finito. La regressione logistica del nome deriva dal fatto che la curva dei dati viene compressa tramite una trasformazione logistica per ridurre l'effetto dei valori estremi. Per altre informazioni sull'implementazione e sulla personalizzazione dell'algoritmo, vedere [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](microsoft-logistic-regression-algorithm-technical-reference.md).  
  
## <a name="data-required-for-logistic-regression-models"></a>Dati necessari per i modelli di regressione logistica  
 Quando si preparano i dati da utilizzare nel training di un modello di regressione logistica, è importante comprendere i requisiti dell'algoritmo specifico, tra cui la quantità di dati necessari e la modalità di utilizzo dei dati.  
  
 I requisiti di un modello di regressione logistica sono i seguenti:  
  
 **Una colonna a chiave singola** Ogni modello deve contenere una colonna numerica o di testo che identifichi in modo univoco ogni record. Le chiavi composte non sono consentite.  
  
 **Colonne di input** Ogni modello deve contenere almeno una colonna di input che contiene i valori utilizzati come fattori di analisi. È possibile includere tutte le colonne di input desiderate, ma a seconda del numero di valori in ciascuna colonna, l'aggiunta di colonne supplementari può implicare un aumento del tempo necessario per il training del modello.  
  
 **Almeno una colonna stimabile** Il modello deve contenere almeno una colonna stimabile di qualsiasi tipo di dati, inclusi i dati numerici continui. I valori della colonna stimabile possono anche essere considerati come input per il modello oppure è possibile specificare che devono essere utilizzati solo per la stima. Le tabelle nidificate non sono consentite per le colonne stimabili, ma possono essere utilizzate come input.  
  
 Per informazioni più dettagliate sui tipi di contenuto e i tipi di dati supportati per i modelli di regressione logistica, vedere la sezione Requisiti di [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](microsoft-logistic-regression-algorithm-technical-reference.md).  
  
## <a name="viewing-a-logistic-regression-model"></a>Visualizzazione di un modello di regressione logistica  
 Per esplorare il modello, è possibile utilizzare il Visualizzatore Microsoft Neural Network oppure Microsoft Generic Content Tree Viewer.  
  
 Quando il modello viene visualizzato tramite il Visualizzatore Microsoft Neural Network, Analysis Services mostra i fattori che contribuiscono a un determinato risultato, in ordine di importanza. È possibile scegliere un attributo e i valori da confrontare. Per altre informazioni, vedere [Visualizzare un modello utilizzando il Visualizzatore Microsoft Neural Network](browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 Per ulteriori informazioni, è possibile esplorare i dettagli del modello tramite Microsoft Generic Content Tree Viewer. Il contenuto di un modello di regressione logistica include un nodo marginale che mostra tutti gli input utilizzati per il modello e le subnet per gli attributi stimabili. Per altre informazioni, vedere [Mining Model Content for Logistic Regression Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-logistic-regression-models.md).  
  
## <a name="creating-predictions"></a>Creazione di stime  
 Dopo il training del modello, è possibile creare query rispetto al contenuto del modello per ottenere i coefficienti di regressione e altri dettagli oppure è possibile utilizzare il modello per fare delle stime.  
  
-   Per informazioni generali sulla creazione di query in base a un modello di data mining, vedere [Query di data mining](data-mining-queries.md).  
  
-   Per esempi di query su un modello di regressione lineare, vedere [Esempi di query sul modello di clustering](clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Note  
  
-   Non supporta il drill-through. Questo perché la struttura di nodi nel modello di data mining non corrisponde necessariamente in modo diretto ai dati sottostanti.  
  
-   Non supporta la creazione di dimensioni di data mining.  
  
-   Supporta l'utilizzo di modelli di data mining OLAP.  
  
-   Non supporta l'utilizzo del linguaggio PMML (Predictive Model Markup Language) per la creazione di modelli di data mining.  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto dei modelli di data mining per i modelli di regressione logistica &#40;Analysis Services - Data mining&#41;](mining-model-content-for-logistic-regression-models.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Logistic Regression](microsoft-logistic-regression-algorithm-technical-reference.md)   
 [Esempi di query sul modello di regressione logistica](logistic-regression-model-query-examples.md)  
  
  
