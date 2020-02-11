---
title: SetToArray (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c52c2641d21c20c91ec7548cafc969e506801b08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036987"
---
# <a name="settoarray-mdx"></a>SetToArray (MDX)


  Converte uno o più set in una matrice da utilizzare in una funzione definita dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SetToArray(Set_Expression1 [ ,Set_Expression2,...n ][ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **SetToArray** converte uno o più set in una matrice da utilizzare in una funzione definita dall'utente. Il numero di dimensioni nella matrice risultante corrisponde al numero di set specificati.  
  
 L'espressione numerica facoltativa può specificare i valori per le celle della matrice. Se non viene specificata un'espressione numerica, il cross join dei set viene valutato nel contesto corrente.  
  
 Le coordinate delle celle nella matrice risultante corrispondono alla posizione dei set nell'elenco. Ad esempio, per i tre set `SA`, `SB` e `SC`, ognuno dei quali contiene due elementi, l'istruzione MDX `SetToArray(SA, SB, SC)` crea la matrice tridimensionale seguente:  
  
```  
(SA1, SB1, SC1) (SA2, SB1, SC1) (SA1, SB2, SC1) (SA2, SB2, SC1)   
(SA1, SB1, SC2) (SA2, SB1, SC2) (SA1, SB2, SC2) (SA2, SB2, SC2)   
```  
  
> [!NOTE]  
>  Il tipo restituito della funzione **SetToArray** è il tipo VARIANT, VT_ARRAY. Pertanto, l'output della funzione **SetToArray** deve essere utilizzato solo come input per una funzione definita dall'utente.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita una matrice.  
  
```  
SetToArray([Geography].[Geography].Members, [Measures].[Internet Sales Amount])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
