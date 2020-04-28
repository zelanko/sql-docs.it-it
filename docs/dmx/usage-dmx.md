---
title: Utilizzo (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b961282ba6bc25caa260a3e156f843a413a5ef1a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893116"
---
# <a name="usage-dmx"></a>Utilizzo (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quando si utilizza DMX (Data Mining Extensions) per definire un nuovo modello di data mining [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]in, è necessario specificare il modo in cui l'algoritmo Data mining che compila il modello utilizzerà ogni colonna. Le colonne possono essere dei tipi seguenti:  
  
-   **Codice**  
  
-   **Key Sequence**  
  
-   **Chiave temporale**  
  
-   **Stimare**  
  
-   **PredictOnly**  
  
 In DMX le colonne non specificate vengono gestite come colonne di input.  
  
 Per elaborare correttamente un modello, è necessario indicare all'algoritmo la colonna chiave che identifica univocamente ogni riga, la colonna di destinazione per la creazione delle stime, se si sta creando un modello stimabile e le colonne da utilizzare come colonne di input per creare le relazioni che consentono di stimare la colonna di destinazione.  
  
 Le colonne specificate come tipo di **stima** vengono utilizzate come colonne di input e di output. Le colonne specificate come **PredictOnly** vengono utilizzate solo come colonne di output. Determinati algoritmi possono gestire le colonne Predict in modo diverso.  
  
 Per ulteriori informazioni sui tipi di utilizzo delle colonne [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supportati da, vedere [colonne del modello di data mining](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
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
  
  
