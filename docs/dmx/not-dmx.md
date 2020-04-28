---
title: NOT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4a28c6be2c956636f303ccc561936f799c63b64
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68008247"
---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
