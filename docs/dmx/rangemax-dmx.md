---
title: RangeMax (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 08882071e142fa97139dc2a89adffaa8e5d5f738
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970668"
---
# <a name="rangemax-dmx"></a>RangeMax (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Restituisce il limite superiore del bucket stimato individuato per una colonna discretizzata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RangeMax(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Colonne scalari.  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **RangeMax** può essere utilizzata in [SELECT DISTINCT FROM &#60;Model &#62; &#40;query DMX&#41;](../dmx/select-distinct-from-model-dmx.md) . Quando viene utilizzato con questo tipo di query, il riferimento alla colonna scalare può contenere colonne discrete o continue stimabili o di input.  
  
 Se utilizzata con [SELECT FROM &#60;model&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), le funzioni **RangeMin**, **RangeMid**e **RangeMax** restituiscono i valori limite effettivi del bucket specificato. Se ad esempio si esegue una stima su una colonna discretizzata, la query restituirà il numero del bucket stimato nella colonna discretizzata. Le funzioni **RangeMin**, **RangeMid**e **RangeMax** descrivono il bucket specificato dalla stima. Quando si utilizza la funzione **RangeMax** con un'istruzione PREDICTION JOIN, il riferimento alla colonna scalare può contenere solo colonne discrete e stimabili.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i valori minimi, massimi e medi della colonna continua Yearly Income nel modello di data mining TM Decision Tree.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)   
 [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
  
