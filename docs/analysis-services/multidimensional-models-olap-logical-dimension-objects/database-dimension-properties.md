---
title: Proprietà delle dimensioni del database | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7c7944ab279f2b036a3acd7cf75bd775d0ec6d6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68180780"
---
# <a name="database-dimension-properties"></a>Proprietà delle dimensioni del database
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Nelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], le caratteristiche di una dimensione sono definite dai metadati per la dimensione, in base alle impostazioni di diverse proprietà della dimensione e gli attributi o le gerarchie contenute nella dimensione. Nella tabella seguente vengono descritte le proprietà delle dimensioni in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**AttributeAllMemberName**|Specifica il nome del membro Totale per gli attributi in una dimensione.|  
|**Regole di confronto**|Determina le regole di confronto utilizzate dalla dimensione.|  
|**CurrentStorageMode**|Contiene la modalità di archiviazione corrente per la dimensione.|  
|**DependsOnDimension**|Contiene l'ID di un'altra dimensione da cui dipende la dimensione, se presente.|  
|**Descrizione**|Contiene la descrizione della dimensione.|  
|**ErrorConfiguration**|Impostazioni configurabili per la gestione degli errori, relative alla gestione di chiavi duplicate, chiavi sconosciute, limiti di errore, azione da intraprendere in caso di rilevamento di un errore, file di log degli errori e gestione della chiave Null.|  
|**ID**|Contiene l'identificatore univoco (ID) della dimensione.|  
|**Lingua**|Specifica la lingua predefinita per la dimensione.|  
|**MdxMissingMemberMode**|Determina la modalità di gestione dei membri mancanti per le istruzioni MDX (Multidimensional Expressions).|  
|**MiningModelID**|Contiene l'ID del modello di data mining a cui è associata la dimensione di data mining. Questa proprietà è applicabile solo se la dimensione è una dimensione di un modello di data mining.|  
|**Name**|Specifica il nome della dimensione.|  
|**ProactiveCaching**|Definisce le impostazioni di memorizzazione nella cache attiva per la dimensione.|  
|**ProcessingGroup**|Specifica il gruppo di elaborazione. I valori sono ByAttribute o ByTable. Il valore predefinito è **ByAttribute**.|  
|**ProcessingMode**|Indica se in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] l'indicizzazione e l'aggregazione devono venire eseguite durante o dopo l'elaborazione.|  
|**ProcessingPriority**|Determina la priorità di elaborazione della dimensione durante le operazioni in background, ad esempio clustering, indicizzazione o aggregazione lenta.|  
|**Origine**|Identifica la vista origine dati a cui è associata la dimensione.|  
|**StorageMode**|Determina la modalità di archiviazione per la dimensione.|  
|**Tipo**|Specifica il tipo della dimensione.|  
|**UnknownMember**|Indica se il membro sconosciuto è visibile.|  
|**UnknownMemberName**|Specifica la didascalia, nella lingua predefinita della dimensione, per il membro sconosciuto della dimensione.|  
|**WriteEnabled**|Indica se i writeback della dimensione sono disponibili, in base alle autorizzazioni di sicurezza.|  
  
> [!NOTE]  
>  Per altre informazioni sull'impostazione di valori per le proprietà ErrorConfiguration e UnknownMember quando si lavora con i valori null e altri problemi di integrità dei dati, vedere [la gestione di problemi di integrità dei dati di Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi e gerarchie di attributi](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Gerarchie definite dall'utente](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Relazioni tra dimensioni](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
