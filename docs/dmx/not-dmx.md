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
manager: kfile
ms.openlocfilehash: 053eb905edb1379bfdc40ec010dc6d4efadcba26
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62503850"
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
  
## <a name="remarks"></a>Note  
 Per consentire all'operatore di eseguire la negazione logica, l'argomento viene gestito come valore booleano, per cui 0 equivale a FALSE e tutti gli altri valori a TRUE. Se *Expression1* è TRUE, l'operatore restituisce FALSE. Se *Expression1* è FALSE, l'operatore restituisce TRUE. La tabella seguente illustra come viene eseguita la negazione logica.  
  
|Valore di Expression1|Valore restituito|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Gli operatori logici &#40;DMX&#41;](../dmx/operators-logical.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
