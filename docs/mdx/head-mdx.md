---
title: Head (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e6d8da7a5813f7e99c022e19f18de2800598885
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67906003"
---
# <a name="head-mdx"></a>Head (MDX)


  Restituisce il primo numero specificato di elementi in un set, mantenendo i duplicati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numero*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Head** restituisce il numero specificato di Tuple dall'inizio del set specificato. L'ordine degli elementi viene mantenuto. Il valore predefinito di Count è 1. Se il numero specificato di Tuple è minore di 1, la funzione **Head** restituisce un set vuoto. Se il numero di tuple specificato supera il numero di tuple nel set, la funzione restituisce il set originale.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono restituite le cinque sottocategorie di prodotti più vendute, indipendentemente dalla gerarchia, in base al profitto lordo del rivenditore. La funzione **Head** viene utilizzata per restituire solo i primi 5 set nel risultato dopo che il risultato viene ordinato utilizzando la funzione **Order** .  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Tail &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [Elemento &#40;tupla&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [Elemento &#40;membro&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [Rango &#40;MDX&#41;](../mdx/rank-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
