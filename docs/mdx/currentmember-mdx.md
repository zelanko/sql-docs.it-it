---
title: CurrentMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 374a38d07c3174e799d01199e20e822f85deed13
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892927"
---
# <a name="currentmember-mdx"></a>CurrentMember (MDX)


  Restituisce il membro corrente in una gerarchia specificata durante l'iterazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Hierarchy_Expression.CurrentMember  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hierarchy_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
## <a name="remarks"></a>Note  
 Il membro su cui si opera a ogni passaggio di un'iterazione in un set di membri della gerarchia corrisponde al membro corrente. La funzione **CurrentMember** restituisce tale membro.  
  
> [!IMPORTANT]  
>  Quando una dimensione contiene una sola gerarchia visibile, è possibile fare riferimento alla gerarchia con il nome della dimensione o della gerarchia poiché il nome della dimensione viene risolto in base all'unica gerarchia visibile che contiene. `Measures.CurrentMember` è ad esempio un'espressione MDX valida perché esegue la risoluzione nell'unica gerarchia nella dimensione Measures.  
  
## <a name="examples"></a>Esempi  
 Nella query seguente viene illustrato il modo in cui è possibile utilizzare **CurrentMember** per trovare il membro corrente dalle gerarchie delle colonne, delle righe e dell'asse delle sezioni:  
  
 `WITH MEMBER MEASURES.CURRENTDATE AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTPRODUCT AS`  
  
 `[Product].[Product Categories].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTMEASURE AS`  
  
 `MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTCUSTOMER AS`  
  
 `[Customer].[Customer Geography].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `[Product].[Product Categories].[Category].MEMBERS`  
  
 `*`  
  
 `{MEASURES.CURRENTDATE, MEASURES.CURRENTPRODUCT,MEASURES.CURRENTMEASURE, MEASURES.CURRENTCUSTOMER}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Customer].[Customer Geography].[Country].&[Australia])`  
  
 Il membro corrente cambia su una gerarchia utilizzata su un asse in una query. Pertanto, è possibile modificare anche il membro corrente su altre gerarchie nella stessa dimensione che non vengono utilizzate su un asse. Questo comportamento è denominato "auto-exists" ed è possibile trovare altri dettagli in [concetti chiave di &#40;Analysis Services&#41;MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services). Ad esempio, nella query seguente viene illustrato come il membro corrente sulla gerarchia di Calendar Year della dimensione Date cambia con il membro corrente sulla gerarchia Calendar, quando quest'ultimo viene visualizzato sull'asse delle righe:  
  
 `WITH MEMBER MEASURES.CURRENTYEAR AS`  
  
 `[Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `{MEASURES.CURRENTYEAR}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 **CurrentMember** è molto importante per fare in modo che i calcoli riconoscano il contesto della query in cui vengono utilizzati. Nell'esempio seguente viene restituita la quantità dell'ordine di ogni prodotto e la percentuale di quantità dell'ordine per categoria e modello, dal cubo **Adventure Works** . La funzione **CurrentMember** identifica il prodotto la cui quantità dell'ordine deve essere utilizzata durante il calcolo.  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty  
(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
