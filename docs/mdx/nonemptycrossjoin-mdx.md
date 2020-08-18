---
description: NonEmptyCrossjoin (MDX)
title: NonEmptyCrossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6fafaad2f6fa0f46d826bf94b26ceb6fdbe9df55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471803"
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
  
 *Numero*  
 Espressione numerica valida che specifica il numero di set da restituire.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **NonEmptyCrossjoin** restituisce il prodotto incrociato di due o più set come set, escluse le tuple vuote o le tuple senza dati forniti dalle tabelle dei fatti sottostanti. A causa del funzionamento della funzione **NonEmptyCrossjoin** , tutti i membri calcolati vengono automaticamente esclusi.  
  
 Se *count* non è specificato, la funzione Cross join tutti i set specificati ed esclude i membri vuoti dal set risultante. Se si specifica un numero di set, la funzione eseguirà il cross join dei numeri di set specificati, a partire dal primo set specificato. La funzione **NonEmptyCrossjoin** utilizza tutti i set rimanenti specificati nei set successivi specificati, ma che non sono stati aggiunti tra loro per determinare quali membri sono considerati non vuoti nel set risultante cross join. La funzione **NonEmptyCrossjoin** rispetta l'impostazione **NON_EMPTY_BEHAVIOR** delle misure calcolate.  
  
> [!IMPORTANT]  
>  Questa funzione è deprecata e non deve essere utilizzata, poiché viene mantenuta solo per gestire la compatibilità con le versioni precedenti. È invece consigliabile utilizzare la funzione [Exists (MDX)](../mdx/exists-mdx.md) con l'argomento nome gruppo di misure o la funzione [NonEmpty (MDX)](../mdx/nonempty-mdx.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
