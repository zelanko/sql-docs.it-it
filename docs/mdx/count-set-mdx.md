---
description: Count (Set) (MDX)
title: Conteggio (set) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3a8760d4df4aa1479aaa9ad365c92a5168eb3869
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341527"
---
# <a name="count-set-mdx"></a>Count (Set) (MDX)


  Restituisce il numero di celle in un set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Standard syntax  
Count(Set_Expression [ , ( EXCLUDEEMPTY | INCLUDEEMPTY ) ] )  
  
Alternate syntax  
Set_Expression.Count  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Count (set)** include o esclude le celle vuote, a seconda della sintassi utilizzata. Se si utilizza la sintassi standard, le celle vuote possono essere escluse o incluse utilizzando rispettivamente i flag **EXCLUDEEMPTY** o **INCLUDEEMPTY** . Se si utilizza la sintassi alternativa, la funzione includerà sempre le celle vuote.  
  
 Per escludere le celle vuote nel conteggio di un set, utilizzare la sintassi standard e il flag facoltativo **EXCLUDEEMPTY** .  
  
> [!NOTE]  
>  Per impostazione predefinita, la funzione **Count (set)** conta le celle vuote. Al contrario, la funzione **count** in OLE DB che conta un set esclude le celle vuote per impostazione predefinita.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene contato il numero di celle nel set di membri che comprende i figli della gerarchia dell'attributo Model Name nella dimensione Product.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene conteggiato il numero di prodotti nella dimensione Product utilizzando la funzione **DrilldownLevel** in combinazione con la funzione **count** .  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 Nell'esempio seguente vengono restituiti i rivenditori con vendite in calo rispetto al trimestre di calendario precedente, utilizzando la funzione **count** insieme alla funzione **Filter** e a una serie di altre funzioni. Questa query utilizza la funzione di **aggregazione** per supportare la selezione di più membri Geography, ad esempio per la selezione da un elenco a discesa in un'applicazione client.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
   (Filter  
      (Existing(Reseller.Reseller.Reseller),  
         [Measures].[Reseller Sales Amount]   
         < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
      )  
   )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate  
   ( {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
   )  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})  
      })  
   ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,  
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
   ,[Measures].[Declining Reseller Sales])  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Conteggio &#40;dimensione&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Conteggio &#40;livelli di gerarchia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Conteggio &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40;&#41;MDX ](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40;&#41;MDX ](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize &#40;&#41;MDX ](../mdx/hierarchize-mdx.md)   
 [Proprietà &#40;&#41;MDX ](../mdx/properties-mdx.md)   
 [Aggregazione MDX &#40;&#41;](../mdx/aggregate-mdx.md)   
 [Filtrare &#40;&#41;MDX ](../mdx/filter-mdx.md)   
 [PrevMember &#40;&#41;MDX ](../mdx/prevmember-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
