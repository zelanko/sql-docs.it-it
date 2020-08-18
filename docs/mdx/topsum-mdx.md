---
description: TopSum (MDX)
title: TopSum (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 665a1ace9df98303da19b861cdd3ce6340ec8368
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412910"
---
# <a name="topsum-mdx"></a>TopSum (MDX)


  Ordina un set e restituisce gli elementi superiori il cui totale cumulativo è maggiore o uguale al valore specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
TopSum(Set_Expression, Value, Numeric_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Valore*  
 Espressione numerica valida che specifica il valore in base a cui ogni tupla viene valutata.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) che restituisce una misura.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **TopSum** calcola la somma di una misura specificata valutata su un set specificato, ordinando il set in ordine decrescente. La funzione restituisce quindi gli elementi con i valori più alti il cui totale per l'espressione numerica specificata corrisponde almeno al valore specificato. La funzione restituisce il subset più piccolo di un set il cui totale cumulativo corrisponde almeno al valore specificato. Gli elementi restituiti sono ordinati dal più grande al più piccolo.  
  
> [!IMPORTANT]  
>  Analogamente alla funzione [BottomSum](../mdx/bottomsum-mdx.md) , la funzione **TopSum** interrompe sempre la gerarchia.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito per la categoria Bike il set più piccolo di membri del livello City nella gerarchia Geography della dimensione Geography il cui totale cumulativo calcolato utilizzando la misura Reseller Sales Amount corrisponde almeno alla somma di 6.000.000 (a partire dai membri di questo set con il numero di vendite più elevato).  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopSum  
   ({[Geography].[Geography].[City].Members}  
   , 6000000  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
