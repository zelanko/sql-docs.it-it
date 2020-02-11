---
title: Architettura logica (Analysis Services-Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], about mining structures
- logical architecture [Data Mining]
- architecture [Analysis Services], mining models
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: 4e0cbf46-cc60-4e91-a292-9a69f29746f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5702e3e2e5b12edecff4dd6d6f46b632575d211d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084271"
---
# <a name="logical-architecture-analysis-services---data-mining"></a>Architettura logica (Analysis Services – Data mining)
  Il processo di data mining è basato sull'interazione di più componenti.  
  
-   Si accede a origini dati in un database SQL Server o a qualsiasi altra origine i cui dati verranno utilizzati a scopo di training, testing o stima.  
  
-   Si definiscono strutture e modelli di data mining tramite [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o Visual Studio.  
  
-   Si gestiscono oggetti di data mining e si creano stime e query tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Dopo avere completato la soluzione, è possibile distribuirla a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Il processo di creazione di questi oggetti della soluzione è già stato descritto in altri argomenti. Per altre informazioni, vedere [Soluzioni di data mining](data-mining-solutions.md).  
  

  
##  <a name="bkmk_SourceData"></a>Dati di origine di data mining  
 Nella soluzione di data mining vengono archiviate solo le associazioni, non i dati utilizzati nel processo di data mining. I dati potrebbero essere contenuti in un database creato in una versione precedente di SQL Server, in un sistema CRM o anche in un file flat. Quando si esegue il training della struttura o del modello tramite elaborazione, viene creato e archiviato un riepilogo statistico dei dati in una cache che può essere resa persistente per l'utilizzo in operazioni successive o eliminata dopo l'elaborazione. Per altre informazioni, vedere [Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md).  
  
 Si combinano dati diversi all'interno dell'oggetto vista origine dati (DSV) di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che fornisce un livello di astrazione sopra l'origine dati. È possibile specificare join tra le tabelle o aggiungere tabelle con una relazione molti-a-uno per creare colonne di tabelle nidificate. La definizione di questi oggetti, l'origine dati e la vista origine dati, viene archiviata all'interno della soluzione con le estensioni di file *.ds e \*.dsv. Per ulteriori informazioni sulla creazione e sull' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzo di origini dati e viste origine dati, vedere [origini dati supportate &#40;SSAS multidimensionale&#41;](../multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
 È inoltre possibile definire e modificare origini dati e viste origine dati tramite AMO o XMLA. Per altre informazioni sull'uso di questi oggetti a livello di programmazione, vedere [Panoramica dell'architettura logica &#40;Analysis Services - Dati multidimensionali&#41;](../multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md).  
  

  
##  <a name="bkmk_Structures"></a>Strutture di data mining  
 Una struttura di data mining è un contenitore di dati logico che definisce il dominio di dati in base al quale vengono compilati i modelli di data mining. Una sola struttura di data mining può supportare più modelli di data mining.  
  
 Quando è necessario utilizzare i dati nella soluzione di data mining, Analysis Services legge i dati dall'origine e genera una cache di aggregazioni e altre informazioni. Per impostazione predefinita, questa cache è resa persistente in modo che i dati di training possano essere riutilizzati per supportare modelli aggiuntivi. Se è necessario eliminare la cache, modificare la proprietà `CacheMode` nell'oggetto struttura di data mining sul valore `ClearAfterProcessing`. Per altre informazioni, vedere [Classi di data mining AMO](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes).  
  
 
  [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] consente anche di separare i dati in set di dati di training e di test, in modo da poter testare i modelli di data mining rispetto a un set di dati selezionato a caso e rappresentativo. I dati in realtà non vengono archiviati separatamente; piuttosto i dati del case nella cache della struttura vengono contrassegnati da una proprietà che indica se tale particolare caso viene utilizzato per il training o il test. Se la cache viene eliminata, non è possibile recuperare tali informazioni.  
  
 Per altre informazioni, vedere [Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md).  
  
 Una struttura di data mining può contenere tabelle nidificate. In una tabella nidificata vengono forniti dettagli aggiuntivi sul case di cui viene definito il modello nella tabella di dati primaria. Per altre informazioni, vedere [Tabelle annidate &#40;Analysis Services - Data mining&#41;](nested-tables-analysis-services-data-mining.md)  
  
 
  
##  <a name="bkmk_Models"></a>Modelli di data mining  
 Prima dell'elaborazione, un modello di data mining è solo una combinazione di proprietà di metadati. Tali proprietà specificano una struttura di data mining e un algoritmo di data mining e definiscono una raccolta di impostazioni di parametri e filtri che influiscono sul modo in cui i dati vengono elaborati. Per altre informazioni, vedere [Modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-models-analysis-services-data-mining.md).  
  
 Quando si elabora il modello, i dati di training archiviati nella cache della struttura di data mining sono utilizzati per generare modelli, basati sia sulle proprietà statistiche dei dati sia sull'euristica definita dall'algoritmo e dai relativi parametri. Questo processo è noto come *training* del modello.  
  
 Il risultato del training è un set di dati riepilogativi, contenuti nel *contenuto del modello*in cui sono descritti i modelli rilevati e vengono fornite le regole in base a cui generare le stime. Per altre informazioni, vedere [Contenuto del modello di data mining &#40;Analysis Services - Data mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
 In casi limitati è anche possibile esportare la struttura logica del modello in un file che rappresenta formule di modello e associazioni dati secondo un formato standard, il linguaggio PMML (Predictive Modeling Markup Language). È possibile importare questa struttura logica in altri sistemi che utilizzano PMML e il modello descritto può quindi essere utilizzato per la stima. Per altre informazioni, vedere [Informazioni sull'istruzione DMX Select](/sql/dmx/understanding-the-dmx-select-statement).  
  

  
##  <a name="bkmk_CustomObjects"></a>Oggetti di data mining personalizzati  
 Altri oggetti utilizzati nel contesto di un progetto di data mining, ad esempio grafici di accuratezza o query di stima, non vengono resi persistenti all'interno della soluzione, ma possono essere inseriti nello script utilizzando ASSL o compilati tramite AMO.  
  
 Inoltre, è possibile estendere i servizi e le funzionalità disponibili su un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aggiungendo questi oggetti personalizzati:  
  
 **Assembly personalizzati**  
 Gli assembly .NET possono essere definiti tramite qualsiasi linguaggio conforme a CLR o COM, quindi registrati con un'istanza di SQL Server. I file di assembly vengono caricati dal percorso definito dall'applicazione e una copia viene salvata nel server insieme ai dati. La copia del file di assembly viene utilizzata per caricare l'assembly a ogni avvio del servizio.  
  
 Per altre informazioni, vedere [Gestione di assembly di modelli multidimensionali](../multidimensional-models/multidimensional-model-assemblies-management.md).  
  
 **Stored procedure personalizzate**  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Il data mining di supporta l'uso di stored procedure per usare oggetti di data mining. È possibile creare stored procedure personalizzate per estendere le funzionalità e utilizzare più facilmente i dati restituiti da query di stima e query contenuto.  
  
 [Definizione delle stored procedure](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
 Le seguenti stored procedure sono supportate per l'utilizzo nell'esecuzione della convalida incrociata.  
  
 [Stored procedure di data mining &#40;Analysis Services-&#41;di data mining](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
 Inoltre, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono presenti molte stored procedure di sistema utilizzate internamente per il data mining. Benché le stored procedure di sistema siano per uso interno, possono rivelarsi utili scelte rapide. Microsoft si riserva il diritto di modificare tali stored procedure in base alle esigenze; pertanto, per l'utilizzo in fase di produzione, si consiglia di creare query tramite DMX, AMO o XMLA.  
  
 **Algoritmi plug-in personalizzati**  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornisce un meccanismo per la creazione di algoritmi personalizzati e l'aggiunta di tali algoritmi come nuovo servizio di data mining all'istanza del server.  
  
 In Analysis Services vengono utilizzate le interfacce COM per comunicare con gli algoritmi plug-in. Per altre informazioni sull'implementazione dei nuovi algoritmi, vedere [Algoritmi plug-in](plugin-algorithms.md).  
  
 Prima di utilizzare i nuovi algoritmi è necessario registrarli. Per registrare un algoritmo, aggiungere i metadati richiesti per gli algoritmi al file con estensione ini dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. È necessario aggiungere le informazioni a ogni istanza in cui si intende utilizzare il nuovo algoritmo. Dopo l'aggiunta dell'algoritmo, è possibile riavviare l'istanza e utilizzare il set di righe dello schema MINING_SERVICES per visualizzare il nuovo algoritmo, inclusi i provider e le opzioni supportati.  
  

  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione di oggetti del modello multidimensionale](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
