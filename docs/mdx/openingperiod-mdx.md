---
title: OpeningPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 07f94c3ed850af10120b1de7d95941bc5c90e826
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088225"
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)


  Restituisce il primo elemento di pari livello tra i discendenti di un livello specificato, facoltativamente in corrispondenza di un membro specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
OpeningPeriod( [ Level_Expression [ , Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione è principalmente finalizzata all'utilizzo con una dimensione temporale, ma può essere utilizzata con qualsiasi dimensione.  
  
-   Se viene specificata un'espressione di livello, la funzione **OpeningPeriod** utilizza la gerarchia che contiene il livello specificato e restituisce il primo elemento di pari livello tra i discendenti del membro predefinito al livello specificato.  
  
-   Se vengono specificate sia un'espressione di livello che un'espressione di membro, la funzione **OpeningPeriod** restituisce il primo elemento di pari livello tra i discendenti del membro specificato al livello specificato all'interno della gerarchia contenente il livello specificato.  
  
-   Se non viene specificata né un'espressione di livello né un'espressione di membro, la funzione **OpeningPeriod** utilizza il livello predefinito e il membro della dimensione con un tipo di tempo.  
  
> [!NOTE]  
>  La funzione [ClosingPeriod](../mdx/closingperiod-mdx.md) è simile alla funzione **OpeningPeriod** , con la differenza che la funzione **ClosingPeriod** restituisce l'ultimo elemento di pari livello anziché il primo elemento di pari livello.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il valore predefinito della misura relativa al membro FY2002 della dimensione Date (il cui tipo semantico è temporale). Viene restituito questo membro poiché il livello Fiscal Year è il primo discendente del livello [Totale], la gerarchia Fiscal è la gerarchia predefinita poiché costituisce la prima gerarchia definita dall'utente nella raccolta di gerarchie e il membro FY2002 è il primo elemento di pari livello nella gerarchia a questo livello.  
  
```  
SELECT OpeningPeriod() ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituito il valore predefinito della misura relativa al membro 1 luglio 2001 al livello Date.Date.Date della gerarchia dell'attributo Date.Date. Tale membro costituisce il primo elemento di pari livello del discendente del livello [Totale] nella gerarchia dell'attributo Date.Date.  
  
```  
SELECT OpeningPeriod([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituito il valore predefinito della misura relativa al membro gennaio 2003, che costituisce il primo elemento di pari livello del discendente del membro 2003 a livello di anno nella gerarchia definita dall'utente Calendar.  
  
```  
SELECT OpeningPeriod([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituito il valore predefinito della misura relativa al membro luglio 2002, che costituisce il primo elemento di pari livello del discendente del membro 2003 a livello di anno nella gerarchia definita dall'utente Fiscal.  
  
```  
SELECT OpeningPeriod([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Conteggio &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;&#41;MDX](../mdx/firstsibling-mdx.md)  
  
  
