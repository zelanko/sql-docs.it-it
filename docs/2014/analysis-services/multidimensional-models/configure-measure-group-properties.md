---
title: Configurare le proprietà del gruppo di misure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], measure groups
ms.assetid: fa66bdb6-60b8-413c-ac2a-00e4d09f60a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7571457847d8ffb0388608b7d634cc19261a609
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076665"
---
# <a name="configure-measure-group-properties"></a>Configurare le proprietà dei gruppi di misure
  Le proprietà dei gruppi di misure consentono di definirne il funzionamento.  
  
## <a name="measure-group-properties"></a>Proprietà dei gruppi di misure  
 Le proprietà dei gruppi di misure determinano i comportamenti dell'intero gruppo di misure e impostano i comportamenti predefiniti per alcune proprietà delle misure all'interno di un gruppo di misure.  
  
|Proprietà|Definizione|  
|--------------|----------------|  
|`AggregationPrefix`|Si applica all'archiviazione ROLAP. Assegna un prefisso comune alle viste indicizzate in SQL Server, usato per archiviare le aggregazioni per le partizioni associate a questo gruppo di misure.|  
|`DataAggregation`|Questa proprietà è riservata per utilizzi futuri e attualmente non ha alcun effetto. Pertanto, è consigliabile non modificare questa impostazione.|  
|`Description`|È possibile usare questa proprietà per documentare il gruppo di misure.|  
|`ErrorConfiguration`|Impostazioni configurabili per la gestione degli errori, relative alla gestione di chiavi duplicate, chiavi sconosciute, chiavi Null, limiti di errore, azione da eseguire in caso di rilevamento di un errore e file di log degli errori. Vedere [Configurazione errori per l'elaborazione di cubi, partizioni e dimensioni &#40;SSAS - multidimensionale&#41;](error-configuration-for-cube-partition-and-dimension-processing.md).|  
|`EstimatedRows`|Specifica il numero stimato di righe della tabella dei fatti.|  
|`EstimatedSize`|Specifica la dimensione stimata (in byte) del gruppo di misure.|  
|`ID`|Specifica l'identificatore dell'oggetto.|  
|`IgnoreUnrelatedDimensions`|Determina se le dimensioni non correlate devono essere forzate al livello principale in caso di inclusione in una query di membri di dimensioni non correlate al gruppo di misure. L'impostazione predefinita è `True`.|  
|`Name`|Nome della misura. Questa proprietà è di sola lettura.|  
|`ProactiveCaching`|Impostazioni configurabili per la gestione degli errori, relative alla gestione di chiavi duplicate, chiavi sconosciute, chiavi Null, limiti di errore, azione da eseguire in caso di rilevamento di un errore e file di log degli errori.|  
|`ProcessingMode`|Indica se l'indicizzazione e l'aggregazione devono essere eseguite durante o dopo l'elaborazione. Le opzioni sono Regular e LazyAggregations. LazyAggregations consente di eseguire l'aggregazione come attività in background.|  
|`ProcessingPriority`|Determina la priorità di elaborazione del cubo durante operazioni in background, ad esempio indicizzazione e aggregazioni lente Il valore predefinito è **0**.|  
|`StorageLocation`|Percorso di archiviazione del file system per il gruppo di misure. Se non è specificato alcun valore, il percorso verrà ereditato dal cubo contenente il gruppo di misure.|  
|`StorageMode`|Modalità di archiviazione per il gruppo di misure. I valori disponibili sono MOLAP, ROLAP o HOLAP.|  
|`Type`|Specifica il tipo del gruppo di misure.|  
  
  
