---
description: Utilizzo delle funzioni di tupla
title: Uso delle funzioni di tupla | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d858fa6e67712a6ab93608dae20a15dca629c01e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500494"
---
# <a name="using-tuple-functions"></a>Utilizzo delle funzioni di tupla


  Una funzione di tupla recupera una tupla da un set o mediante la risoluzione della rappresentazione stringa di una tupla.  
  
 Le funzioni di tupla, come le funzioni membro e le funzioni sui set, sono essenziali per la negoziazione delle strutture multidimensionali che si trovano in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Sono disponibili tre funzioni di tupla in MDX, [Current &#40;mdx&#41;](../mdx/current-mdx.md), [Item &#40;Tuple&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md) e [StrToTuple &#40;MDX ](../mdx/strtotuple-mdx.md)&#41;. Nell'esempio di query seguente viene illustrato l'utilizzo di ciascuna di queste funzioni:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of Years and Countries`  
  
 `SET MyTuples AS  [Date].[Calendar Year].[Calendar Year].MEMBERS * [Customer].[Country].[Country].MEMBERS`  
  
 `//Returns a string representation of that set using the Current and Generate functions`  
  
 `MEMBER MEASURES.CURRENTDEMO AS GENERATE(MyTuples, TUPLETOSTR(MyTuples.CURRENT), ", ")`  
  
 `//Retrieves the fourth tuple from that set and displays it as a string`  
  
 `MEMBER MEASURES.ITEMDEMO AS TUPLETOSTR(MyTuples.ITEM(3))`  
  
 `//Creates a tuple consisting of the measure Internet Sales Amount and the country Australia from a string`  
  
 `MEMBER MEASURES.STRTOTUPLEDEMO AS STRTOTUPLE("([Measures].[Internet Sales Amount]" + ", [Customer].[Country].&[Australia])")`  
  
 `SELECT{MEASURES.CURRENTDEMO,MEASURES.ITEMDEMO,MEASURES.STRTOTUPLEDEMO} ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Uso di funzioni membro](../mdx/using-member-functions.md)   
 [Utilizzo delle funzioni sui set](../mdx/using-set-functions.md)  
  
  
