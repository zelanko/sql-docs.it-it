---
title: Operatori di confronto (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fcbfb95070783db002d34870e5508df5322210d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008205"
---
# <a name="operators---comparison"></a>Operatori di confronto
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  È possibile utilizzare operatori di confronto con dati scalari in qualsiasi espressione DMX (Data Mining Extensions [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]) in. Questi operatori restituiscono un tipo di dati Boolean, ovvero TRUE o FALSE a seconda che venga soddisfatta o meno la condizione specificata.  
  
 Gli operatori di confronto supportati da DMX sono indicati nella tabella seguente.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[&#60; &#40;inferiore&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è minore di quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#62; &#40;maggiore di&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è maggiore di quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[= &#40;uguale a&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#60;&#62; &#40;diverso da&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è diverso da quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#60;= &#40;minore o uguale a&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è minore o uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#62;= &#40;maggiore o uguale a&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è maggiore o uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
  
 Nelle istruzioni e nelle funzioni DMX è possibile utilizzare gli operatori di confronto anche per stabilire se una condizione è verificata o meno.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Espressioni &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
