---
title: '&lt;(Minore di) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 54cf739762944683b1fe9063aa3e79896639ffc4
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969212"
---
# <a name="lt-less-than-dmx"></a>&lt;(Minore di) DMX
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Esegue un'operazione di confronto che determina se il valore di un'espressione DMX (Data Mining Extensions) è minore di quello di un'altra espressione DMX.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DMX_Expression < DMX_Expression  
```  
  
#### <a name="parameters"></a>Parametri  
 *DMX_Expression*  
 Espressione DMX valida.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che contiene TRUE se entrambi i parametri sono non Null e il valore del primo parametro è minore di quello del secondo. Tale valore booleano contiene FALSE se entrambi i parametri sono non Null e il valore del primo parametro è maggiore o uguale a quello del secondo. Il valore booleano contiene un valore Null se un parametro o entrambi restituiscono un valore Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori di confronto &#40;DMX&#41;](../dmx/operators-comparison.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
