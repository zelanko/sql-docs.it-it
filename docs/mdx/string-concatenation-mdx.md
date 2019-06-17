---
title: + (Concatenazione di stringhe) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 292d671fb3b971c30b6e261e3b851aba1ead9b36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150009"
---
# <a name="-string-concatenation-mdx"></a>+ (concatenazione di stringhe) (MDX)


  Esegue un'operazione di stringa che concatena due o più tuple o stringhe di caratteri oppure una combinazione di stringhe e tuple.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>Parametri  
 *String_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un valore stringa.  
  
## <a name="return-value"></a>Valore restituito  
 Valore con il tipo di dati del parametro con precedenza maggiore.  
  
## <a name="remarks"></a>Note  
 È necessario che alle due espressioni sia applicato lo stesso tipo di dati oppure che un'espressione possa essere convertita in modo implicito nel tipo di dati dell'altra espressione. Se una delle due espressioni restituisce un valore Null, l'operatore restituirà il risultato dell'altra espressione.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
