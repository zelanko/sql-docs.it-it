---
description: '&lt;&gt; (Diverso da) DMX'
title: '&lt;&gt; (Diverso da) (DMX) | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8aebff9e74a7c310a2af650c0cebbcaed2c91e9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426223"
---
# <a name="ltgt-not-equal-to-dmx"></a>&lt;&gt; (Diverso da) DMX
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Esegue un'operazione di confronto che determina se il valore di un'espressione DMX (Data Mining Extensions) è diverso da quello di un'altra espressione DMX.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DMX_Expression <> DMX_Expression  
```  
  
#### <a name="parameters"></a>Parametri  
 *DMX_Expression*  
 Espressione DMX valida.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che contiene TRUE se entrambi i parametri sono non Null e il valore del primo parametro è diverso da quello del secondo. Tale valore booleano contiene FALSE se entrambi i parametri sono non Null e il valore del primo parametro è uguale a quello del secondo. Il valore booleano contiene un valore Null se un parametro o entrambi restituiscono un valore Null.  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori di confronto &#40;DMX&#41;](../dmx/operators-comparison.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
