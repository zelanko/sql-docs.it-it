---
title: NonEmptyCrossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d152b51e0c1c996e0bb3309e554a70683937493
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088349"
---
# <a name="nonemptycrossjoin-mdx"></a>NonEmptyCrossjoin (MDX)


  Restituisce un set che contiene il prodotto incrociato di uno o più set, escludendo le tuple vuote e le tuple a cui non sono associati dati di tabelle dei fatti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
NonEmptyCrossjoin(Set_Expression1 [ ,Set_Expression2,...] [,Count ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Count*  
 Espressione numerica valida che specifica il numero di set da restituire.  
  
## <a name="remarks"></a>Note  
 Il **NonEmptyCrossjoin** funzione restituisce il prodotto incrociato di due o più set di set, escludendo le tuple vuote o le tuple senza dati ottenuti dalle tabelle dei fatti sottostanti. A causa di come la **NonEmptyCrossjoin** funzione lavori, tutti calcolati i membri vengono automaticamente esclusi.  
  
 Se *conteggio* non viene specificato, la funzione cross join tutti i set specificati ed esclude i membri vuoti dal set risultante. Se si specifica un numero di set, la funzione eseguirà il cross join dei numeri di set specificati, a partire dal primo set specificato. Il **NonEmptyCrossjoin** funzione Usa tutti i set rimanenti specificati nei set successivi, ma che non sono stati cross join, per determinare quali membri sono considerati non vuoti in risultante dal cross set unito. Il **NonEmptyCrossjoin** funzione rispetta le **NON_EMPTY_BEHAVIOR** impostazione delle misure calcolate.  
  
> [!IMPORTANT]  
>  Questa funzione è deprecata e non deve essere utilizzata, poiché viene mantenuta solo per gestire la compatibilità con le versioni precedenti. È invece consigliabile usare la [Exists (MDX)](../mdx/exists-mdx.md) canonica con gli argomenti Nome gruppo di misure o il [NonEmpty (MDX)](../mdx/nonempty-mdx.md) (funzione).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
