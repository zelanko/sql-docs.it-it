---
title: IS (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29d251c05639d928f3ea5a9925a4cc21935e0529
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62630883"
---
# <a name="is-mdx"></a>IS (MDX)


  Esegue un confronto logico tra due espressioni di oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>Parametri  
 *Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un riferimento a un oggetto MDX.  
  
 *Expression2*  
 Espressione MDX valida che restituisce un riferimento a un oggetto MDX.  
  
## <a name="return-value"></a>Valore restituito  
 Valore booleano che restituisce **true** se entrambi gli argomenti fanno riferimento allo stesso oggetto; in caso contrario, **false**. Se il **NULL** parola chiave viene specificato, restituisce l'operatore **true** se *Expression1* è **null**; in caso contrario, **false** .  
  
## <a name="remarks"></a>Note  
 Il **IS** operatore viene spesso usato per determinare se tuple e membri sono idempotenti, vale a dire che sono esattamente equivalenti.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come utilizzare il **IS** operatore per verificare se il membro corrente su un asse è un membro specifico:  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
