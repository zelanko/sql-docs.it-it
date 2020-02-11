---
title: Istruzione FREEZE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4738dab411fe55808034a6d9d81a16994089ea74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138294"
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
 [Istruzioni di scripting MDX &#40;&#41;MDX](../mdx/mdx-scripting-statements-mdx.md)  
  
  
