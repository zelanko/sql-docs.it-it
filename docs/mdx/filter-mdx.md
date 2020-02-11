---
title: Filter (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a70bceed4cdccf6a22f0cfea4e5093634f88f1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132686"
---
# <a name="filter-mdx"></a>Filter (MDX)


  Restituisce il set risultante dal filtro di un set specificato in base a una condizione di ricerca.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Logical_Expression*  
 Espressione logica MDX (Multidimensional Expression) valida che restituisce true o false.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Filter** valuta l'espressione logica specificata rispetto a ogni tupla nel set specificato. La funzione restituisce un set costituito da ogni tupla nel set specificato in cui l'espressione logica restituisce **true**. Se nessuna tupla restituisce **true**, viene restituito un set vuoto.  
  
 La funzione **Filter** funziona in modo simile a quella della funzione [IIf](../mdx/iif-mdx.md) . La funzione **IIf** restituisce solo una delle due opzioni in base alla valutazione di un'espressione logica MDX, mentre la funzione **Filter** restituisce un set di tuple che soddisfano la condizione di ricerca specificata. In effetti, la funzione **Filter** viene eseguita `IIf(Logical_Expression, Set_Expression.Current, NULL)` su ogni tupla del set e restituisce il set risultante.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo della funzione Filter sull'asse Rows di una query, per restituire solo le date in cui Internet Sales Amount è maggiore di $10.000:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 La funzione Filter può essere utilizzata anche nelle definizioni di membri calcolati. Nell'esempio seguente viene restituita la somma `Measures.[Order Quantity]` del membro, aggregato sui primi nove mesi di 2003 contenuti nella `Date` dimensione, dal cubo **Adventure Works** . La funzione **PeriodsToDate** definisce le tuple nel set su cui opera la funzione di **aggregazione** . La funzione **Filter** limita le tuple restituite a quelle con valori inferiori per la misura Reseller Sales Amount per il periodo di tempo precedente.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
