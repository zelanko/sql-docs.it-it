---
title: Metodi di discretizzazione (data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content types [data mining]
- discretization [Analysis Services]
- columns [data mining], discretization
- THRESHOLDS method
- CLUSTERS method
- DiscretizationBuckets property
- AUTOMATIC method
- EQUAL_AREAS method
- coding [Data Mining]
ms.assetid: 02c0df7b-6ca5-4bd0-ba97-a5826c9da120
author: minewiskan
ms.author: owend
ms.openlocfilehash: feca59697c1c78a08e629b62856053f2d2ce6d6d
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522557"
---
# <a name="discretization-methods-data-mining"></a>Metodi di discretizzazione (data mining)
  Per il corretto funzionamento di alcuni algoritmi utilizzati per creare data mining modelli in sono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] necessari tipi di contenuto specifici. L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes, ad esempio, non può utilizzare colonne continue come input, né stimare valori continui. Alcune colonne, inoltre, possono contenere un numero talmente elevato di valori da impedire all'algoritmo di identificare con facilità schemi significativi nei dati, in base ai quali creare un modello.  
  
 In tali casi, è possibile discretizzare i dati nelle colonne in modo da poter utilizzare gli algoritmi per generare un modello di data mining. Per*discretizzazione* si intende il processo di raggruppamento in bucket dei valori, in modo da limitare il numero di stati possibili. I bucket stessi vengono considerati come valori ordinati e discreti. È possibile discretizzare sia colonne numeriche che colonne stringa.  
  
 Esistono vari metodi per discretizzare i dati, Se la soluzione di data mining usa dati relazionali, è possibile controllare il numero di bucket da usare per il raggruppamento dei dati impostando il valore della proprietà <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> . Il numero predefinito di bucket è 5.  
  
 Se la soluzione di data mining usa i dati provenienti da un cubo OLAP (Online Analytical Processing), l'algoritmo di data mining calcola automaticamente il numero di bucket da generare usando l'equazione seguente, dove n è il numero di valori Distinct di dati nella colonna:  
  
 `Number of Buckets = sqrt(n)`  
  
 Se si vuole evitare che il numero di bucket venga calcolato automaticamente da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , è possibile usare la proprietà <xref:Microsoft.AnalysisServices.DimensionAttribute.DiscretizationBucketCount%2A> per specificare manualmente tale numero.  
  
 Nella tabella seguente vengono descritti i metodi che è possibile utilizzare per la discretizzazione dei dati in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Metodo di discretizzazione|Descrizione|  
|---------------------------|-----------------|  
|`AUTOMATIC`|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina il metodo di discretizzazione da usare.|  
|`CLUSTERS`|L'algoritmo suddivide i dati in gruppi eseguendo il campionamento dei dati di training, l'inizializzazione su un numero di punti casuali e quindi diverse iterazioni dell'algoritmo Microsoft Clustering tramite il metodo di clustering EM (Expectation Maximization). Il metodo `CLUSTERS` è utile in quanto è valido per qualsiasi curva di distribuzione, ma richiede tempi di elaborazione più lunghi rispetto agli altri metodi di discretizzazione.<br /><br /> È possibile utilizzare tale metodo solo per le colonne numeriche.|  
|`EQUAL_AREAS`|L'algoritmo suddivide i dati in gruppi che contengono lo stesso numero di valori. Questo metodo è particolarmente appropriato per le curve di distribuzione normali, ma non consente di ottenere risultati attendibili se la distribuzione include un numero elevato di valori che appartengono a un gruppo ristretto all'interno dei dati continui. Se ad esempio metà degli elementi ha un costo 0, metà dei dati corrisponderà a un singolo punto della curva. In tale distribuzione, questo metodo suddivide i dati in modo da stabilire una discretizzazione uguale in più aree, generando una rappresentazione non corretta dei dati.|  
  
## <a name="remarks"></a>Commenti  
  
-   Per discretizzare le stringhe, è possibile utilizzare il metodo `EQUAL_AREAS`.  
  
-   Per discretizzare i dati, il metodo `CLUSTERS` utilizza un campione casuale di 1000 record. Se si desidera evitare che l'algoritmo esegua il campionamento dei dati, utilizzare il metodo `EQUAL_AREAS`.  
  
-   Nell'esercitazione relativa al modello di data mining di rete neurale viene descritto il modo in cui la discretizzazione può essere personalizzata. Per ulteriori informazioni, vedere la [lezione 5: compilazione dei modelli di rete neurale e di regressione logistica &#40;esercitazione intermedia sul Data Mining&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;&#41;di data mining](content-types-data-mining.md)   
 [Tipi di contenuto &#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining-algorithms-analysis-services-data-mining.md)   
 [Strutture di data mining &#40;Analysis Services-&#41;di data mining](mining-structures-analysis-services-data-mining.md)   
 [Tipi di dati &#40;&#41;di data mining](data-types-data-mining.md)   
 [Colonne struttura di data mining](mining-structure-columns.md)   
 [Distribuzioni delle colonne &#40;Data mining&#41;](column-distributions-data-mining.md)  
  
  
