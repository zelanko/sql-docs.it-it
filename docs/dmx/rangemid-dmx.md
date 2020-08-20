---
description: RangeMid (DMX)
title: RangeMid (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f6645750341fff6ba15438503956d5be5e8662f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500906"
---
# <a name="rangemid-dmx"></a>RangeMid (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Restituisce il punto medio del bucket stimato individuato per una colonna discretizzata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Colonne scalari discretizzate.  
  
## <a name="return-type"></a>Tipo restituito  
 Valore scalare.  
  
## <a name="remarks"></a>Osservazioni  
 Se utilizzata con [SELECT FROM &#60;model&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), le funzioni **RangeMin**, **RangeMid**e **RangeMax** restituiscono i valori limite effettivi del bucket specificato. Se ad esempio si esegue una stima su una colonna discretizzata, la query restituirà il numero del bucket stimato nella colonna discretizzata. Le funzioni **RangeMin**, **RangeMid**e **RangeMax** descrivono il bucket specificato dalla stima. Quando si utilizza la funzione **RangeMid** con un'istruzione PREDICTION JOIN, il riferimento alla colonna scalare può contenere solo colonne discrete e stimabili.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti i valori minimi, massimi e medi della colonna continua Yearly Income in un modello di data mining TM Decision Tree.  
  
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
 [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)   
 [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
  
