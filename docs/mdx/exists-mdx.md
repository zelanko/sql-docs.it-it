---
title: Esiste (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 781c03283c39ab5ec100ba7f7d83b3cbe19a7c19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139178"
---
# <a name="exists-mdx"></a>Exists (MDX)


  Restituisce il set di tuple del primo set specificato in cui esiste almeno una tupla del secondo set specificato. Questa funzione consente di eseguire manualmente ciò che la funzione Auto Exist esegue automaticamente. Per altre informazioni su auto EXIST, vedere [concetti chiave di MDX &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
 Se l'opzione facoltativa \<nome del gruppo di misure > viene specificato, la funzione restituisce le tuple che esiste con uno o più tuple dal secondo set e le tuple cui sono associate righe della tabella dei fatti del gruppo di misure specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Exists( Set_Expression1 , Set_Expression2 [, MeasureGroupName] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *MeasureGroupName*  
 Espressione stringa valida che specifica il nome di un gruppo di misure.  
  
## <a name="remarks"></a>Note  
  
1.  Le righe di gruppo di misure con misure contenenti valori null contribuiscono alla **Exists** quando viene specificato l'argomento MeasureGroupName. Questa è la differenza tra questo form EXISTS e la funzione Nonempty: se la proprietà NullProcessing di queste misure è impostata su Preserve, ciò significa che le misure saranno indicati i valori Null quando vengono eseguite query in base a tale parte del cubo. NonEmpty rimuoverà sempre le tuple da un set con valori di misura Null, mentre Exists con l'argomento MeasureGroupName non filtrerà tuple cui sono associate righe di gruppo di misure, anche se i valori di misura sono Null.  
  
2.  Se *MeasureGroupName* parametro viene utilizzato, i risultati variano in base se sono presenti misure visibili nel gruppo di misure cui si fa riferimento; se non sono disponibili misure visibili nel gruppo di misure cui si fa riferimento, EXISTS restituisce sempre un set vuoto, indipendentemente dai valori della *Set_Expression1* e *Set_Expression2*.  
  
## <a name="examples"></a>Esempi  
 Clienti che vivono in California:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
) ON 1   
FROM [Adventure Works]  
  
```  
  
 Clienti che vivono in California con vendite:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 Clienti con vendite:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, , "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 Clienti che hanno acquistato biciclette:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Product].[Product Categories].[Category].&[1]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [NonEmpty &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
