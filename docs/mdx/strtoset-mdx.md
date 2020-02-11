---
title: StrToSet (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 729dae70fce03b3dec1394900126b216d09dc497
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036794"
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)


  Restituisce il set specificato da una stringa in formato MDX (Multidimensional Expressions).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Specification*  
 Espressione stringa valida che specifica, direttamente o indirettamente, un set.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **StrToSet** restituisce il set specificato nell'espressione stringa. La funzione **StrToSet** viene in genere utilizzata con funzioni definite dall'utente per restituire una specifica set da una funzione esterna a un'istruzione MDX o quando una query MDX è parametrizzata.  
  
-   Quando viene utilizzato il flag CONSTRAINED, la specifica del set deve contenere nomi di membri completi o non qualificati oppure un set di tuple contenenti nomi di membri completi o non qualificati racchiusi tra parentesi graffe {}. Questo flag viene utilizzato per ridurre il rischio di attacchi intrusivi tramite la stringa specificata. Se si specifica una stringa non direttamente risolvibile in nomi di membro completi o non qualificati, verrà visualizzato l'errore seguente: "Le restrizioni imposte dal flag CONSTRAINED nella funzione STRTOSET sono state violate".  
  
-   Quando non viene utilizzato il flag CONSTRAINED, è possibile risolvere la specifica di set specificata in un'espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
-   Per comprendere meglio le differenze tra set e membri, vedere Utilizzo di espressioni set e Utilizzo delle espressioni di membro.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il set di membri della gerarchia dell'attributo State-Province mediante la funzione **StrToSet** . La specifica di set contiene un'espressione set MDX valida.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituito un errore a causa del flag CONSTRAINED. Sebbene la specifica di set contenga un'espressione MDX valida, per il flag CONSTRAINED la specifica di set deve includere nomi di membri completi o non qualificati.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 Nell'esempio seguente viene restituita la misura Reseller Sales Amount per Germania e Canada. La specifica di set inclusa nella stringa specificata contiene nomi di membri completi, come richiesto dal flag CONSTRAINED.  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
