---
title: MemberValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 73a54986a951095b16465cd4934b4dfd447d38bb
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63456713"
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)


  Restituisce il valore di un membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="return-value"></a>Valore restituito  
 Il valore del membro restituito contiene le informazioni seguenti, elencate in base all'ordine in cui appaiono nel valore restituito:  
  
-   Associazione del valore, se definita.  
  
-   Chiave con il tipo di dati originale se non esiste un'associazione del nome oppure se la chiave e la didascalia sono associate alla stessa colonna.  
  
-   Didascalia del membro.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono restituiti l'associazione del valore, la chiave del membro e la didascalia della prima data nella dimensione Date del cubo Adventure Works.  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
