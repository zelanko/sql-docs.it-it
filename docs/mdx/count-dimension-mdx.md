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
manager: kfile
ms.openlocfilehash: 6ee8fe09f7a840d32511d3a208a4621612ee9939
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63285048"
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
 [Count &#40;Tuple&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Conteggio &#40;livelli di gerarchia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
