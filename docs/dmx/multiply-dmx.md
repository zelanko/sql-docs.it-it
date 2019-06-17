---
title: '* (Moltiplicazione) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f73e3e55045dd4ea9d4c2476540d2f7223d16eb0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62502075"
---
# <a name="-multiply-dmx"></a>* (moltiplicazione) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Esegue un'operazione aritmetica di moltiplicazione tra due numeri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parametri  
 *Numeric_Expression*  
 Espressione DMX (Data Mining Extensions) valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore con il tipo di dati del parametro con precedenza maggiore.  
  
## <a name="remarks"></a>Note  
 È necessario che alle due espressioni sia applicato lo stesso tipo di dati oppure che un'espressione possa essere convertita in modo implicito nel tipo di dati dell'altra espressione. Se una delle due espressioni restituisce un valore Null, l'operatore restituirà un valore Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori aritmetici &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
