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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105330"
---
# <a name="iif-mdx"></a>IIf (MDX)


  Vengono restituite diverse espressioni del ramo a seconda che una condizione Boolean sia true o false.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>Argomenti  
 La funzione IIf accetta tre argomenti: iif (\<condition >, \<quindi creare un ramo >, \<else branch >).  
  
 *Logical_Expression*  
 Una condizione che restituisce **true** (1) o **false** (0). Deve essere un'espressione logica MDX (Multidimensional Expression) valida.  
  
 *Expression1 Hint [Eager | Strict | Lazy]]*  
 Utilizzato quando l'espressione logica restituisce **true**. Expression1 deve essere un'espressione MDX (Multidimensional Expression) valida.  
  
 *Expression2 Hint [Eager | Strict | Lazy]]*  
 Utilizzato quando l'espressione logica restituisce **false**. Expression2 deve essere un'espressione MDX (Multidimensional Expression) valida.  
  
## <a name="remarks"></a>Note  
 La condizione specificata dall'espressione logica viene valutata **false** quando il valore di questa espressione è zero. Restituisce qualsiasi altro valore **true**.  
  
 Quando la condizione è **true**, il **IIf** funzione restituisce la prima espressione. In caso contrario, la funzione restituisce la seconda espressione.  
  
 Le espressioni specificate possono restituire valori oppure oggetti MDX. Le espressioni specificate non devono inoltre essere necessariamente dello stesso tipo.  
  
 Il **IIf** funzione non è consigliata per la creazione di un set di membri in base ai criteri di ricerca. Usare invece i [filtro](../mdx/filter-mdx.md) funzione da valutare ogni membro di un set specificato in base a un'espressione logica e restituire un subset di membri.  
  
> [!NOTE]  
>  Se una delle espressioni restituisce NULL, quando la condizione viene soddisfatta il set di risultati sarà NULL.  
  
 Hint è un modificatore facoltativo che determina il modo e il momento in cui l'espressione viene valutata. Consente di eseguire l'override del piano di query predefinito specificando il modo in cui l'espressione viene valutata.  
  
-   Tramite EAGER l'espressione viene valutata nel sottospazio IIF originale.  
  
-   Tramite STRICT l'espressione viene valutata solo nel sottospazio limitato creato dall'espressione della condizione logica.  
  
-   Tramite LAZY l'espressione viene valutata in modalità cella per cella.  
  
 Mentre EAGER e STRICT si applicano solo ai rami then-else di IIF, LAZY si applica a tutte le espressioni MDX. Qualsiasi espressione MDX può essere seguita da un HINT LAZY tramite cui l'espressione verrà valutata in modalità cella per cella.  
  
 EAGER e STRICT si escludono a vicenda nell'hint e possono essere utilizzati nella stessa funzione IIF(,,) in diverse espressioni.  
  
 Per altre informazioni, vedere [hint per la Query funzione IIF in SQL Server Analysis Services 2008](https://go.microsoft.com/fwlink/?LinkId=269540) e [piani di esecuzione e gli hint di piano per la funzione IIF di MDX e l'istruzione CASE](https://go.microsoft.com/fwlink/?LinkId=269565).  
  
## <a name="examples"></a>Esempi  
 La query seguente viene illustrato un semplice utilizzo del **IIF** all'interno di una misura calcolata per restituire uno dei due diversi valori di stringa quando la misura Internet Sales Amount è maggiore o minore di $10.000:  
  
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
  
 Di seguito è riportato un esempio di **IIF** restituendo uno di due set nella funzione Generate per creare un set complesso di tuple su righe:  
  
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
  
  
