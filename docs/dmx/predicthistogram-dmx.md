---
title: PredictHistogram (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fdc63d1c93d1290c701233cb94f71f157c771182
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893855"
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce una tabella che rappresenta un istogramma per la stima di una colonna specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Riferimento a colonna scalare o riferimento a colonna cluster. Può essere utilizzata con tutti i tipi di algoritmi, a eccezione di [!INCLUDE[msCoName](../includes/msconame-md.md)] Association Rules.  
  
## <a name="return-type"></a>Tipo restituito  
 Tabella.  
  
## <a name="remarks"></a>Note  
 Un istogramma genera colonne di statistiche. La struttura delle colonne dell'istogramma restituito dipende dal tipo di riferimento di colonna usato con la funzione **PredictHistogram** .  
  
## <a name="scalar-columns"></a>Colonne scalari  
 Per un \<riferimento a colonna scalare >, l'istogramma restituito dalla funzione **PredictHistogram** è costituito dalle colonne seguenti:  
  
-   Valore stimato.  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]gli algoritmi di data mining non supportano **$ProbabilityVariance**. Per gli algoritmi [!INCLUDE[msCoName](../includes/msconame-md.md)] questa colonna contiene sempre 0.  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]gli algoritmi di data mining non supportano **$ProbabilityStdev**. Per gli algoritmi [!INCLUDE[msCoName](../includes/msconame-md.md)] questa colonna contiene sempre 0.  
  
-   **$AdjustedProbability**  
  
     La colonna **$AdjustedProbability** è un' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] estensione della OLE DB [!INCLUDE[msCoName](../includes/msconame-md.md)] per la specifica di data mining.  
  
## <a name="cluster-columns"></a>Colonne cluster  
 L'istogramma restituito dalla funzione **PredictHistogram** per un \<riferimento a una colonna cluster > è costituito dalle colonne seguenti:  
  
-   **$Cluster** (rappresenta il nome del cluster)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito lo stato stimato della colonna Bike Buyer in una query singleton. La query restituisce anche i primi due stati più probabili dell'attributo Bike Buyer, in base alla probabilità adattata ottenuta tramite la funzione **PredictHistogram** .  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Guida di riferimento &#40;alle&#41; funzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni &#40;di stima generali DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
