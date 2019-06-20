---
title: ParallelPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c1f495ce1fad9a318ea5e6c1f3fadd88f8313cd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473081"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)


  Restituisce un membro di un periodo precedente nella stessa posizione relativa del membro specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
 *Index*  
 Espressione numerica valida che specifica il numero di periodi paralleli per l'intervallo.  
  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Note  
 Pur essendo simili per il [Cousin](../mdx/cousin-mdx.md) funzione, il **ParallelPeriod** funzione è più strettamente correlata alle serie temporali. Il **ParallelPeriod** funzione recupera il predecessore del membro specificato al livello specificato, consente di trovare pari livello del predecessore con il numero di posizioni specificato e infine restituisce il periodo parallelo del membro specificato tra il discendenti dell'elemento di pari livello.  
  
 Il **ParallelPeriod** funzione contiene i valori predefiniti seguenti:  
  
-   Se viene specificata né un'espressione di livello né un'espressione di membro, il valore del membro predefinito è il membro corrente della prima gerarchia nella prima dimensione di tipo *ora* nel gruppo di misure.  
  
-   Se si specifica un'espressione di livello, ma non viene specificata un'espressione di membro, il valore del membro predefinito è *Level_Expression*. **Hierarchy.CurrentMember**.  
  
-   Il valore di indice predefinito è 1.  
  
-   Il livello predefinito è il livello dell'elemento padre del membro specificato.  
  
 Il **ParallelPeriod** funzione è equivalente all'istruzione MDX seguente:  
  
 `Cousin(Member_Expression, Ancestor(Member_Expression, Level_Expression) .Lag(Numeric_Expression))`  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il periodo parallelo per il mese di ottobre 2003 con un intervallo di tre periodi, in base al livello trimestre. Viene così restituito il mese di gennaio 2003.  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Quarter]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituito il periodo parallelo per il mese di ottobre 2003 con un intervallo di tre periodi, in base al livello semestre. Viene così restituito il mese di aprile 2002.  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Semester]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
