---
title: IsInNode (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e4c7df84bc7bf3a4804db76d952b1219100ef5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008365"
---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
