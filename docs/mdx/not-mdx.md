---
description: NOT (MDX)
title: NOT (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6c0cfa43896457397f2e2e08bac0b3de1d61e73f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471783"
---
# <a name="not-mdx"></a>NOT (MDX)


  Esegue la negazione logica di un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parametri  
 *Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che restituisce **false** se l'argomento restituisce **true**. in caso contrario, **true**.  
  
## <a name="remarks"></a>Osservazioni  
 L'operatore **not** considera l'espressione come un valore booleano (zero, 0, come **false**; in caso contrario, **true**) prima che l'operatore esegua la negazione logica. Nella tabella seguente viene illustrato il modo in cui l'operatore **not** esegue la negazione logica.  
  
|*Expression1*|Valore restituito|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)  
  
  
