---
title: Parola chiave EXISTING (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ceaeac711ed30028dab3bc09827df9b6ae1f0e0a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725355"
---
# <a name="existing-keyword-mdx"></a>Parola chiave EXISTING (MDX)
  Forza la valutazione di un determinato set all'interno del contesto corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione set MDX (Multidimensional Expression) valida.  
  
## <a name="remarks"></a>Note  
 Per impostazione predefinita, i set vengono valutati all'interno del contesto del cubo che include i membri del set. È tuttavia possibile forzare la valutazione di un set specificato all'interno del contesto corrente utilizzando la parola chiave `Existing`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il numero dei rivenditori le cui vendite sono diminuite nel periodo di tempo precedente, in base ai valori del membro State-Province selezionati dall'utente valutati tramite la funzione `Aggregate`. È tuttavia possibile forzare la valutazione di un set specificato all'interno del contesto corrente utilizzando la parola chiave [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) e [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) vengono usate per restituire i valori relativi alla diminuzione delle vendite per le categorie di prodotti nella dimensione Product. Il `Existing` parola chiave forza il set nel `Filter` funzione deve essere valutata nel contesto corrente, vale a dire, per i membri Washington e Oregon della gerarchia dell'attributo State-Province.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
      (Filter  
         (Existing  
            (Reseller.Reseller.Reseller)  
         , [Measures].[Reseller Sales Amount] <   
            ([Measures].[Reseller Sales Amount]  
               ,[Date].Calendar.PrevMember  
            )  
        )  
      )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate   
      ( {[Geography].[State-Province].&[WA]&[US]  
         , [Geography].[State-Province].&[OR]&[US] }   
      )  
SELECT NON EMPTY HIERARCHIZE   
      (AddCalculatedMembers   
         (   
            {DrillDownLevel  
               ({[Product].[All Products]}  
               )  
            }   
         )   
      ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE   
      ( [Geography].[State-Province].x  
        , [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
        ,[Measures].[Declining Reseller Sales]  
      )  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Count &#40;Set&#41; &#40;MDX&#41;](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers &#40;MDX&#41;](/sql/mdx/addcalculatedmembers-mdx)   
 [Aggregate &#40;MDX&#41;](/sql/mdx/aggregate-mdx)   
 [Filter &#40;MDX&#41;](/sql/mdx/filter-mdx)   
 [Properties &#40;MDX&#41;](/sql/mdx/properties-mdx)   
 [DrilldownLevel &#40;MDX&#41;](/sql/mdx/drilldownlevel-mdx)   
 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
