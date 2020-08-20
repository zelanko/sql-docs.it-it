---
description: Exists (MDX)
title: Exists (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e025449634106003ea6e5d624f0d4a621ef3b93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494914"
---
# <a name="exists-mdx"></a>Exists (MDX)


  Restituisce il set di tuple del primo set specificato in cui esiste almeno una tupla del secondo set specificato. Questa funzione consente di eseguire manualmente ciò che la funzione Auto Exist esegue automaticamente. Per ulteriori informazioni su auto exists, vedere [concetti chiave in MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services).  
  
 Se \<Measure Group Name> viene specificato il parametro facoltativo, la funzione restituisce le tuple esistenti con una o più tuple del secondo set e le tuple a cui sono associate righe nella tabella dei fatti del gruppo di misure specificato.  
  
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
  
## <a name="remarks"></a>Osservazioni  
  
1.  Quando viene specificato l'argomento MeasureGroupName, le righe del gruppo di misure con misure che contengono valori null contribuiscono a **esistere** . Questa è la differenza tra questo formato di EXISTS e la funzione NonEmpty: se la proprietà NullProcessing di queste misure è impostata su Preserve, ciò significa che le misure visualizzeranno i valori null quando le query vengono eseguite su tale parte del cubo. Non Empty rimuoverà sempre le tuple da un set con valori di misura null, mentre Exists con l'argomento MeasureGroupName non filtra le tuple a cui sono associate righe del gruppo di misure, anche se i valori della misura sono null.  
  
2.  Se si utilizza il parametro *MeasureGroupName* , i risultati variano a seconda che esistano misure visibili nel gruppo di misure a cui si fa riferimento. Se non sono presenti misure visibili nel gruppo di misure a cui si fa riferimento, EXISTs restituisce sempre un set vuoto, indipendentemente dai valori di *Set_Expression1* e *Set_Expression2*.  
  
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
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [Crossjoin &#40;&#41;MDX ](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;&#41;MDX ](../mdx/nonemptycrossjoin-mdx.md)   
 [&#40;MDX non empty&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
