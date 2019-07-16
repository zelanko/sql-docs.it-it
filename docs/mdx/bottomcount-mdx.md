---
title: BottomCount (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bd09c823e09270ebf7c9851b3c6760baf720db39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016954"
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)


  Dispone un set in ordine crescente e restituisce il numero specificato di tuple nel set specificato con i valori più bassi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Count*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Note  
 Se si specifica un'espressione numerica, la funzione dispone in ordine crescente le tuple nel set specificato in base al valore dell'espressione numerica specificata, valutato sul set. Il **BottomCount** funzione restituisce quindi il numero specificato di tuple con valore più basso.  
  
> [!IMPORTANT]  
>  Il **BottomCount** funzione, come le [TopCount](../mdx/topcount-mdx.md) function, rispetta mai la gerarchia.  
  
 Se non viene specificata un'espressione numerica, la funzione restituisce il set di membri in ordine naturale, senza alcun ordinamento, analogamente i [Tail (MDX)](../mdx/tail-mdx.md) (funzione).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita la misura Reseller Order Quantity per ogni anno di calendario per le cinque sottocategorie di prodotti meno vendute, ordinate in base alla misura Reseller Sales Amount.  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
