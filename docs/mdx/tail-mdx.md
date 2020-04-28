---
title: Tail (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d48a374d7d84c1137f082eb12dec638557b14e5a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036658"
---
# <a name="tail-mdx"></a>Tail (MDX)


  Restituisce un subset dalla fine di un set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Tail(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numero*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **tail** restituisce il numero specificato di Tuple dalla fine del set specificato. L'ordine degli elementi viene mantenuto. Il valore predefinito di *count* è 1. Se il numero specificato di tuple è minore di 1, la funzione restituisce il set vuoto. Se il numero di tuple specificato supera il numero di tuple nel set, la funzione restituisce il set originale.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita la misura Reseller Sales per le cinque sottocategorie di prodotti più vendute, indipendentemente dalla gerarchia, in base a Reseller Gross Profit. La funzione **tail** viene utilizzata per restituire solo gli ultimi cinque set nel risultato dopo che il risultato viene ordinato in ordine inverso utilizzando la funzione **Order** .  
  
```  
SELECT Tail  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BASC  
      )  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
