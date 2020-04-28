---
title: Utilizzo di funzioni logiche | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 723d481bc858d7d1db4a63cbb32ab5614eddbb55
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097158"
---
# <a name="using-logical-functions"></a>Utilizzo di funzioni logiche


  Una funzione logica esegue un confronto o un'operazione logica su oggetti ed espressioni e restituisce un valore booleano. Le funzioni logiche sono fondamentali nelle espressioni MDX per determinare la posizione di un membro.  
  
 La funzione logica più comunemente utilizzata è la funzione **IsEmpty** . Per ulteriori informazioni sull'utilizzo della funzione **IsEmpty** , vedere [utilizzo di valori vuoti](../mdx/working-with-empty-values.md).  
  
 Nella query seguente viene illustrato come utilizzare le funzioni per l' **oggetto e il** **predecessore** :  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)  
  
  
