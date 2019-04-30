---
title: Tipi (DMX) del contenuto | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 002dfef00f428f7fe87f3de06eb174e0566282c7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853489"
---
# <a name="content-types-dmx"></a>Tipi di contenuto (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Per funzionare correttamente, oltre al tipo di dati gli algoritmi di data mining richiedono anche altre informazioni, ad esempio il tipo di contenuto. Il tipo di contenuto consente all'algoritmo di determinare come utilizzare i dati nella colonna.  
  
 Ogni algoritmo supporta tipi di contenuto specifici. L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes, ad esempio, non può utilizzare colonne continue. Per utilizzare colonne continue in un modello [!INCLUDE[msCoName](../includes/msconame-md.md)], è necessario discretizzarne i dati. Per funzionare correttamente alcuni algoritmi richiedono tipi di contenuto specifici. L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series, ad esempio, richiede una colonna chiave temporale per identificare il periodo di tempo in cui sono stati raccolti i dati.  
  
 Per tipi di una descrizione completa del contenuto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supportati, vedere [tipi di contenuto &#40;Data Mining&#41;](../analysis-services/data-mining/content-types-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
