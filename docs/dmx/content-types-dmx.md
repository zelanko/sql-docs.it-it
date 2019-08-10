---
title: Tipi di contenuto (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: da8a5e5602b877c12284d8410f6b2a1c7da6bc58
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889148"
---
# <a name="content-types-dmx"></a>Tipi di contenuto (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Per funzionare correttamente, oltre al tipo di dati gli algoritmi di data mining richiedono anche altre informazioni, ad esempio il tipo di contenuto. Il tipo di contenuto consente all'algoritmo di determinare come utilizzare i dati nella colonna.  
  
 Ogni algoritmo supporta tipi di contenuto specifici. L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes, ad esempio, non può utilizzare colonne continue. Per utilizzare colonne continue in un modello [!INCLUDE[msCoName](../includes/msconame-md.md)], è necessario discretizzarne i dati. Per funzionare correttamente alcuni algoritmi richiedono tipi di contenuto specifici. L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series, ad esempio, richiede una colonna chiave temporale per identificare il periodo di tempo in cui sono stati raccolti i dati.  
  
 Per una descrizione completa dei tipi di contenuto supportati [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] da, vedere [data mining &#40;&#41;dei tipi di contenuto](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining).  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Elementi di sintassi &#40;DMX&#41; di Data Mining Extensions](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Guida di riferimento &#40;alle&#41; funzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento &#40;agli&#41; operatori DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento &#40;alle&#41; istruzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenzioni della &#40;sintassi&#41; DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funzioni &#40;di stima generali DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
