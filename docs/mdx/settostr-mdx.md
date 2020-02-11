---
title: SetToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3965c3cc8ea2a2f2de292ca0c75e49c957e04f02
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036975"
---
# <a name="settostr-mdx"></a>SetToStr (MDX)


  Restituisce una stringa in formato MDX (Multidimensional Expression) corrispondente al set specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione viene utilizzata per trasferire una rappresentazione stringa di un set a una funzione esterna per l'analisi. La stringa restituita è racchiusa tra parentesi graffe {}, con ogni elemento del set separato da una virgola.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita una stringa contenente tutti i membri della gerarchia dell'attributo Geography.Country.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
