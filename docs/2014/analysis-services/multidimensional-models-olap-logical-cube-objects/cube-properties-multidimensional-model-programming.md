---
title: Proprietà cubo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Collation property
- ID property
- ErrorConfiguration property
- cubes [Analysis Services], properties
- Description property
- DefaultMeasure property
- ProcessingMode property
- AggregationPrefix property
- EstimatedRows property
- Visible property
- StorageLocation property
- StorageMode property
- ScriptErrorHandlingMode property
- Source property
- ScriptCacheProcessingMode property
- Language property
- Name property
- properties [Analysis Services], cubes
- ProcessingPriority property
- ProactiveCaching property
ms.assetid: 72ca3387-620d-4473-8e23-7fe1f2b3d5bf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d2b99362f242ff7f815e9ceb9f67db9c80983c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727647"
---
# <a name="cube-properties"></a>Proprietà dei cubi
  I cubi dispongono di proprietà che è possibile impostare per influire sul funzionamento a livello di cubo. Nella tabella seguente è disponibile un riepilogo di tali proprietà.  
  
> [!NOTE]  
>  Alcune proprietà vengono impostate automaticamente quando si crea il cubo e non possono essere modificate.  
  
 Per ulteriori informazioni su come impostare le proprietà del cubo, vedere [Progettazione cubi &#40;Analysis Services-&#41;di dati multidimensionali ](../cube-designer-analysis-services-multidimensional-data.md).  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`AggregationPrefix`|Specifica il prefisso comune utilizzato per i nomi di aggregazioni.|  
|`Collation`|Specifica l'identificatore delle impostazioni locali (LCID) e il flag di confronto, separati da un carattere di sottolineatura, ad esempio Latin1_General_C1_AS.|  
|`DefaultMeasure`|Contiene un'espressione MDX (Multidimensional Expression) che definisce la misura predefinita per il cubo.|  
|`Description`|Fornisce una descrizione del cubo, che può essere esposta in applicazioni client.|  
|`ErrorConfiguration`|Contiene le impostazioni configurabili per la gestione degli errori, relative alla gestione di chiavi duplicate, chiavi sconosciute, limiti di errore, azione da intraprendere in caso di rilevamento di un errore, file di log degli errori e gestione della chiave Null.|  
|`EstimatedRows`|Specifica il numero di righe stimate nel cubo.|  
|`ID`|Contiene l'identificatore univoco (ID) del cubo.|  
|`Language`|Specifica l'identificatore della lingua predefinita del cubo.|  
|`Name`|Specifica il nome descrittivo del cubo.|  
|`ProactiveCaching`|Definisce le impostazioni di memorizzazione nella cache attiva per il cubo.|  
|`ProcessingMode`|Indica se l'indicizzazione e l'aggregazione devono essere eseguite durante o dopo l'elaborazione. Le opzioni **regular** sono regular `lazy`o.|  
|`ProcessingPriority`|Determina la priorità di elaborazione del cubo durante operazioni in background, ad esempio indicizzazione e aggregazioni lente Il valore predefinito è **0**.|  
|`ScriptCacheProcessingMode`|Indica se la cache script deve essere compilata durante o dopo l'elaborazione. Le opzioni **regular** sono regular `lazy`e.|  
|`ScriptErrorHandlingMode`|Determina la gestione degli errori. Le opzioni disponibili sono `IgnoreNone` o `IgnoreAll`.|  
|`Source`|Visualizza la vista origine dati utilizzata per il cubo.|  
|`StorageLocation`|Specifica il percorso di archiviazione nel file system per il cubo. Se non viene specificato alcun valore, il percorso viene ereditato dal database contenente l'oggetto del cubo.|  
|`StorageMode`|Specifica la modalità di archiviazione per il cubo. I valori `MOLAP`sono `ROLAP`, o`HOLAP``.`|  
|`Visible`|Determina la visibilità del cubo.|  
  
> [!NOTE]  
>  Per ulteriori informazioni sull'impostazione dei valori per la proprietà ErrorConfiguration quando si utilizzano valori null e altri problemi di integrità dei dati, vedere [gestione dei problemi di integrità dei dati in Analysis Services 2005](https://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Vedi anche  
 [Caching attivo &#40;partizioni&#41;](partitions-proactive-caching.md)  
  
  
