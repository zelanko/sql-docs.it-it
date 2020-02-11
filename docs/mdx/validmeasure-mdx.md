---
title: ValidMeasure (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b3bce4baf3dc3499621f67defd40a4579e9cd460
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037948"
---
# <a name="validmeasure-mdx"></a>ValidMeasure (MDX)


  Restituisce il valore di una misura in un cubo forzando le dimensioni inapplicabili al livello Totale (o al membro predefinito se non aggregabile) al momento della restituzione del risultato per una tupla specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ValidMeasure(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Tuple_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una tupla.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **ValidMeasure** restituisce il valore di una tupla, ignorando gli attributi che non hanno alcuna relazione con il gruppo di misure della misura di cui la tupla restituisce il valore. Un attributo può non essere correlato a una misura per i due motivi riportati di seguito:  
  
-   La dimensione dell'attributo non ha alcuna relazione con il gruppo di misure della misura nella tupla.  
  
-   La dimensione dell'attributo non ha alcuna relazione con il gruppo di misure della misura, ma l'attributo di granularità non è l'attributo chiave e l'attributo di granularità non ha alcuna relazione diretta con l'attributo nella tupla.  
  
 Il comportamento specificato da questa funzione è il comportamento predefinito sul lato server ed è controllato dalla proprietà **IgnoreUnrelatedDimensions** sull'oggetto gruppo di misure.  
  
 Per ogni attributo nella tupla specificata con granularità, ovvero in una tupla in cui il membro non corrisponde a quello Totale), la coordinata corrente viene spostata nel modo seguente:  
  
-   Gli attributi correlati al membro dell'attributo specificato vengono spostati al membro esistente con il membro corrente.  
  
-   Gli attributi che stabiliscono una correlazione con il membro dell'attributo specificato vengono spostati al membro Totale oppure al membro predefinito se la gerarchia non è aggregabile.  
  
-   Gli attributi non correlati vengono spostati al membro Totale (in base alla misura).  
  
## <a name="example"></a>Esempio  
 La query seguente illustra il modo in cui la funzione ValidMeasure può essere utilizzata per eseguire l'override del comportamento della proprietà IgnoreUnrelatedDimensions. Nel cubo Adventure Works la proprietà IgnoreUnrelatedDimensions del gruppo di misure Sales Targets è impostata su False. Poiché il join tra la dimensione Date e questo gruppo di misure viene eseguito a livello di granularità Calendar Quarter, per impostazione predefinita la misura Sales Quota restituirà Null sotto il valore Calendar Quarter, sebbene sia presente un calcolo nello script MDX che alloca valori oltre il livello Month. La funzione ValidMeasure può essere utilizzata in una misura calcolata per fare in modo che la misura Sales Quota si comporti come se la proprietà IgnoreUnrelatedDimensions fosse impostata su True e per imporre la visualizzazione del valore dell'elemento Calendar Quarter corrente.  
  
```  
WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])  
SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,  
[Date].[Calendar].MEMBERS ON 1  
FROM [Adventure Works]  
```  
  
 In modo analogo, poiché il gruppo di misure Sales Targets non ha alcuna relazione con la dimensione Promotion, sotto il membro Totale di ogni gerarchia relativa a Promotion restituirà Null. Come indicato in precedenza, questo comportamento può essere modificato tramite la funzione ValidMeasure:  
  
 `WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])`  
  
 `SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,`  
  
 `[Promotion].[Promotions].members ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
