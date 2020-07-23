---
title: DrilldownLevelBottom (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2ddfb32ec5d7d5fb93e6dff12c41e56a7f789604
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970062"
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)


  Esegue il drill-down, fino al livello immediatamente inferiore, dei membri di livello più basso di un set al livello specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Count*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
 *Numeric_Expression*  
 facoltativo. Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
 *Include_Calc_Members*  
 facoltativo. Parola chiave che consente di aggiungere i membri calcolati ai risultati del drill-down.  
  
## <a name="remarks"></a>Osservazioni  
 Se viene specificata un'espressione numerica, la funzione **DrilldownLevelBottom** Ordina in ordine crescente gli elementi figlio di ogni membro nel set specificato, in base al valore specificato, valutato sul set di membri figlio. Se non è specificata un'espressione numerica, la funzione dispone in ordine crescente membri figlio di ciascun membro nel set specificato, in base ai valori delle celle rappresentate dal set di membri figlio, determinato dal contesto di query. Questo comportamento è simile alle funzioni BottomCount e Tail (MDX) che restituiscono un set di membri in ordine naturale, senza alcun ordinamento.  
  
 Dopo l'ordinamento, la funzione **DrilldownLevelBottom** restituisce un set contenente i membri padre e il numero di membri figlio, specificato in *count*, con il valore più basso.  
  
 La funzione **DrilldownLevelBottom** è simile alla funzione [DrilldownLevel](../mdx/drilldownlevel-mdx.md) , ma anziché includere tutti gli elementi figlio per ogni membro al livello specificato, la funzione **DrilldownLevelBottom** restituisce il numero più basso di membri figlio.  
  
 Eseguendo una query sulla proprietà XMLA MdpropMdxDrillFunctions è possibile verificare il livello di supporto fornito dal server per le funzioni di drill-through. per informazioni dettagliate, vedere [Proprietà XMLA supportate &#40;&#41;XMLA](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti gli ultimi tre membri figlio del livello Product Category in base alla misura predefinita. Nel cubo di esempio Adventure Works gli ultimi tre membri figlio per Accessories sono Tires and Tubes, Pumps e Panniers. Nella finestra Query MDX di Management Studio è possibile passare a Products | Product Categories | Members | All Products | Accessories per visualizzare l'elenco completo. È possibile incrementare l'argomento Count per restituire più membri.  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene illustrato l'uso del flag di **INCLUDE_CALC_MEMBERS** , usato per includere i membri calcolati nel livello di drill-down. La misura [Reseller Order Count] viene aggiunta all'istruzione **DrilldownLevelBottom** per garantire che i risultati siano ordinati in base a tale misura. Per visualizzare il membro calcolato, è necessario incrementare Count almeno a 9.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DrilldownLevel &#40;&#41;MDX](../mdx/drilldownlevel-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
