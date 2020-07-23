---
title: Tipi di contenuto (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a0c44e0ea90b253cee5564a327d49c34c1ae78a
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969892"
---
# <a name="content-types-dmx"></a>Tipi di contenuto (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Per funzionare correttamente, oltre al tipo di dati gli algoritmi di data mining richiedono anche altre informazioni, ad esempio il tipo di contenuto. Il tipo di contenuto consente all'algoritmo di determinare come utilizzare i dati nella colonna.  
  
 Ogni algoritmo supporta tipi di contenuto specifici. L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes, ad esempio, non può utilizzare colonne continue. Per utilizzare colonne continue in un modello [!INCLUDE[msCoName](../includes/msconame-md.md)], è necessario discretizzarne i dati. Per funzionare correttamente alcuni algoritmi richiedono tipi di contenuto specifici. L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series, ad esempio, richiede una colonna chiave temporale per identificare il periodo di tempo in cui sono stati raccolti i dati.  
  
 Per una descrizione completa dei tipi di contenuto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supportati da, vedere [tipi di contenuto &#40;&#41;di data mining ](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
