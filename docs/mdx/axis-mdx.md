---
description: Axis (MDX)
title: Axis (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 47e0da231b0792e0099f5e6ee4fe8eda9fb45f9d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421935"
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
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Axis** usa la posizione in base zero di un asse per restituire il set di tuple su un asse. Ad esempio, `Axis(0)` restituisce l'asse COLUMNS, `Axis(1)` restituisce l'asse ROWS e così via. Impossibile utilizzare la funzione **Axis** sull'asse dei filtri. Questa funzione può essere utilizzata per rendere i membri calcolati specifici del contesto della query eseguita. Ad esempio, potrebbe essere necessario un membro calcolato che fornisce la somma solo dei membri selezionati sull'asse delle righe. Può essere utilizzata anche per rendere la definizione di un asse dipendente dalla definizione di un altro asse: ad esempio, ordinando il contenuto dell'asse delle righe in base al valore del primo elemento sull'asse delle colonne.  
  
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
  
  
