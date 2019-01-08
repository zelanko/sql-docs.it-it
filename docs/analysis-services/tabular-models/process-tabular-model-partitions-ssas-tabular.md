---
title: Elaborare partizioni di modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f4b4cb7307c30d03b80ef800d6808f5ce85deaa5
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072018"
---
# <a name="process-tabular-model-partitions"></a>Elaborare partizioni di modelli tabulari 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente dalle altre. Nelle attività di questo argomento viene descritto come elaborare le partizioni in un database modello tramite la finestra di dialogo **Elabora partizioni** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="bkmk_create_new"></a> Per elaborare una partizione  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sulla tabella contenente le partizioni che si desidera elaborare, quindi scegliere **Partizioni**.  
  
2.  Nella finestra di dialogo **Partizioni** fare clic sul pulsante Elabora in **Partizioni**.  
  
3.  Nel **elabora partizione/i** nella finestra di dialogo il **modalità** listbox, selezionare una delle modalità di elaborazione seguenti:  
  
    |Modalità|Descrizione|  
    |----------|-----------------|  
    |**Elaborazione predefinita**|Rileva lo stato di elaborazione di un oggetto partizione ed esegue l'elaborazione necessaria per recapitare oggetti partizione non elaborati o elaborati parzialmente in uno stato di elaborazione completa. Vengono caricati i dati per le tabelle vuote e le partizioni; vengono compilate o ricompilate le gerarchie, le colonne calcolate e le relazioni.|  
    |**Elaborazione completa**|Elabora un oggetto partizione e tutti gli oggetti in esso contenuti. Quando viene eseguita l'elaborazione completa per un oggetto che è stato già elaborato, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono eliminati tutti i dati dell'oggetto, quindi quest'ultimo viene elaborato. Questo tipo di elaborazione è necessario quando è stata apportata una modifica strutturale a un oggetto.|  
    |**Elaborare dati**|Carica i dati in una partizione o in una tabella senza ricompilare le gerarchie o le relazioni oppure ricalcolare le colonne calcolate e le misure.|  
    |**Elaborazione pulizia**|Rimuove tutti i dati da una partizione.|  
    |**Elaborazione aggiunta**|Aggiornare in modo incrementale la partizione con i nuovi dati.|  
  
4.  Nella colonna della casella di controllo **Elabora** selezionare le partizioni che si desidera elaborare con la modalità scelta, quindi fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni di modelli tabulari](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Creare e gestire partizioni di modelli tabulari](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
