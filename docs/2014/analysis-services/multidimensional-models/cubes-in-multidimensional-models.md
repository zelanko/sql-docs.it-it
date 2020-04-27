---
title: Cubi nei modelli multidimensionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OLAP objects [Analysis Services], cubes
- cubes [Analysis Services], about cubes
- cubes [Analysis Services]
- OLAP [Analysis Services], cubes
ms.assetid: e0f7acf3-4b07-41fc-a5fc-ac30b4a56c54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7ce00bc87ca17c97996023d7cb9a4745b9882f3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076112"
---
# <a name="cubes-in-multidimensional-models"></a>Cubi nei modelli multidimensionali
  Un cubo è una struttura multidimensionale che contiene informazioni per scopi analitici. Un cubo è principalmente costituito da dimensioni e misure. Le dimensioni definiscono la struttura del cubo utilizzata per effettuare delle sezioni, mentre le misure forniscono valori numerici aggregati di interesse per l'utente finale. Come struttura logica, un cubo consente a un'applicazione client di recuperare i valori delle misure, come se si trovassero nelle celle del cubo. Le celle vengono definite per ogni possibile valore riepilogato. Una cella del cubo è definita dall'intersezione dei membri della dimensione e contiene i valori aggregati delle misure a quell'intersezione specifica.  
  
## <a name="benefits-of-using-cubes"></a>Vantaggi derivanti dall'utilizzo dei cubi  
 Un cubo rappresenta un contenitore in cui vengono archiviati tutti i dati correlati a scopo di analisi.  
  
## <a name="components-of-cubes"></a>Componenti dei cubi  
 Un cubo è composto dagli elementi seguenti:  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|Dimensioni|[Dimensioni nei modelli multidimensionali](dimensions-in-multidimensional-models.md)|  
|Misure e gruppi di misure|[Creare misure e gruppi di misure nei modelli multidimensionali](create-measures-and-measure-groups-in-multidimensional-models.md)|  
|Partizioni|[Partizioni nei modelli multidimensionali](partitions-in-multidimensional-models.md)|  
|prospettive|[Prospettive nei modelli multidimensionali](perspectives-in-multidimensional-models.md)|  
|Gerarchie|[Creare gerarchie definite dall'utente](user-defined-hierarchies-create.md)|  
|Azioni|[Azioni nei modelli multidimensionali](actions-in-multidimensional-models.md)|  
|Indicatori KPI|[Indicatori KPI nei modelli multidimensionali](key-performance-indicators-kpis-in-multidimensional-models.md)|  
|Calcoli|[Calcoli nei modelli multidimensionali](calculations-in-multidimensional-models.md)|  
|Traduzioni|[Traduzioni nei modelli multidimensionali](translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Creare un cubo mediante la Creazione guidata cubo](create-a-cube-using-the-cube-wizard.md)|Viene illustrato come utilizzare la Creazione guidata cubo per definire un cubo, le dimensioni, gli attributi delle dimensioni e le gerarchie definite dall'utente.|  
|[Creare misure e gruppi di misure nei modelli multidimensionali](create-measures-and-measure-groups-in-multidimensional-models.md)|Descrive come definire i gruppi di misure.|  
|[Calcoli nei modelli multidimensionali](calculations-in-multidimensional-models.md)|Descrive come definire e configurare un calcolo in uno script MDX.|  
|[Azioni nei modelli multidimensionali](actions-in-multidimensional-models.md)|Descrive come definire e configurare un'azione.|  
|[Prospettive nei modelli multidimensionali](perspectives-in-multidimensional-models.md)|Descrive come definire e configurare una prospettiva.|  
|[Definizione delle stored procedure](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|Descrive come utilizzare le stored procedure.|  
  
  
