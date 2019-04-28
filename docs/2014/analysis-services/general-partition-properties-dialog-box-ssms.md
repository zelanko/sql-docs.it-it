---
title: Generale (finestra di dialogo Proprietà partizione) (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.general.f1
ms.assetid: efb505be-354f-4d23-8f2d-3e76fa50d27b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 612a997e51e23c6b8d3b1860fbc74df79de6c73c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731956"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>Generale (finestra di dialogo Proprietà partizione) (SSMS)
  La pagina **Generale** della finestra di dialogo **Proprietà partizione** di SQL Server Management Studio consente di impostare le proprietà generali di una partizione in un gruppo di misure di un cubo contenuto in un database di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**ID progettazione aggregazioni**|Consente di visualizzare l'identificatore della progettazione di aggregazioni utilizzato dalla partizione.|  
|**Aggregation Prefix**|Consente di visualizzare il prefisso predefinito delle istanze di aggregazione contenute nella partizione.|  
|**Timestamp creazione**|Consente di visualizzare la data e l'ora di creazione della partizione.|  
|**Modalità di archiviazione corrente**|Consente di visualizzare la modalità di archiviazione corrente della partizione.<br /><br /> Nota: Questa modalità può variare a seconda delle impostazioni di memorizzazione nella cache attiva della partizione. Per altre informazioni sulla memorizzazione nella cache attiva, vedere [Memorizzazione nella cache attiva &#40;partizioni&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|**Descrizione**|Consente di modificare la descrizione della partizione.|  
|**Numero stimato di righe**|Consente di digitare il numero stimato di righe nell'origine dei dati sottostante rappresentata dalla partizione. Questo valore viene utilizzato durante l'elaborazione per stimare il tempo e l'archiviazione necessari per elaborare la partizione.|  
|**Dimensioni stimate**|Consente di visualizzare le dimensioni stimate della partizione.|  
|**ID**|Consente di visualizzare l'identificatore della partizione.|  
|**Ultima elaborazione**|Consente di visualizzare la data e l'ora dell'ultima elaborazione della partizione.|  
|**Ultimo aggiornamento schema**|Consente di visualizzare la data e l'ora dell'ultimo aggiornamento dei metadati della partizione.|  
|**Name**|Consente di visualizzare il nome della partizione.|  
|**Modalità di elaborazione**|Consente di selezionare la modalità di elaborazione della partizione. Per altre informazioni sulle modalità di elaborazione per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oggetti, vedere [l'elaborazione di oggetti modello multidimensionale](multidimensional-models/processing-a-multidimensional-model-analysis-services.md).|  
|**ID origine dati remota**|Consente di visualizzare l'identificatore dell'origine dei dati remota da cui viene recuperata l'origine dei dati della partizione.<br /><br /> Nota: Questa proprietà contiene un valore solo per le partizioni remote.|  
|**sezione**|Consente di visualizzare l'espressione che identifica la sezione di dati rappresentata dalla partizione.|  
|**Origine**|Consente di visualizzare la tabella o la query che rappresenta l'origine dei dati della partizione.|  
|**Stato**|Consente di visualizzare lo stato di elaborazione corrente della partizione.|  
|**Percorso di archiviazione**|Consente di visualizzare la cartella in cui vengono archiviati i dati della partizione.<br /><br /> Nota: Questa proprietà contiene un valore solo se un percorso di archiviazione diverso dal percorso di archiviazione predefinito per il [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è specificata l'istanza.|  
|**Tipo**|Consente di visualizzare il tipo di partizione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni &#40;Analysis Services - Dati multidimensionali&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Partizioni remote](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [Finestra di dialogo proprietà di partizione &#40;SQL Server Management Studio&#41;](partition-properties-dialog-box-ssms.md)   
 [Selezione &#40;finestra di dialogo Proprietà partizione&#41; &#40;SQL Server Management Studio&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [La memorizzazione nella cache &#40;finestra di dialogo Proprietà partizione&#41; &#40;SQL Server Management Studio&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [Configurazione errori per cubi, partizioni e l'elaborazione della dimensione &#40;SSAS - multidimensionale&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
