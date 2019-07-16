---
title: Operatori aritmetici | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1898f3e9807d2ea4f80f99e9a7ef27e672d58a18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017079"
---
# <a name="arithmetic-operators"></a>Operatori aritmetici


  Nel linguaggio MDX (Multidimensional Expressions) è possibile utilizzare gli operatori aritmetici per eseguire qualsiasi tipo di calcolo aritmetico, incluse addizioni, sottrazioni, moltiplicazioni e divisioni.  
  
 MDX supporta gli operatori aritmetici elencati nella tabella seguente.  
  
|Operator|Descrizione|  
|--------------|-----------------|  
|[+ (addizione)](../mdx/add-mdx.md)|Esegue la somma di due numeri.|  
|[/ (Divide)](../mdx/divide-mdx-operator-reference.md)|Esegue una divisione di un numero per un altro.|  
|[* (moltiplicazione)](../mdx/multiply-mdx.md)|Moltiplica due numeri.|  
|[- (sottrazione)](../mdx/subtract-mdx.md)|Sottrae un numero da un altro.|  
|^ (elevamento a potenza)|Eleva un numero a un altro numero.|  
  
> [!NOTE]  
>  In MDX non sono incluse funzioni per ottenere la radice quadrata di un numero. Per ottenere la radice quadrata di un numero, elevarlo alla potenza di 0,5 utilizzando l'operatore ^.  
  
## <a name="order-of-precedence"></a>Ordine di precedenza  
 L'ordine di precedenza per gli operatori aritmetici in un'espressione MDX è determinato dalle regole seguenti:  
  
-   Se un'espressione include più operatori aritmetici, verranno eseguite per prime le operazioni di moltiplicazione e divisione, seguite da sottrazione e addizione.  
  
-   Se tutti gli operatori aritmetici in un'espressione hanno la stessa precedenza, verranno applicati procedendo da sinistra a destra.  
  
-   Le espressioni tra parentesi hanno la precedenza su tutte le altre operazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento agli operatori MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Gli operatori &#40;sintassi MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
