---
description: Item (Tuple) (MDX)
title: Elemento (tupla) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1e98e6901c018a6c8be5187024e5462cc8d19547
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483954"
---
# <a name="item-tuple-mdx"></a>Item (Tuple) (MDX)


  Restituisce una tupla da un set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *String_Expression1*  
 Espressione stringa valida che in genere è una tupla espressa come stringa.  
  
 *String_Expression2*  
 Espressione stringa valida che in genere è una tupla espressa come stringa.  
  
 *Index*  
 Espressione numerica valida che specifica la tupla in base alla posizione all'interno del set da restituire.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Item** restituisce una tupla dal set specificato. Esistono tre modi possibili per chiamare la funzione **Item** :  
  
-   Se viene specificata una singola espressione stringa, la funzione **Item** restituisce la tupla specificata. ad esempio "([2005].Q3, [Store05])".  
  
-   Se viene specificata più di un'espressione stringa, la funzione **Item** restituisce la tupla definita dalle coordinate specificate. Il numero di stringhe deve corrispondere al numero di assi e ogni stringa deve identificare una gerarchia univoca, ad esempio "[2005].Q3", "[Store05]".  
  
-   Se viene specificato un valore integer, la funzione **Item** restituisce la tupla che si trova nella posizione in base zero specificata da *index*.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito ([1996],Sales):  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 Nell'esempio seguente viene utilizzata un'espressione di livello e vengono restituiti l'importo delle vendite su Internet per ogni State-Province in Australia e la relativa percentuale sul totale delle vendite su Internet per l'Australia. In questo esempio viene utilizzata la funzione Item per estrarre la prima (e solo la tupla) dal set restituito dalla funzione **predecessori** .  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
