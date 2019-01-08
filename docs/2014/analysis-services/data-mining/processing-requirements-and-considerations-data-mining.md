---
title: L'elaborazione di requisiti e considerazioni (Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], objects
- mining structures [Analysis Services], processing
- mining models [Analysis Services], processing
ms.assetid: f7331261-6f1c-4986-b2c7-740f4b92ca44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 181e2a367f6196d50f90aee77ca9590f55ba0ce4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369723"
---
# <a name="processing-requirements-and-considerations-data-mining"></a>Requisiti e considerazioni sull'elaborazione (data mining)
  In questo argomento vengono illustrate alcune considerazioni tecniche da tenere presenti quando si elaborano oggetti di data mining. Per una spiegazione generale dell'elaborazione e della modalità di applicazione al data mining, vedere [Elaborazione di oggetti di data mining](processing-data-mining-objects.md).  
  
 [Query sull'archivio relazionale](#bkmk_QueryReqs)  
  
 [Elaborazione di strutture di data mining](#bkmk_ProcessStructures)  
  
 [Elaborazione di modelli di data mining](#bkmk_ProcessModels)  
  
##  <a name="bkmk_QueryReqs"></a> Query sull'archivio relazionale durante l'elaborazione  
 Per il data mining, l'elaborazione prevede tre fasi: esecuzione di query sui dati di origine, determinazione di statistiche non elaborate e utilizzo della definizione e dell'algoritmo del modello per eseguire il training del modello di data mining.  
  
 Il server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue query sul database che fornisce i dati non elaborati. Tale database può essere un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o una versione precedente del motore di database di SQL Server. Quando si elabora una struttura di data mining, i dati presenti nell'origine vengono trasferiti nella struttura di data mining e resi persistenti su disco in un nuovo formato compresso. Non tutte le colonne dell'origine dati vengono elaborate, ma solo quelle incluse nella struttura di data mining, come definito dalle associazioni.  
  
 Con questi dati, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene compilato un indice di tutti i dati e le colonne discretizzate e viene creato un indice separato per le colonne continue. Per ogni tabella nidificata, viene eseguita una query per creare l'indice e viene generata una query aggiuntiva per elaborare le relazioni tra ogni coppia di tabella nidificata e tabella del case. La creazione di più query è necessaria per elaborare uno speciale archivio dati multidimensionale interno. È possibile limitare il numero di query inviate da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'archivio relazionale impostando la proprietà del server, `DatabaseConnectionPoolMax`. Per altre informazioni, vedere [Proprietà OLAP](../server-properties/olap-properties.md).  
  
 Quando si elabora il modello, quest'ultimo non legge nuovamente i dati dall'origine dati, ma ne ottiene il riepilogo dalla struttura di data mining. Utilizzando il cubo creato e i dati dell'indice e del case memorizzati nella cache, nel server vengono creati thread indipendenti per eseguire il training dei modelli.  
  
 Per altre informazioni sulle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che supportano l'elaborazione parallela dei modelli, vedere [funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473).  
  
##  <a name="bkmk_ProcessStructures"></a> Elaborazione di strutture di data mining  
 È possibile elaborare una struttura di data mining insieme a tutti i modelli dipendenti o separatamente. L'elaborazione di una struttura di data mining separatamente dai modelli può essere utile quando si prevede che l'elaborazione di alcuni modelli richieda molto tempo e si desidera rinviare tale operazione.  
  
 Per altre informazioni, vedere [Elaborare una struttura di data mining](process-a-mining-structure.md).  
  
 Se si desidera risparmiare spazio su disco, ricordarsi che in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] i dati delle strutture di data mining memorizzati nella cache vengono conservati localmente. Ciò significa che tutti i dati di training vengono scritti nel disco rigido locale. Se non si desidera memorizzare i dati nella cache, è possibile modificare il comportamento predefinito impostando la proprietà <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> nella struttura di data mining su `ClearAfterProcessing`. La cache verrà eliminata dopo l'elaborazione dei modelli; tuttavia, verrà anche disabilitato il drill-through sulla struttura di data mining. Per altre informazioni, vedere [Query drill-through &#40;Data mining&#41;](drillthrough-queries-data-mining.md).  
  
 Inoltre, se si cancella la cache, non sarà possibile utilizzare il set di test di controllo eventualmente specificato e la definizione della partizione del set di test andrà persa. Per altre informazioni sui set di test dei dati di controllo, vedere [Set di dati di training e di testing](training-and-testing-data-sets.md).  
  
##  <a name="bkmk_ProcessModels"></a> Elaborazione di modelli di data mining  
 È possibile elaborare un modello di data mining separatamente dalla struttura di data mining associata oppure elaborare tutti i modelli basati sulla struttura insieme alla struttura stessa.  
  
 Per altre informazioni, vedere [Elaborare un modello di data mining](process-a-mining-model.md).  
  
 Tuttavia, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], non è possibile selezionare più modelli di data mining da elaborare con la struttura. Se è necessario controllare quali modelli vengono elaborati, è necessario selezionarli singolarmente o utilizzare XMLA o DMX per elaborarli in serie.  
  
## <a name="when-reprocessing-is-required"></a>Necessità di rielaborazione  
 È necessario elaborare i modelli di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] definiti prima di poter iniziare a usarli. È inoltre necessario rielaborare i modelli di data mining ogni volta che si modifica la struttura del modello di data mining, si aggiornano i dati di training, si modifica un modello di data mining esistente oppure si aggiunge un nuovo modello di data mining alla struttura.  
  
 I modelli di data mining vengono inoltre elaborati in questi scenari:  
  
 **Distribuzione di un progetto**: A seconda delle impostazioni del progetto e lo stato corrente del progetto, modelli di data mining nel progetto vengono in genere elaborati completamente quando viene distribuito il progetto.  
  
 Quando si inizia la distribuzione, l'elaborazione viene avviata automaticamente, a meno che nel server di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vi sia una versione elaborata in precedenza e non siano state apportate modifiche strutturali. È possibile distribuire un progetto selezionando **Distribuisci soluzione** nell'elenco a discesa o premendo F5. È possibile:  
  
 Per altre informazioni sull'impostazione delle proprietà di distribuzione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che consentono di controllare la modalità di distribuzione dei modelli di data mining, vedere [Deployment of Data Mining Solutions](deployment-of-data-mining-solutions.md)(Distribuzione di soluzioni di data mining).  
  
 **Spostamento di un modello di data mining**: Quando si sposta un modello di data mining tramite il comando EXPORT, viene esportata solo la definizione del modello, che include il nome della struttura di data mining che si prevede di fornire dati al modello.  
  
 Requisiti di rielaborazione per gli scenari seguenti utilizzando i comandi EXPORT e IMPORT:  
  
-   La struttura di data mining esiste nell'istanza di destinazione e la struttura di data mining è in uno stato non elaborato.  
  
     È necessario rielaborare sia la struttura sia il modello.  
  
-   La struttura di data mining esiste nell'istanza di destinazione ed è stata elaborata. È stato esportato solo il modello di data mining.  
  
     Il modello può essere utilizzato senza elaborazione.  
  
-   È inoltre stata esportata la definizione della struttura di data mining tramite la parola chiave WITH DEPENDENCIES.  
  
     È necessario rielaborare sia la struttura sia il modello.  
  
 Per altre informazioni, vedere [Esportare e importare gli oggetti di data mining](export-and-import-data-mining-objects.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md)   
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md)   
 [Elaborazione degli oggetti modello multidimensionale](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
