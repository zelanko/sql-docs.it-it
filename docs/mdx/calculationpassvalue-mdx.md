---
title: CalculationPassValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae667d2cecb65f2525aaf855d3d1b70d40a59b21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016868"
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue (MDX)


  Restituisce il valore numerico o il valore stringa di un'espressione MDX (Multidimensional Expression) valutata sulla sessione di calcolo specificata di un cubo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      Numeric syntax  
CalculationPassValue(Numeric_Expression,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
String syntax  
CalculationPassValue(String_Expression ,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
```  
  
## <a name="arguments"></a>Argomenti  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
 *String_Expression*  
 Espressione stringa valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero espresso come stringa.  
  
 *Pass_Value*  
 Espressione numerica valida che specifica il numero della sessione di calcolo.  
  
 ABSOLUTE  
 Il valore di un flag di accesso che specifica che il *Pass_Value* parametro contiene l'indice in base zero della sessione di calcolo. ABSOLUTE è il valore del flag di accesso predefinito se non viene specificato alcun valore per il flag di accesso.  
  
 RELATIVE  
 Il valore di un flag di accesso che specifica che il *Pass_Value* parametro contiene un offset relativo dalla sessione di calcolo del calcolo del trigger. Se l'offset viene risolto in un indice di sessione di calcolo minore di 0, verrà utilizzata la sessione di calcolo 0 e non verrà generato alcun errore.  
  
 ALL  
 Quando questo flag è impostato, tutti i valori sono Null a eccezione di quelli caricati dal motore di archiviazione. Quando non è impostato, i valori vengono aggregati senza l'applicazione di alcun calcolo.  
  
## <a name="remarks"></a>Note  
 Se si specifica un'espressione numerica, la funzione restituisce un valore numerico valutando l'espressione numerica MDX specificata nella sessione di calcolo specificata, facoltativamente modificato da un flag di accesso e da un modificatore di flag di accesso.  
  
 Se viene fornita un'espressione stringa, la funzione restituisce un valore stringa valutando l'espressione stringa MDX specificata nella sessione di calcolo specificato e, facoltativamente modificato da un flag di accesso e un modificatore di flag di accesso *.*  
  
 Con la risoluzione automatica delle ricorsioni in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], questa funzione ha molte applicazioni pratiche.  
  
> [!NOTE]  
>  Solo gli amministratori possono utilizzare il **CalculationPassValue** funzione all'interno di uno script MDX. Se si esegue uno script MDX che contiene questa funzione nel contesto di un ruolo che non dispone di privilegi di amministratore, verrà generato un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
