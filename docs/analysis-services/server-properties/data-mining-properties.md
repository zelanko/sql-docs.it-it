---
title: Proprietà di Data Mining di Analysis Services | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd1440e5ce0649d31f0ae6c0577c61e9e081a800
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072028"
---
# <a name="data-mining-properties"></a>Proprietà di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà di data mining del server elencate nelle tabelle seguenti. Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Si applica a:** solo in modalità server multidimensionale  
  
## <a name="non-specific-category"></a>Categoria Non-Specific  
 **AllowSessionMiningModels**  
 Proprietà booleana che indica se è possibile creare modelli di data mining di sessione.  
  
 Il valore predefinito di questa proprietà è False per indicare che i modelli di data mining di sessione non possono essere creati.  
  
 **AllowAdHocOpenRowsetQueries**  
 Proprietà booleana che indica se sono consentite query ad hoc su set di righe aperti.  
  
 Il valore predefinito di questa proprietà è False per indicare che le query su set di righe aperti non sono consentite durante una sessione.  
  
 **AllowedProvidersInOpenRowset**  
 Proprietà stringa che indica i provider ammessi in un set di righe aperto; comprende un elenco separato da virgole/punti e virgola di ProgID di provider o il valore [All].  
  
 **MaxConcurrentPredictionQueries**  
 Proprietà a Signed Integer a 32 bit che definisce il numero massimo di query di stima simultanee.  
  
## <a name="algorithms-category"></a>Categoria Algorithms  
 **Microsoft_Association_Rules\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_Association_Rules è attivato.  
  
 **Microsoft_Clustering\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_Clustering è attivato.  
  
 **Microsoft_Decision_Trees\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_DecisionTrees è attivato.  
  
 **Microsoft_Naive_Bayes\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_ Naive_Bayes è attivato.  
  
 **Microsoft_Neural_Network\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_Neural_Network è attivato.  
  
 **Microsoft_Sequence_Clustering\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_Sequence_Clustering è attivato.  
  
 **Microsoft_Time_Series\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_Time_Series è attivato.  
  
 **Microsoft_Linear_Regression\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_Linear_Regression è attivato.  
  
 **Microsoft_Logistic_Regression\ Enabled**  
 Proprietà booleana che indica se l'algoritmo Microsoft_Logistic_Regression è attivato.  
  
> [!NOTE]  
>  Oltre alle proprietà che definiscono i servizi data mining disponibili nel server, esistono proprietà di data mining che definiscono il comportamento di algoritmi specifici. Configurare tali proprietà quando si crea un modello di data mining singolo, non a livello di server. Per altre informazioni, vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Architettura fisica &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
