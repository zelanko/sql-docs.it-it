---
title: Membri (set) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d3e5bb14455d2d2ea67c4187e8e1a2a420031944
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138260"
---
# <a name="members-set-mdx"></a>Members (Set) (MDX)


  Restituisce il set di membri di una dimensione, di un livello o di una gerarchia.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Hierarchy expression syntax  
Hierarchy_Expression.Members  
  
Level expression Syntax  
Level_Expression.Members  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hierarchy_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
## <a name="remarks"></a>Osservazioni  
 Se viene specificata un'espressione di gerarchia, la funzione **Members (set)** restituisce il set di tutti i membri all'interno della gerarchia specificata, esclusi i membri calcolati. Per ottenere il set di tutti i membri, calcolati o in altro modo, in una gerarchia utilizzare la funzione [AllMembers &#40;MDX&#41;](../mdx/allmembers-mdx.md)  
  
 Se viene specificata un'espressione di livello, la funzione **Members (set)** restituisce il set di tutti i membri all'interno del livello specificato.  
  
> [!IMPORTANT]  
>  Quando una dimensione contiene una sola gerarchia visibile, è possibile fare riferimento alla gerarchia con il nome della dimensione o della gerarchia poiché in questo scenario il nome della dimensione viene risolto in base all'unica gerarchia visibile che contiene. Measures.Members è ad esempio un'espressione MDX valida perché esegue la risoluzione nell'unica gerarchia nella dimensione Measures.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il set di tutti i membri contenuti nella gerarchia Calendar Year del cubo Adventure Works.  
  
```  
SELECT   
   [Date].[Calendar].[Calendar Year].Members ON 0  
FROM  
   [Adventure Works]  
  
```  
  
 Nell'esempio seguente vengono restituiti i quantitativi ordinati per il 2003 per ogni membro del livello `[Product].[Products].[Product Line]`. La funzione **Members** restituisce un set che rappresenta tutti i membri del livello.  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
