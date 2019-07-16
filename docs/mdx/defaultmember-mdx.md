---
title: DefaultMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c5843ec42cf4ba712a2e55c9cc96dd6f482c0760
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047087"
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)


  Restituisce il membro predefinito di una gerarchia.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hierarchy_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce una gerarchia.  
  
## <a name="remarks"></a>Note  
 Il membro predefinito di un attributo viene utilizzato per valutare le espressioni se un attributo non è incluso in una query.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa il **DefaultMember** funzione, in combinazione con la **nome** funzione per restituire il membro predefinito per la dimensione Destination Currency nel cubo Adventure Works. Nell'esempio viene restituito **dollaro Statunitense**. Il **Name** funzione viene utilizzata per restituire il nome della misura anziché la proprietà predefinita della misura, ovvero **valore**.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Definire un membro predefinito](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
