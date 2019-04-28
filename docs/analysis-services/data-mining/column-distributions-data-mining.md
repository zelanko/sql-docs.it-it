---
title: Distribuzioni delle colonne (Data Mining) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 83da6c1ba0a278d2d6b80f309a7bc7f6a1688ba4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724995"
---
# <a name="column-distributions-data-mining"></a>Distribuzioni delle colonne (Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]è possibile definire le distribuzioni delle colonne di una struttura di data mining per determinare la modalità con cui gli algoritmi elaborano i dati di tali colonne durante la creazione dei modelli di data mining. Per alcuni algoritmi è utile definire la distribuzione dei dati nelle colonne continue prima di elaborare il modello, se è noto che tali colonne contengono valori con distribuzioni comuni. Se non si definiscono le distribuzioni, i modelli di data mining risultanti possono produrre stime meno accurate, perché gli algoritmi dispongono di meno informazioni per l'interpretazione dei dati.  
  
 Gli algoritmi disponibili in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supportano i tipi di distribuzioni seguenti:  
  
 **Normale**  
 I valori della colonna continua formano un istogramma con una distribuzione normale.  
  
 ![Istogramma con distribuzione normale](../../analysis-services/data-mining/media/normal-distribution.gif "istogramma con distribuzione normale")  
  
 **Logaritmica normale**  
 I valori della colonna continua formano un istogramma in cui l'estremità superiore della curva è allungata e l'estremità inferiore è asimmetrica.  
  
 ![Istogramma con distribuzione lognormale](../../analysis-services/data-mining/media/log-normal-distribution.gif "istogramma con distribuzione lognormale")  
  
 **Uniforme**  
 I valori della colonna continua formano una curva uniforme, in cui tutti i valori hanno la stessa probabilità.  
  
 ![Istogramma con distribuzione uniforme](../../analysis-services/data-mining/media/uniform-distribution.gif "istogramma con distribuzione uniforme")  
  
 Per altre informazioni sugli algoritmi forniti da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;Data mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Metodi di discretizzazione &#40;Data mining&#41;](../../analysis-services/data-mining/discretization-methods-data-mining.md)   
 [Distribuzioni &#40;DMX&#41;](../../dmx/distributions-dmx.md)   
 [Colonne della struttura di data mining](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
