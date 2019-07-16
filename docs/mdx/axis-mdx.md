---
title: Asse (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa65c1531be29273c0a838b978109bbd1c8a2b18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016986"
---
# <a name="axis-mdx"></a>Axis (MDX)


  Restituisce il set di tuple su un asse specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>Argomenti  
 *Axis_Number*  
 Espressione numerica valida che specifica il numero dell'asse.  
  
## <a name="remarks"></a>Note  
 Il **asse** funzione utilizza la posizione in base zero di un asse per restituire il set di tuple su un asse. Ad esempio, `Axis(0)` restituisce l'asse COLUMNS, `Axis(1)` restituisce l'asse ROWS e così via. Il **asse** funzione non può essere utilizzata sull'asse del filtro. Questa funzione può essere utilizzata per rendere i membri calcolati specifici del contesto della query eseguita. Ad esempio, potrebbe essere necessario un membro calcolato che fornisce la somma solo dei membri selezionati sull'asse delle righe. Può essere utilizzata anche per rendere la definizione di un asse dipendente dalla definizione di un altro asse: ad esempio, ordinando il contenuto dell'asse delle righe in base al valore del primo elemento sull'asse delle colonne.  
  
> [!NOTE]  
>  Un asse può fare riferimento solo a un asse precedente. Ad esempio, `Axis(0)` deve essere successiva alla valutazione dell'asse COLUMNS, come avviene quando viene eseguita su un asse ROW o PAGE.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio di query seguente viene illustrato l'utilizzo della funzione Axis:  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SETTOSTR(AXIS(1))`  
  
 `SELECT MEASURES.AXISDEMO ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Nell'esempio seguente viene illustrato come utilizzare la funzione Axis all'interno di un membro calcolato:  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SUM(AXIS(1), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.AXISDEMO} ON 0,`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
