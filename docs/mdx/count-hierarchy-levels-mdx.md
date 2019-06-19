---
title: Conteggio (livelli di gerarchia) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 657ce658704b519c31dfaa2186429a7df4110308
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63306812"
---
# <a name="count-hierarchy-levels-mdx"></a>Count (Hierarchy Levels) (MDX)


  Restituisce il numero di livelli in una gerarchia.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hierarchy_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
## <a name="remarks"></a>Note  
 Restituisce il numero di livelli in una gerarchia, incluso il livello `[All]` se pertinente.  
  
> [!IMPORTANT]  
>  Quando una dimensione contiene una sola gerarchia visibile, è possibile fare riferimento alla gerarchia con il nome della dimensione o della gerarchia poiché il nome della dimensione viene risolto in base all'unica gerarchia visibile che contiene. `Measures.Levels.Count` è ad esempio un'espressione MDX valida perché esegue la risoluzione nell'unica gerarchia nella dimensione Measures.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il numero dei livelli presenti nella gerarchia definita dall'utente Product Categories del cubo Adventure Works.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Conteggio &#40;dimensione&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Count &#40;Tuple&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
