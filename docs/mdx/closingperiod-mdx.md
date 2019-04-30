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
manager: kfile
ms.openlocfilehash: c6c9dea03a4b09ae4dcbe66e6712a542b1920ce0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181587"
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
  
## <a name="remarks"></a>Note  
 Questa funzione è principalmente finalizzata all'utilizzo con una dimensione di tipo temporale, ma può essere utilizzata con qualsiasi dimensione.  
  
-   Se viene specificata un'espressione di livello, il **ClosingPeriod** funzione utilizza la dimensione che contiene il livello specificato e restituisce l'ultimo elemento di pari livello tra i discendenti del membro predefinito al livello specificato.  
  
-   Se vengono specificate sia un'espressione di livello che un'espressione di membro, il **ClosingPeriod** funzione restituisce l'ultimo elemento di pari livello tra i discendenti del membro specificato al livello specificato.  
  
-   Se viene specificata né un'espressione di livello né un'espressione di membro, il **ClosingPeriod** funzione Usa il livello predefinito e un membro della dimensione (se presente) del cubo con un tipo temporale.  
  
 Il **ClosingPeriod** funzione è equivalente all'istruzione MDX seguente:  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)` (Indici per tabelle con ottimizzazione per la memoria).  
  
> [!NOTE]  
>  Il [OpeningPeriod](../mdx/openingperiod-mdx.md) funzione è simile al **ClosingPeriod** funzionare, tranne il fatto che il **OpeningPeriod** funzione restituisce il primo elemento di pari livello anziché l'ultimo elemento di pari livello.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il valore predefinito della misura relativa al membro FY2007 della dimensione Date (il cui tipo semantico è temporale). Viene restituito questo membro poiché il livello Fiscal Year è il primo discendente del livello [Totale], la gerarchia Fiscal è la gerarchia predefinita poiché costituisce la prima gerarchia definita dall'utente nella raccolta di gerarchie e il membro FY 2007 è l'ultimo elemento di pari livello nella gerarchia a questo livello.  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 L'esempio seguente restituisce il valore predefinito della misura per il 30 novembre 2006 membro al livello di gerarchia dell'attributo date. Tale membro costituisce l'ultimo elemento di pari livello del discendente del livello [Totale] nella gerarchia dell'attributo Date.Date.  
  
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
 [OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)  
  
  
