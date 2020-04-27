---
title: Oggetti Cube (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc9b813f5310acad9d6dfa2b844adae6168fc1f9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702639"
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Oggetti cubo (Analysis Services - Dati multidimensionali)
    
## <a name="introducing-cube-objects"></a>Introduzione agli oggetti cubo  
 Un oggetto <xref:Microsoft.AnalysisServices.Cube> semplice è composto da informazioni di base, dimensioni e gruppi di misure. Le informazioni di base includono il nome e la misura predefinita del cubo, l'origine dati, la modalità di archiviazione e altro.  
  
 La raccolta Dimensions contiene il set effettivo di dimensioni utilizzate nel cubo dalla raccolta di dimensioni del database. È necessario definire tutte le dimensioni nella raccolta di dimensioni del database prima di potervi fare riferimento nel cubo. Le dimensioni private non sono disponibili [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]in.  
  
 I gruppi di misure sono set di misure nel cubo. Un gruppo di misure è una raccolta di misure con una vista origine dati comune e un set di dimensioni comune. Un gruppo di misure è l'unità di elaborazione delle misure. I gruppi di misure possono essere elaborati singolarmente, per poi essere visualizzati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|||  
|-|-|  
|Argomento||  
|[Azioni &#40;Analysis Services - Dati multidimensionali&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[Aggregations and Aggregation Designs](aggregations-and-aggregation-designs.md)||  
|[Calcoli](calculations.md)||  
|[Celle del cubo &#40;Analysis Services Dati multidimensionali&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[Proprietà dei cubi](cube-properties-multidimensional-model-programming.md)||  
|[Archiviazione di cubi &#40;Analysis Services-Dati multidimensionali&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[Traduzioni di cubi](cube-translations.md)||  
|[Relazioni tra dimensioni](dimension-relationships.md)||  
|[Indicatori KPI nei modelli multidimensionali](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[Misure e gruppi di misure](../multidimensional-models/measures-and-measure-groups.md)||  
|[Partizioni &#40;Analysis Services - Dati multidimensionali&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[prospettive](perspectives.md)||  
  
  
