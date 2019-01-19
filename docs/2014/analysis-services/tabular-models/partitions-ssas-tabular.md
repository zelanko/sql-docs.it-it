---
title: Partizioni (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8126278319caff77a3d4ff6a334ed985c190288e
ms.sourcegitcommit: 2e8783e6bedd9597207180941be978f65c2c2a2d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2019
ms.locfileid: "54405641"
---
# <a name="partitions-ssas-tabular"></a>Partizioni (SSAS tabulare)
  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente dalle altre. Quelle create tramite la finestra di dialogo Partizioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante la creazione di modelli vengono applicate al database dell'area di lavoro modello. Quando il modello viene distribuito, le partizioni definite per il database dell'area di lavoro modello vengono duplicate nel database modello distribuito. È possibile creare e gestire ulteriori partizioni per un database modello distribuito utilizzando la finestra di dialogo Partizioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  Nelle informazioni fornite in questo argomento vengono descritte le partizioni generate durante la creazione di modelli utilizzando la finestra di dialogo Gestione partizioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per informazioni sulla creazione e gestione delle partizioni per un modello distribuito, vedere [Creare e gestire partizioni di modelli tabulari &#40;SSAS tabulare&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Attività correlate](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> Vantaggi  
 Le partizioni, nei modelli tabulari, consentono di dividere una tabella in oggetti partizione logici. Ogni partizione può quindi essere elaborata indipendentemente dalle altre. Ad esempio, è possibile che in una tabella siano inclusi determinati set di righe contenenti dati che raramente vengono modificati, a differenza di altri set i cui dati vengono invece modificati spesso. In questi casi, non è necessario elaborare tutti i dati quando in realtà si desidera effettuare tale operazione solo per una parte. Le partizioni consentono di dividere parti di dati che devono essere elaborati di frequente dai dati che possono invece essere elaborati meno frequentemente.  
  
 Un modello di progetto efficace consente di utilizzare le partizioni per eliminare elaborazioni e successivi carichi del processore non necessari nei server Analysis Services assicurando, nel contempo, che i dati vengano elaborati e aggiornati con una frequenza tale da riflettere i dati più recenti dalle origini dati. La modalità con cui le partizioni vengono implementate e utilizzate durante la creazione di modelli può essere molto diversa se riguarda modelli distribuiti. Tenere presente che, durante la fase di creazione dei modelli, è possibile che si utilizzi solo un subset dei dati che alla fine si troveranno nel modello distribuito.  
  
### <a name="processing-partitions"></a>Elaborazione di partizioni  
 L'elaborazione dei modelli distribuiti viene eseguita utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]oppure eseguendo uno script contenente il comando di elaborazione e che consente di specificare opzioni e impostazioni di elaborazione. Quando si creano modelli utilizzando [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], è possibile eseguire operazioni di elaborazione tramite un comando Elabora nel menu Modello o nella barra degli strumenti. Un'operazione di elaborazione può essere specificata per una partizione, una tabella o per qualsiasi altro elemento.  
  
 Quando viene eseguita un'operazione di elaborazione, viene effettuata una connessione all'origine dati utilizzando la connessione dati. I nuovi dati importati in tabelle, relazioni e gerarchie del modello vengono ricompilati per ogni tabella, mentre i calcoli nelle colonne calcolate e nelle misure calcolate vengono calcolati nuovamente.  
  
 Dividendo ulteriormente una tabella in partizioni logiche, è possibile determinare in modo selettivo quali dati in ogni partizione vengono elaborati, nonché quando e come eseguire tale operazione Quando si distribuisce un modello, l'elaborazione delle partizioni può essere completata manualmente tramite la finestra di dialogo Partizioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o utilizzando uno script che consente di eseguire un comando di elaborazione.  
  
### <a name="partitions-in-the-model-workspace-database"></a>Partizioni nel database dell'area di lavoro modello  
 In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]è possibile creare nuove partizioni nonché modificare, unire o eliminare partizioni tramite Gestione partizioni. Partition Manager offre due modalità per la selezione di tabelle, righe e colonne per una partizione: Modalità di query SQL e modalità anteprima tabella. Tutte le partizioni sono definite tramite una query SQL; tuttavia, utilizzando la modalità Anteprima tabella, è possibile visualizzare in anteprima e selezionare i dati da includere nella partizione. La query SQL viene creata e convalidata automaticamente. Poiché la modalità Anteprima tabella è la stessa anteprima tabella disponibile nella finestra di dialogo Modifica proprietà tabella e nella pagina Anteprima tabella dell'Importazione guidata tabella, il numero massimo di righe visualizzabili in anteprima è 50.  
  
### <a name="partitions-in-a-deployed-model-database"></a>Partizioni in un database modello distribuito  
 Quando si distribuisce un modello, le partizioni per il database modello distribuito verranno visualizzate come oggetti di database in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. È possibile creare, modificare, unire ed eliminare partizioni per un modello distribuito tramite la finestra di dialogo Partizioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. La gestione delle partizioni per un modello distribuito in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] non rientra nell'ambito di questo argomento. Per altre informazioni sulla gestione delle partizioni in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vedere [Creare e gestire partizioni di modelli tabulari &#40;SSAS tabulare&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Creare e gestire partizioni nel database dell'area di lavoro &#40;SSAS tabulare&#41;](workspace-database-ssas-tabular.md)|Viene descritto come creare e gestire partizioni nel database dell'area di lavoro del modello tramite Gestione partizioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|  
|[Elaborare partizioni nel Database dell'area di lavoro &#40;tabulare di SSAS&#41;](process-partitions-in-the-workspace-database-ssas-tabular.md)|Viene descritto come elaborare (aggiornare) le partizioni nel database dell'area di lavoro modello.|  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità DirectQuery &#40;SSAS tabulare&#41;](directquery-mode-ssas-tabular.md)   
 [Elaborare dati &#40;SSAS tabulare&#41;](../process-data-ssas-tabular.md)  
  
  
