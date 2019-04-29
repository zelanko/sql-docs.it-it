---
title: Elaborazione di Analysis Services oggetti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OLAP objects [Analysis Services], processing
- OLAP objects [Analysis Services]
ms.assetid: c7e1f66f-16ca-43da-b8c7-4d3e1fa8b58d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 704b775a881bc3c08f9789229231e05b56005257
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62736789"
---
# <a name="processing-analysis-services-objects"></a>Elaborazione di oggetti di Analysis Services
  L'elaborazione interessa i tipi di oggetto di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] seguenti: database, cubi, dimensioni, gruppi di misure, partizioni e strutture e modelli di data mining di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Per ogni tipo di oggetto è possibile specificare il livello di elaborazione o impostare l'opzione Elaborazione predefinita in modo che [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] selezioni automaticamente il livello di elaborazione ottimale. Per altre informazioni sui diversi livelli di elaborazione per ogni oggetto, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
 È importante conoscere le conseguenze dell'elaborazione per ridurre l'occorrenza di ripercussioni negative. Ad esempio, l'elaborazione completa di una dimensione imposta automaticamente tutte le partizioni dipendenti da tale dimensione su uno stato di non elaborazione. In tal modo i cubi interessati diventano non disponibili per l'esecuzione di query fino all'elaborazione delle partizioni dipendenti.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
 [Elaborazione di un database](#bkmk_procdb)  
  
 [Elaborazione di una dimensione](#bkmk_procdim)  
  
 [Elaborazione di un cubo](#bkmk_proccube)  
  
 [Elaborazione di un gruppo di misure](#bkmk_procmeasure)  
  
 [Elaborazione di una partizione](#bkmk_procpartition)  
  
 [Elaborazione di strutture e modelli di data mining](#bkmk_procdm)  
  
##  <a name="bkmk_procdb"></a> Elaborazione di un database  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]un database contiene oggetti, ma non dati. Quando si elabora un database, si indica al server di elaborare in modo ricorsivo gli oggetti in cui sono archiviati i dati del modello, ad esempio dimensioni, partizioni, strutture di data mining e modelli di data mining.  
  
 Quando si elabora un database, vengono elaborati tutti i modelli di data mining, le partizioni e le dimensioni corrispondenti o solo alcuni di questi elementi. Il tipo di elaborazione varia a seconda dello stato di ogni oggetto e dell'opzione di elaborazione selezionata. Per altre informazioni, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
##  <a name="bkmk_proccube"></a> Elaborazione di un cubo  
 Un cubo può essere considerato un oggetto wrapper per gruppi di misure e partizioni. È costituito da dimensioni e da una o più misure archiviate in partizioni. Le dimensioni definiscono il layout dei dati nel cubo. Durante l'elaborazione di un cubo, viene eseguita una query SQL per recuperare i valori dalla tabella dei fatti in modo da popolare ogni membro del cubo con valori di misura appropriati. A ogni percorso specifico di un nodo del cubo corrisponde un valore o un valore calcolabile.  
  
 Quando si elabora un cubo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elabora tutte le dimensioni del cubo non ancora elaborate e alcune o tutte le partizioni incluse nei gruppi di misure del cubo. Il tipo di elaborazione varia a seconda dello stato degli oggetti al momento in cui si avvia l'elaborazione e dall'opzione di elaborazione selezionata. Per altre informazioni sulle opzioni di elaborazione, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
 Con l'elaborazione di un cubo vengono creati file leggibili dal computer contenenti dati delle tabelle dei fatti rilevanti. Le eventuali aggregazioni create vengono archiviate in file di dati aggregati. Il cubo è quindi disponibile per l'esplorazione in Esplora oggetti di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o in Esplora soluzioni di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
##  <a name="bkmk_procdim"></a> Elaborazione di una dimensione  
 Quando si elabora una dimensione, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] formula ed esegue query su tabelle delle dimensioni per restituire le informazioni necessarie per l'elaborazione.  
  
|Country|Sales Region|State|  
|-------------|------------------|-----------|  
|United States|West|California|  
|United States|West|Oregon|  
|United States|West|Washington|  
  
 L'elaborazione stessa consente di trasformare i dati tabulari in gerarchie utilizzabili. Tali gerarchie sono nomi di membri completamente articolati e vengono rappresentate internamente da percorsi numerici univoci. Nell'esempio seguente viene illustrata una rappresentazione testuale di una gerarchia.  
  
||  
|-|  
|[United States]|  
|[United States].[West]|  
|[United States].[West].[California]|  
|[United States].[West].[Oregon]|  
|[United States].[West].[Washington]|  
  
 Tramite l'elaborazione delle dimensioni non è possibile creare o aggiornare i membri calcolati definiti a livello di cubo. I membri calcolati sono interessati quando viene aggiornata la definizione del cubo. Inoltre, tramite l'elaborazione delle dimensioni non è possibile creare né aggiornare le aggregazioni, tuttavia è possibile che l'elaborazione delle dimensioni provochi l'eliminazione delle aggregazioni. Le aggregazioni vengono create o aggiornate solo durante l'elaborazione delle partizioni.  
  
 Quando si elabora una dimensione, è importante tenere presente che la dimensione potrebbe essere utilizzata in più cubi. Durante l'elaborazione della dimensione tali cubi vengono contrassegnati come non elaborati e diventano non disponibili per le query. Per elaborare contemporaneamente sia la dimensione che i cubi correlati, è necessario utilizzare le impostazioni di elaborazione batch. Per altre informazioni, vedere [Elaborazione batch &#40;Analysis Services&#41;](batch-processing-analysis-services.md).  
  
##  <a name="bkmk_procmeasure"></a> Elaborazione di un gruppo di misure  
 Quando si elabora un gruppo di misure, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elabora alcune o tutte le partizioni del gruppo all'interno del gruppo di misure e tutte le dimensioni non elaborate che fanno parte del gruppo di misure. Il tipo di elaborazione varia a seconda dell'opzione di elaborazione selezionata. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile elaborare uno o più gruppi di misure senza influire sugli altri gruppi di misure di un cubo.  
  
> [!NOTE]  
>  È possibile elaborare singoli gruppi di misure a livello di programmazione o tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Non è possibile elaborare singoli gruppi di misure in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], a meno che l'elaborazione non venga eseguita in base alla partizione.  
  
##  <a name="bkmk_procpartition"></a> Elaborazione di una partizione  
 Un'amministrazione efficiente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include il processo di partizionamento dei dati. L'elaborazione di partizioni è un processo che implica considerazioni sull'utilizzo del disco rigido e sui vincoli di spazio, insieme alle limitazioni relative alle strutture di dati imposte da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per garantire risposte rapide alle query e una velocità effettiva di elaborazione elevata, periodicamente è necessario creare, elaborare e unire le partizioni. È estremamente importante riconoscere e gestire le partizioni per evitare l'integrazione di dati ridondanti durante l'unione delle partizioni. Per altre informazioni, vedere [Unire partizioni in Analysis Services &#40;SSAS - Modelli multidimensionali&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
 Quando si elabora una partizione, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elabora anche tutte le dimensioni non elaborate presenti nella partizione, a seconda dell'opzione di elaborazione selezionata. L'utilizzo di partizioni offre numerosi vantaggi a livello di elaborazione. È possibile elaborare una partizione senza influire sulle altre partizioni di un cubo. Le partizioni risultano utili per l'archiviazione di dati soggetti al writeback delle celle. La funzionalità di writeback consente all'utente di eseguire analisi di simulazione tramite il writeback di nuovi dati nella partizione per verificare l'effetto delle modifiche previste. Se si utilizza la funzionalità di writeback delle celle di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è necessario utilizzare una partizione writeback. L'elaborazione di partizioni in parallelo risulta utile in quanto in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] la capacità di elaborazione viene utilizzata in modo più efficiente, con una conseguente riduzione significativa del tempo di elaborazione complessivo. È inoltre possibile elaborare le partizioni in modo sequenziale.  
  
##  <a name="bkmk_procdm"></a> Elaborazione di strutture e modelli di data mining  
 Una struttura di data mining definisce il dominio da cui verranno compilati i modelli di data mining. Una singola struttura può contenere più modelli di data mining. È possibile elaborare una struttura di data mining separatamente dai relativi modelli di data mining associati. In tal caso, la struttura viene popolata con i dati di training dell'origine dei dati.  
  
 Quando si elabora un modello di data mining, i dati di training passano attraverso gli algoritmi del modello di data mining, viene eseguito il training del modello tramite l'algoritmo di data mining e vengono compilati i contenuti. Per altre informazioni sull'oggetto modello di data mining, vedere [Strutture di data mining &#40;Analysis Services - Data mining&#41;](../data-mining/mining-structures-analysis-services-data-mining.md).  
  
 Per altre informazioni sull'elaborazione di strutture e modelli di data mining, vedere [Requisiti e considerazioni sull'elaborazione &#40;Data mining&#41;](../data-mining/processing-requirements-and-considerations-data-mining.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti e approcci per l'elaborazione &#40;Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md)   
 [Elaborazione batch &#40;Analysis Services&#41;](batch-processing-analysis-services.md)   
 [Elaborazione degli oggetti modello multidimensionale](processing-a-multidimensional-model-analysis-services.md)  
  
  
