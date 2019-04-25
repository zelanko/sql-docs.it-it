---
title: Operatori (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 072d0a36a4803f4de1d50ba066e4e86e5d171c5c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62502052"
---
# <a name="operators-dmx"></a>Operatori (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  È possibile usare gli operatori di Data Mining Extensions (DMX) per eseguire operazioni aritmetiche, di confronto, concatenazione e operazioni logiche in una query nel [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizza gli operatori per eseguire le azioni seguenti:  
  
-   Ricercare oggetti o valori che soddisfano una specifica condizione.  
  
-   Effettuare una scelta tra due valori o espressioni.  
  
 In DMX sono disponibili diverse categorie di operatori, descritti nelle sezioni seguenti. Per altre informazioni sui singoli operatori, vedere [Data Mining Extensions &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
|Categoria di operatori|Tipo di operazione|  
|-----------------------|-----------------------|  
|[Operatori aritmetici &#40;DMX&#41;](../dmx/operators-arithmetic.md)|Esecuzione di addizioni, sottrazioni, moltiplicazioni e divisioni.|  
|[Gli operatori di confronto &#40;DMX&#41;](../dmx/operators-comparison.md)|Confronto di un valore con un altro valore o un'espressione.|  
|[Gli operatori logici &#40;DMX&#41;](../dmx/operators-logical.md)|Stabilire se una condizione è vera, ad esempio AND, OR e NOT.|  
|[Gli operatori unari &#40;DMX&#41;](../dmx/operators-unary.md)|Esecuzione di un'operazione su un singolo operando.|  
  
 In DMX è possibile utilizzare gli operatori per combinare semplici espressioni in modo da ottenere espressioni più complesse. Nelle espressioni complesse gli operatori vengono valutati nell'ordine definito dalle regole di precedenza degli operatori di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Gli operatori con precedenza superiore vengono eseguiti prima di quelli con precedenza inferiore. Per altre informazioni sulle espressioni, vedere [espressioni &#40;DMX&#41;](../dmx/expressions-dmx.md).  
  
 Quando si combinano espressioni semplici per ottenere un'espressione complessa, il tipo di dati dell'espressione risultante viene determinato combinando le regole degli operatori con le regole sulla precedenza dei tipi di dati. Se il risultato è un carattere o un valore Unicode, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ne determina le regole di confronto combinando le regole degli operatori con le regole sulla precedenza delle regole di confronto. Sono previste inoltre regole per determinare precisione, scala e lunghezza del risultato in base alla precisione, alla scala e alla lunghezza delle varie espressioni semplici.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
