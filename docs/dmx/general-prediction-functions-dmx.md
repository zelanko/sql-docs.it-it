---
title: Funzioni di stima correlate (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8eff7603fa0d0be0e90af201e524554f5e336ea8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937791"
---
# <a name="general-prediction-functions-dmx"></a>Funzioni di stima correlate (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  È possibile usare la **seleziona** istruzione nel Data Mining Extensions (DMX) per creare diversi tipi di query. Una query può essere utilizzata per restituire informazioni sul modello di data mining stesso, per eseguire nuove stime o per modificare il modello eseguendone il training con i nuovi dati. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] offre un'ampia gamma di funzioni specializzate che consentono di controllare il tipo di informazioni restituite in una query. Aggiungendo queste funzioni a una query DMX, è possibile recuperare statistiche o colonne di dati aggiuntive. Tuttavia, ogni tipo di query e ogni tipo di modello supportano solo determinate funzioni.  
  
## <a name="common-functions"></a>Funzioni comuni  
 È possibile utilizzare le funzioni per estendere i risultati restituiti da un modello di data mining. È possibile usare le funzioni seguenti per qualsiasi **seleziona** istruzione che restituisce un'espressione di tabella:  
  
|||  
|-|-|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 Inoltre, le funzioni seguenti sono supportate per quasi tutti i tipi di modello:  
  
-   [È presente &#40;DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 I singoli algoritmi possono supportare funzioni aggiuntive. Per un elenco delle funzioni supportate da ogni tipo di modello, vedere [query di Data Mining](../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="functions-specific-to-select-syntax"></a>Funzioni specifiche per la sintassi SELECT  
 Nella tabella seguente sono elencate le funzioni che è possibile usare per ogni tipo di **seleziona** istruzione.  
  
 Per informazioni generali sulla funzioni in DMX, vedere [Data Mining Extensions &#40;DMX&#41; Function Reference](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
|Tipo di query|Funzioni supportate|Note|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM \<modello >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|Queste funzioni possono essere utilizzate per fornire valori massimi, valori minimi e medie per qualsiasi colonna che contenga un tipo di dati numerico, indipendentemente dal fatto che sia continua o sia stata discretizzata.|  
|[SELECT FROM \<modello >. CONTENUTO](../dmx/select-from-model-content-dmx.md)<br /><br /> oppure<br /><br /> [SELECT FROM \<modello >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Questa funzione recupera i nodi figlio per il nodo specificato nel modello e può essere utilizzata, ad esempio, per scorrere i nodi nel contenuto del modello di data mining. La disposizione dei nodi nel contenuto del modello di data mining dipende dal tipo di modello. Per informazioni sulla struttura per ogni tipo di modello di data mining, vedere [contenuto dei modelli di Data Mining &#40;Analysis Services - Data Mining&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).<br /><br /> Se il contenuto del modello di data mining è stato salvato come dimensione, è anche possibile utilizzare altre funzioni MDX (Multidimensional Expression) disponibili per l'esecuzione di query su una gerarchia di attributo.|  
|[SELECT FROM \<modello >. CASE](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [Classe ClientSettingsGeneralFlag](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|La funzione Lag è supportata solo per i modelli time series.<br /><br /> La funzione IsTestCase è supportata nei modelli che si basano su una struttura che è stata creata utilizzando l'opzione di controllo, per creare un set di dati di testing. Se il modello non è basato su una struttura con un set di test di controllo, tutti i case vengono considerati case di training.|  
|[SELECT FROM \<modello >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|In questo contesto, la funzione IsInNode restituisce un caso appartenente a un set di esempio idealizzati.|  
|SELECT FROM \<modello >. PMML|Non applicabile. Utilizzare la funzione XML.|Le rappresentazioni PMML sono supportate solo per i tipi di modello seguenti:<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees<br /><br /> [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering|  
|[SELECT FROM \<modello > PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|Funzioni di stima specifiche dell'algoritmo utilizzato per compilare il modello.|Per un elenco di funzioni di stima per ogni tipo di modello, vedere [query di Data Mining](../analysis-services/data-mining/data-mining-queries.md).|  
|[SELECT FROM \<modello >](../dmx/select-from-model-dmx.md)|Funzioni di stima specifiche dell'algoritmo utilizzato per compilare il modello.|Per un elenco di funzioni di stima per ogni tipo di modello, vedere [query di Data Mining](../analysis-services/data-mining/data-mining-queries.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
