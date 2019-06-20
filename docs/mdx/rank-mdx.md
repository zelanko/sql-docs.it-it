---
title: Rank (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1d234f02c8dfcd36073059210c1999cb95f5ab0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200669"
---
# <a name="rank-mdx"></a>Rank (MDX)


  Restituisce il rango in base uno di una tupla specificata in un set specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Rank(Tuple_Expression, Set_Expression [ ,Numeric Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Tuple_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una tupla.  
  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Note  
 Se viene specificata un'espressione numerica, la **Rank** funzione determina il rango in base uno della tupla specificata valutando l'espressione numerica specificata in base alla tupla. Se viene specificata un'espressione numerica, la **Rank** funzione assegna lo stesso rango alle tuple con valori duplicati nel set. L'assegnazione dello stesso rango a valori duplicati influisce sui ranghi delle tuple successive del set. Si supponga, ad esempio, che un set sia composto dalle tuple `{(a,b), (e,f), (c,d)}`. In questo caso il valore della tupla `(a,b)` corrisponde a quello della tupla `(c,d)`. Se il rango della tupla `(a,b)` è 1, anche il rango di `(a,b)` e `(c,d)` sarà 1. Il rango della tupla `(e,f)`, tuttavia, sarà 3. Questo set non può contenere tuple con rango 2.  
  
 Se non viene specificata un'espressione numerica, la **Rank** funzione restituisce la posizione ordinale in base uno della tupla specificata.  
  
 Il **Rank** funzione non esegue alcun ordinamento del set.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente restituisce il set di tuple contenente i clienti e le date di acquisto, utilizzando il **filtro**, **NonEmpty**, **elemento**, e **Rank** funzioni per individuare l'ultima data in cui ogni cliente ha eseguito un acquisto.  
  
```  
WITH SET MYROWS AS FILTER  
   (NONEMPTY  
      ([Customer].[Customer Geography].MEMBERS  
         * [Date].[Date].[Date].MEMBERS  
         , [Measures].[Internet Sales Amount]  
      ) AS MYSET  
   , NOT(MYSET.CURRENT.ITEM(0)  
      IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))  
   )  
SELECT [Measures].[Internet Sales Amount] ON 0,  
MYROWS ON 1  
FROM [Adventure Works]  
```  
  
 L'esempio seguente usa il **ordine** funzione, anziché **Rank** funzione per classificare i membri della gerarchia City in base alla misura Reseller Sales Amount e visualizzarli in ordine di rango. Tramite il **ordine** funzione per ordinare il set di membri della gerarchia City, l'ordinamento viene eseguito una sola volta ed è seguito da un'analisi lineare prima di essere visualizzato in modo ordinato.  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Ordine di &#40;MDX&#41;](../mdx/order-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
