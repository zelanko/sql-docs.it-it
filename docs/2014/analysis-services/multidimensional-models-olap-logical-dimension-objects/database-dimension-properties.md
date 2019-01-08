---
title: Proprietà delle dimensioni del database | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- metadata [Analysis Services]
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 075548ef-08a3-413c-8ee0-4a074c276fcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 34de23fca71f4dc7949a04a36323d19d35826fa9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359823"
---
# <a name="database-dimension-properties"></a>Proprietà delle dimensioni del database
  Nelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], le caratteristiche di una dimensione sono definite dai metadati per la dimensione, in base alle impostazioni di diverse proprietà della dimensione e gli attributi o le gerarchie contenute nella dimensione. Nella tabella seguente vengono descritte le proprietà delle dimensioni in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`AttributeAllMemberName`|Specifica il nome del membro Totale per gli attributi in una dimensione.|  
|`Collation`|Determina le regole di confronto utilizzate dalla dimensione.|  
|`CurrentStorageMode`|Contiene la modalità di archiviazione corrente per la dimensione.|  
|`DependsOnDimension`|Contiene l'ID di un'altra dimensione da cui dipende la dimensione, se presente.|  
|`Description`|Contiene la descrizione della dimensione.|  
|`ErrorConfiguration`|Impostazioni configurabili per la gestione degli errori, relative alla gestione di chiavi duplicate, chiavi sconosciute, limiti di errore, azione da intraprendere in caso di rilevamento di un errore, file di log degli errori e gestione della chiave Null.|  
|`ID`|Contiene l'identificatore univoco (ID) della dimensione.|  
|`Language`|Specifica la lingua predefinita per la dimensione.|  
|`MdxMissingMemberMode`|Determina la modalità di gestione dei membri mancanti per le istruzioni MDX (Multidimensional Expressions).|  
|`MiningModelID`|Contiene l'ID del modello di data mining a cui è associata la dimensione di data mining. Questa proprietà è applicabile solo se la dimensione è una dimensione di un modello di data mining.|  
|`Name`|Specifica il nome della dimensione.|  
|`ProactiveCaching`|Definisce le impostazioni di memorizzazione nella cache attiva per la dimensione.|  
|`ProcessingGroup`|Specifica il gruppo di elaborazione. I valori sono ByAttribute o ByTable. Il valore predefinito è `ByAttribute`.|  
|`ProcessingMode`|Indica se in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] l'indicizzazione e l'aggregazione devono venire eseguite durante o dopo l'elaborazione.|  
|`ProcessingPriority`|Determina la priorità di elaborazione della dimensione durante le operazioni in background, ad esempio clustering, indicizzazione o aggregazione lenta.|  
|`Source`|Identifica la vista origine dati a cui è associata la dimensione.|  
|`StorageMode`|Determina la modalità di archiviazione per la dimensione.|  
|`Type`|Specifica il tipo della dimensione.|  
|`UnknownMember`|Indica se il membro sconosciuto è visibile.|  
|`UnknownMemberName`|Specifica la didascalia, nella lingua predefinita della dimensione, per il membro sconosciuto della dimensione.|  
|`WriteEnabled`|Indica se i writeback della dimensione sono disponibili, in base alle autorizzazioni di sicurezza.|  
  
> [!NOTE]  
>  Per altre informazioni sull'impostazione di valori per le proprietà ErrorConfiguration e UnknownMember quando si lavora con i valori null e altri problemi di integrità dei dati, vedere [la gestione di problemi di integrità dei dati di Analysis Services 2005](https://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi e gerarchie di attributi](attributes-and-attribute-hierarchies.md)   
 [Gerarchie definite dall'utente](user-hierarchies.md)   
 [Relazioni tra dimensioni](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
