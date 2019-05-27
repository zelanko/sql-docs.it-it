---
title: Distribuzioni delle colonne (Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5db71b5a94285f8ae63afeb65bec3f9807f8da27
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66085710"
---
# <a name="column-distributions-data-mining"></a>Distribuzioni delle colonne (Data mining)
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]è possibile definire le distribuzioni delle colonne di una struttura di data mining per determinare la modalità con cui gli algoritmi elaborano i dati di tali colonne durante la creazione dei modelli di data mining. Per alcuni algoritmi è utile definire la distribuzione dei dati nelle colonne continue prima di elaborare il modello, se è noto che tali colonne contengono valori con distribuzioni comuni. Se non si definiscono le distribuzioni, i modelli di data mining risultanti possono produrre stime meno accurate, perché gli algoritmi dispongono di meno informazioni per l'interpretazione dei dati.  
  
 Gli algoritmi disponibili in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supportano i tipi di distribuzioni seguenti:  
  
 `Normal`  
 I valori della colonna continua formano un istogramma con una distribuzione normale.  
  
 ![Istogramma con distribuzione normale](../media/normal-distribution.gif "istogramma con distribuzione normale")  
  
 `Log Normal`  
 I valori della colonna continua formano un istogramma in cui l'estremità superiore della curva è allungata e l'estremità inferiore è asimmetrica.  
  
 ![Istogramma con distribuzione lognormale](../media/log-normal-distribution.gif "istogramma con distribuzione lognormale")  
  
 `Uniform`  
 I valori della colonna continua formano una curva uniforme, in cui tutti i valori hanno la stessa probabilità.  
  
 ![Istogramma con distribuzione uniforme](../media/uniform-distribution.gif "istogramma con distribuzione uniforme")  
  
 Per altre informazioni sugli algoritmi forniti da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;Data mining&#41;](content-types-data-mining.md)   
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md)   
 [Metodi di discretizzazione &#40;Data mining&#41;](discretization-methods-data-mining.md)   
 [Distribuzioni &#40;DMX&#41;](/sql/dmx/distributions-dmx)   
 [Colonne della struttura di data mining](mining-structure-columns.md)  
  
  
