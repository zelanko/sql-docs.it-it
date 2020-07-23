---
title: E (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea3cacd8fe2d80e6037cf83df9eea1fd112a4b05
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971828"
---
# <a name="and-dmx"></a>AND (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Esegue la congiunzione logica di due espressioni numeriche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>Parametri  
 *Expression1*  
 Espressione DMX (Data Mining Extensions) valida che restituisce un valore numerico.  
  
 *Expression2*  
 Espressione DMX valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che restituisce TRUE se entrambi i parametri restituiscono TRUE, FALSE in caso contrario.  
  
## <a name="remarks"></a>Osservazioni  
 Per consentire all'operatore di eseguire la congiunzione logica, entrambi i parametri vengono gestiti come valori booleani, per cui 0 equivale a FALSE e tutti gli altri valori a TRUE. Nella tabella seguente sono elencati i valori restituiti per le varie combinazioni dei valori dei parametri.  
  
|Valore di Expression1|Valore di Expression2|Valore restituito|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|FALSE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatori logici &#40;&#41;DMX](../dmx/operators-logical.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
