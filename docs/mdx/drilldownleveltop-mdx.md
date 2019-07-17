---
title: DrilldownLevelTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 461c91d7261b42b5828e2c515a89e8203f40e357
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049271"
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)


  Esegue il drill-down, fino al livello immediatamente inferiore, dei membri di livello più alto di un set al livello specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Count*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
 *Include_Calc_Members*  
 Parola chiave per l'aggiunta di membri calcolati ai risultati del drill-down.  
  
## <a name="remarks"></a>Note  
 Se viene specificata un'espressione numerica, la **DrilldownLevelTop** funzione dispone in ordine decrescente, gli elementi figlio di ogni membro nel set specificato in base al valore dell'espressione numerica, valutato sul set di figlio membri. Se non viene specificata un'espressione numerica, la funzione dispone in ordine decrescente i membri figlio di ogni membro nel set specificato in base ai valori delle celle rappresentate dal set di membri figlio, come determinato dal contesto della query.  
  
 Dopo l'ordinamento, il **DrilldownLevelTop** funzione restituisce un set che contiene i membri padre e il numero di membri figlio, specificato in *conteggio,* con il valore più alto.  
  
 Il **DrilldownLevelTop** funzione è simile al [DrilldownLevel](../mdx/drilldownlevel-mdx.md) funzione, ma anziché includere tutti gli elementi figlio di ogni membro nel livello specificato, il **DrilldownLevelTop** funzione restituisce il numero più alto di membri figlio.  
  
 L'esecuzione di query la proprietà XMLA MdpropMdxDrillFunctions consente di verificare il livello di supporto che il server garantisce per le funzioni di drill; visualizzare [proprietà XMLA supportate &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) per informazioni dettagliate.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente restituisce i primi tre membri figlio del livello Product Category in base alla misura predefinita. Nel cubo di esempio Adventure Work i primi tre membri figlio per Accessories sono Bike Racks, Bike Stands e Bottles and Cages. Nella finestra Query MDX di Management Studio è possibile passare a Products | Product Categories | Members | All Products | Accessories per visualizzare l'elenco completo. È possibile incrementare l'argomento Count per restituire più membri.  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 L'esempio seguente viene illustrato l'utilizzo di **include_calc_members** flag, per includere i membri calcolati di drill-down a livello di. La misura [Reseller Order Count] viene inclusa nella **DrilldownLevelTop** istruzione per assicurare che i valori restituiti vengono ordinati in base a tale misura.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
