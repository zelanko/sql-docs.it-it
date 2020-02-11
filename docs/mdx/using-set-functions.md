---
title: Utilizzo di funzioni set | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 52e0c140acb944a774f5ab167bb81c662e3e32d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038048"
---
# <a name="using-set-functions"></a>Utilizzo delle funzioni sui set


  Una funzione sui set recupera un set da una dimensione, da una gerarchia, da un livello o attraversando i percorsi assoluti e relativi dei membri di tali oggetti, costruendo i set in vari modi.  
  
 Le funzioni sui set, come le funzioni membro e le funzioni di tupla, sono essenziali per la negoziazione delle strutture multidimensionali utilizzate in Analysis Services. Le funzioni sui set sono essenziali anche per ottenere risultati dalle query MDX, perché le espressioni set definiscono gli assi di una query MDX.  
  
 Una delle funzioni set più comuni è rappresentata dai [membri &#40;impostare&#41; &#40;funzione&#41;MDX](../mdx/members-set-mdx.md) , che consente di recuperare un set contenente tutti i membri di una dimensione, una gerarchia o un livello. Nell'esempio seguente viene illustrato l'utilizzo di questa funzione all'interno di una query:  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Un'altra funzione di uso comune è [Crossjoin &#40;funzione MDX&#41;](../mdx/crossjoin-mdx.md) . Questa funzione restituisce un set di tuple che rappresenta il prodotto cartesiano dei set passati come parametri. In termini pratici, consente di creare assi "nidificati" o "con campi incrociati" nelle query:  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns a set containing every combination of all of the members`  
  
 `//on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension and all of the members on the Category level`  
  
 `//of the Category hierarchy on the Product dimension`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 I [discendenti &#40;funzione MDX&#41;](../mdx/descendants-mdx.md) sono simili alla funzione **Children** , ma sono più potenti. Restituisce i discendenti di qualsiasi membro a uno o più livelli in una gerarchia:  
  
 SELECT  
  
 [Measures].[Internet Sales Amount]  
  
 ON Columns,  
  
 //Restituisce un set contenente tutte le date comprese nel calendario  
  
 //2004 nella gerarchia Calendar della dimensione Date  
  
 DESCENDANTS(  
  
 [DATE]. [Calendario]. [Anno di calendario]. & [2004]  
  
 , [Date].[Calendar].[Date])  
  
 ON Rows  
  
 FROM [Adventure Works]  
  
 L' [ordine &#40;funzione MDX&#41;](../mdx/order-mdx.md) consente di ordinare il contenuto di un set in ordine crescente o decrescente in base a una determinata espressione numerica. La query seguente restituisce gli stessi membri nelle righe della query precedente, ma in questo caso i membri vengono ordinati in base alla misura Internet Sales Amount:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//ordered by Internet Sales Amount`  
  
 `ORDER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount], BDESC)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Questa query illustra anche come passare come parametro il set restituito da una funzione sui set (Descendants) a un'altra funzione sui set (Order).  
  
 Il filtraggio di un set in base a determinati criteri è molto utile durante la scrittura di query. a tale scopo, è possibile utilizzare la funzione [Filter &#40;MDX&#41;](../mdx/filter-mdx.md) , come illustrato nell'esempio seguente:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//where Internet Sales Amount is greater than $70000`  
  
 `FILTER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount]>70000)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Esistono altre funzioni più sofisticate che consentono di applicare filtri a un set con modalità diverse. Ad esempio, nella query seguente viene illustrato il [conteggio &#40;funzione MDX&#41;](../mdx/topcount-mdx.md) restituisce i primi n elementi di un set:  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing the top 10 Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension by Internet Sales Amount`  
  
 `TOPCOUNT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,10, [Measures].[Internet Sales Amount])`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 Infine, è possibile eseguire una serie di operazioni sui set logici utilizzando funzioni come [Intersect &#40;mdx&#41;](../mdx/intersect-mdx.md), [Union &#40;MDX&#41;](../mdx/union-mdx.md) e [ad eccezione &#40;funzioni MDX&#41;](../mdx/except-mdx-function.md) . La query seguente illustra l’utilizzo delle ultime due funzioni:  
  
 `SELECT`  
  
 `//Returns a set containing the Measures Internet Sales Amount, Internet Tax Amount and`  
  
 `//Internet Total Product Cost`  
  
 `UNION(`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}`  
  
 `, {[Measures].[Internet Total Product Cost]}`  
  
 `)`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//except the January 1st 2004`  
  
 `EXCEPT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,{[Date].[Calendar].[Date].&[915]})`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;sintassi MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Uso di funzioni membro](../mdx/using-member-functions.md)   
 [Utilizzo delle funzioni di tupla](../mdx/using-tuple-functions.md)  
  
  
