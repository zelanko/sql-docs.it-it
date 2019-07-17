---
title: Conteggio (Dimension) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b84c5a1902e80f8abe3828f4be1b5d570ec026ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104809"
---
# <a name="count-dimension-mdx"></a>Count (Dimension) (MDX)


  Restituisce il numero di gerarchie in un cubo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Note  
 Restituisce il numero di gerarchie di un cubo, inclusa la gerarchia `[Measures].[Measures]`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il numero delle gerarchie presenti nel cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Conteggio &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Conteggio &#40;livelli di gerarchia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
