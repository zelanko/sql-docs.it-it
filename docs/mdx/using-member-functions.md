---
title: Uso delle funzioni membro | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1c9979b6b9fcb04115695cbe8d9c224e1c6c1f57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63251603"
---
# <a name="using-member-functions"></a>Utilizzo delle funzioni membro


  Una funzione membro è una funzione MDX (Multidimensional Expressions) che restituisce un membro. Le funzioni membro, come le funzioni di tupla e le funzioni sui set, sono essenziali per la negoziazione delle strutture multidimensionali che si trovano in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Delle molte funzioni membro in MDX, la più importante è il **CurrentMember** funzione, che viene usato per determinare il membro corrente in una gerarchia. La query seguente illustra come usarlo, insieme con il **padre**, **predecessore**, e **Prevmember** funzioni:  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Le funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Uso delle funzioni di tupla](../mdx/using-tuple-functions.md)   
 [Uso delle funzioni sui set](../mdx/using-set-functions.md)  
  
  
