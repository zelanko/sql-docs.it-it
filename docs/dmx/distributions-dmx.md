---
title: Distribuzioni (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3c3544e73726dafa713b45cf08aba0e20631a869
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969862"
---
# <a name="distributions-dmx"></a>Distribuzioni (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  In [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è possibile definire il contenuto delle colonne in una struttura di data mining per influire sul modo in cui gli algoritmi elaborano i dati in tali colonne durante la creazione dei modelli di data mining. Per alcuni algoritmi è utile definire la distribuzione dei dati nelle colonne continue prima di elaborare il modello, se è noto che tali colonne contengono valori con distribuzioni comuni. Se non si definiscono le distribuzioni, i modelli di data mining risultanti possono produrre stime meno accurate, perché gli algoritmi dispongono di meno informazioni per l'interpretazione dei dati.  
  
 Gli algoritmi di data mining [!INCLUDE[msCoName](../includes/msconame-md.md)] supportano i tipi di distribuzioni seguenti:  
  
 **NORMALE**  
 I valori della colonna continua formano un istogramma con una distribuzione di Gauss normale.  
  
 **Logaritmica normale**  
 I valori della colonna continua formano un istogramma in cui i logaritmi dei valori seguono una distribuzione normale.  
  
 **UNIFORM**  
 I valori della colonna continua formano una curva uniforme, in cui tutti i valori hanno la stessa probabilità.  
  
 Per ulteriori informazioni sugli [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi di data mining, vedere [algoritmi di data mining &#40;Analysis Services-data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining). I provider di algoritmi di terze parti possono supportare ulteriori tipi di distribuzioni. Per determinare i tipi di distribuzione supportati da un algoritmo, utilizzare il set di righe dello schema **SUPPORTED_DISTRIBUTION_FLAGS** .  
  
 Per ulteriori informazioni sui tipi di distribuzione, vedere [distribuzioni di colonne &#40;&#41;di data mining ](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;&#41;di data mining](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
