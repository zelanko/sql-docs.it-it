---
title: Distribuzioni (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fda2eb169985eb670614f611764fbf149c71a42d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892797"
---
# <a name="distributions-dmx"></a>Distribuzioni (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  In [!INCLUDE[msCoName](../includes/msconame-md.md)] èpossibiledefinire[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]il contenuto delle colonne in una struttura di data mining per influire sul modo in cui gli algoritmi elaborano i dati in tali colonne durante la creazione dei modelli di data mining. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Per alcuni algoritmi è utile definire la distribuzione dei dati nelle colonne continue prima di elaborare il modello, se è noto che tali colonne contengono valori con distribuzioni comuni. Se non si definiscono le distribuzioni, i modelli di data mining risultanti possono produrre stime meno accurate, perché gli algoritmi dispongono di meno informazioni per l'interpretazione dei dati.  
  
 Gli algoritmi di data mining [!INCLUDE[msCoName](../includes/msconame-md.md)] supportano i tipi di distribuzioni seguenti:  
  
 **NORMALE**  
 I valori della colonna continua formano un istogramma con una distribuzione di Gauss normale.  
  
 **Logaritmica normale**  
 I valori della colonna continua formano un istogramma in cui i logaritmi dei valori seguono una distribuzione normale.  
  
 **UNIFORM**  
 I valori della colonna continua formano una curva uniforme, in cui tutti i valori hanno la stessa probabilità.  
  
 Per ulteriori informazioni sugli [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmi di data mining, vedere [algoritmi di data mining &#40;Analysis Services-Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining). I provider di algoritmi di terze parti possono supportare ulteriori tipi di distribuzioni. Per determinare i tipi di distribuzione supportati da un algoritmo, utilizzare il set di righe dello schema **SUPPORTED_DISTRIBUTION_FLAGS** .  
  
 Per ulteriori informazioni sui tipi di distribuzione, vedere [ &#40;data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)per le distribuzioni di colonne.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Elementi di sintassi &#40;DMX&#41; di Data Mining Extensions](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Guida di riferimento &#40;alle&#41; funzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento &#40;agli&#41; operatori DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento &#40;alle&#41; istruzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenzioni della &#40;sintassi&#41; DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funzioni &#40;di stima generali DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
