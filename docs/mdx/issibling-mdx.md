---
description: IsSibling (MDX)
title: Elemento di pari livello (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: dc43d132e9fca9f691ab76aa43851aadf6c52b47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483974"
---
# <a name="issibling-mdx"></a>IsSibling (MDX)


  Indica se il membro specificato è di pari livello rispetto a un altro membro specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IsSibling(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Member_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione di **pari livello** restituisce **true** se il primo membro specificato è un elemento di pari livello del secondo membro specificato. In caso contrario, la funzione restituisce **false**.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito TRUE se il membro corrente della gerarchia Fiscal nella dimensione Date è un elemento di pari livello di luglio 2002:  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
