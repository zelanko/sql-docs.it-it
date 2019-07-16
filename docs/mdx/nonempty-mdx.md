---
title: NonEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45daf970f69322cad36bbe5419bf1dc8cc8009b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088337"
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)


  Restituisce il set delle tuple non vuote da un set specificato, in base al prodotto incrociato tra il set specificato e un secondo set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
NONEMPTY(set_expression1 [,set_expression2])  
```  
  
## <a name="arguments"></a>Argomenti  
 *set_expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *set_expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Note  
 Questa funzione restituisce le tuple del primo set specificato che risultano non vuote quando vengono valutate sulle tuple del secondo set. Il **NonEmpty** funzione tiene conto dei calcoli e mantiene le tuple duplicate. Se non viene specificato un secondo set, l'espressione viene valutata nel contesto delle coordinate correnti dei membri delle gerarchie degli attributi e delle misure del cubo.  
  
> [!NOTE]  
>  Utilizzare questa funzione anziché deprecate [NonEmptyCrossjoin &#40;MDX&#41; ](../mdx/nonemptycrossjoin-mdx.md) (funzione).  
  
> [!IMPORTANT]  
>  Non sono le tuple a essere non vuote, bensì le celle a cui fanno riferimento le tuple.  
  
## <a name="examples"></a>Esempi  
 La query seguente viene illustrato un esempio semplice di **NonEmpty**, restituendo tutti i clienti che hanno un valore non null per Internet Sales Amount in data 1 luglio 2001:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 L'esempio seguente restituisce il set di tuple contenente i clienti e le date di acquisto, utilizzando il **filtro** (funzione) e il **NonEmpty** funzioni per individuare l'ultima data in cui ogni cliente ha eseguito un acquisto:  
  
 `WITH SET MYROWS AS FILTER`  
  
 `(NONEMPTY`  
  
 `([Customer].[Customer Geography].[Customer].MEMBERS`  
  
 `* [Date].[Date].[Date].MEMBERS`  
  
 `, [Measures].[Internet Sales Amount]`  
  
 `) AS MYSET`  
  
 `, NOT(MYSET.CURRENT.ITEM(0)`  
  
 `IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))`  
  
 `)`  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `MYROWS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)   
 [Filter &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
