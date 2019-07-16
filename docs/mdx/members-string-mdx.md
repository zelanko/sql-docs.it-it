---
title: I membri (String) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05df2d0a846af30d46e702c1d5489945d57c9115
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001500"
---
# <a name="members-string-mdx"></a>Members (String) (MDX)


  Restituisce un membro specificato da un'espressione stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Name*  
 Espressione stringa valida che specifica il nome di un membro.  
  
## <a name="remarks"></a>Note  
 Il **membri (String)** funzione restituisce un singolo membro il cui nome è specificato. In genere, si usa la **membri (String)** funzione con funzioni esterne, fornendo al **membri (String)** una stringa che identifica un membro di funzione e il **membri (String)**  funzione restituisce il valore per tale membro specificato.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa il **membri (String)** funzione per convertire la stringa specificata in un membro valido e quindi restituisce la misura predefinita per il membro specificato nella stringa. La stringa specificata è racchiusa tra virgolette singole. La misura predefinita è Reseller Sales Amount.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
