---
description: (divisione) (DMX)
title: Dividere (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2249701d074f12e0fc4dc3383d2e62b31ac275f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414067"
---
# <a name="divide-dmx"></a>(divisione) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Esegue un'operazione aritmetica di divisione di un numero per un altro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>Parametri  
 *Dividendo*  
 Espressione DMX (Data Mining Extensions) valida che restituisce un valore numerico.  
  
 *Divisore*  
 Espressione DMX valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore con il tipo di dati del parametro con precedenza maggiore.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore restituito da questo operatore rappresenta il quoziente della divisione tra la prima e la seconda espressione.  
  
 È necessario che alle due espressioni sia applicato lo stesso tipo di dati oppure che un'espressione possa essere convertita in modo implicito nel tipo di dati dell'altra espressione. Se il divisore restituisce un valore Null, verrà generato un errore. Se il divisore e il dividendo restituiscono entrambi un valore Null, l'operatore restituirà un valore Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori aritmetici &#40;&#41;DMX ](../dmx/operators-arithmetic.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Divide &#40;espressione SSIS&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;divide&#41; &#40;&#41;Transact-SQL ](../t-sql/language-elements/divide-transact-sql.md)  
  
  
