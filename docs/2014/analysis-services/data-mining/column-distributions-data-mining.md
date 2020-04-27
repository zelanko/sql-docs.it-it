---
title: Distribuzioni di colonne (data mining) | Microsoft Docs
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
ms.openlocfilehash: 6c7eab32f251b9622c6ac77febf2c004806c024b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174593"
---
# <a name="column-distributions-data-mining"></a>Distribuzioni delle colonne (Data mining)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]è possibile definire le distribuzioni delle colonne in una struttura di data mining per influire sul modo in cui gli algoritmi elaborano i dati in tali colonne durante la creazione dei modelli di data mining. Per alcuni algoritmi è utile definire la distribuzione dei dati nelle colonne continue prima di elaborare il modello, se è noto che tali colonne contengono valori con distribuzioni comuni. Se non si definiscono le distribuzioni, i modelli di data mining risultanti possono produrre stime meno accurate, perché gli algoritmi dispongono di meno informazioni per l'interpretazione dei dati.

 Gli algoritmi disponibili in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supportano i tipi di distribuzioni seguenti:

 `Normal`I valori per la colonna continua formano un istogramma con una distribuzione normale.

 ![Istogramma con distribuzione normale](../media/normal-distribution.gif "Istogramma con distribuzione normale")

 `Log Normal`I valori per la colonna continua formano un istogramma, in cui la curva è allungata all'estremità superiore ed è inclinata verso l'estremità inferiore.

 ![Istogramma con distribuzione normale dei log](../media/log-normal-distribution.gif "Istogramma con distribuzione normale dei log")

 `Uniform`I valori per la colonna continua formano una curva piatta, in cui tutti i valori sono ugualmente probabili.

 ![Istogramma con distribuzione uniforme](../media/uniform-distribution.gif "Istogramma con distribuzione uniforme")

 Per altre informazioni sugli algoritmi forniti da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md).

## <a name="see-also"></a>Vedi anche
 [Tipi di contenuto &#40;data mining&#41;](content-types-data-mining.md) le strutture di data mining &#40;i metodi [di discretizzazione Analysis Services di](mining-structures-analysis-services-data-mining.md) data mining&#41;le distribuzioni &#40;di [data mining](discretization-methods-data-mining.md)&#41;[DMX &#40;](/sql/dmx/distributions-dmx) [colonne della struttura](mining-structure-columns.md) di data mining


