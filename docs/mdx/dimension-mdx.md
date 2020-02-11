---
title: Dimension (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 58bee93a4cef37a8a5a71211b292a16392687f12
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67999955"
---
# <a name="dimension-mdx"></a>Dimension (MDX)


  Restituisce la gerarchia contenente il membro, il livello o la gerarchia specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.Dimension  
  
Level syntax  
Level_Expression.Dimension  
  
Member syntax  
Member_Expression.Dimension  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hierarchy_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
### <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata la funzione **Dimension** , in combinazione con la funzione **Name** , per restituire il nome della gerarchia del membro specificato.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Name  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente la funzione Dimension viene utilizzata in combinazione con le funzioni Levels e Count per restituire il numero di livelli presenti nella gerarchia che contiene il membro specificato.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene utilizzata la funzione **Dimension** , in combinazione con i **membri** e le funzioni **count** , per restituire il numero di membri nella gerarchia che contiene il membro specificato.  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Conteggio &#40;livelli di gerarchia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Conteggio &#40;set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [Livelli &#40;&#41;MDX](../mdx/levels-mdx.md)   
 [Membri &#40;set&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
