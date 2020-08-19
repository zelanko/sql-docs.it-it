---
description: Wtd (MDX)
title: WTD (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b45e583da6f7fc18712e432a0c504c3bc813141e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421885"
---
# <a name="wtd-mdx"></a>Wtd (MDX)


  Restituisce un set di membri di pari livello dallo stesso livello di un membro dato, iniziando dal primo membro di pari livello e terminando con il membro dato, in base al vincolo imposto dal livello Settimana della dimensione temporale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Se non viene specificata un'espressione di membro, l'impostazione predefinita è il membro corrente della prima gerarchia con un livello di tipo weeks nella prima dimensione di tipo time (**time. CurrentMember**) nel gruppo di misure.  
  
 La funzione **WTD** è una funzione di collegamento per la funzione [PeriodsToDate](../mdx/periodstodate-mdx.md) in cui il livello è impostato su *weeks*. In altre parole, `Wtd(Member_Expression)` equivale a `PeriodsToDate(Week_Level_Expression,Member_Expression)`.  
  
## <a name="see-also"></a>Vedere anche  
 [QTD &#40;&#41;MDX ](../mdx/qtd-mdx.md)   
 [MTD &#40;&#41;MDX ](../mdx/mtd-mdx.md)   
 [YTD &#40;&#41;MDX ](../mdx/ytd-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
