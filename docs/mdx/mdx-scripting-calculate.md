---
description: Istruzione CALCULATE (MDX)
title: Istruzione CALCULATE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6ec4d0e86c2719613527ec7ea8206f980deebc3a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429763"
---
# <a name="mdx-scripting---calculate"></a>Scripting MDX - CALCULATE


  Consente di popolare tutte le celle di un cubo con un valore di aggregazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>Argomenti  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 Quando si crea un cubo utilizzando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], l'istruzione CALCULATE viene automaticamente inclusa come prima istruzione nello script MDX del cubo. L'istruzione CALCULATE indica alle celle del cubo di eseguire l'aggregazione a partire dalle celle con una granularità più bassa. Dopo l'aggregazione di una cella, l'utilizzo delle espressioni per popolare le celle con una granularità più bassa influisce sul valore aggregato delle celle con una granularità superiore. Sebbene questa aggregazione sia consigliabile nella maggior parte dei casi, è possibile non applicarla o eseguire altre istruzioni prima di questa.  
  
 L'istruzione CALCULATE non può essere inclusa in un sottocubo nidificato all'interno dello script MDX. Un sottocubo nidificato viene definito utilizzando l'istruzione SCOPE. Per ulteriori informazioni sull'istruzione SCOPE, vedere [istruzione scope &#40;&#41;MDX ](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  I membri calcolati non vengono aggregati.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di scripting MDX &#40;&#41;MDX ](../mdx/mdx-scripting-statements-mdx.md)   
 [Nozioni fondamentali sullo scripting MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [Definire le assegnazioni e altri comandi script](https://docs.microsoft.com/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
  
