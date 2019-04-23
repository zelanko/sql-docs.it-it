---
title: L'elaborazione di oggetti (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
- writeback [Analysis Services], XML for Analysis
- out-of-line bindings
- processing objects [XML for Analysis]
- XMLA, objects
ms.assetid: a65b3249-303d-49c6-98af-6ac6eed11a03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab38ea9b58e891d813a3ca73f43d20a364275da0
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156128"
---
# <a name="processing-objects-xmla"></a>Elaborazione di oggetti (XMLA)
  Nelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], l'elaborazione è il passaggio o serie di passaggi necessari per trasformare i dati in informazioni per l'analisi di business. L'elaborazione varia a seconda del tipo di oggetto, ma rappresenta sempre una fase della trasformazione dei dati in informazioni.  
  
 Per elaborare un' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dell'oggetto, è possibile usare il [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comando. In un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] il comando `Process` può elaborare gli oggetti seguenti:  
  
-   Cubi  
  
-   Database  
  
-   Dimensioni  
  
-   Gruppi di misure  
  
-   Modelli di data mining  
  
-   Strutture di data mining  
  
-   Partizioni  
  
 Per controllare l'elaborazione di oggetti, al comando `Process` sono associate varie proprietà che possono essere impostate. Il comando `Process` dispone di proprietà che controllano la quantità dell'elaborazione e gli oggetti che verranno elaborati e indicano se utilizzare associazioni out-of-line nonché le modalità di gestione degli errori e delle tabelle writeback.  
  
## <a name="specifying-processing-options"></a>Impostazione delle opzioni di elaborazione  
 Il [tipo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) proprietà del `Process` comando si specifica l'opzione di elaborazione da utilizzare per l'elaborazione dell'oggetto. Per altre informazioni sulle opzioni di elaborazione, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](../multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 Nella tabella seguente sono elencate le costanti per la proprietà `Type` e sono indicati i vari oggetti che possono essere elaborati utilizzando ciascuna costante.  
  
|Valore della proprietà `Type`|Oggetti applicabili|  
|--------------------|------------------------|  
|*ProcessFull*|Cubo, database, dimensione, gruppo di misure, modello di data mining, struttura di data mining, partizione|  
|*ProcessAdd*|Dimensione, partizione|  
|*ProcessUpdate*|Dimension|  
|*ProcessIndexes*|Dimensione, cubo, gruppo di misure, partizione|  
|*ProcessData*|Dimensione, cubo, gruppo di misure, partizione|  
|*ProcessDefault*|Cubo, database, dimensione, gruppo di misure, modello di data mining, struttura di data mining, partizione|  
|*ProcessClear*|Cubo, database, dimensione, gruppo di misure, modello di data mining, struttura di data mining, partizione|  
|*ProcessStructure*|Cubo, struttura di data mining|  
|*ProcessClearStructureOnly*|Struttura di data mining|  
|*ProcessScriptCache*|Cube|  
  
 Per altre informazioni sull'elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetti, vedere [l'elaborazione di oggetti modello multidimensionale](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="specifying-objects-to-be-processed"></a>Specifica degli oggetti da elaborare  
 Il [oggetti](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà del `Process` comando contiene l'identificatore dell'oggetto da elaborare. In un comando `Process` è possibile specificare solo un oggetto, ma l'elaborazione di un oggetto determina anche l'elaborazione di qualsiasi oggetto figlio. L'elaborazione di un gruppo di misure in un cubo, ad esempio, determina l'elaborazione di tutte le partizioni di tale gruppo, mentre l'elaborazione di un database determina l'elaborazione di tutti gli oggetti, quali cubi, dimensioni e strutture di data mining, contenuti nel database.  
  
 Se si imposta l'attributo `ProcessAffectedObjects` del comando `Process` su true, viene elaborato qualsiasi oggetto correlato interessato dall'elaborazione di quello specificato. Ad esempio, se una dimensione viene aggiornata in modo incrementale usando il *ProcessUpdate* nell'opzione di elaborazione di `Process` comando, è anche qualsiasi partizione le cui le aggregazioni vengono invalidate a causa di membri aggiunti o eliminati elaborati dal [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se `ProcessAffectedObjects` è impostato su true. In questo caso, un unico comando `Process` può elaborare più oggetti in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ma in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono determinati gli ulteriori oggetti da elaborare oltre all'oggetto specificato nel comando `Process`.  
  
 È possibile tuttavia elaborare più oggetti contemporaneamente, ad esempio dimensioni, tramite più comandi `Process` in un comando `Batch`. Le operazioni batch consentono di controllare a livello più dettagliato l'elaborazione in serie o parallela di oggetti in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rispetto all'utilizzo dell'attributo `ProcessAffectedObjects` e consentono di ottimizzare l'approccio all'elaborazione per i database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di dimensioni maggiori. Per altre informazioni sull'esecuzione di operazioni batch, vedere [esecuzione di operazioni Batch &#40;XMLA&#41;](performing-batch-operations-xmla.md).  
  
## <a name="specifying-out-of-line-bindings"></a>Specifica di associazioni out-of-line  
 Se il `Process` comando non è contenuto in un `Batch` comando, è possibile specificare associazioni out-of-line nel [associazioni](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla), [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla), e [DataSourceView ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) delle proprietà del `Process` comando per gli oggetti da elaborare. Le associazioni out-of-line sono riferimenti a origini dati, viste origine dati e altri oggetti in cui l'associazione è presente solo durante l'esecuzione del comando `Process`. Tali associazioni sostituiscono qualsiasi associazione esistente associata agli oggetti elaborati. Se non è specificata alcuna associazione out-of-line, vengono utilizzate le associazioni attualmente associate agli oggetti da elaborare.  
  
 Le associazioni out-of-line vengono utilizzate nelle seguenti situazioni:  
  
-   Elaborazione incrementale di una partizione in cui è necessario specificare una tabella dei fatti alternativa o un filtro sulla tabella dei fatti esistente per garantire che le righe non vengono contate due volte.  
  
-   Usando un'attività flusso di dati in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per fornire i dati durante l'elaborazione di una dimensione, un modello di data mining o una partizione.  
  
 Le associazioni out-of-line vengono descritte come parte del linguaggio ASSL (Analysis Services Scripting Language). Per altre informazioni sulle associazioni out-of-line in ASSL, vedere [origini dati e associazioni &#40;multidimensionale di SSAS&#41;](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
### <a name="incrementally-updating-partitions"></a>Aggiornamento incrementale di partizioni  
 Per eseguire l'aggiornamento incrementale di una partizione già elaborata, è necessario utilizzare un'associazione out-of-line poiché l'associazione specificata per la partizione fa riferimento a dati della tabella dei fatti già aggregati all'interno della partizione. Se si esegue l'aggiornamento incrementale di una partizione già elaborata tramite il comando `Process`, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono effettuate le operazioni seguenti:  
  
-   Creazione di una partizione temporanea con una struttura identica a quella della partizione da aggiornare in modo incrementale.  
  
-   Elaborazione della partizione temporanea tramite l'associazione out-of-line specificata nel comando `Process`.  
  
-   Unione della partizione temporanea con la partizione esistente selezionata.  
  
 Per altre informazioni sull'unione di partizioni utilizzando XML for Analysis (XMLA), vedere [unione di partizioni &#40;XMLA&#41;](merging-partitions-xmla.md).  
  
## <a name="handling-processing-errors"></a>Gestione degli errori di elaborazione  
 Il [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) proprietà del `Process` comando consente di specificare come gestire gli errori rilevati durante l'elaborazione di un oggetto. Ad esempio durante l'elaborazione di una dimensione in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene rilevato un valore duplicato nella colonna chiave dell'attributo chiave. Poiché le chiavi dell'attributo devono essere univoche, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elimina i record duplicati. In base il [KeyDuplicate](https://docs.microsoft.com/bi-reference/assl/properties/keyduplicate-element-assl) proprietà di `ErrorConfiguration`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è stato possibile:  
  
-   Continuazione dell'elaborazione della dimensione poiché il messaggio viene ignorato.  
  
-   Restituzione di un messaggio che indica che in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è stata rilevata una chiave duplicata e continuazione dell'elaborazione.  
  
 Le condizioni analoghe per cui `ErrorConfiguration` specifica opzioni durante un comando `Process` sono numerose.  
  
## <a name="managing-writeback-tables"></a>Gestione di tabelle writeback  
 Se il comando `Process` rileva una partizione abilitata per la scrittura oppure un cubo o un gruppo di misure per tale partizione la cui elaborazione non è ancora stata completata, è possibile che per tale partizione non esista una tabella writeback. Il [WritebackTableCreation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/writebacktablecreation-element-xmla) proprietà delle `Process` comando determina se [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve creare una tabella writeback.  
  
## <a name="examples"></a>Esempi  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene elaborato completamente il database di esempio [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="code"></a>Codice  
  
```  
<Process xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Descrizione  
 Elabora in modo incrementale nell'esempio seguente il **Internet_Sales_2004** partizionare nel **Internet Sales** gruppo di misure del **Adventure Works DW** cubo nel [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] esempio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database. Il `Process` comando viene aggiunta aggregazioni per l'ordine date successive al 31 dicembre 2006 alla partizione tramite un'associazione out-of-line query nel `Bindings` proprietà del `Process` comando per recuperare le righe della tabella dei fatti da cui generare aggregazioni da aggiungere alla partizione.  
  
### <a name="code"></a>Codice  
  
```  
<Process ProcessAffectedObjects="true" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  
