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
ms.openlocfilehash: 2ef32a9e133c199aae0779c819736d77e0d15c45
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670066"
---
# <a name="isdescendant-dmx"></a>IsDescendant (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica se il nodo corrente discende dal nodo specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>Tipo restituito  
 Tipo booleano.  
  
## <a name="remarks"></a>Commenti  
 IsSelected **viene usato** solo in [SELECT FROM &#60;Model&#62;. CONTENUTO &#40;&#41;DMX](../dmx/select-from-model-content-dmx.md) e [selezionare da &#60;modello&#62;. DIMENSION_CONTENT &#40;query&#41;DMX](../dmx/select-from-model-dimension-content-dmx.md) .  
  
## <a name="examples"></a>Esempio  
 Nell'esempio seguente vengono restituiti tutti i case discendenti dal nodo specificato nella funzione IsDescendant.  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
