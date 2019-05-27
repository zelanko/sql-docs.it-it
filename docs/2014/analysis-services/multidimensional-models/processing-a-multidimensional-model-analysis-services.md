---
title: Elaborazione degli oggetti modello multidimensionale | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- online mode [Analysis Services]
- processing objects [Analysis Services]
- partitions [Analysis Services], processing
- jobs [Analysis Services]
- objects [Analysis Services], processing
- reprocessing objects
- impact analysis [Analysis Services]
- dimensions [Analysis Services], processing
- project mode [Analysis Services]
- cubes [Analysis Services], processing
ms.assetid: 625aa5a6-aa09-4bac-be8a-778fa81c5a61
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d4952724f19a3c7010884feac0254f4f75d90ff
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073357"
---
# <a name="multidimensional-model-object-processing"></a>Elaborazione di oggetti del modello multidimensionale
  L'elaborazione è un passaggio, o una serie di passaggi, durante i quali tramite Analysis Services vengono caricati i dati da un'origine dati relazionale in un modello multidimensionale. Per gli oggetti in cui viene utilizzata l'archiviazione MOLAP, i dati vengono salvati su disco nella cartella dei file di database. Per l'archiviazione ROLAP, l'elaborazione avviene su richiesta, in risposta a una query MDX su un oggetto. Per gli oggetti in cui viene utilizzata l'archiviazione ROLAP, l'elaborazione si riferisce all'aggiornamento della cache prima della restituzione dei risultati della query.  
  
 Per impostazione predefinita, l'elaborazione viene eseguita quando si distribuisce una soluzione nel server. È anche possibile elaborare tutta o parte di una soluzione, ad hoc tramite strumenti quali [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]o in base a una pianificazione tramite [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e SQL Server Agent. Quando si apporta una modifica strutturale al modello, ad esempio la rimozione di una dimensione o la modifica del relativo livello di compatibilità, sarà necessario eseguire di nuovo l'elaborazione per sincronizzare gli aspetti fisici e logici del modello.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
 [Prerequisiti](#bkmk_prereq)  
  
 [Scelta di uno strumento o di un approccio](#bkmk_tool)  
  
 [Elaborazione di oggetti](#bkmk_proc)  
  
 [Reprocessing Objects](#bkmk_reproc)  
  
##  <a name="bkmk_prereq"></a> Prerequisiti  
  
-   L'elaborazione richiede autorizzazioni amministrative sull'istanza di Analysis Services. Se si elabora in modo interattivo da [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], è necessario essere un membro del ruolo di amministratore del server sull'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Per l'elaborazione che viene eseguita in modalità automatica, ad esempio utilizzando un pacchetto SSIS che si pianifica tramite SQL Server Agent, l'account utilizzato per eseguire il pacchetto deve essere un membro del ruolo di amministratore del server. Per altre informazioni sull'impostazione di autorizzazioni di amministratore, vedere [Concedi autorizzazioni di amministratore del Server &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
-   L'account utilizzato per recuperare i dati viene specificato nell'oggetto origine dati, come opzione di rappresentazione, se si utilizza l'autenticazione di Windows, o come nome utente nella stringa di connessione, in caso di utilizzo dell'autenticazione del database. L'account deve disporre delle autorizzazioni di lettura su origini dati relazionali utilizzate dal modello.  
  
-   Prima di poter elaborare gli oggetti è necessario distribuire il progetto o la soluzione.  
  
     Inizialmente, durante le prime fasi di sviluppo del modello, la distribuzione e l'elaborazione vengono eseguite insieme. Tuttavia, è possibile impostare opzioni per elaborare il modello in un secondo momento, dopo la distribuzione della soluzione. Per altre informazioni sulla distribuzione, vedere [Distribuire progetti di Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md).  
  
##  <a name="bkmk_tool"></a> Scelta di uno strumento o di un approccio  
 È possibile elaborare gli oggetti in modo interattivo usando un'applicazione client quale [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]o un'operazione controllata da script eseguita come processo di SQL Server Agent o pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 La modalità di elaborazione di un database varia notevolmente a seconda che il modello sia in fase di sviluppo attivo o in produzione. Una volta distribuito un modello a un server di produzione, è necessario controllare strettamente l'elaborazione per assicurare l'integrità e la disponibilità di dati multidimensionali. Poiché gli oggetti sono interdipendenti, l'elaborazione in genere produce un effetto a catena sul modello poiché altri oggetti vengono elaborati o non elaborati congiuntamente. Se alcuni oggetti vengono lasciati in stato non elaborato, le query per tali dati non verranno risolte, provocando errori nei report o nelle applicazioni in cui vengono utilizzate. Quando si sviluppa una strategia per l'elaborazione di un database di produzione, valutare l'utilizzo di script o pacchetti di [!INCLUDE[ssIS](../../includes/ssis-md.md)] sottoposti a debug e test per evitare che si verifichino errori dell'operatore o si trascurino passaggi.  
  
 Per altre informazioni, vedere [Strumenti e approcci per l'elaborazione &#40;Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md).  
  
##  <a name="bkmk_proc"></a> Elaborazione di oggetti  
 Il processo di elaborazione influisce sugli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] seguenti: gruppi di misure, partizioni, dimensioni, cubi, modelli di data mining, strutture di data mining e database. Se un oggetto contiene uno o più oggetti, l'elaborazione dell'oggetto di livello superiore causa la propagazione dell'elaborazione a tutti gli oggetti di livello inferiore. Un cubo, ad esempio, contiene in genere uno o più gruppi di misure, ognuno dei quali contiene una o più partizioni, e dimensioni. Se si elabora un cubo, verranno elaborati tutti i gruppi di misure che lo costituiscono e le dimensioni attualmente non elaborate. Per altre informazioni sull'elaborazione di oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , vedere [Elaborazione di oggetti di Analysis Services](processing-analysis-services-objects.md).  
  
 Durante il processo di elaborazione, è possibile accedere agli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per l'esecuzione di query. Il processo di elaborazione funziona all'interno di una transazione, della quale è possibile eseguire il commit o il rollback. Se i processi di elaborazione hanno esito negativo, viene eseguito il rollback della transazione. In caso di esito positivo, verrà applicato un blocco esclusivo all'oggetto durante il commit delle modifiche, a indicare che l'oggetto è temporaneamente non disponibile per le query o l'elaborazione. Durante la fase di commit della transazione è ancora possibile inviare query all'oggetto, ma tali query verranno accodate fino al termine del commit.  
  
 In un processo di elaborazione, l'opzione di elaborazione impostata per ogni oggetto determina se l'oggetto verrà elaborato e con quale modalità. Per altre informazioni sulle opzioni di elaborazione specifiche che è possibile applicare a ogni oggetto, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
##  <a name="bkmk_reproc"></a> Reprocessing Objects  
 È necessario rielaborare i cubi che contengono elementi non elaborati prima di poterli esplorare. I cubi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contengono gruppi di misure e partizioni che devono essere elaborate prima di eseguire query su un cubo. L'elaborazione di un cubo in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] causa l'elaborazione automatica di tutte le dimensioni che costituiscono il cubo se tali dimensioni non sono elaborate. Dopo che un oggetto è stato elaborato per la prima volta, è necessario rielaborarlo parzialmente o completamente se si verificano le situazioni seguenti:  
  
-   La struttura dell'oggetto viene modificata, ad esempio eliminando una colonna in una tabella dei fatti.  
  
-   La progettazione delle aggregazioni per l'oggetto viene modificata.  
  
-   È necessario aggiornare i dati dell'oggetto.  
  
 Per l'elaborazione degli oggetti in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è possibile selezionare un'opzione di elaborazione o consentire a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di determinare il tipo di elaborazione appropriata. I metodi di elaborazione disponibili si differenziano l'uno dall'altro e variano sia in base al tipo di oggetto che alle modifiche apportate all'oggetto dopo l'ultima elaborazione. Se si imposta [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per la selezione automatica di un metodo di elaborazione, verrà usato il metodo che restituisce l'oggetto in uno stato di elaborazione completa nel minor tempo possibile. Per altre informazioni, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Architettura logica &#40;Analysis Services - Dati multidimensionali&#41;](olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Oggetti di database &#40;Analysis Services - Dati multidimensionali&#41;](olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
