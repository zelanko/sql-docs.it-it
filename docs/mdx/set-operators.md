---
title: Operatori sui set | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df58b5c7f6da05700f00b4ec5fd46b81926dd3bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150164"
---
# <a name="set-operators"></a>Operatori sui set


  Nel linguaggio MDX (Multidimensional Expressions) gli operatori sui set eseguono operazioni su membri o set e restituiscono set. Gli operatori sui set vengono spesso utilizzati come alternativa a molte funzioni sui set nelle espressioni MDX.  
  
 MDX supporta gli operatori sui set elencati nella tabella seguente.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[- (Eccezione)](../mdx/except-mdx-operator.md)|Restituisce le differenze tra due set, rimuovendo i membri duplicati.<br /><br /> Questo operatore è funzionalmente equivalente per la [tranne](../mdx/except-mdx-function.md) (funzione).|  
|[* (Crossjoin)](../mdx/crossjoin-mdx-operator-reference.md)|Restituisce il prodotto incrociato di due set.<br /><br /> Questo operatore è funzionalmente equivalente per la [Crossjoin](../mdx/crossjoin-mdx.md) (funzione).|  
|[: (Intervallo)](../mdx/range-mdx.md)|Restituisce un set disposto in ordine naturale, in cui i due membri specificati costituiscono gli endpoint e tutti i membri compresi tra questi ultimi vengono inclusi come membri del set.|  
|[+ (Unione)](../mdx/union-mdx-operator-reference.md)|Restituisce l'unione di due set, escludendo i membri duplicati.<br /><br /> Questo operatore è funzionalmente equivalente per la [Union &#40;MDX&#41; ](../mdx/union-mdx.md) (funzione).|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Gli operatori &#40;sintassi MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
