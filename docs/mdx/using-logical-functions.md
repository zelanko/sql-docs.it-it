---
title: Uso di funzioni logiche | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a63d8cb22a8533cf352acb690f87916e2e9d568d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249832"
---
# <a name="using-logical-functions"></a>Utilizzo di funzioni logiche


  Una funzione logica esegue un confronto o un'operazione logica su oggetti ed espressioni e restituisce un valore booleano. Le funzioni logiche sono fondamentali nelle espressioni MDX per determinare la posizione di un membro.  
  
 La funzione logica più diffuso è il **IsEmpty** (funzione). Per altre informazioni su come usare il **IsEmpty** function, vedere [uso di valori vuoti](../mdx/working-with-empty-values.md).  
  
 La query seguente viene illustrato come utilizzare il **IsLeaf** e **IsAncestor** funzioni:  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Le funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)  
  
  
