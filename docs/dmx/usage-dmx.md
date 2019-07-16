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
ms.openlocfilehash: 4f576243ead99869ae4b12dfc4e79a1a6d57f5cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939898"
---
# <a name="usage-dmx"></a>Utilizzo (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quando si usa Data Mining Extensions (DMX) per definire un nuovo modello di data mining in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], è necessario specificare come algoritmo di data mining che compila il modello di utilizzo di ciascuna colonna. Le colonne possono essere dei tipi seguenti:  
  
-   **Key**  
  
-   **Sequenza di tasti**  
  
-   **Chiave temporale**  
  
-   **Predict**  
  
-   **PredictOnly**  
  
 In DMX le colonne non specificate vengono gestite come colonne di input.  
  
 Per elaborare correttamente un modello, è necessario indicare all'algoritmo la colonna chiave che identifica univocamente ogni riga, la colonna di destinazione per la creazione delle stime, se si sta creando un modello stimabile e le colonne da utilizzare come colonne di input per creare le relazioni che consentono di stimare la colonna di destinazione.  
  
 Le colonne specificate come le **Predict** tipo vengono utilizzate come colonne di input e di output. Le colonne specificate come **PredictOnly** vengono usati solo come colonne di output. Determinati algoritmi possono gestire le colonne Predict in modo diverso.  
  
 Per altre informazioni sulla colonna utilizzo tipi [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supportati, vedere [colonne del modello di Data Mining](../analysis-services/data-mining/mining-model-columns.md).  
  
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
  
  
