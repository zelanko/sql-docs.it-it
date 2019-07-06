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
manager: kfile
ms.openlocfilehash: 2dde2a96b34485fd6d460699a20055e289f2f1ad
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597473"
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
  
 *Count*  
 Espressione numerica valida che specifica il numero di tuple che devono essere restituite.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
 *Hierarchy*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
 *Ricorsivo*  
 Una parola chiave che indica il confronto ricorsivo tra set.  
  
 *Include_Calc_Members*  
 Una parola chiave per consentire l'inclusione dei membri calcolati nei risultati del drill-down.  
  
## <a name="remarks"></a>Note  
 Se viene specificata un'espressione numerica, la **DrilldownMemberTop** funzione dispone in ordine decrescente, gli elementi figlio di ogni membro nel primo set in base al valore dell'espressione numerica, valutato sul set di figlio membri. Se non viene specificata un'espressione numerica, la funzione dispone in ordine decrescente i membri figlio di ogni membro nel primo set in base ai valori delle celle rappresentate dal set di membri figlio, determinato dal contesto di query. Questo comportamento è simile alle funzioni TopCount e Head (MDX) che restituiscono un set di membri in ordine naturale, senza alcun ordinamento.  
  
 Dopo l'ordinamento, il **DrilldownMemberTop** funzione restituisce un set che contiene i membri padre e il numero di membri figlio, specificato in *conteggio,* con il valore più elevato e sono contenuti in entrambi i set .  
  
 Se **RICORSIVA** viene specificato, la funzione ordina il primo set come descritto in precedenza, quindi confronta in modo ricorsivo i membri del primo set, organizzati in una gerarchia, con il secondo set. La funzione recupera il numero più alto di membri figlio per ogni membro nel primo set presente anche nel secondo set.  
  
 Il primo set può contenere tuple anziché membri. La funzione per il drill-down di tuple è un'estensione di OLE DB e restituisce un set di tuple anziché di membri.  
  
 Il **DrilldownMemberTop** funzione è simile al [DrilldownMember](../mdx/drilldownmember-mdx.md) funzionare, ma anziché includere tutti gli elementi figlio per ogni membro nel primo set che è anche presente nel secondo set, il **DrilldownMemberTop** funzione restituisce il numero più alto di membri figlio per ogni membro.  
  
 L'esecuzione di query la proprietà XMLA MdpropMdxDrillFunctions consente di verificare il livello di supporto che il server garantisce per le funzioni di drill; visualizzare [proprietà XMLA supportate &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) per informazioni dettagliate.  
  
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
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
