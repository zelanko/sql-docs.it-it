---
description: Lead (MDX)
title: Lead (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ca78bdeca6103758d5d102ed8b85eb00b3138e18
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387327"
---
# <a name="lead-mdx"></a>Lead (MDX)


  Restituisce il membro che segue il membro specificato del numero specificato di posizioni nel livello del membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Index*  
 Espressione numerica valida che specifica il numero di posizioni dei membri.  
  
## <a name="remarks"></a>Osservazioni  
 Le posizioni dei membri all'interno di un livello vengono determinate dall'ordine naturale della gerarchia dell'attributo. La numerazione delle posizioni è in base zero.  
  
 Se il lead specificato è zero (0), la funzione **Lead** restituisce il membro specificato.  
  
 Se il lead specificato è negativo, la funzione **Lead** restituisce un membro precedente.  
  
 `Lead(1)` equivale alla funzione [NextMember](../mdx/nextmember-mdx.md) . `Lead(-1)` equivale alla funzione [PrevMember](../mdx/prevmember-mdx.md) .  
  
 La funzione **Lead** è simile alla funzione [lag](../mdx/lag-mdx.md) , ad eccezione del fatto che la funzione **lag** Cerca nella direzione opposta rispetto alla funzione **Lead** . In altre parole, `Lead(n)` equivale a `Lag(-n)`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il valore per dicembre 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituito il valore per marzo 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
