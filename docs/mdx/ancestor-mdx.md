---
title: Predecessore (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 464f8504850c6aa13f1cf040f9429be56f7181be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298494"
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
  
 *distanza*  
 Espressione numerica valida che specifica la distanza dal membro specificato.  
  
## <a name="remarks"></a>Note  
 Con il **predecessore** (funzione), specifica la funzione con un'espressione di membro MDX e quindi specificare un'espressione MDX di un livello predecessore del membro oppure un'espressione numerica che rappresenta il numero di livelli sopra tale membro. Con queste informazioni, il **predecessori** funzione restituisce il membro predecessore a tale livello.  
  
> [!NOTE]  
>  Per restituire un set contenente il membro predecessore, anziché il solo membro predecessore, utilizzare il [predecessori &#40;MDX&#41; ](../mdx/ancestors-mdx.md) (funzione).  
  
 Se viene specificata un'espressione di livello, il **predecessore** funzione restituisce il predecessore del membro specificato al livello specificato. Se il membro specificato non è incluso nella stessa gerarchia del livello specificato, la funzione restituisce un errore.  
  
 Se viene specificata una distanza, la **predecessore** funzione restituisce il predecessore del membro specificato che corrisponde al numero di passaggi specificato nella gerarchia specificata dall'espressione di membro. Un membro può essere specificato come membro di una gerarchia dell'attributo, una gerarchia definita dall'utente o, in alcuni casi, una gerarchia padre-figlio. Con il numero 1 viene restituito l'elemento padre di un membro, mentre con il numero 2 viene restituito l'elemento padre del padre di un membro, se esistente. Il numero 0 restituisce il membro stesso.  
  
> [!NOTE]  
>  Utilizzare questa forma del **predecessore** funzione nei casi in cui il livello dell'elemento padre è sconosciuto o non può essere rinominato.  
  
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
  
  
