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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68088388"
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)


  Restituisce un set contenente il membro specificato da una stringa in formato MDX (Multidimensional Expressions).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Name*  
 Espressione stringa valida che rappresenta il nome di un membro.  
  
## <a name="remarks"></a>Osservazioni  
 Se il nome del membro specificato esiste, la funzione **NameToSet** restituisce un set contenente tale membro. In caso contrario, la funzione restituisce un set vuoto.  
  
> [!NOTE]  
>  Il nome del membro specificato deve essere costituito esclusivamente da un nome di membro e non può corrispondere a un'espressione di membro. Per usare un'espressione di membro, vedere [StrToSet &#40;&#41;MDX ](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituito il valore predefinito della misura per il nome del membro specificato.  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
