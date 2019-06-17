---
title: Sviluppo con XMLA in Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 99ccf53ab36d68ab0b03fa042d08e00d65703228
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63265092"
---
# <a name="developing-with-xmla-in-analysis-services"></a>Sviluppo con XMLA in Analysis Services
  XML for Analysis (XMLA) è protocollo XML basato su SOAP, progettato in modo specifico per accedere a tutti i dati di qualsiasi origine dati multidimensionale standard accessibile tramite una connessione HTTP. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] l'unico protocollo utilizzato durante la comunicazione con applicazioni client è XMLA. Fondamentalmente, tutte le librerie client supportate da Analysis Services formulano richieste e risposte in XMLA.  
  
 Gli sviluppatori possono utilizzare XMLA per integrare un'applicazione client con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], senza dipendenze dalle interfacce .NET Framework o COM. I requisiti delle applicazioni che includono l'hosting su un'ampia gamma di piattaforme possono essere soddisfatti tramite XMLA e una connessione HTTP a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è completamente conforme alla specifica del 1.1 di XMLA, estendendola inoltre all'abilitazione del supporto della definizione, della modifica e del controllo dei dati. Le estensioni di Analysis Services vengono denominate ASSL (Analysis Services Scripting Language). L'utilizzo combinato di XMLA e ASSL abilita un set di funzionalità più ampio rispetto a quello fornito dal solo protocollo XMLA. Per altre informazioni su ASSL, vedere [lo sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Gestione di connessioni e sessioni &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)|Viene descritto come connettersi a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e come gestire sessioni e informazioni sullo stato in XMLA.|  
|[Gestione degli errori e avvisi &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/handling-errors-and-warnings-xmla.md)|Descrive il modo in cui [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce le informazioni di errore e di avviso per metodi e comandi in XMLA.|  
|[Definizione e identificazione di oggetti &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)|Descrive identificatori di oggetto e riferimenti all'oggetto e il modo in cui utilizzarli in comandi XMLA.|  
|[La gestione delle transazioni &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-transactions-xmla.md)|Illustra come usare il [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla), [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla), e [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) comandi per definire e gestire una transazione su XMLA corrente in modo esplicito sessione.|  
|[Annullamento di comandi &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|Viene descritto come utilizzare il [annullare](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)comando per annullare comandi, sessioni e connessioni in XMLA.|  
|[Esecuzione di operazioni Batch &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md)|Viene descritto come utilizzare il [Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando per eseguire XMLA più comandi, in serie o in parallelo, all'interno della stessa transazione o come transazioni separate, tramite un singolo XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) (metodo).|  
|[Creazione e modifica di oggetti &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md)|Viene descritto come utilizzare il [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla), [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), e [Elimina](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) comandi, insieme agli elementi di Analysis Services Scripting Language (ASSL), per definire, modificare o rimuovere oggetti da un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza.|  
|[Blocco e sblocco di database &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/locking-and-unlocking-databases-xmla.md)|Illustra come usare il [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) e [Unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comandi per bloccare e sbloccare un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database.|  
|[Elaborazione di oggetti &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)|Viene descritto come utilizzare il [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comando per elaborare un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetto.|  
|[Unione di partizioni &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)|Viene descritto come utilizzare il [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) comando per unire partizioni in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza.|  
|[Progettazione di aggregazioni &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)|Viene descritto come utilizzare il [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) comando, in iterativo o in modalità batch, per progettare aggregazioni per una progettazione delle aggregazioni in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Backup, ripristino e sincronizzazione di database &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)|Viene descritto come utilizzare il [Backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) e [ripristinare](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) comandi per eseguire il backup e ripristinare un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database da un file di backup.<br /><br /> Descrive anche come usare il [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) comando per sincronizzare un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database con un database esistente nella stessa istanza o in un'istanza diversa.|  
|[Inserimento, aggiornamento ed eliminazione di membri &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)|Viene descritto come utilizzare il [inserire](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [Update](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla), e [Drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) comandi per aggiungere, modificare o eliminare membri da una dimensione abilitata per la scrittura.|  
|[Aggiornamento di celle &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md)|Viene descritto come utilizzare il [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) comando per modificare i valori delle celle in una partizione abilitata per la scrittura.|  
|[Gestione delle cache &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-caches-xmla.md)|Illustra come usare il [ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) comando per cancellare le cache di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetti.|  
|[Monitoraggio di tracce &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/monitoring-traces-xmla.md)|Viene descritto come utilizzare il ["Subscribe"](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla) comando per sottoscrivere e monitorare una traccia esistente in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza.|  
  
## <a name="data-mining-with-xmla"></a>Data mining in XMLA  
 In XML for Analysis sono completamente supportati i set di righe dello schema di data mining. Questi set di righe forniscono informazioni per eseguire query sui modelli di data mining utilizzando il [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) (metodo). Per altre informazioni sui set di righe dello schema di data mining, vedere [set di righe dello Schema di Data Mining](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets)  
  
 Per altre informazioni su DMX, vedere [Data Mining Extensions &#40;DMX&#41; riferimento](../../dmx/data-mining-extensions-dmx-reference.md).  
  
## <a name="namespace-and-schema"></a>Spazio dei nomi e schema  
  
### <a name="namespace"></a>Spazio dei nomi  
 Lo schema definito in questa specifica utilizza lo spazio dei nomi XML `http://schemas.microsoft.com/AnalysisServices/2003/Engine` e l'abbreviazione standard "DDL".  
  
### <a name="schema"></a>schema  
 La definizione di uno schema XML Schema Definition Language (XSD) per il linguaggio di definizione dell'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è basata sulla definizione degli elementi e della gerarchia dello schema descritti in questa sezione.  
  
## <a name="extensibility"></a>Estendibilità  
 Estendibilità dello schema del linguaggio di definizione oggetto viene fornito per mezzo di un' **annotazione** elemento incluso in tutti gli oggetti. Tale elemento può contenere qualsiasi valore XML valido da qualsiasi spazio dei nomi XML (diverso dallo spazio dei nomi di destinazione che definisce il linguaggio DDL), soggetto alle regole seguenti:  
  
-   Il valore XML può contenere solo elementi.  
  
-   Ogni elemento deve avere un nome univoco. È consigliabile che il valore di **nome** fanno riferimento a nomi di destinazione.  
  
 Queste regole vengono imposte, in modo che il contenuto del **annotazione** tag può essere esposti come set di coppie nome/valore tramite gli oggetti DSO (Decision Support) 9.0.  
  
 I commenti e spazi vuoti all'interno di **annotazione** tag che non sono inclusi in un elemento figlio non possono essere mantenuti. Tutti gli elementi devono inoltre essere di lettura/scrittura. Gli elementi di sola lettura vengono ignorati.  
  
 Lo schema del linguaggio di definizione dell'oggetto è chiuso, poiché il server non consente la sostituzione di tipi derivati per gli elementi definiti nello schema. Di conseguenza il server accetta solo il set di elementi definito in questa sezione e nessun altro elemento né attributo. Gli elementi sconosciuti provocano la generazione di un errore da parte del motore di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Informazioni sull'architettura Microsoft OLAP](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
