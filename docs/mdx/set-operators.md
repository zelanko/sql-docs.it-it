---
title: Operatori set | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6ad0b92a970c3618584365d9ad6e99420daef05d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037007"
---
# <a name="set-operators"></a>Operatori sui set


  Nel linguaggio MDX (Multidimensional Expressions) gli operatori sui set eseguono operazioni su membri o set e restituiscono set. Gli operatori sui set vengono spesso utilizzati come alternativa a molte funzioni sui set nelle espressioni MDX.  
  
 MDX supporta gli operatori sui set elencati nella tabella seguente.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[-(Eccetto)](../mdx/except-mdx-operator.md)|Restituisce le differenze tra due set, rimuovendo i membri duplicati.<br /><br /> Dal punto di vista funzionale, questo operatore equivale alla funzione [except](../mdx/except-mdx-function.md) .|  
|[* (Crossjoin)](../mdx/crossjoin-mdx-operator-reference.md)|Restituisce il prodotto incrociato di due set.<br /><br /> Dal punto di vista funzionale, questo operatore equivale alla funzione [Crossjoin](../mdx/crossjoin-mdx.md) .|  
|[: (Range)](../mdx/range-mdx.md)|Restituisce un set disposto in ordine naturale, in cui i due membri specificati costituiscono gli endpoint e tutti i membri compresi tra questi ultimi vengono inclusi come membri del set.|  
|[+ (Unione)](../mdx/union-mdx-operator-reference.md)|Restituisce l'unione di due set, escludendo i membri duplicati.<br /><br /> Dal punto di vista funzionale, questo operatore equivale alla funzione di [unione &#40;MDX&#41;](../mdx/union-mdx.md) .|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)   
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX](../mdx/mdx-operator-reference-mdx.md)   
 [Operatori &#40;sintassi MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
