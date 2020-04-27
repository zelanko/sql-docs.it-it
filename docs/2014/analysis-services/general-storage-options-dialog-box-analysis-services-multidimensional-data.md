---
title: Generale (finestra di dialogo Opzioni di archiviazione) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.storage.f1
ms.assetid: ee1fac79-ae15-4c3c-9a98-33db04388817
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3c7ddd5311232ae12b3eb9f66adc0cd1f5714b32
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081005"
---
# <a name="general-storage-options-dialog-box-analysis-services---multidimensional-data"></a>Generale (finestra di dialogo Opzioni di archiviazione) (Analysis Services - Dati multidimensionali)
  La scheda **Generale** della finestra di dialogo **Opzioni di archiviazione** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] consente di definire le impostazioni della modalità di archiviazione e della memorizzazione nella cache attiva per una dimensione, un cubo, un gruppo di misure o una partizione.  
  
> [!NOTE]  
>  Prima di modificare queste impostazioni, è consigliabile acquisire dimestichezza con la modalità di archiviazione e la funzionalità di memorizzazione nella cache attiva. Per altre informazioni, vedere [Memorizzazione nella cache attiva &#40;partizioni&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="options"></a>Opzioni  
  
|Termine|Definizione|  
|----------|----------------|  
|**Modalità di archiviazione**|Consente di selezionare la modalità di archiviazione da utilizzare per l'oggetto.<br /><br /> **MOLAP**<br /> L'oggetto utilizza l'archiviazione OLAP multidimensionale (MOLAP).<br /><br /> **HOLAP**<br /> L'oggetto utilizza l'archiviazione OLAP ibrido (HOLAP).<br /><br /> **ROLAP**<br /> L'oggetto utilizza l'archiviazione OLAP relazionale (ROLAP).|  
|**Attivazione della memorizzazione nella cache attiva.**|Attiva la memorizzazione nella cache attiva.<br /><br /> Nota: se questa opzione non è selezionata, tutte le opzioni ad eccezione di **Modalità di archiviazione** sono disabilitate.|  
|**Aggiorna la cache in caso di modifiche ai dati**|Consente di usare il metodo di notifica selezionato nella scheda **Notifiche** per aggiornare l'immagine MOLAP dell'oggetto ogni volta che viene ricevuta una notifica. Per altre informazioni sulla scheda **Notifiche**, vedere [Notifiche &#40;finestra di dialogo Opzioni di archiviazione&#41; &#40;Analysis Services - Dati multidimensionali&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).<br /><br /> Nota: se **Abilita memorizzazione nella cache attiva** non è selezionata, questa opzione è disabilitata.|  
|**Intervallo di inattività**|Consente di impostare l'intervallo e le unità di tempo minimi in cui non vi sono attività nell'oggetto prima dell'avvio della memorizzazione nella cache attiva per creare la nuova immagine MOLAP dell'oggetto.<br /><br /> Nota: se **Aggiorna la cache in caso di modifiche ai dati** non è selezionata, questa opzione è disabilitata.|  
|**Intervallo di inattività sostitutivo**|Consente di impostare l'intervallo e le unità di tempo massimi in cui viene avviato la memorizzazione nella cache attiva dopo la ricezione di una notifica relativa all'oggetto per creare una nuova immagine MOLAP dell'oggetto, indipendentemente dall'attività corrente dell'oggetto. Le notifiche ricevute dopo l'esaurimento di questo intervallo non annullano il processo relativo all'immagine MOLAP avviato dall'intervallo.<br /><br /> Nota: se **Aggiorna la cache in caso di modifiche ai dati** non è selezionata, questa opzione è disabilitata. Si noti inoltre che questa opzione non deve essere impostata se **modalità di archiviazione** è impostata su **HOLAP**.|  
|**Elimina cache obsoleta**|Specifica il periodo compreso tra l'inizio della creazione di una nuova cache MOLAP e la rimozione di quella esistente.<br /><br /> Nota: se **Abilita memorizzazione nella cache attiva** non è selezionata, questa opzione è disabilitata. Si noti inoltre che questa opzione non deve essere impostata se **modalità di archiviazione** è impostata su HOLAP.|  
|**Latenza**|Consente di selezionare l'intervallo e le unità di tempo del periodo compreso tra l'inizio della creazione di una nuova cache MOLAP e la rimozione di quella esistente.<br /><br /> Nota: se **Elimina cache obsoleta** non è selezionata, questa opzione è disabilitata. Si noti inoltre che questa opzione non deve essere impostata se **modalità di archiviazione** è impostata su **HOLAP**.|  
|**Aggiorna periodicamente la cache**|Aggiorna regolarmente l'immagine MOLAP, indipendentemente dalla notifica.<br /><br /> Nota: se **Abilita memorizzazione nella cache attiva** non è selezionata, questa opzione è disabilitata. Si noti inoltre che questa opzione non deve essere impostata se **modalità di archiviazione** è impostata su **HOLAP**.|  
|**Intervallo di ricompilazione**|Consente di selezionare l'intervallo e le unità di tempo per il periodo in cui, dopo la creazione di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] una nuova immagine MOLAP, avvia di nuovo il processo di immagine MOLAP per l'oggetto, indipendentemente dalla notifica. Le notifiche ricevute dopo l'esaurimento di questo intervallo non annullano il processo relativo all'immagine MOLAP avviato dall'intervallo.<br /><br /> Nota: se **Aggiorna periodicamente la cache** non è selezionata, questa opzione è disabilitata. Si noti inoltre che questa opzione non deve essere impostata se **modalità di archiviazione** è impostata su **HOLAP**.|  
|**Online immediatamente**|Consente di portare gli oggetti online immediatamente. Se questa opzione è impostata, gli oggetti utilizzeranno l'archiviazione ROLAP sottostante per risolvere le query durante la ricompilazione della cache MOLAP. Se invece non è impostata, gli oggetti verranno portati online solo dopo il completamento della cache MOLAP relativa all'oggetto.|  
|**Attiva aggregazioni ROLAP**|Consente di utilizzare le viste materializzate sull'origine dei dati sottostante per archiviare le aggregazioni.<br /><br /> Nota: se l'origine dei dati sottostante non supporta viste materializzate, verrà generato un errore durante l'elaborazione dell'oggetto.|  
|**Applica impostazioni alle dimensioni**|Applica le impostazioni della modalità di archiviazione e della memorizzazione nella cache attiva alle dimensioni associate.|  
  
## <a name="see-also"></a>Vedi anche  
 [Finestra di dialogo Opzioni di archiviazione &#40;Analysis Services-Dati multidimensionali&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)   
 [Notifiche &#40;finestra di dialogo Opzioni di archiviazione&#41; &#40;Analysis Services Dati multidimensionali&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)  
  
  
