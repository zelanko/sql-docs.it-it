---
title: Operatori di confronto | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e3aa00334d98af02521005679174feb3b28c55f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68001520"
---
# <a name="comparison-operators"></a>Operatori di confronto


  Gli operatori di confronto possono essere utilizzati solo con dati scalari. È possibile utilizzare operatori di confronto in qualsiasi espressione MDX (Multidimensional Expressions).  
  
 Per verificare la presenza di una condizione, è inoltre possibile utilizzare gli operatori di confronto nelle istruzioni e nelle funzioni MDX, ad esempio la funzione MDX [IIf](../mdx/iif-mdx.md) . Se si utilizzano operatori di confronto per verificare una condizione, sarà tuttavia necessario verificare di disporre delle autorizzazioni appropriate, prima di tentare di modificare i dati in base a tale condizione. Tutti gli utenti che hanno accesso ai dati effettivi e possono eseguire query su tali dati possono utilizzare operatori di confronto in ulteriori query, ma la possibilità di effettuare l'accesso non implica che tali utenti abbiano o dovrebbero avere le autorizzazioni appropriate per modificare i dati. Per mantenere l'integrità dei dati, è inoltre consigliabile limitare il numero degli utenti autorizzati a eseguire query e a modificare i dati.  
  
 Gli operatori di confronto restituiscono un tipo di dati Boolean, ovvero TRUE o FALSE a seconda che la condizione specificata sia soddisfatta o meno.  
  
 MDX supporta gli operatori di confronto elencati nella tabella seguente.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[= (uguale a)](../mdx/equal-to-mdx.md)|Per argomenti non Null, restituisce TRUE se l'argomento a sinistra è uguale a quello a destra, FALSE in caso contrario.<br /><br /> Se uno dei due argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null, a meno che non venga eseguito il confronto `0=null`. In questo caso il valore booleano conterrà TRUE.|  
|[<>  (diverso da)](../mdx/not-equal-to-mdx.md)|Per argomenti non Null, restituisce TRUE se l'argomento a sinistra è diverso da quello a destra, FALSE in caso contrario.<br /><br /> Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[> (maggiore di)](../mdx/greater-than-mdx.md)|Per argomenti non Null, restituisce TRUE se l'argomento a sinistra ha un valore maggiore di quello a destra, FALSE in caso contrario.<br /><br /> Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[>= (maggiore o uguale a)](../mdx/greater-than-or-equal-to-mdx.md)|Per argomenti non Null, restituisce TRUE se l'argomento a sinistra ha un valore maggiore o uguale a quello a destra, FALSE in caso contrario.<br /><br /> Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[< (minore di)](../mdx/less-than-mdx.md)|Per argomenti non null, restituisce TRUE se l'argomento a sinistra ha un valore minore di quello a destra; in caso contrario, FALSE.<br /><br /> Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[<= (minore o uguale a)](../mdx/less-than-or-equal-to-mdx.md)|Per argomenti non NULL, restituisce TRUE se l'argomento a sinistra ha un valore minore o uguale a quello a destra, FALSE in caso contrario.<br /><br /> Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)   
 [Operatori &#40;sintassi MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
