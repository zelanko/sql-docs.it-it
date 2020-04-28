---
title: Membri (String) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 05df2d0a846af30d46e702c1d5489945d57c9115
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
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
  
## <a name="remarks"></a>Osservazioni  
 La funzione **Members (String)** restituisce un singolo membro il cui nome è specificato. In genere si usa la funzione **Members (String)** con funzioni esterne, fornendo alla funzione **Members (String)** una stringa che identifica un membro e la funzione **Members (String)** restituisce il valore per il membro specificato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la funzione **Members (String)** per convertire la stringa specificata in un membro valido e quindi viene restituita la misura predefinita per il membro specificato nella stringa. La stringa specificata è racchiusa tra virgolette singole. La misura predefinita è Reseller Sales Amount.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
