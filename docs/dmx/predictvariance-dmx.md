---
description: PredictVariance (DMX)
title: PredictVariance (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 49791a6f1db662735be529e2f39fb347f8f858fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487751"
---
# <a name="predictvariance-dmx"></a>PredictVariance (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Restituisce la varianza di una colonna specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
PredictVariance(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Colonna scalare.  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare del tipo specificato da *\<scalar column reference>* .  
  
## <a name="remarks"></a>Osservazioni  
 Se il riferimento alla colonna è discreto, **PredictVariance** restituisce 0 perché la varianza non può essere calcolata da valori discreti.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato un natural prediction join per determinare la probabilità che un individuo sia un acquirente di biciclette sulla base del modello di data mining TM Decision Tree e la varianza per la stima.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictVariance([Bike Buyer]) AS [Variance]  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
