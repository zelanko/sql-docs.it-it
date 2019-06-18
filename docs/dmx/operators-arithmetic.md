---
title: Operatori aritmetici (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: edbe8a3404217f330b5b62a9d433c7d560b28656
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62502691"
---
# <a name="operators---arithmetic"></a>Operatori aritmetici
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  È possibile usare gli operatori aritmetici di Data Mining Extensions (DMX) per eseguire calcoli aritmetici in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], tra cui addizione, sottrazione, moltiplicazione e divisione.  
  
 Gli operatori aritmetici supportati da DMX sono indicati nella tabella seguente.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[+ &#40;Add&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Somma due numeri.|  
|[- &#40;Subtract&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Sottrae un numero da un altro.|  
|[&#42; &#40;Multiply&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Esegue una moltiplicazione tra due numeri.|  
|[&#40;Divide&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Esegue una divisione di un numero per un altro.|  
  
 L'ordine di precedenza per gli operatori aritmetici in un'espressione DMX è determinato dalle regole seguenti:  
  
-   Se un'espressione include più operatori aritmetici, verranno eseguite per prime le operazioni di moltiplicazione e divisione, seguite da sottrazione e addizione.  
  
-   Se tutti gli operatori aritmetici di un'espressione hanno la stessa precedenza, le operazioni verranno eseguite da sinistra a destra.  
  
-   Le espressioni tra parentesi hanno la precedenza su tutte le altre operazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Expressions &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
