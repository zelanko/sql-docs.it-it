---
title: NOT (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4031b887eb0a42580d6ae8debf6c9177ff67efc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088231"
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
 Valore booleano che restituisce **false** se l'argomento restituisce **true**; in caso contrario, **true**.  
  
## <a name="remarks"></a>Note  
 Il **non** gestisce l'espressione come un valore booleano (zero, 0, come **false**; in caso contrario, **true**) prima che l'operatore esegue la negazione logica. La tabella seguente illustra come la **non** operatore esegue la negazione logica.  
  
|*Expression1*|Valore restituito|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
