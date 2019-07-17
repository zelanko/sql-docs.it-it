---
title: Data Mining Extensions (DMX) di riferimento agli operatori | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e0dfafb74e6e86185872ea8e736b95dce7d4058
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070915"
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>Guida di riferimento agli operatori DMX (Data Mining Extensions)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Il linguaggio di Data Mining Extensions (DMX) nella [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta gli operatori aritmetici, assegnazione, confronto, logici e unari. Gli operatori supportati da DMX sono elencati nella tabella seguente.  
  
|Operator|Descrizione|  
|--------------|-----------------|  
|[+ &#40;Add&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Operatore aritmetico che esegue una somma tra due numeri.|  
|[- &#40;Sottrarre&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Operatore aritmetico che sottrae un numero da un altro.|  
|[&#42;&#40;Moltiplica&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Operatore aritmetico che esegue una moltiplicazione tra due numeri.|  
|[&#40;Divide&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Operatore aritmetico che divide un numero per un altro.|  
|[&#60;&#40;Minore di&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è minore di quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#62;&#40;Maggiore di&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è maggiore di quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[= &#40;Uguale a&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#60;&#62;&#40;Non è uguale a&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è diverso da quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#60;= &#40;Minore o uguale a&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è minore o uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#62;= &#40;Maggiore o uguale a&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è maggiore o uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[AND &#40;DMX&#41;](../dmx/and-dmx.md)|Operatore logico che esegue la congiunzione di due espressioni numeriche.|  
|[NOT &#40;DMX&#41;](../dmx/not-dmx.md)|Operatore logico che esegue la negazione di un'espressione numerica.|  
|[OR &#40;DMX&#41;](../dmx/or-dmx.md)|Operatore logico che esegue la disgiunzione di due espressioni numeriche.|  
|[+ &#40;Positivo&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|Operatore unario che restituisce il valore positivo di un'espressione numerica.|  
|[- &#40;Negativo&#41; &#40;DMX&#41;](../dmx/negative-dmx.md)|Operatore unario che restituisce il valore negativo di un'espressione numerica.|  
|[Doppia barra &#40;commento&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|Indica una stringa di testo che non deve essere eseguita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È possibile nidificare i commenti in un'istruzione DMX, includerli alla fine di una riga di codice o inserirli in una riga distinta.|  
|[- &#40;Commento&#41; &#40;DMX&#41; riepilogo](../dmx/comment-dmx-summary.md)|Indica una stringa di testo che non deve essere eseguita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È possibile nidificare i commenti in un'istruzione DMX, includerli alla fine di una riga di codice o inserirli in una riga distinta.|  
|[Barra asterisco &#40;commento&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|Indica una stringa di testo che non deve essere eseguita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È possibile nidificare i commenti in un'istruzione DMX, includerli alla fine di una riga di codice o inserirli in una riga distinta.|  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
