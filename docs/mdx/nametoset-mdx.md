---
title: NameToSet (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 77731495eb058da05f6c61be391591a40725e579
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088388"
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)


  Restituisce un set che contiene il membro specificato da una stringa di formato Multidimensional.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Name*  
 Espressione stringa valida che rappresenta il nome di un membro.  
  
## <a name="remarks"></a>Note  
 Se il nome del membro specificato esiste, il **NameToSet** funzione restituisce un set contenente tale membro. In caso contrario, la funzione restituisce un set vuoto.  
  
> [!NOTE]  
>  Il nome del membro specificato deve essere costituito esclusivamente da un nome di membro e non può corrispondere a un'espressione di membro. Per usare un'espressione di membro, vedere [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il valore predefinito della misura per il nome del membro specificato.  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
