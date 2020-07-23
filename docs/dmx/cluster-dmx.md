---
title: Cluster (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0cd7b2e0a78f2d47349de2701572b2f9dc4b0095
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969922"
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Restituisce il cluster che con maggiore probabilità contiene il case di input.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>Si applica a  
 È possibile utilizzare questa funzione solo se il modello di data mining sottostante supporta il clustering.  
  
## <a name="return-type"></a>Tipo restituito  
 La funzione **cluster** non richiede parametri.  
  
 La funzione **cluster** restituisce un valore scalare di un nome di cluster. Tuttavia, se si utilizza questa funzione come argomento di un'altra funzione, è necessario considerarla come \<cluster column reference> .  
  
## <a name="remarks"></a>Osservazioni  
 Il **cluster** può essere usato anche come `<` riferimento a una colonna cluster `>` per una funzione **PredictHistogram** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata una query singleton con [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) e funzioni cluster per restituire la distanza del singolo case da ogni cluster del modello di data mining TM clustering e la probabilità che il singolo case sia presente in ogni cluster.  
  
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
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
