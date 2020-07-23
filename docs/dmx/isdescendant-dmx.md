---
title: Descendant (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bab465fe98c9509eaa99999a321317ee8013a74d
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969762"
---
# <a name="isdescendant-dmx"></a>IsDescendant (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Indica se il nodo corrente discende dal nodo specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>Tipo restituito  
 Tipo booleano.  
  
## <a name="remarks"></a>Osservazioni  
 IsSelected **viene usato** solo in [SELECT FROM &#60;Model&#62;. CONTENUTO &#40;&#41;DMX](../dmx/select-from-model-content-dmx.md) e [selezionare da &#60;modello&#62;. DIMENSION_CONTENT &#40;query&#41;DMX](../dmx/select-from-model-dimension-content-dmx.md) .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti tutti i case discendenti dal nodo specificato nella funzione IsDescendant.  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
