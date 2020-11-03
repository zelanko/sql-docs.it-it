---
description: TopPercent (MDX)
title: Percentuale (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f275628747d0b17ede6c76f67961fe5233e788c4
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243540"
---
# <a name="toppercent-mdx"></a>TopPercent (MDX)


  Dispone un set in ordine decrescente e restituisce un set di tuple con i valori più alti il cui totale cumulativo è maggiore o uguale alla percentuale specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
TopPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Percentuale*  
 Espressione numerica valida che specifica la percentuale di tuple da restituire.  
  
> [!IMPORTANT]  
>  La *percentuale* deve essere un valore positivo. i valori negativi generano un errore.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **topercent** calcola la somma dell'espressione numerica specificata valutata sul set specificato, ordinando il set in ordine decrescente. La funzione restituisce quindi gli elementi con i valori più alti la cui percentuale cumulativa del valore sommato totale corrisponde almeno alla percentuale specificata. La funzione restituisce il subset più piccolo di un set il cui totale cumulativo corrisponde almeno alla percentuale specificata. Gli elementi restituiti sono ordinati dal più grande al più piccolo.  
  
> [!WARNING]  
>  Se *Numeric_Expression*  restituisce un valore negativo, il numero di **righe restituisce solo** una riga (1).  
>   
>  Vedere il secondo esempio per una presentazione dettagliata di questo comportamento.  
  
> [!IMPORTANT]  
>  Analogamente alla funzione [BottomPercent](../mdx/bottompercent-mdx.md) , la funzione di **percentuale di percentuale** interrompe sempre la gerarchia.  
  
## <a name="examples"></a>Esempi  

### <a name="a-return-toppercent"></a>R. Restituisci percentuale

 Nell'esempio seguente vengono restituite le migliori città che contribuiscono al primo 10% delle vendite dei rivenditori per la categoria della bicicletta. Il risultato viene disposto in ordine decrescente a iniziare con la città con il valore massimo di vendite.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopPercent  
   ({[Geography].[Geography].[City].Members}  
   , 10  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
```  
  
 Tramite l'espressione sopra indicata vengono prodotti i risultati seguenti:  
  
|City|Reseller Sales Amount|  
|-|---------------------------|  
|Toronto|$3.508.904,84|  
|Londra|$1.521.530,09|  
|Seattle|$1.209.418,16|  
|Parigi|$1.170.425,18|  
  
 Il set di dati originale può essere ottenuto con la query seguente e può restituire 588 righe:  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
Order  
   ({[Geography].[Geography].[City].Members}  
   , [Measures].[Reseller Sales Amount]  
   , BDESC  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
  
```  
  
### <a name="b-understand-the-effect-of-negative-values"></a>B. Comprendere l'effetto dei valori negativi

 La procedura dettagliata seguente consente di comprendere l'effetto dei valori negativi nell' *Numeric_Expression* . Prima compilare un contesto in cui è possibile presentare il comportamento.  
  
 Nella query seguente viene restituita una tabella di rivenditori 'Sales Amount', 'Total Product Cost' e 'Gross Profit', disposto in ordine decrescente di profitto. Per il profitto sono presenti solo valori negativi e quindi la perdita più piccola appare all'inizio.  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  ORDER( [Product].[Product Categories].[Bikes].[Touring Bikes].children, [Measures].[Reseller Gross Profit], BDESC )   ON rows  
FROM [Adventure Works]  
  
```  
  
 La query precedente restituisce i risultati seguenti: le righe della sezione centrale sono state rimosse per leggibilità.  
  
|Touring Bikes|Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157.444,56|$163.112,57|($5.668,01)|  
|Touring-2000 blu, 46|$321.027,03|$333.021,50|($11.994,47)|  
|Touring-3000 blu, 62|$87.773,61|$100.133,52|($12.359,91)|  
|...|...|...|...|  
|Touring-1000 giallo, 46|$1.016.312,83|$1.234.454,27|($218.141,44)|  
|Touring-1000 Yellow, 60|$1.184.363,30|$1.443.407,51|($259.044,21)|  
  
 Ora, se è stato richiesto di presentare le prime biciclette al 100% in base al profitto si scriverebbe una query come quella riportata di seguito.  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  TOPPERCENT( [Product].[Product Categories].[Bikes].[Touring Bikes].children, 100,[Measures].[Reseller Gross Profit] )   ON rows  
FROM [Adventure Works]  
  
```  
  
 La query chiede il cento percento (100%), ossia tutte le righe devono essere restituite. Tuttavia, poiché nel *Numeric_Expression* sono presenti valori negativi, viene restituita una sola riga.  
  
|Touring Bikes|Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157.444,56|$163.112,57|($5.668,01)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
