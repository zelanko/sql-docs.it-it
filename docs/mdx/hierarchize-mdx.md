---
title: Hierarchize (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8ab2c866f201c53684c316282a143b4f672cb8e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68105427"
---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)


  Ordina i membri di un set in una gerarchia.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Hierarchize** organizza i membri del set specificato in ordine gerarchico. e mantiene sempre i duplicati.  
  
-   Se non si specifica **post** , la funzione ordina i membri in un livello nell'ordine naturale. ovvero, se non sono specificate altre condizioni di ordinamento, secondo l'ordinamento predefinito dei membri nella gerarchia. I membri figlio seguono immediatamente i membri padre corrispondenti.  
  
-   Se viene specificato **post** , la funzione **Hierarchize** Ordina i membri in un livello usando un ordine post-naturale. In altri termini, i membri figlio precedono i relativi elementi padre.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene eseguito il drill-up del membro Canada. La funzione **Hierarchize** viene usata per organizzare i membri del set specificato in ordine gerarchico, che è richiesto dalla funzione **DrillupMember** .  
  
```  
SELECT DrillUpMember   
   (  
      Hierarchize  
         (  
            {[Geography].[Geography].[Country].[Canada]  
            ,[Geography].[Geography].[Country].[United States]  
            ,[Geography].[Geography].[State-Province].[Alberta]  
            ,[Geography].[Geography].[State-Province].[Brunswick]  
            ,[Geography].[Geography].[State-Province].[Colorado]   
            }  
         ), {[Geography].[Geography].[Country].[United States]}  
   )  
ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituita la somma `Measures.[Order Quantity]` del membro, aggregato sui primi nove mesi di 2003 contenuti nella `Date` dimensione, dal cubo **Adventure Works** . La funzione **PeriodsToDate** definisce le tuple nel set su cui opera la funzione di aggregazione. La funzione **Hierarchize** organizza i membri del set specificato di membri dalla dimensione Product in ordine gerarchico.  
  
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
  
  
