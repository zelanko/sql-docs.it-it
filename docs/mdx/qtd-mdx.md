---
title: Qtd (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8856b28d8eec76d2bc262c4209b007c0a7fa04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020645"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  Restituisce un set di membri di pari livello dallo stesso livello di un membro specificato, a partire dal primo elemento di pari livello e terminando con il membro dato, in base al vincolo del livello *trimestre* della dimensione temporale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Se non è specificata un'espressione di membro, l'impostazione predefinita è il membro corrente della prima gerarchia con un livello di tipo *trimestri* nella prima dimensione di tipo *Time* nel gruppo di misure.  
  
 La funzione **QTD** è una funzione di collegamento per la funzione [PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md) il cui argomento dell'espressione di livello è impostato su *Quarter*. In altre parole, dal punto di vista funzionale `Qtd(Member_Expression)` equivale a `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita la somma `Measures.[Order Quantity]` del membro, aggregata nei primi due mesi del terzo trimestre dell'anno di calendario 2003 contenuti nella `Date` dimensione, dal cubo **Adventure Works** .  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
