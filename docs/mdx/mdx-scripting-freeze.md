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
manager: kfile
ms.openlocfilehash: cd652a9f308bd7a564a61d165f9c47875a900737
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187573"
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
  
## <a name="remarks"></a>Note  
 Il **FREEZE** istruzione blocca i valori delle celle del sottocubo specificato, impedendo le successive istruzioni MDX passa script dalla modifica dei valori nel calcolo successivo.  
  
 Nell'esempio seguente A e B rappresentano sottocubi in uno script di calcolo MDX:  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 A questo punto, sia A che B sono uguali a 3.  
  
 Viene ora inserita la **Freeze** funzione per bloccare le celle nel sottocubo A:  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 Ora A è uguale a 2 e B è uguale a 3.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di scripting MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
