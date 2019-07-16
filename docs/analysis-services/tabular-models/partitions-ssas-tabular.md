---
title: Partizioni nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d26b1b1558ca546fb47660488b15dc777c5ad87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162726"
---
# <a name="partitions"></a>Partizioni
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente dalle altre. Le partizioni create usando la finestra di dialogo partizioni in SSDT durante la creazione di modelli si applicano al database dell'area di lavoro modello. Quando il modello viene distribuito, le partizioni definite per il database dell'area di lavoro modello vengono duplicate nel database modello distribuito. È inoltre possibile creare e gestire partizioni per un database modello distribuito tramite la finestra di dialogo partizioni in SQL Server Management Studio.  Le informazioni fornite in questo argomento vengono descritte le partizioni create durante la creazione di modelli tramite la finestra di dialogo Gestione partizioni in SSDT. Per informazioni sulla creazione e gestione delle partizioni per un modello distribuito, vedere [creare e gestire partizioni di modelli tabulari](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_benefits"></a> Vantaggi  
 Le partizioni, nei modelli tabulari, consentono di dividere una tabella in oggetti partizione logici. Ogni partizione può quindi essere elaborata indipendentemente dalle altre. Ad esempio, è possibile che in una tabella siano inclusi determinati set di righe contenenti dati che raramente vengono modificati, a differenza di altri set i cui dati vengono invece modificati spesso. In questi casi, non è necessario elaborare tutti i dati quando in realtà si desidera effettuare tale operazione solo per una parte. Le partizioni consentono di dividere parti di dati che devono essere elaborati di frequente dai dati che possono invece essere elaborati meno frequentemente.  
  
 Un modello di progetto efficace consente di utilizzare le partizioni per eliminare elaborazioni e successivi carichi del processore non necessari nei server Analysis Services assicurando, nel contempo, che i dati vengano elaborati e aggiornati con una frequenza tale da riflettere i dati più recenti dalle origini dati. La modalità con cui le partizioni vengono implementate e utilizzate durante la creazione di modelli può essere molto diversa se riguarda modelli distribuiti. Tenere presente che, durante la fase di creazione dei modelli, è possibile che si utilizzi solo un subset dei dati che alla fine si troveranno nel modello distribuito.  
  
### <a name="processing-partitions"></a>Elaborazione di partizioni  
 Per i modelli distribuiti, l'elaborazione avviene tramite SQL Server Management Studio o eseguendo uno script che include il comando di elaborazione e specifica le impostazioni e opzioni di elaborazione. Durante la creazione di modelli tramite SSDT, è possibile eseguire operazioni di elaborazione tramite un comando elabora nel menu modello o sulla barra degli strumenti. Un'operazione di elaborazione può essere specificata per una partizione, una tabella o per qualsiasi altro elemento.  
  
 Quando viene eseguita un'operazione di elaborazione, viene effettuata una connessione all'origine dati utilizzando la connessione dati. I nuovi dati importati in tabelle, relazioni e gerarchie del modello vengono ricompilati per ogni tabella, mentre i calcoli nelle colonne calcolate e nelle misure calcolate vengono calcolati nuovamente.  
  
 Dividendo ulteriormente una tabella in partizioni logiche, è possibile determinare in modo selettivo quali dati in ogni partizione vengono elaborati, nonché quando e come eseguire tale operazione Quando si distribuisce un modello, l'elaborazione di partizioni può essere eseguita manualmente mediante la finestra di dialogo partizioni in SQL Server Management Studio o tramite uno script che esegue un comando di elaborazione.  
  
### <a name="partitions-in-the-model-workspace-database"></a>Partizioni nel database dell'area di lavoro modello  
 È possibile creare nuove partizioni, modificare, unire o eliminare partizioni tramite Gestione partizioni in SSDT. A seconda del livello di compatibilità del modello di che creazione, gestione partizioni offre due modalità per la selezione di tabelle, righe e colonne per una partizione: Per i modelli tabulari 1400, le partizioni sono definite tramite una query M oppure è possibile usare la modalità di progettazione per aprire l'Editor di Query. Per tabulari 1100, 1103, modelli tabulari 1200, usare la modalità anteprima tabella e query SQL. 
  
### <a name="partitions-in-a-deployed-model-database"></a>Partizioni in un database modello distribuito  
 Quando si distribuisce un modello, le partizioni per il database modello distribuito verranno visualizzato come oggetti di database in SQL Server Management Studio. Si può creare, modificare, unire ed eliminare le partizioni per un modello distribuito tramite la finestra di dialogo partizioni in SQL Server Management Studio. Gestione delle partizioni per un modello distribuito in SQL Server Management Studio non è compreso nell'ambito di questo argomento. Per altre informazioni sulla gestione delle partizioni in SQL Server Management Studio, vedere [creare e gestire partizioni di modelli tabulari](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Creare e gestire partizioni nel database dell'area di lavoro](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)|Viene descritto come creare e gestire partizioni nel database dell'area di lavoro modello tramite Gestione partizioni in SSDT.|  
|[Elaborare partizioni nel database dell'area di lavoro](../../analysis-services/tabular-models/process-partitions-in-the-workspace-database-ssas-tabular.md)|Viene descritto come elaborare (aggiornare) le partizioni nel database dell'area di lavoro modello.|  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Elaborare dati](../../analysis-services/tabular-models/process-data-ssas-tabular.md)  
  
  
