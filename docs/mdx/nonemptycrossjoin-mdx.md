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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
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
  
 *Conteggio*  
 Espressione numerica valida che specifica il numero di set da restituire.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **NonEmptyCrossjoin** restituisce il prodotto incrociato di due o più set come set, escluse le tuple vuote o le tuple senza dati forniti dalle tabelle dei fatti sottostanti. A causa del funzionamento della funzione **NonEmptyCrossjoin** , tutti i membri calcolati vengono automaticamente esclusi.  
  
 Se *count* non è specificato, la funzione Cross join tutti i set specificati ed esclude i membri vuoti dal set risultante. Se si specifica un numero di set, la funzione eseguirà il cross join dei numeri di set specificati, a partire dal primo set specificato. La funzione **NonEmptyCrossjoin** utilizza tutti i set rimanenti specificati nei set successivi specificati, ma che non sono stati aggiunti tra loro per determinare quali membri sono considerati non vuoti nel set risultante cross join. La funzione **NonEmptyCrossjoin** rispetta l'impostazione **NON_EMPTY_BEHAVIOR** delle misure calcolate.  
  
> [!IMPORTANT]  
>  Questa funzione è deprecata e non deve essere utilizzata, poiché viene mantenuta solo per gestire la compatibilità con le versioni precedenti. È invece consigliabile utilizzare la funzione [Exists (MDX)](../mdx/exists-mdx.md) con l'argomento nome gruppo di misure o la funzione [NonEmpty (MDX)](../mdx/nonempty-mdx.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
