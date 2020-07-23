---
title: DrilldownMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1f387d0524ea22aca3c2bb7eb073af07bbdf0612
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970052"
---
# <a name="drilldownmember-mdx"></a>DrilldownMember (MDX)


  Esegue il drill-down dei membri di un set specificato presenti in un secondo set specificato.  
  
 La funzione esegue in alternativa il drill-down su un set di tuple utilizzando la prima gerarchia di tuple o la gerarchia specificata facoltativamente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DrillDownMember(<Set_Expression1>, <Set_Expression2> [,[<Target_Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]])  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Target_Hierarchy*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
 *Ricorsiva*  
 Una parola chiave che indica il confronto ricorsivo tra set.  
  
 *Include_Calc_Members*  
 Una parola chiave per consentire l'inclusione dei membri calcolati nei risultati del drill-down.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione restituisce un set di membri figlio ordinati in base alla gerarchia e comprende i membri specificati nel primo set che sono presenti anche nel secondo set. Il drill-down non verrà eseguito sui membri padre se il primo set contiene il membro padre e uno o più figli. Il primo set può avere qualsiasi dimensionalità, mentre il secondo deve contenere un set unidimensionale. L'ordine originale dei membri nel primo set viene mantenuto, con la sola differenza che nel set di risultati della funzione tutti i membri figlio vengono indicati immediatamente sotto il membro padre corrispondente. La funzione ottiene il set di risultati recuperando il membro figlio di ogni membro del primo set presente anche nel secondo set. Se viene specificato **RIcorsivo** , la funzione continua a confrontare in modo ricorsivo i membri del set di risultati in base al secondo set, recuperando gli elementi figlio per ogni membro nel set di risultati presente anche nel secondo set fino a quando non si trovano altri membri del set di risultati nel secondo set.  
  
 Eseguendo una query sulla proprietà XMLA **MdpropMdxDrillFunctions** è possibile verificare il livello di supporto fornito dal server per le funzioni di drill-through. per informazioni dettagliate, vedere [Proprietà XMLA supportate &#40;&#41;XMLA](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
 Il primo set può contenere tuple anziché membri. La funzione per il drill-down di tuple è un'estensione di OLE DB e restituisce un set di tuple anziché di membri.  
  
> [!IMPORTANT]  
>  Il drill-down di un membro non verrà eseguito se tale membro è immediatamente seguito da uno dei relativi figli. L'ordine dei membri nel set è importante sia per le famiglie di funzioni drill-down * che drillup \* .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eseguito il drill-down nel membro Australia del primo set, presente anche nel secondo set.  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   )  
   ON 0  
   FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene eseguito il drill-down nel membro Australia del primo set, presente anche nel secondo set. Poiché tuttavia è specificato l'argomento RECURSIVE, la funzione confronta ricorsivamente i membri del set di risultati, ovvero i membri del livello State-Province, con i membri del secondo set e recupera il membro figlio di ogni membro del set di risultati (i membri del livello City) presente anche nel secondo set fino a quando nel secondo set non viene individuato alcun membro del set di risultati.  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   ,RECURSIVE)  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
