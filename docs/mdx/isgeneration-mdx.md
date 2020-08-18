---
description: IsGeneration (MDX)
title: Generazione (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e7b7f3df41af6af51a826352814fc6aef52ef0a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471833"
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
  
## <a name="remarks"></a>Osservazioni  
 La funzione di **generazione** restituisce **true** se il membro specificato si trova nel numero di generazione specificato. In caso contrario, la funzione restituisce **false**. Inoltre, se il membro specificato restituisce un membro vuoto, la funzione di **generazione** restituisce **false**.  
  
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
  
  
