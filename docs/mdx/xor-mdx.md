---
title: XOR (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9115fc1e226e05c788206706d59a5435bfd1c5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251493"
---
# <a name="xor-mdx"></a>XOR (MDX)


  Esegue un'operazione di esclusione logica tra due espressioni numeriche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>Parametri  
 *Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un valore numerico.  
  
 *Expression2*  
 Espressione MDX valida che restituisce un valore numerico.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che restituisce **true** se un unico argomento restituisce **true**; in caso contrario, **false**.  
  
## <a name="remarks"></a>Note  
 Il **XOR** gestisce entrambi i parametri come valori booleani (zero, 0, come **false**; in caso contrario, **true**) prima di eseguire l'esclusione logica. La tabella seguente illustra come la **XOR** operatore esegue l'esclusione logica.  
  
|*Expression1*|*Expression2*|Valore restituito|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**false**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
