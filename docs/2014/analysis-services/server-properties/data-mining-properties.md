---
title: Proprietà di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ClusterCount property
- AllowedProvidersInOpenRowset property
- MinimumSeriesValue property
- ScoreMethod property
- MinimumImportance property
- ModellingCardinality property
- BrentTolerance property
- ComplexityPenalty property
- MaximumItemsetCount property
- MinimumSupport property
- AllowSessionMiningModels property
- HoldoutPercentage property
- ClusterCountPrior property
- MaximumSequenceStates property
- OptimizedPredictionCount property
- data mining [Analysis Services], properties
- MaximumStates property
- MaximumContinuousInputAttributes property
- MaximumOutputAttributes property
- AllowAdHocOpenRowsetQueries property
- Enabled property
- HistoricModelGap property
- SampleSize property
- MaximumInputAttributes property
- PeriodicityHint property
- MissingValueSubstitution property
- SplitMethod property
- ForceRegressor property
- MaximumBucketsForContinuousSplit property
- MaxConcurrentPredictionQueries property
- MinimumItemsetSize property
- AcyclicGraph property
- HoldoutMethod property
- StoppingTolerance property
- properties [data mining]
- AutoDetectPeriodicity property
- HoldoutTolerance property
- MinimumLeafCases property
- HoldoutSeed property
- MinimumClusterCases property
- ClusterCountDeviation property
- MinimumDependencyProbability property
- ClusteringMethod property
- MaximumItemsetSize property
- HiddenNodeRatio property
- MaximumSeriesValue property
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96106fc8bc50a2a1b19c54a6970eeeb72952d82d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069063"
---
# <a name="data-mining-properties"></a>Proprietà di data mining
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà di data mining del server elencate nelle tabelle seguenti. Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Si applica a:** Solo modalità server multidimensionale  
  
## <a name="non-specific-category"></a>Categoria Non-Specific  
 `AllowSessionMiningModels`  
 Proprietà booleana che indica se è possibile creare modelli di data mining di sessione.  
  
 Il valore predefinito di questa proprietà è False per indicare che i modelli di data mining di sessione non possono essere creati.  
  
 `AllowAdHocOpenRowsetQueries`  
 Proprietà booleana che indica se sono consentite query ad hoc su set di righe aperti.  
  
 Il valore predefinito di questa proprietà è False per indicare che le query su set di righe aperti non sono consentite durante una sessione.  
  
 `AllowedProvidersInOpenRowset`  
 Proprietà stringa che indica i provider ammessi in un set di righe aperto; comprende un elenco separato da virgole/punti e virgola di ProgID di provider o il valore [All].  
  
 `MaxConcurrentPredictionQueries`  
 Proprietà a Signed Integer a 32 bit che definisce il numero massimo di query di stima simultanee.  
  
## <a name="algorithms-category"></a>Categoria Algorithms  
 `Microsoft_Association_Rules\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_Association_Rules è attivato.  
  
 `Microsoft_Clustering\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_Clustering è attivato.  
  
 `Microsoft_Decision_Trees\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_DecisionTrees è attivato.  
  
 `Microsoft_Naive_Bayes\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_ Naive_Bayes è attivato.  
  
 `Microsoft_Neural_Network\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_Neural_Network è attivato.  
  
 `Microsoft_Sequence_Clustering\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_Sequence_Clustering è attivato.  
  
 `Microsoft_Time_Series\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_Time_Series è attivato.  
  
 `Microsoft_Linear_Regression\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_Linear_Regression è attivato.  
  
 `Microsoft_Logistic_Regression\ Enabled`  
 Proprietà booleana che indica se l'algoritmo Microsoft_Logistic_Regression è attivato.  
  
> [!NOTE]  
>  Oltre alle proprietà che definiscono i servizi data mining disponibili nel server, esistono proprietà di data mining che definiscono il comportamento di algoritmi specifici. Configurare tali proprietà quando si crea un modello di data mining singolo, non a livello di server. Per altre informazioni, vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Architettura fisica &#40;Analysis Services-&#41;di data mining](../data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Configurare le proprietà del server in Analysis Services](server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
