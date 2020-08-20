---
description: Ancestor (MDX)
title: Predecessore (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9e08a0f281a9e48c3416bb00f6ee47322d554d9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461663"
---
# <a name="ancestor-mdx"></a>Ancestor (MDX)


  Funzione che restituisce il predecessore di un membro specificato al livello specificato oppure alla distanza specificata dal membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Level syntax  
Ancestor(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestor(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
 *Distanza*  
 Espressione numerica valida che specifica la distanza dal membro specificato.  
  
## <a name="remarks"></a>Osservazioni  
 Con la funzione **predecessore** , si fornisce la funzione con un'espressione di membro MDX e quindi si fornisce un'espressione MDX di un livello che è un predecessore del membro o un'espressione numerica che rappresenta il numero di livelli al di sopra di tale membro. Con queste informazioni, la funzione **progenitori** restituisce il membro predecessore a tale livello.  
  
> [!NOTE]  
>  Per restituire un set contenente il membro predecessore, anziché solo il membro predecessore, usare i predecessori [&#40;funzione MDX&#41;](../mdx/ancestors-mdx.md) .  
  
 Se viene specificata un'espressione di livello, la funzione **predecessore** restituisce il predecessore del membro specificato al livello specificato. Se il membro specificato non è incluso nella stessa gerarchia del livello specificato, la funzione restituisce un errore.  
  
 Se viene specificata una distanza, la funzione **predecessore** restituisce il predecessore del membro specificato che corrisponde al numero di passaggi specificato nella gerarchia specificata dall'espressione del membro. Un membro può essere specificato come membro di una gerarchia dell'attributo, una gerarchia definita dall'utente o, in alcuni casi, una gerarchia padre-figlio. Con il numero 1 viene restituito l'elemento padre di un membro, mentre con il numero 2 viene restituito l'elemento padre del padre di un membro, se esistente. Il numero 0 restituisce il membro stesso.  
  
> [!NOTE]  
>  Utilizzare questo formato della funzione **predecessore** per i casi in cui il livello dell'elemento padre è sconosciuto o non può essere denominato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata un'espressione di livello e vengono restituiti l'importo delle vendite su Internet per ogni State-Province in Australia e la relativa percentuale sul totale delle vendite su Internet per l'Australia.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
   [Measures].[Internet Sales Amount],    
      Ancestor   
         (  
         [Customer].[Customer Geography].CurrentMember,  
            [Customer].[Customer Geography].[Country]  
         )  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
        [Customer].[Customer Geography].[Country].&[Australia],  
           [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene utilizzata un'espressione numerica e vengono restituiti l'importo delle vendite su Internet per ogni State-Province in Australia e la relativa percentuale sul totale delle vendite su Internet per tutti i paesi.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
      [Measures].[Internet Sales Amount],  
         Ancestor   
            ([Customer].[Customer Geography].CurrentMember, 2)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
         [Customer].[Customer Geography].[Country].&[Australia],  
            [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
