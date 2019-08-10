---
title: Valore (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f373f626d778c4d77ec5843dca5bb11da728451d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887451"
---
# <a name="value-mdx"></a>Value (MDX)


  Restituisce il valore del membro corrente della dimensione di tipo misure che si interseca con il membro corrente delle gerarchie dell'attributo nel contesto della query.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
## <a name="remarks"></a>Note  
 La funzione **value** restituisce il valore del membro specificato sotto forma di stringa. L'argomento **value** è facoltativo perché il valore di un membro è la proprietà predefinita di un membro e è un valore che viene restituito per un membro se non viene specificato alcun altro valore. Per ulteriori informazioni sulle proprietà dei membri, vedere [proprietà &#40;intrinseche dei&#41; membri MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) e [proprietà &#40;dei membri definite&#41;dall'utente MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito il valore di un membro, così come viene esplicitamente restituito il nome di tale membro.  
  
```  
WITH MEMBER [Date].[Calendar].NumericValue as [Date].[Calendar].[July 1, 2001].Value  
MEMBER [Date].[Calendar].MemberName AS [Date].[Calendar].[July 1, 2001].Name  
  
SELECT {[Date].[Calendar].NumericValue, [Date].[Calendar].MemberName} ON 0  
from [Adventure Works]  
```  
  
 Nell'esempio seguente viene restituito il valore di un membro, come valore predefinito restituito per un membro su un asse.  
  
```  
SELECT {[Date].[Calendar].[July 1, 2001]} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [Properties &#40;MDX&#41;](../mdx/properties-mdx.md)   
 [Nome &#40;MDX&#41;](../mdx/name-mdx.md)   
 [&#40;MDX univoco&#41;](../mdx/uniquename-mdx.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
