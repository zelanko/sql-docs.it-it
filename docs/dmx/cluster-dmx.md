---
title: Cluster (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa7df2782b8102e386c70d5e874a25f7868dbb1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071083"
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce il cluster che con maggiore probabilità contiene il case di input.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>Si applica a  
 È possibile utilizzare questa funzione solo se il modello di data mining sottostante supporta il clustering.  
  
## <a name="return-type"></a>Tipo restituito  
 Il **Cluster** funzione non richiede parametri.  
  
 Il **Cluster** funzione restituisce un valore scalare di un nome del cluster. Tuttavia, se si usa questa funzione come argomento di un'altra funzione, il risultato costituirà come un \<riferimento alla colonna del cluster >.  
  
## <a name="remarks"></a>Note  
 **Cluster** può essere utilizzato anche come un `<`riferimento a una colonna del cluster`>` per una **PredictHistogram** (funzione).  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente usa una query singleton con le [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) e alle funzioni di restituire la distanza del singolo case da ogni cluster del modello di data mining TM Clustering del Cluster e il probabilità che il singolo case esista in ogni cluster.  
  
```  
SELECT  
  PredictHistogram(Cluster())  
FROM  
  [TM Clustering]  
  NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
