---
title: DrilldownMemberTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ebb3054ab25729ef5d75034dbee1d720f4dd928
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031246"
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)


  Esegue il drill-down dei membri di un set specificato presenti in un secondo set specificato, limitando il set di risultati al numero specificato di membri. La funzione esegue in alternativa il drill-down su un set di tuple utilizzando la prima gerarchia di tuple o la gerarchia specificata facoltativamente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Conteggio*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
 *Gerarchia*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
 *Ricorsiva*  
 Una parola chiave che indica il confronto ricorsivo tra set.  
  
 *Include_Calc_Members*  
 Una parola chiave per consentire l'inclusione dei membri calcolati nei risultati del drill-down.  
  
## <a name="remarks"></a>Osservazioni  
 Se viene specificata un'espressione numerica, la funzione **DrilldownMemberTop** Ordina in ordine decrescente gli elementi figlio di ogni membro nel primo set in base al valore dell'espressione numerica, valutato sul set di membri figlio. Se non viene specificata un'espressione numerica, la funzione dispone in ordine decrescente i membri figlio di ogni membro nel primo set in base ai valori delle celle rappresentate dal set di membri figlio, determinato dal contesto di query. Questo comportamento è simile alle funzioni TopCount e Head (MDX) che restituiscono un set di membri in ordine naturale, senza alcun ordinamento.  
  
 Dopo l'ordinamento, la funzione **DrilldownMemberTop** restituisce un set contenente i membri padre e il numero di membri figlio, specificato in *Count,* con il valore più alto e sono contenuti in entrambi i set.  
  
 Se viene specificato **RIcorsivo** , la funzione ordina il primo set come descritto in precedenza, quindi confronta in modo ricorsivo i membri del primo set, organizzati in una gerarchia, rispetto al secondo set. La funzione recupera il numero più alto di elementi figlio per ogni membro nel primo set presente anche nel secondo set.  
  
 Il primo set può contenere tuple anziché membri. La funzione per il drill-down di tuple è un'estensione di OLE DB e restituisce un set di tuple anziché di membri.  
  
 La funzione **DrilldownMemberTop** è simile alla funzione [DrilldownMember](../mdx/drilldownmember-mdx.md) , ma anziché includere tutti gli elementi figlio per ogni membro del primo set presente anche nel secondo set, la funzione **DrilldownMemberTop** restituisce il numero più alto di membri figlio per ogni membro.  
  
 Eseguendo una query sulla proprietà XMLA MdpropMdxDrillFunctions è possibile verificare il livello di supporto fornito dal server per le funzioni di drill-through. per informazioni dettagliate, vedere [Proprietà XMLA supportate &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
## <a name="example"></a>Esempio  
 L'esempio seguente esegue il drill-down della categoria clothing per restituire le tre sottocategorie di abbigliamento con la quantità superiore di ordini spediti.  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
