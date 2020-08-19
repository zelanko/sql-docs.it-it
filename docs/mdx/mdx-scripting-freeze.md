---
description: Istruzione FREEZE (MDX)
title: Istruzione FREEZE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41c71987fec932b2693740792a8d86e200fcf526
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429743"
---
# <a name="mdx-scripting---freeze"></a>Scripting MDX - FREEZE


  Blocca sui valori correnti i valori delle celle del sottocubo specificato. Se vengono bloccati, i valori delle celle non subiscono gli effetti delle modifiche apportate ad altre celle.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>Argomenti  
 *Subcube_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un sottocubo.  
  
## <a name="remarks"></a>Osservazioni  
 L'istruzione **Freeze** blocca i valori delle celle in un sottocubo specificato, evitando che le istruzioni successive in uno script MDX modifichino i valori nei successivi passaggi di calcolo.  
  
 Nell'esempio seguente A e B rappresentano sottocubi in uno script di calcolo MDX:  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 A questo punto, sia A che B sono uguali a 3.  
  
 A questo punto si inserisce la funzione **Freeze** per bloccare le celle del sottocubo:  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 Ora A è uguale a 2 e B è uguale a 3.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di scripting MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
