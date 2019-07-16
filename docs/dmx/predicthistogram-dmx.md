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
ms.openlocfilehash: 61a90dc7fa034fc8983246aa4eb7119832a2d47d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008008"
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
 Un istogramma genera colonne di statistiche. La struttura della colonna dell'istogramma restituito dipende dal tipo di riferimento di colonna che viene usato con il **PredictHistogram** (funzione).  
  
## <a name="scalar-columns"></a>Colonne scalari  
 Per un \<riferimento a colonna scalare >, l'istogramma che il **PredictHistogram** restituito dalla funzione le colonne seguenti:  
  
-   Valore stimato.  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi di data mining non supportano **$ProbabilityVariance**. Per gli algoritmi [!INCLUDE[msCoName](../includes/msconame-md.md)] questa colonna contiene sempre 0.  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi di data mining non supportano **$ProbabilityStdev**. Per gli algoritmi [!INCLUDE[msCoName](../includes/msconame-md.md)] questa colonna contiene sempre 0.  
  
-   **$AdjustedProbability**  
  
     Il **$AdjustedProbability** colonna è un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] estensione per il [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB specifiche di Data Mining.  
  
## <a name="cluster-columns"></a>Colonne cluster  
 L'istogramma che il **PredictHistogram** funzione restituisce per una \<riferimento alla colonna del cluster > è costituito da colonne seguenti:  
  
-   **$Cluster** (rappresenta il nome del cluster)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito lo stato stimato della colonna Bike Buyer in una query singleton. La query restituisce anche gli stati più probabili prime due dell'attributo Bike Buyer, in base alla probabilità adattata ottenuta mediante il **PredictHistogram** (funzione).  
  
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
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
