---
description: StrToSet (MDX)
title: StrToSet (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 882ab646af51d4b1edbe0a1240eaaed7cbfa5422
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386777"
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
  
-   Quando viene utilizzato il flag CONSTRAINED, la specifica del set deve contenere nomi di membri completi o non qualificati oppure un set di tuple contenenti nomi di membri completi o non qualificati racchiusi tra parentesi graffe {} . Questo flag viene utilizzato per ridurre il rischio di attacchi intrusivi tramite la stringa specificata. Se si specifica una stringa non direttamente risolvibile in nomi di membro completi o non qualificati, verrà visualizzato l'errore seguente: "Le restrizioni imposte dal flag CONSTRAINED nella funzione STRTOSET sono state violate".  
  
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
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
