---
description: FirstSibling (MDX)
title: FirstSibling (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 265c3bce4ad873ec3c5d8ae0760455f87b1855f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387477"
---
# <a name="firstsibling-mdx"></a>FirstSibling (MDX)


  Restituisce il primo membro figlio del padre di un membro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Member_Expression.FirstSibling   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
### <a name="example"></a>Esempio  
 La query seguente restituisce il primo membro di pari livello rispetto all'anno fiscale 2003 nella gerarchia Fiscal, ovvero l'anno fiscale 2002.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstSibling ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
