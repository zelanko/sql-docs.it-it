---
title: IIf (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 87b7b030776c1c18bb13307bf97db721fe472bd3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68105330"
---
# <a name="iif-mdx"></a>IIf (MDX)


  Vengono restituite diverse espressioni del ramo a seconda che una condizione Boolean sia true o false.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>Argomenti  
 La funzione IIf accetta tre argomenti: IIf (\<Condition>, \<then Branch>, \<else Branch>).  
  
 *Logical_Expression*  
 Condizione che restituisce **true** (1) o **false** (0). Deve essere un'espressione logica MDX (Multidimensional Expression) valida.  
  
 *Hint expression1 [eager | Strict | Lazy]]*  
 Utilizzato quando l'espressione logica restituisce **true**. Expression1 deve essere un'espressione MDX (Multidimensional Expression) valida.  
  
 *Hint expression2 [eager | Strict | Lazy]]*  
 Utilizzato quando l'espressione logica restituisce **false**. Expression2 deve essere un'espressione MDX (Multidimensional Expression) valida.  
  
## <a name="remarks"></a>Osservazioni  
 La condizione specificata dall'espressione logica restituisce **false** quando il valore di questa espressione è zero. Qualsiasi altro valore restituisce **true**.  
  
 Quando la condizione è **true**, la funzione **IIf** restituisce la prima espressione. In caso contrario, la funzione restituisce la seconda espressione.  
  
 Le espressioni specificate possono restituire valori oppure oggetti MDX. Le espressioni specificate non devono inoltre essere necessariamente dello stesso tipo.  
  
 La funzione **IIf** non è consigliata per la creazione di un set di membri in base ai criteri di ricerca. Utilizzare invece la funzione [Filter](../mdx/filter-mdx.md) per valutare ogni membro di un set specificato in base a un'espressione logica e restituire un subset di membri.  
  
> [!NOTE]  
>  Se una delle espressioni restituisce NULL, quando la condizione viene soddisfatta il set di risultati sarà NULL.  
  
 Hint è un modificatore facoltativo che determina il modo e il momento in cui l'espressione viene valutata. Consente di eseguire l'override del piano di query predefinito specificando il modo in cui l'espressione viene valutata.  
  
-   Tramite EAGER l'espressione viene valutata nel sottospazio IIF originale.  
  
-   Tramite STRICT l'espressione viene valutata solo nel sottospazio limitato creato dall'espressione della condizione logica.  
  
-   Tramite LAZY l'espressione viene valutata in modalità cella per cella.  
  
 Mentre EAGER e STRICT si applicano solo ai rami then-else di IIF, LAZY si applica a tutte le espressioni MDX. Qualsiasi espressione MDX può essere seguita da un HINT LAZY tramite cui l'espressione verrà valutata in modalità cella per cella.  
  
 EAGER e STRICT si escludono a vicenda nell'hint e possono essere utilizzati nella stessa funzione IIF(,,) in diverse espressioni.  
  
 Per ulteriori informazioni, vedere [hint per la query della funzione IIF in SQL Server Analysis Services 2008](https://go.microsoft.com/fwlink/?LinkId=269540) e [piani di esecuzione e hint di piano per la funzione MDX IIf e l'istruzione case](https://go.microsoft.com/fwlink/?LinkId=269565).  
  
## <a name="examples"></a>Esempi  
 Nella query seguente viene illustrato un semplice utilizzo di **IIf** all'interno di una misura calcolata per restituire uno dei due valori stringa diversi quando la misura Internet Sales Amount è maggiore o minore di $10000:  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 IIF viene spesso utilizzata per gestire gli errori delle divisioni per zero all'interno di misure calcolate, come nell'esempio seguente:  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 Di seguito è riportato un esempio di **IIf** che restituisce uno dei due set all'interno della funzione generate per creare un set complesso di Tuple nelle righe:  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 In questo esempio viene infine illustrato l'utilizzo degli hint di piano:  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
