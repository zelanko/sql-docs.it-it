---
title: Lag (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7e95af96249b64f86bb1466283e8a1a38a32d90
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905768"
---
# <a name="lag-mdx"></a>Lag (MDX)


  Restituisce il membro che precede il membro specificato del numero specificato di posizioni al livello del membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Indice*  
 Espressione numerica valida che specifica il numero di posizioni tra i membri.  
  
## <a name="remarks"></a>Osservazioni  
 Le posizioni dei membri all'interno di un livello vengono determinate dall'ordine naturale della gerarchia dell'attributo. La numerazione delle posizioni è in base zero.  
  
 Se il ritardo specificato è zero, la funzione **lag** restituisce il membro specificato.  
  
 Se il ritardo specificato è negativo, la funzione **lag** restituisce un membro successivo.  
  
 `Lag(1)`equivale alla funzione [PrevMember](../mdx/prevmember-mdx.md) . `Lag(-1)`equivale alla funzione [NextMember](../mdx/nextmember-mdx.md) .  
  
 La funzione **lag** è simile alla funzione [Lead](../mdx/lead-mdx.md) , ad eccezione del fatto che la funzione **Lead** Cerca nella direzione opposta rispetto alla funzione **lag** . In altre parole, `Lag(n)` equivale a `Lead(-n)`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il valore per dicembre 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituito il valore per marzo 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
