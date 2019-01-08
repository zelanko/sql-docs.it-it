---
title: Elaborare partizioni nel database dell'area di lavoro di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f81d61411ef8815d23407b9aee1df4cf56e70de
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072148"
---
# <a name="process-partitions-in-the-workspace-databse"></a>Elaborare partizioni nel database dell'area di lavoro 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente dalle altre. Nelle attività di questo argomento viene descritto come elaborare le partizioni nel database dell'area lavoro modello tramite la finestra di dialogo **Elabora partizioni** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Dopo aver distribuito un modello in un'altra istanza di Analysis Services, gli amministratori di database possono creare e gestire partizioni nel modello (distribuito) tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], script o utilizzando un pacchetto di IS. Per altre informazioni, vedere [creare e gestire partizioni di modelli tabulari](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
###  <a name="bkmk_create_new"></a> Per elaborare una partizione  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]fare clic sul menu **Modello** , scegliere **Elabora** (Aggiorna) e quindi fare clic su **Elabora partizioni**.  
  
2.  Nella casella di riepilogo **Modalità** selezionare una delle modalità di elaborazione seguenti:  
  
    |Modalità|Descrizione|  
    |----------|-----------------|  
    |**Elaborazione predefinita**|Rileva lo stato di elaborazione di un oggetto partizione ed esegue l'elaborazione necessaria per recapitare oggetti partizione non elaborati o elaborati parzialmente in uno stato di elaborazione completa. Vengono caricati i dati per le tabelle vuote e le partizioni; vengono compilate o ricompilate le gerarchie, le colonne calcolate e le relazioni.|  
    |**Elaborazione completa**|Elabora un oggetto partizione e tutti gli oggetti in esso contenuti. Quando viene eseguita l'elaborazione completa per un oggetto che è stato già elaborato, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono eliminati tutti i dati dell'oggetto, quindi quest'ultimo viene elaborato. Questo tipo di elaborazione è necessario quando è stata apportata una modifica strutturale a un oggetto.|  
    |**Elaborare dati**|Carica i dati in una partizione o in una tabella senza ricompilare le gerarchie o le relazioni oppure ricalcolare le colonne calcolate e le misure.|  
    |**Elaborazione pulizia**|Rimuove tutti i dati da una partizione.|  
    |**Elaborazione aggiunta**|Aggiornare in modo incrementale la partizione con i nuovi dati.|  
  
3.  Nella colonna della casella di controllo **Elabora** selezionare le partizioni che si desidera elaborare con la modalità scelta, quindi fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [Creare e gestire partizioni nel database dell'area di lavoro](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)  
  
  
