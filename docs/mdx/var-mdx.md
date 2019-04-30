---
title: Var (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14caf6e96b41fdf2e7f8b4d20f16852e890bd166
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251505"
---
# <a name="var-mdx"></a>Var (MDX)


  Restituisce la varianza del campione di un'espressione numerica valutata su un set, utilizzando la formula della popolazione non distorta (dividendo *n*).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Numeric_Expression*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
## <a name="remarks"></a>Note  
 Il **Var** funzione restituisce la varianza non distorta di un'espressione numerica specificata valutata su un set specificato.  
  
 Il **Var** funzione utilizza la formula della popolazione non distorta e il [VarP](../mdx/varp-mdx.md) funzione utilizza la formula della popolazione distorta.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
