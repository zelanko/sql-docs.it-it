---
description: DefaultMember (MDX)
title: DefaultMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6037d5089b9d0fa67599728ce35082432b0a570c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456671"
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
  
## <a name="remarks"></a>Osservazioni  
 Il membro predefinito di un attributo viene utilizzato per valutare le espressioni se un attributo non è incluso in una query.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la funzione **DefaultMember** , in combinazione con la funzione **Name** , per restituire il membro predefinito per la dimensione di tipo valuta di destinazione nel cubo Adventure Works. Nell'esempio viene restituito il **dollaro statunitense**. La funzione **Name** viene utilizzata per restituire il nome della misura anziché la proprietà predefinita della misura, ovvero **value**.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX ](../mdx/mdx-function-reference-mdx.md)   
 [Definire un membro predefinito](https://docs.microsoft.com/analysis-services/multidimensional-models/attribute-properties-define-a-default-member)  
  
  
