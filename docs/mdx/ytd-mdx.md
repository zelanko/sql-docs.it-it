---
title: YTD (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e3fcd823dea5d651cd7be9295fa4c6bba25380c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125757"
---
# <a name="ytd-mdx"></a>Ytd (MDX)


  Restituisce i membri di un set di pari livello dallo stesso livello di un membro dato, iniziando il primo elemento di pari livello e terminando con il membro dato, in base al vincolo imposto dal *anno* livello nella dimensione temporale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Ytd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Note  
 Se non viene specificata un'espressione di membro, il valore predefinito è il membro corrente della prima gerarchia con un livello di tipo *anni* nella prima dimensione di tipo *ora* nel gruppo di misure.  
  
 Il **Ytd** è una funzione di scelta rapida per il [PeriodsToDate](../mdx/periodstodate-mdx.md) in cui la proprietà Type della gerarchia dell'attributo su cui si basa il livello è impostato su *anni*. In altre parole, `Ytd(Member_Expression)` equivale a `PeriodsToDate(Year_Level_Expression,Member_Expression)`. Si noti che questa funzione non funzionerà quando la proprietà Type è impostata su *FiscalYears*.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente restituisce la somma del `Measures.[Order Quantity]` membro, aggregato sui primi otto mesi dell'anno di calendario 2003 contenuti nella `Date` dimensione, dalle **Adventure Works** cubo.  
  
```  
WITH MEMBER [Date].[Calendar].[First8MonthsCY2003] AS  
    Aggregate(  
        YTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First8MonthsCY2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 **YTD** viene spesso usato in combinazione con nessun parametro specificato, il che significa che il [CurrentMember &#40;MDX&#41; ](../mdx/currentmember-mdx.md) funzione visualizzerà un totale cumulativo year-to-date in un report, come illustrato di nella query seguente:  
  
 `WITH MEMBER MEASURES.YTDDEMO AS`  
  
 `AGGREGATE(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDDEMO} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
