---
title: IsGeneration (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a726470f89f2d3ea1677259e849735a09909a42d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629405"
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)


  Indica se il membro specificato è incluso in una generazione specifica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Generation_Number*  
 Espressione numerica valida che specifica la generazione rispetto alla quale il membro specificato viene valutato.  
  
## <a name="remarks"></a>Note  
 Il **IsGeneration** funzione restituisce **true** se il membro specificato è il numero di generazione specificata. In caso contrario, la funzione restituisce **false**. Inoltre, se il membro specificato restituisce un membro vuoto, il **IsGeneration** funzione restituisce **false**.  
  
 I membri foglia hanno indice di generazione 0. L'indice di generazione dei membri non foglia viene determinato aggiungendo 1 all'indice di generazione più alto ottenuto dall'unione di tutti i membri figlio del membro specificato. Dato il modo in cui viene determinato l'indice di generazione dei membri non foglia, è possibile che un determinato membro non foglia appartenga a più generazioni.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito TRUE se [Date].[Fiscal].CurrentMember è parte della seconda generazione:  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
