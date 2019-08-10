---
title: Istruzione CALCULATE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a873c2a6a60e3e6283c3c24fa4b9d28757e57ffb
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893349"
---
# <a name="mdx-scripting---calculate"></a>Scripting MDX - CALCULATE


  Consente di popolare tutte le celle di un cubo con un valore di aggregazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>Argomenti  
 Nessuna  
  
## <a name="remarks"></a>Note  
 Quando si crea un cubo utilizzando [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], l'istruzione CALCULATE viene automaticamente inclusa come prima istruzione nello script MDX del cubo. L'istruzione CALCULATE indica alle celle del cubo di eseguire l'aggregazione a partire dalle celle con una granularità più bassa. Dopo l'aggregazione di una cella, l'utilizzo delle espressioni per popolare le celle con una granularità più bassa influisce sul valore aggregato delle celle con una granularità superiore. Sebbene questa aggregazione sia consigliabile nella maggior parte dei casi, è possibile non applicarla o eseguire altre istruzioni prima di questa.  
  
 L'istruzione CALCULATE non può essere inclusa in un sottocubo nidificato all'interno dello script MDX. Un sottocubo nidificato viene definito utilizzando l'istruzione SCOPE. Per ulteriori informazioni sull'istruzione SCOPE, vedere [ &#40;istruzione Scope MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  I membri calcolati non vengono aggregati.  
  
## <a name="see-also"></a>Vedere anche  
 [MDX (istruzioni &#40;di SCRIPTing MDX)&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [Nozioni fondamentali sullo scripting MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [Definire le assegnazioni e altri comandi script](https://docs.microsoft.com/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
  
