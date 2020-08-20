---
description: Min (MDX)
title: Min (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c93abf0f98b04994f028379b8bd576deff4b7ea1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483814"
---
# <a name="min-mdx"></a>Min (MDX)


  Restituisce il valore minimo di un'espressione numerica valutata su un set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Min( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Osservazioni  
 Se si specifica un'espressione numerica, questa viene valutata sull'intero set e restituisce il valore minimo di tale valutazione. Se non viene specificata un'espressione numerica, il set specificato viene valutato nel contesto corrente dei membri del set e viene restituito il valore minimo di tale valutazione.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora i valori Null durante il calcolo del valore minimo di un set di numeri.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il valore minimo delle vendite trimestrali per ogni sottocategoria e paese del cubo Adventure Works.  
  
```  
WITH MEMBER Measures.x AS Min   
   ([Date].[Calendar].CurrentMember.Children  
      , [Measures].[Reseller Order Quantity]  
   )  
SELECT Measures.x ON 0  
,NON EMPTY [Date].[Calendar].[Calendar Quarter]*   
   [Product].[Product Categories].[Subcategory].members *  
   [Geography].[Geography].[Country].Members  
ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
