---
description: Manipolazione dei dati MDX - CLEAR CALCULATIONS
title: Istruzione CLEAR CALCULATIONs (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 06f3fc9d29630f3f69b994c2b4e7cf809b6b9efd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387005"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>Manipolazione dei dati MDX - CLEAR CALCULATIONS


  Rimuove tutti i calcoli dal cubo e ripristina la sessione di calcolo 0 del cubo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Cube_Expression*  
 Espressione di cubo MDX (Multidimensional Expression) valida.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile omettere la clausola **from** quando il contesto del cubo è noto, ad esempio in uno script MDX.  
  
> [!NOTE]  
>  Questa istruzione può essere eseguita soltanto da un amministratore di database o del server oppure da un membro di un ruolo che ha accesso ai dati di origine nel cubo (ReadSourceData=true)  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di manipolazione dei dati MDX &#40;&#41;MDX ](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
