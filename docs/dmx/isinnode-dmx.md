---
title: IsInNode (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 063c436f2e0d76ca891f332f25be385c2f16fdfa
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969663"
---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Indica se il nodo specificato contiene o meno il case corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>Tipo restituito  
 Tipo booleano.  
  
## <a name="remarks"></a>Osservazioni  
 **IsInNode** viene usato solo in [SELECT FROM &#60;Model&#62;. CASI &#40;&#41;DMX](../dmx/select-from-model-cases-dmx.md) e [selezionare da &#60;modello&#62;. SAMPLE_CASES &#40;query&#41;DMX](../dmx/select-from-model-sample-cases-dmx.md) .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti tutti i case utilizzati per creare il modello associato al nodo specificato nella funzione IsInNode.  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
