---
title: NOT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 98c40dba282c82f124d4e4ac009a046a44a283cb
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971633"
---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Operatore logico che esegue la negazione logica di un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parametri  
 *Expression1*  
 Espressione DMX valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che restituisce FALSE se l'argomento restituisce TRUE e viceversa.  
  
## <a name="remarks"></a>Osservazioni  
 Per consentire all'operatore di eseguire la negazione logica, l'argomento viene gestito come valore booleano, per cui 0 equivale a FALSE e tutti gli altri valori a TRUE. Se *expression1* è true, l'operatore restituisce false. Se *expression1* è false, l'operatore restituisce true. La tabella seguente illustra come viene eseguita la negazione logica.  
  
|Valore di Expression1|Valore restituito|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatori logici &#40;&#41;DMX](../dmx/operators-logical.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
