---
title: ToggleDrillState (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58acac77e4826855997791476b0602699452b7b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228084"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)


  Alterna lo stato di drill dei membri tra le modalità di drill-down e drill-up.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Ricorsivo*  
 (Facoltativo) Una parola chiave che indica il confronto ricorsivo tra set. Il **ToggleDrillState** funzione è una combinazione delle **DrillupMember** e **DrilldownMember** funzioni. La ricorsione si applica solo quando il membro è incluso il **DrilldownMember** dello stato.  
  
 *Include_calc_members*  
 (Facoltativo) Flag che indica se includere i membri calcolati, se presenti, al livello di drill-down.  
  
## <a name="remarks"></a>Note  
 Il **ToggleDrillState** funzione Alterna lo stato di drill di ogni membro del secondo set presente nel primo set. Il primo set può contenere tuple con qualsiasi dimensionalità, mentre il secondo deve contenere membri di una sola dimensione. Il **ToggleDrillState** funzione è una combinazione delle **DrillupMember** e **DrilldownMember** funzioni. Se il membro *m*del secondo set è presente nel primo set e tale membro è eseguito il drill-(vale a dire, ha un discendente che lo segue immediatamente), quindi `DrillupMember(Set_Expression1, {m})` viene applicato al membro o una tupla nel primo set. Se tale *m* membro è drill-up (non vi è alcun discendente del *m* che seguono immediatamente *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` viene applicato al primo set.  
  
 Se l'opzione facoltativa **RICORSIVA** flag viene utilizzato, il drill-up e drill-down vengono applicati in modo ricorsivo. Per altre informazioni sul flag recursive, vedere la [DrillupMember](../mdx/drillupmember-mdx.md) e [DrilldownMember](../mdx/drilldownmember-mdx.md) funzioni.  
  
 L'esecuzione di query la proprietà XMLA MdpropMdxDrillFunctions consente di verificare il livello di supporto che il server garantisce per le funzioni di drill; visualizzare [proprietà XMLA supportate &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) per informazioni dettagliate.  
  
 Vedere [Database Journal: Funzioni Set MDX: La funzione ToggleDrillState ()](https://go.microsoft.com/fwlink/?LinkId=517759) per scenari ed esempi che includono questa funzione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono eseguiti il drill-down del membro Australia e il drill-up del membro United States del primo set.  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
