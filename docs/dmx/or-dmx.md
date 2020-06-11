---
title: O (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9ce963b2322e19e4e3a98982a88f99d3546cabc2
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83668733"
---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Operatore logico che esegue la disgiunzione logica di due espressioni numeriche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>Parametri  
 *Expression1*  
 Espressione DMX (Data Mining Extensions) valida che restituisce un valore numerico.  
  
 *Expression2*  
 Espressione DMX valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che restituisce TRUE se uno o entrambi gli argomenti restituiscono TRUE, FALSE in caso contrario.  
  
## <a name="remarks"></a>Commenti  
 Per consentire all'operatore di eseguire la disgiunzione logica, entrambi gli argomenti vengono gestiti come valori booleani, per cui 0 equivale a FALSE e tutti gli altri valori a TRUE. Se uno o entrambi gli argomenti restituiscono TRUE, l'operatore restituirà TRUE. Se *expression1* restituisce true e *expression2* restituisce false, l'operatore restituisce true.  
  
 La tabella seguente illustra come viene eseguita la disgiunzione logica.  
  
|Valore di Expression1|Valore di Expression2|Valore restituito|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatori logici &#40;&#41;DMX](../dmx/operators-logical.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
