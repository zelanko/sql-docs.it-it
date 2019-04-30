---
title: L'elaborazione di oggetti (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 59a581f7e70f3fc1afd7eb7c1eaf4751d32719d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261655"
---
# <a name="processing-objects-xmla"></a>Elaborazione di oggetti (XMLA)
  Nelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], l'elaborazione è il passaggio o serie di passaggi necessari per trasformare i dati in informazioni per l'analisi di business. L'elaborazione varia a seconda del tipo di oggetto, ma rappresenta sempre una fase della trasformazione dei dati in informazioni.  
  
 Per elaborare un' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dell'oggetto, è possibile usare il [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comando. Il **processo** comando è possibile elaborare gli oggetti seguenti in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza:  
  
-   Cubi  
  
-   Database  
  
-   Dimensioni  
  
-   Gruppi di misure  
  
-   Modelli di data mining  
  
-   Strutture di data mining  
  
-   Partizioni  
  
 Per controllare l'elaborazione di oggetti, il **processo** comando è associate varie proprietà che è possibile impostare. Il **processo** comando ha le proprietà che controllano: quantità dell'elaborazione, quali oggetti verranno elaborati, se si desidera usare le associazioni out-of-line, come gestire gli errori e come gestire tabelle writeback.  
  
## <a name="specifying-processing-options"></a>Impostazione delle opzioni di elaborazione  
 Il [tipo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) proprietà delle **processo** comando si specifica l'opzione di elaborazione da utilizzare per l'elaborazione dell'oggetto. Per altre informazioni sulle opzioni di elaborazione, vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 Nella tabella seguente sono elencate le costanti per la **tipo** proprietà e i vari oggetti che possono essere elaborati utilizzando ciascuna costante.  
  
|**Tipo** valore|Oggetti applicabili|  
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
  
 Per altre informazioni sull'elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetti, vedere [elaborazione di un modello multidimensionale &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="specifying-objects-to-be-processed"></a>Specifica degli oggetti da elaborare  
 Il [oggetti](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) proprietà delle **processo** comando contiene l'identificatore dell'oggetto da elaborare. È possibile specificare solo un oggetto un **processo** comando, ma l'elaborazione di un oggetto elabora inoltre tutti gli oggetti figlio. L'elaborazione di un gruppo di misure in un cubo, ad esempio, determina l'elaborazione di tutte le partizioni di tale gruppo, mentre l'elaborazione di un database determina l'elaborazione di tutti gli oggetti, quali cubi, dimensioni e strutture di data mining, contenuti nel database.  
  
 Se si imposta la **ProcessAffectedObjects** attributo delle **processo** comando su true, le relative oggetto interessato dall'elaborazione dell'oggetto specificato viene anche elaborato. Ad esempio, se una dimensione viene aggiornata in modo incrementale usando il *ProcessUpdate* nell'opzione di elaborazione il **processo** comando, qualsiasi partizione le cui le aggregazioni vengono invalidate a causa di membri in corso aggiunta o eliminazione viene elaborata anche [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se **ProcessAffectedObjects** è impostato su true. In questo caso, un singolo **processo** comando è possibile elaborare più oggetti in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza, ma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina quali oggetti oltre all'oggetto specificato nel **processo** comando deve anche essere elaborato.  
  
 Tuttavia, è possibile elaborare più oggetti, ad esempio dimensioni, nello stesso momento usando più **processo** comandi all'interno di un **Batch** comando. Operazioni batch offrono un livello di controllo per l'elaborazione seriale o parallelo degli oggetti in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza rispetto all'uso del **ProcessAffectedObjects** attributo e consentono di ottimizzare l'approccio all'elaborazione di dimensioni maggiori [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database. Per altre informazioni sull'esecuzione di operazioni batch, vedere [esecuzione di operazioni Batch &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="specifying-out-of-line-bindings"></a>Specifica di associazioni out-of-line  
 Se il **processo** comando non è contenuto in un **Batch** comando, è possibile specificare associazioni out-of-line nel [associazioni](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla), [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasource-element-xmla), e [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) delle proprietà del **processo** comando per gli oggetti da elaborare. Le associazioni out-of-line sono riferimenti a origini dati, viste origine dati e altri oggetti in cui l'associazione è presente solo durante l'esecuzione del **processo** comando e cui eseguire l'override di qualsiasi binding esistente associato il oggetti in fase di elaborazione. Se non è specificata alcuna associazione out-of-line, vengono utilizzate le associazioni attualmente associate agli oggetti da elaborare.  
  
 Le associazioni out-of-line vengono utilizzate nelle seguenti situazioni:  
  
-   Elaborazione incrementale di una partizione in cui è necessario specificare una tabella dei fatti alternativa o un filtro sulla tabella dei fatti esistente per garantire che le righe non vengono contate due volte.  
  
-   Usando un'attività flusso di dati in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per fornire i dati durante l'elaborazione di una dimensione, un modello di data mining o una partizione.  
  
 Le associazioni out-of-line vengono descritte come parte del linguaggio ASSL (Analysis Services Scripting Language). Per altre informazioni sulle associazioni out-of-line in ASSL, vedere [origini dati e associazioni &#40;multidimensionale di SSAS&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
### <a name="incrementally-updating-partitions"></a>Aggiornamento incrementale di partizioni  
 Per eseguire l'aggiornamento incrementale di una partizione già elaborata, è necessario utilizzare un'associazione out-of-line poiché l'associazione specificata per la partizione fa riferimento a dati della tabella dei fatti già aggregati all'interno della partizione. Quando l'aggiornamento incrementale di una partizione già elaborata tramite il **processo** comando, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esegue le azioni seguenti:  
  
-   Creazione di una partizione temporanea con una struttura identica a quella della partizione da aggiornare in modo incrementale.  
  
-   Elabora la partizione temporanea tramite l'associazione out-of-line specificata nel **processo** comando.  
  
-   Unione della partizione temporanea con la partizione esistente selezionata.  
  
 Per altre informazioni sull'unione di partizioni utilizzando XML for Analysis (XMLA), vedere [unione di partizioni &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md).  
  
## <a name="handling-processing-errors"></a>Gestione degli errori di elaborazione  
 Il [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) proprietà delle **processo** comando consente di specificare come gestire gli errori rilevati durante l'elaborazione di un oggetto. Ad esempio durante l'elaborazione di una dimensione in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene rilevato un valore duplicato nella colonna chiave dell'attributo chiave. Poiché le chiavi dell'attributo devono essere univoche, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elimina i record duplicati. In base il [KeyDuplicate](https://docs.microsoft.com/bi-reference/assl/properties/keyduplicate-element-assl) proprietà di **ErrorConfiguration**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è stato possibile:  
  
-   Continuazione dell'elaborazione della dimensione poiché il messaggio viene ignorato.  
  
-   Restituzione di un messaggio che indica che in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è stata rilevata una chiave duplicata e continuazione dell'elaborazione.  
  
 Esistono numerose condizioni analoghe per cui **ErrorConfiguration** fornisce opzioni durante un **processo** comando.  
  
## <a name="managing-writeback-tables"></a>Gestione di tabelle writeback  
 Se il **processo** comando rileva una partizione abilitata per la scrittura o un cubo o gruppo di misure per tale partizione, che non è già completamente elaborato, una tabella writeback non può già esistere per la partizione. Il [WritebackTableCreation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/writebacktablecreation-element-xmla) proprietà delle **processo** comando determina se [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve creare una tabella writeback.  
  
## <a name="examples"></a>Esempi  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente viene elaborato completamente il database di esempio [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="code"></a>Codice  
  
```  
<Process xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Descrizione  
 Elabora in modo incrementale nell'esempio seguente il **Internet_Sales_2004** partizionare nel **Internet Sales** gruppo di misure del **Adventure Works DW** cubo nel [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] esempio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database. Il **processo** comando aggiunge le aggregazioni per l'ordine date successive al 31 dicembre 2006 nella partizione usando un'associazione di query out-of-line nel **associazioni** proprietà del **processo**  comando per recuperare le righe della tabella dei fatti da cui generare le aggregazioni da aggiungere alla partizione.  
  
### <a name="code"></a>Codice  
  
```  
<Process ProcessAffectedObjects="true" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
  
