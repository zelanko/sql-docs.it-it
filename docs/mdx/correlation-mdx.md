---
description: Correlation (MDX)
title: Correlazione (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae050b681830b81ffa63ae82c714d69d54b03c91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387647"
---
# <a name="correlation-mdx"></a>Correlation (MDX)


  Restituisce il coefficiente di correlazione di coppie x-y di valori, valutato su un set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Correlation( Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression_y*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse Y.  
  
 *Numeric_Expression_x*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero che rappresenta i valori per l'asse X.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione di **correlazione** calcola il coefficiente di correlazione di due coppie di valori eseguendo prima la valutazione del set specificato rispetto alla prima espressione numerica per ottenere i valori per l'asse y. La funzione valuta quindi il set specificato in base alla seconda espressione numerica, se presente, per ottenere il set di valori per l'asse x. Se la seconda espressione numerica viene omessa, come valori per l'asse x la funzione utilizza il contesto corrente delle celle contenute nel set specificato.  
  
> [!NOTE]  
>  La funzione di **correlazione** ignora le celle vuote o le celle che contengono testo o valori logici. Tuttavia, la funzione include celle con valori zero.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
