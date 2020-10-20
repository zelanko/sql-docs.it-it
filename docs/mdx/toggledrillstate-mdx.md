---
description: ToggleDrillState (MDX)
title: ToggleDrillState (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: dd716e631adc3ded77f81278c20f754b28199b49
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192321"
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
  
 *Ricorsiva*  
 (Facoltativo) Una parola chiave che indica il confronto ricorsivo tra set. La funzione **ToggleDrillState** è una combinazione delle funzioni **DrillupMember** e **DrilldownMember** . La ricorsione si applica solo quando il membro è nello stato **DrilldownMember** .  
  
 *Include_calc_members*  
 (Facoltativo) Flag che indica se includere i membri calcolati, se presenti, al livello di drill-down.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **ToggleDrillState** consente di impostare lo stato di drill di ogni membro del secondo set presente nel primo set. Il primo set può contenere tuple con qualsiasi dimensionalità, mentre il secondo deve contenere membri di una sola dimensione. La funzione **ToggleDrillState** è una combinazione delle funzioni **DrillupMember** e **DrilldownMember** . Se il membro, *m*, del secondo set è presente nel primo set e il membro viene sottoposto a drill-down, ovvero ha un discendente che lo segue immediatamente, `DrillupMember(Set_Expression1, {m})` viene applicato al membro o alla tupla nel primo set. Se viene effettuato il drill-up del membro *m* , ovvero non esiste alcun discendente di *m* che segue immediatamente *m*, `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` viene applicato al primo set.  
  
 Se viene usato il flag **RIcorsivo** facoltativo, il drill-up e il drill-down vengono applicati in modo ricorsivo. Per ulteriori informazioni sul flag ricorsivo, vedere le funzioni [DrillupMember](../mdx/drillupmember-mdx.md) e [DrilldownMember](../mdx/drilldownmember-mdx.md) .  
  
 Eseguendo una query sulla proprietà XMLA MdpropMdxDrillFunctions è possibile verificare il livello di supporto fornito dal server per le funzioni di drill-through. per informazioni dettagliate, vedere [Proprietà XMLA supportate &#40;&#41;XMLA ](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
 Vedere [database journal: funzioni set MDX: funzione ToggleDrillState ()](https://go.microsoft.com/fwlink/?LinkId=517759) per scenari ed esempi che coinvolgono questa funzione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono eseguiti il drill-down del membro Australia e il drill-up del membro Stati Uniti del primo set.  
  
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
  
