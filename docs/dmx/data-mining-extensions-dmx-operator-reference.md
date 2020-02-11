---
title: Guida di riferimento agli operatori DMX (Data Mining Extensions) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e0dfafb74e6e86185872ea8e736b95dce7d4058
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070915"
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>Guida di riferimento agli operatori DMX (Data Mining Extensions)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Il linguaggio DMX (Data Mining Extensions) in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta operatori aritmetici, di assegnazione, di confronto, logici e unari. Gli operatori supportati da DMX sono elencati nella tabella seguente.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|[+ &#40;aggiungere&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Operatore aritmetico che esegue una somma tra due numeri.|  
|[-&#40;sottrarre&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Operatore aritmetico che sottrae un numero da un altro.|  
|[&#42; &#40;moltiplica&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Operatore aritmetico che esegue una moltiplicazione tra due numeri.|  
|[&#40;divide&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Operatore aritmetico che divide un numero per un altro.|  
|[&#60; &#40;inferiore&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è minore di quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#62; &#40;maggiore di&#41; &#40;DMX&#41;](../dmx/greater-than-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è maggiore di quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[= &#40;uguale a&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#60;&#62; &#40;diverso da&#41; &#40;DMX&#41;](../dmx/not-equal-to-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è diverso da quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#60;= &#40;minore o uguale a&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è minore o uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[&#62;= &#40;maggiore o uguale a&#41; &#40;DMX&#41;](../dmx/greater-than-or-equal-to-dmx.md)|Operatore di confronto. Per gli argomenti che restituiscono valori non Null, restituisce TRUE se il valore dell'argomento a sinistra è maggiore o uguale a quello dell'argomento a destra, FALSE in caso contrario. Se uno degli argomenti o entrambi restituiscono un valore Null, l'operatore restituirà un valore Null.|  
|[E &#40;DMX&#41;](../dmx/and-dmx.md)|Operatore logico che esegue la congiunzione di due espressioni numeriche.|  
|[NON &#40;DMX&#41;](../dmx/not-dmx.md)|Operatore logico che esegue la negazione di un'espressione numerica.|  
|[O &#40;DMX&#41;](../dmx/or-dmx.md)|Operatore logico che esegue la disgiunzione di due espressioni numeriche.|  
|[+ &#40;positivo&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|Operatore unario che restituisce il valore positivo di un'espressione numerica.|  
|[-&#40;&#41; &#40;DMX negativo&#41;](../dmx/negative-dmx.md)|Operatore unario che restituisce il valore negativo di un'espressione numerica.|  
|[Barra doppia &#40;commento&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md)|Indica una stringa di testo che non deve essere eseguita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È possibile nidificare i commenti in un'istruzione DMX, includerli alla fine di una riga di codice o inserirli in una riga distinta.|  
|[--&#40;commento&#41; &#40;Riepilogo&#41; DMX](../dmx/comment-dmx-summary.md)|Indica una stringa di testo che non deve essere eseguita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È possibile nidificare i commenti in un'istruzione DMX, includerli alla fine di una riga di codice o inserirli in una riga distinta.|  
|[Barra &#40;commento&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md)|Indica una stringa di testo che non deve essere eseguita da [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È possibile nidificare i commenti in un'istruzione DMX, includerli alla fine di una riga di codice o inserirli in una riga distinta.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Operatori &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
