---
title: Corrente (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e4962dfd9eba7d3a21710fef33aa39256dcfbfa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249670"
---
# <a name="current-mdx"></a>Current (MDX)


  Restituisce la tupla corrente da un set durante l'iterazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Note  
 La tupla su cui si opera ad ogni passaggio di un'iterazione corrisponde alla tupla corrente. Il **correnti** funzione restituisce tale tupla. È valida solo durante un'iterazione su un set.  
  
 Includono funzioni MDX che eseguono iterazioni in un set di [genera](../mdx/generate-mdx.md) (funzione).  
  
> [!NOTE]  
>  La funzione viene eseguita correttamente solo con set denominati, utilizzando un alias del set o definendo un set denominato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come utilizzare il **correnti** funzione all'interno **genera**:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
