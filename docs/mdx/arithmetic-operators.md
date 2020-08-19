---
description: Operatori aritmetici
title: Operatori aritmetici | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 995e7ce1cb6a3c5d06db1042c00f945ec01e1be6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494994"
---
# <a name="arithmetic-operators"></a>Operatori aritmetici


  Nel linguaggio MDX (Multidimensional Expressions) è possibile utilizzare gli operatori aritmetici per eseguire qualsiasi tipo di calcolo aritmetico, incluse addizioni, sottrazioni, moltiplicazioni e divisioni.  
  
 MDX supporta gli operatori aritmetici elencati nella tabella seguente.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[+ (addizione)](../mdx/add-mdx.md)|Esegue la somma di due numeri.|  
|[/ (divisione)](../mdx/divide-mdx-operator-reference.md)|Esegue una divisione di un numero per un altro.|  
|[* (Moltiplicazione)](../mdx/multiply-mdx.md)|Moltiplica due numeri.|  
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
 [Guida di riferimento agli operatori MDX &#40;&#41;MDX ](../mdx/mdx-operator-reference-mdx.md)   
 [Operatori &#40;sintassi MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
