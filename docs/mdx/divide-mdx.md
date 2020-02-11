---
title: Divisione (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6184aa9d932355cd935a9131848ec27895faea5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68049303"
---
# <a name="divide-mdx"></a>Divisione (MDX)


  Esegue una divisione e restituisce il risultato alternativo o BLANK() della divisione per 0.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>Argomenti  
 *numerator*  
 Dividendo o numero da dividere.  
  
 *denominator*  
 Divisore o numero per cui dividere.  
  
 *alternateresult*  
 (Facoltativo) Il valore restituito se la divisione per zero genera un errore. Se non viene fornito, il valore predefinito è BLANK().  
  
## <a name="remarks"></a>Osservazioni  
 Il risultato alternativo nelle divisione per 0 deve essere una costante.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
