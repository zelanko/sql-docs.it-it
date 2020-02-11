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
ms.openlocfilehash: 2f03c3152e3144b137c079cbdfddeff5b9cd5156
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008171"
---
# <a name="operators-dmx"></a>Operatori (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  È possibile utilizzare gli operatori DMX (Data Mining Extensions) per eseguire operazioni aritmetiche, di confronto, di concatenazione e logiche [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]in una query in.  
  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizza gli operatori per eseguire le azioni seguenti:  
  
-   Ricercare oggetti o valori che soddisfano una specifica condizione.  
  
-   Effettuare una scelta tra due valori o espressioni.  
  
 In DMX sono disponibili diverse categorie di operatori, descritti nelle sezioni seguenti. Per ulteriori informazioni sui singoli operatori, vedere la pagina relativa al [riferimento all'operatore DMX&#41; di Data Mining Extensions &#40;](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
|Categoria di operatori|Tipo di operazione|  
|-----------------------|-----------------------|  
|[Operatori aritmetici &#40;&#41;DMX](../dmx/operators-arithmetic.md)|Esecuzione di addizioni, sottrazioni, moltiplicazioni e divisioni.|  
|[Operatori di confronto &#40;DMX&#41;](../dmx/operators-comparison.md)|Confronto di un valore con un altro valore o un'espressione.|  
|[Operatori logici &#40;&#41;DMX](../dmx/operators-logical.md)|Stabilire se una condizione è vera, ad esempio AND, OR e NOT.|  
|[Operatori unari &#40;&#41;DMX](../dmx/operators-unary.md)|Esecuzione di un'operazione su un singolo operando.|  
  
 In DMX è possibile utilizzare gli operatori per combinare semplici espressioni in modo da ottenere espressioni più complesse. Nelle espressioni complesse gli operatori vengono valutati nell'ordine definito dalle regole di precedenza degli operatori di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Gli operatori con precedenza superiore vengono eseguiti prima di quelli con precedenza inferiore. Per ulteriori informazioni sulle espressioni, vedere [espressioni &#40;&#41;DMX ](../dmx/expressions-dmx.md).  
  
 Quando si combinano espressioni semplici per ottenere un'espressione complessa, il tipo di dati dell'espressione risultante viene determinato combinando le regole degli operatori con le regole sulla precedenza dei tipi di dati. Se il risultato è un carattere o un valore Unicode, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ne determina le regole di confronto combinando le regole degli operatori con le regole sulla precedenza delle regole di confronto. Sono previste inoltre regole per determinare precisione, scala e lunghezza del risultato in base alla precisione, alla scala e alla lunghezza delle varie espressioni semplici.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
