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
ms.openlocfilehash: ff995f08ffef27abca65db10ff2cd38f2dd01e95
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196965"
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
 [Nozioni fondamentali sullo scripting MDX &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [Definire le assegnazioni e altri comandi script](/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
