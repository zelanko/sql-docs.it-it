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
ms.openlocfilehash: b4122c13a5371cc0ffe1c5c6235ad750e7fdadad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020705"
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
  
 *Indice*  
 Espressione numerica valida che specifica il numero di periodi paralleli per l'intervallo.  
  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Sebbene sia simile alla funzione [Cousin](../mdx/cousin-mdx.md) , la funzione **ParallelPeriod** è più strettamente correlata alle serie temporali. La funzione **ParallelPeriod** accetta il predecessore del membro specificato al livello specificato, trova l'elemento di pari livello del predecessore con l'intervallo specificato e infine restituisce il periodo parallelo del membro specificato tra i discendenti dell'elemento di pari livello.  
  
 La funzione **ParallelPeriod** ha i valori predefiniti seguenti:  
  
-   Se non viene specificata né un'espressione di livello né un'espressione di membro, il valore del membro predefinito è il membro corrente della prima gerarchia nella prima dimensione con un tipo di *tempo* nel gruppo di misure.  
  
-   Se viene specificata un'espressione di livello, ma non viene specificata un'espressione di membro, il valore predefinito del membro viene *Level_Expression*. **Hierarchy. CurrentMember**.  
  
-   Il valore di indice predefinito è 1.  
  
-   Il livello predefinito è il livello dell'elemento padre del membro specificato.  
  
 La funzione **ParallelPeriod** è equivalente all'istruzione MDX seguente:  
  
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
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
