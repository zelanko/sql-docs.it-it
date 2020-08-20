---
description: Ordinal (MDX)
title: Ordinale (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 74811da22f8c73536749acad41dfbe859b00eeea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471733"
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)


  Restituisce il valore ordinale in base zero associato a un livello.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>Argomenti  
 *Level_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un livello.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **ordinale** viene spesso utilizzata insieme alle funzioni **IIf** e **CurrentMember** per visualizzare in modo condizionale valori diversi a livelli di gerarchia diversi, in base alla posizione ordinale di ogni cella specifica nel risultato della query. Ad esempio, è possibile usare la funzione **ordinale** per eseguire calcoli a determinati livelli e visualizzare il valore predefinito "N/a" ad altri livelli.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il numero ordinale corrispondente al livello Calendar Quarter nella gerarchia Calendar.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
