---
title: Filtro (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a70bceed4cdccf6a22f0cfea4e5093634f88f1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
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
  
## <a name="remarks"></a>Note  
 Il **filtro** funzione valuta l'espressione logica specificata rispetto a ogni tupla nel set specificato. La funzione restituisce un set costituito da ogni tupla nel set specificato in cui l'espressione logica restituisce **true**. Se nessuna tupla restituisce **true**, viene restituito un set vuoto.  
  
 Il **filtro** funzionamento della funzione in modo analogo a quello delle [IIf](../mdx/iif-mdx.md) (funzione). Il **IIf** funzione restituisce solo una delle due opzioni in base alla valutazione di un'espressione logica MDX, mentre le **filtro** funzione restituisce un set di tuple che soddisfano la condizione di ricerca specificati. In effetti, il **filtro** funzione esegue `IIf(Logical_Expression, Set_Expression.Current, NULL)` su ogni tupla del set e restituisce il set risultante.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato l'utilizzo della funzione Filter sull'asse Rows di una query, per restituire solo le date in cui Internet Sales Amount è maggiore di $10.000:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 La funzione Filter può essere utilizzata anche nelle definizioni di membri calcolati. Nell'esempio seguente restituisce la somma del `Measures.[Order Quantity]` membro, aggregato sui primi nove mesi del 2003 contenuti nella `Date` dimensione, dalle **Adventure Works** cubo. Il **PeriodsToDate** funzione definisce le tuple nel set su cui il **aggregazione** funzione viene eseguita. Il **filtro** funzione limita le tuple da restituire per gli utenti con i valori più bassi per la misura Reseller Sales Amount per il periodo di tempo precedente.  
  
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
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
