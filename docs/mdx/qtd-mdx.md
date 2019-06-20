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
manager: kfile
ms.openlocfilehash: 182a86a05cd0dae6adf85d2168fe884ace910a82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278416"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  Restituisce i membri di un set di pari livello dallo stesso livello di un membro dato, iniziando il primo elemento di pari livello e terminando con il membro dato, in base al vincolo imposto dal *trimestre* livello nella dimensione temporale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Note  
 Se un membro expressionis non specificato, il valore predefinito è il membro corrente della prima gerarchia con un livello di tipo *trimestri* nella prima dimensione di tipo *ora* nel gruppo di misure.  
  
 Il **Qtd** è una funzione di scelta rapida per il [PeriodsToDate &#40;MDX&#41; ](../mdx/periodstodate-mdx.md) funzione il cui argomento Level_Expression è impostato su *trimestre*. In altre parole, dal punto di vista funzionale `Qtd(Member_Expression)` equivale a `PeriodsToDate(Quarter_Level_Expression, Member_Expression)`.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente restituisce la somma del `Measures.[Order Quantity]` membro, aggregato sui primi due mesi del terzo trimestre dell'anno di calendario 2003 contenuti nella `Date` dimensione, dalle **Adventure Works** cubo.  
  
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
  
  
