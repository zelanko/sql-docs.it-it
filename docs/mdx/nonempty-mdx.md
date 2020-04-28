---
title: Non Empty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 45daf970f69322cad36bbe5419bf1dc8cc8009b9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
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
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione restituisce le tuple del primo set specificato che risultano non vuote quando vengono valutate sulle tuple del secondo set. La funzione **NonEmpty** prende in considerazione i calcoli e conserva le tuple duplicate. Se non viene specificato un secondo set, l'espressione viene valutata nel contesto delle coordinate correnti dei membri delle gerarchie degli attributi e delle misure del cubo.  
  
> [!NOTE]  
>  Usare questa funzione invece della funzione deprecata [NonEmptyCrossjoin &#40;&#41;MDX](../mdx/nonemptycrossjoin-mdx.md) .  
  
> [!IMPORTANT]  
>  Non sono le tuple a essere non vuote, bensì le celle a cui fanno riferimento le tuple.  
  
## <a name="examples"></a>Esempi  
 La query seguente mostra un semplice esempio di non **empty**, restituendo tutti i clienti che hanno un valore non null per Internet Sales Amount il 1 ° luglio 2001:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 Nell'esempio seguente viene restituito il set di tuple contenente i clienti e le date di acquisto, utilizzando la funzione di **filtro** e le funzioni non **vuote** per individuare l'ultima data in cui ogni cliente ha effettuato un acquisto:  
  
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
 [DefaultMember &#40;&#41;MDX](../mdx/defaultmember-mdx.md)   
 [Filtrare &#40;&#41;MDX](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;&#41;MDX](../mdx/nonemptycrossjoin-mdx.md)  
  
  
