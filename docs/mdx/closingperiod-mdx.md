---
title: ClosingPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 102485ede0e52389d43bdb64742a2564aaa71419
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016788"
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)


  Restituisce il membro che costituisce l'ultimo elemento di pari livello tra i discendenti di un membro specificato a un livello specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione è principalmente finalizzata all'utilizzo con una dimensione di tipo temporale, ma può essere utilizzata con qualsiasi dimensione.  
  
-   Se viene specificata un'espressione di livello, la funzione **ClosingPeriod** utilizza la dimensione che contiene il livello specificato e restituisce l'ultimo elemento di pari livello tra i discendenti del membro predefinito al livello specificato.  
  
-   Se vengono specificate sia un'espressione di livello che un'espressione di membro, la funzione **ClosingPeriod** restituisce l'ultimo elemento di pari livello tra i discendenti del membro specificato al livello specificato.  
  
-   Se non viene specificata né un'espressione di livello né un'espressione di membro, la funzione **ClosingPeriod** utilizza il livello predefinito e il membro della dimensione, se presente, nel cubo con un tipo di tempo.  
  
 La funzione **ClosingPeriod** è equivalente all'istruzione MDX seguente:  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  La funzione [OpeningPeriod](../mdx/openingperiod-mdx.md) è simile alla funzione **ClosingPeriod** , ad eccezione del fatto che la funzione **OpeningPeriod** restituisce il primo elemento di pari livello anziché l'ultimo elemento di pari livello.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il valore predefinito della misura relativa al membro FY2007 della dimensione Date (il cui tipo semantico è temporale). Viene restituito questo membro poiché il livello Fiscal Year è il primo discendente del livello [Totale], la gerarchia Fiscal è la gerarchia predefinita poiché costituisce la prima gerarchia definita dall'utente nella raccolta di gerarchie e il membro FY 2007 è l'ultimo elemento di pari livello nella gerarchia a questo livello.  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituito il valore per la misura predefinita per il 30 novembre 2006 membro al livello Date. date. date per la gerarchia dell'attributo date. date. Tale membro costituisce l'ultimo elemento di pari livello del discendente del livello [Totale] nella gerarchia dell'attributo Date.Date.  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituito il valore predefinito della misura relativa al membro dicembre 2003, che costituisce l'ultimo elemento di pari livello del discendente del membro 2003 a livello di anno nella gerarchia definita dall'utente Calendar.  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituito il valore predefinito della misura relativa al membro giugno 2003, che costituisce l'ultimo elemento di pari livello del discendente del membro 2003 a livello di anno nella gerarchia definita dall'utente Fiscal.  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [OpeningPeriod &#40;&#41;MDX](../mdx/openingperiod-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;&#41;MDX](../mdx/lastsibling-mdx.md)  
  
  
