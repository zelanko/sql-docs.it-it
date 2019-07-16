---
title: Utilizzo delle espressioni di dimensione | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0373bbda2d0c97946f15e048b7cc49175ca66669
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097159"
---
# <a name="using-dimension-expressions"></a>Utilizzo delle espressioni di dimensione


  In genere le espressioni di dimensione e di gerarchia vengono utilizzate per passare parametri a funzioni nelle espressioni MDX al fine di ottenere membri, set o tuple da una gerarchia.  
  
 Le espressioni di dimensione possono essere solo espressioni semplici perché rappresentano identificatori di oggetto. Visualizzare [espressioni &#40;MDX&#41; ](../mdx/expressions-mdx.md) per una spiegazione delle espressioni semplici e complesse.  
  
## <a name="dimension-expressions"></a>Espressioni di dimensione  
 Un'espressione di dimensione contiene un identificatore di dimensione o una funzione per le dimensioni.  
  
 Le espressioni di dimensione sono utilizzate raramente da sole. In genere infatti si specifica una gerarchia su una dimensione. L'unica eccezione è quando si utilizza la dimensione Measures perché non dispone di gerarchie.  
  
 Nell'esempio seguente viene illustrato un membro calcolato che utilizza l'espressione [Measures] insieme alle funzioni .Members e Count() per restituire il numero di membri sulla dimensione Measures:  
  
 `WITH MEMBER [Measures].[MeasureCount] AS`  
  
 `COUNT([Measures].MEMBERS)`  
  
 `SELECT [Measures].[MeasureCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 Identificatore della dimensione viene visualizzato come *Dimension_Name* nella notazione BNF utilizzata per descrivere istruzioni MDX.  
  
## <a name="hierarchy-expressions"></a>Espressioni di gerarchia  
 Analogamente alle espressioni di dimensione, anche le espressioni di gerarchia contengono un identificatore di gerarchia o una funzione per le gerarchie. Nell'esempio seguente viene illustrato l'utilizzo dell'espressione di gerarchia [Date].[Calendar], insieme alle funzioni .Levels e .Count, per restituire il numero di livelli nella gerarchia Calendar della dimensione Date:  
  
 `WITH MEMBER [Measures].[CalendarLevelCount] AS`  
  
 `[Date].[Calendar].Levels.Count`  
  
 `SELECT [Measures].[CalendarLevelCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 L'utilizzo più comune delle espressioni di gerarchia avviene insieme alla funzione .Members per restituire tutti i membri di una gerarchia. Nell'esempio seguente vengono restituiti tutti i membri di [Date].[Calendar] sull'asse delle righe:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Un identificatore di gerarchia viene visualizzato come *Dimension_Name.Hierarchy_Name* nella notazione BNF utilizzata per descrivere istruzioni MDX.  
  
## <a name="see-also"></a>Vedere anche  
 [Le espressioni &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
