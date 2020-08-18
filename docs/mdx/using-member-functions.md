---
description: Utilizzo delle funzioni membro
title: Uso di funzioni membro | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4cec35f8d09d671b3b426ff5ac9e18797df716ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491408"
---
# <a name="using-member-functions"></a>Utilizzo delle funzioni membro


  Una funzione membro è una funzione MDX (Multidimensional Expressions) che restituisce un membro. Le funzioni membro, come le funzioni di tupla e le funzioni sui set, sono essenziali per la negoziazione delle strutture multidimensionali che si trovano in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Tra le numerose funzioni membro in MDX, la più importante è la funzione **CurrentMember** , che viene utilizzata per determinare il membro corrente in una gerarchia. Nella query seguente viene illustrato come utilizzarla, insieme alle funzioni **padre**, **predecessore**e **PrevMember** :  
  
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
 [Funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Uso delle funzioni di tupla](../mdx/using-tuple-functions.md)   
 [Utilizzo delle funzioni sui set](../mdx/using-set-functions.md)  
  
  
