---
description: Item (Member) (MDX)
title: Elemento (membro) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a374d1fcc7f972828832c2f82375acf640d45fb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483964"
---
# <a name="item-member-mdx"></a>Item (Member) (MDX)


  Restituisce un membro da una tupla specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Tuple_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una tupla.  
  
 *Index*  
 Espressione numerica valida che specifica il membro specifico in base alla posizione nella tupla da restituire.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Item** restituisce un membro dalla tupla specificata. La funzione restituisce il membro trovato nella posizione in base zero specificata da *index*.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il membro `[2003]`, ovvero il primo elemento nella tupla `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).`, nelle colonne:  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
