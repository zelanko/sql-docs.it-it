---
description: Guida di riferimento alle funzioni DMX (Data Mining Extensions)
title: Guida di riferimento alle funzioni DMX (Data Mining Extensions) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3066c971a434f1fab0dd2963003d53e37585983a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414147"
---
# <a name="data-mining-extensions-dmx-function-reference"></a>Guida di riferimento alle funzioni DMX (Data Mining Extensions)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta molte funzioni del linguaggio DMX (Data Mining Extensions). Le funzioni consentono di espandere i risultati di una query di stima in modo da includere informazioni che descrivono ulteriormente la stima. Tramite le funzioni è inoltre possibile ottenere un maggiore controllo sulla modalità con cui vengono restituiti i risultati della stima. Nella tabella seguente vengono forniti i collegamenti alle risorse che illustrano come utilizzare le funzioni in DMX.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)|Vengono elencate le funzioni che è possibile utilizzare con tutti i tipi di modelli e vengono forniti i collegamenti a ulteriori informazioni sull'esecuzione di query su tipi specifici di modelli di data mining.|  
|[Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|Viene fornita una panoramica della costruzione di una query di stima mediante DMX.|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|Restituisce una tabella che contiene un numero specificato di righe a partire dall'ultima, in ordine di rango crescente in base a un'espressione di rango.|  
  
 Nella tabella seguente vengono elencate le funzioni supportate da DMX.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|Restituisce una tabella che contiene le ultime righe di n elementi dell'espressione di tabella in ordine crescente in base all'espressione di rango.|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|Restituisce una tabella che contiene il più piccolo numero di righe, a partire dall'ultima, che consente di ottenere la percentuale restituita da un'espressione specificata, in ordine di rango crescente in base a un'espressione di rango.|  
|[BottomSum &#40;DMX&#41;](../dmx/bottomsum-dmx.md)|Restituisce una tabella che contiene il più piccolo numero di righe, a partire dall'ultima, che consente di ottenere la somma restituita da un'espressione specificata, in ordine di rango crescente in base a un'espressione di rango.|  
|[Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)|Restituisce il cluster che con maggiore probabilità contiene il case di input.|  
|[ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)|Restituisce la probabilità che il case di input appartenga al cluster.|  
|[Esistente &#40;DMX&#41;](../dmx/exists-dmx.md)|Restituisce true se il set di risultati restituito dall'istruzione SELECT specificata contiene almeno una riga.|  
|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Indica se il nodo corrente discende dal nodo specificato.|  
|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|Indica se il nodo specificato contiene o meno il case specificato.|  
|[IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|Indica se un case appartiene al set di test case.|  
|[IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)|Indica se un case appartiene al set di case di training.|  
|[Lag &#40;DMX&#41;](../dmx/lag-dmx.md)|Restituisce l'intervallo di tempo tra la data del case corrente e l'ultima data presente nei dati.|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|Esegue una stima su una colonna specificata.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)|Restituisce la probabilità adattata della colonna stimabile specificata.|  
|[PredictAssociation &#40;DMX&#41;](../dmx/predictassociation-dmx.md)|Consente di stimare l'appartenenza associativa in una colonna.|  
|[PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md)|Restituisce la probabilità che un case di input risulti adatto al modello esistente. Questa funzione può essere utilizzata solo con i modelli di clustering.|  
|[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)|Restituisce una tabella che rappresenta l'istogramma per una colonna specificata.|  
|[PredictNodeId &#40;DMX&#41;](../dmx/predictnodeid-dmx.md)|Restituisce il NodeID del case selezionato.|  
|[PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)|Restituisce la probabilità della colonna specificata.|  
|[PredictSequence &#40;DMX&#41;](../dmx/predictsequence-dmx.md)|Stima i valori successivi in una sequenza.|  
|[PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)|Recupera il valore della deviazione standard per una colonna specificata.|  
|[PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)|Restituisce il valore di supporto della colonna.|  
|[PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md)|Stima i valori futuri di una serie temporale.|  
|[PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)|Restituisce il valore della varianza della colonna specificata.|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|Restituisce il limite superiore del bucket stimato individuato per una colonna discretizzata specificata.|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)|Restituisce il punto medio del bucket stimato individuato per una colonna discretizzata specificata.|  
|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|Restituisce il limite inferiore del bucket stimato individuato per una colonna discretizzata specificata.|  
|[StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)|Restituisce il valore della colonna della struttura di data mining della tabella specificata.|  
|[Conteggio &#40;DMX&#41;](../dmx/topcount-dmx.md)|Restituisce una tabella che contiene un numero specificato di righe a partire dalla prima, in ordine di rango decrescente in base a un'espressione di rango.|  
|[Percentuale &#40;DMX&#41;](../dmx/toppercent-dmx.md)|Restituisce una tabella che contiene il più piccolo numero di righe, a partire dalla prima, che consente di ottenere la percentuale restituita da un'espressione specificata, in ordine di rango decrescente in base a un'espressione di rango.|  
|[&#40;DMX&#41;](../dmx/topsum-dmx.md)|Restituisce una tabella che contiene il più piccolo numero di righe, a partire dalla prima, che consente di ottenere la somma restituita da un'espressione specificata, in ordine di rango decrescente in base a un'espressione di rango.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
