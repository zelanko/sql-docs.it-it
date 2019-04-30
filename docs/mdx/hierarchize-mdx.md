---
title: HIERARCHIZE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4478fb9657ef4577bcae8b5641f53154b2a0486c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224901"
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
  
## <a name="remarks"></a>Note  
 Il **Hierarchize** funzione Organizza i membri del set specificato in ordine gerarchico. e mantiene sempre i duplicati.  
  
-   Se **POST** non viene specificato, la funzione Ordina membri in un livello in base all'ordine naturale. ovvero, se non sono specificate altre condizioni di ordinamento, secondo l'ordinamento predefinito dei membri nella gerarchia. I membri figlio seguono immediatamente i membri padre corrispondenti.  
  
-   Se **POST** è specificato, il **Hierarchize** funzione consente di ordinare i membri di un livello usando un ordine di post-naturale. In altri termini, i membri figlio precedono i relativi elementi padre.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene eseguito il drill-up del membro Canada. Il **Hierarchize** funzione viene utilizzata per organizzare i membri del set specificato in ordine gerarchico, necessario per il **DrillUpMember** (funzione).  
  
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
  
 Nell'esempio seguente restituisce la somma del `Measures.[Order Quantity]` membro, aggregato sui primi nove mesi del 2003 contenuti nella `Date` dimensione, dalle **Adventure Works** cubo. Il **PeriodsToDate** funzione definisce le tuple del set su cui opera la funzione di aggregazione. Il **Hierarchize** funzione Organizza i membri del set specificato di membri della dimensione Product in ordine gerarchico.  
  
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
  
  
