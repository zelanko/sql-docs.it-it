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
manager: kfile
ms.openlocfilehash: f5ab4ee77bad08ab3883645ad5e2628a265aa4e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691072"
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
  
 *Ricorsivo*  
 Una parola chiave che indica il confronto ricorsivo tra set.  
  
 *Include_Calc_Members*  
 Una parola chiave per consentire l'inclusione dei membri calcolati nei risultati del drill-down.  
  
## <a name="remarks"></a>Note  
 Questa funzione restituisce un set di membri figlio ordinati in base alla gerarchia e comprende i membri specificati nel primo set che sono presenti anche nel secondo set. Il drill-down non verrà eseguito sui membri padre se il primo set contiene il membro padre e uno o più figli. Il primo set può avere qualsiasi dimensionalità, mentre il secondo deve contenere un set unidimensionale. L'ordine originale dei membri nel primo set viene mantenuto, con la sola differenza che nel set di risultati della funzione tutti i membri figlio vengono indicati immediatamente sotto il membro padre corrispondente. La funzione ottiene il set di risultati recuperando il membro figlio di ogni membro del primo set presente anche nel secondo set. Se **RICORSIVA** viene specificata, continua la funzione Confronta ricorsivamente i membri del risultato impostati con il secondo set, recuperare gli elementi figlio per ogni membro nel set di risultati presente anche nel secondo set fino a non oltre i membri del set di risultati sono reperibile nel secondo set.  
  
 L'esecuzione di query la proprietà XMLA **MdpropMdxDrillFunctions** consente di verificare il livello di supporto che il server garantisce per le funzioni di drill, vedere [proprietà XMLA supportate &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)per informazioni dettagliate.  
  
 Il primo set può contenere tuple anziché membri. La funzione per il drill-down di tuple è un'estensione di OLE DB e restituisce un set di tuple anziché di membri.  
  
> [!IMPORTANT]  
>  Il drill-down di un membro non verrà eseguito se tale membro è immediatamente seguito da uno dei relativi figli. L'ordine dei membri nel set è rilevante per il drill-down * e il drill-up\* famiglie delle funzioni.  
  
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
  
  
