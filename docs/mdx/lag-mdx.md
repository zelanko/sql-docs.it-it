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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
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
  
 *Index*  
 Espressione numerica valida che specifica il numero di posizioni tra i membri.  
  
## <a name="remarks"></a>Note  
 Le posizioni dei membri all'interno di un livello vengono determinate dall'ordine naturale della gerarchia dell'attributo. La numerazione delle posizioni è in base zero.  
  
 Se il numero di posizioni specificato è uguale a zero, il **Lag** funzione restituisce lo stesso membro specificato.  
  
 Se il numero di posizioni specificato è negativo, il **Lag** funzione restituirà un membro.  
  
 `Lag(1)` equivale al [PrevMember](../mdx/prevmember-mdx.md) (funzione). `Lag(-1)` equivale al [NextMember](../mdx/nextmember-mdx.md) (funzione).  
  
 Il **Lag** funzione è simile al [Lead](../mdx/lead-mdx.md) funzionare, tranne il fatto che il **Lead** funzione esegue la ricerca nella direzione opposta al **Lag** funzione. In altre parole, `Lag(n)` equivale a `Lead(-n)`.  
  
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
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
