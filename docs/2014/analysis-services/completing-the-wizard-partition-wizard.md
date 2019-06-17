---
title: Completamento procedura guidata (Creazione guidata partizione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.finish.f1
ms.assetid: 68a4dd5d-94d9-4a02-be31-949a6da0ef51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7ab4ad7a819c18056ab5901f95caf1b74b23a25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087530"
---
# <a name="completing-the-wizard-partition-wizard"></a>Completamento procedura guidata (Creazione guidata partizione)
  Usare la pagina **Completamento procedura guidata** per assegnare un nome alla partizione, definire la progettazione delle aggregazioni per la partizione ed eventualmente distribuire ed elaborare la partizione dopo aver completato la Creazione guidata partizione.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di digitare un nome per la nuova partizione. Se si sta lavorando con più tabelle, immettere il prefisso che verrà utilizzato con il nome della tabella per creare il nome di ogni partizione.  
  
 **Opzioni di aggregazione**  
 Consente di specificare l'opzione di aggregazione per la partizione.  
  
 Nella tabella seguente vengono elencate le opzioni di aggregazione disponibili.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Progettare le aggregazioni per la partizione adesso**|Le aggregazioni per la nuova partizione vengono progettate al termine della creazione della nuova partizione da parte della Creazione guidata partizione. La selezione di questa opzione determina l'avvio della Progettazione guidata aggregazioni dopo aver scelto **Fine** nella Creazione guidata partizione. Per altre informazioni sulla Progettazione guidata aggregazioni, vedere [Guida sensibile al contesto della Progettazione guidata aggregazioni](aggregation-design-wizard-f1-help.md).|  
|**Progettazione delle aggregazioni in un secondo momento**|La partizione viene creata senza che vengano subito progettate le aggregazioni.|  
|**Copiare la progettazione delle aggregazioni da una partizione esistente**|La progettazione delle aggregazioni viene copiata nella nuova partizione da una partizione esistente nel gruppo di misure. La selezione di questa opzione rende disponibile l'opzione **Copia da** . Usare l'opzione **Copia da** per selezionare la partizione da cui copiare la progettazione delle aggregazioni.<br /><br /> Si noti che le partizioni da unire in futuro devono avere la stessa progettazione delle aggregazioni e struttura di tabella. Per unire la nuova partizione a una partizione esistente nel gruppo di misure, è consigliabile copiare la progettazione delle aggregazioni della partizione esistente nella nuova partizione.|  
  
 **Distribuisci ed elabora adesso**  
 Consente di distribuire ed elaborare la partizione nell'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] specificata nella pagina **Posizioni di elaborazione e archiviazione** . Dopo aver scelto **Fine** in questa pagina, la partizione viene distribuita ed elaborata.  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni &#40;Analysis Services - Dati multidimensionali&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
