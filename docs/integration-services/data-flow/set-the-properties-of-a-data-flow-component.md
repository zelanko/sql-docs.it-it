---
title: Impostare le proprietà di un componente flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 10b397e4fdabefe333854fe04ab37c4bdd92cf38
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71291837"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>Impostazione delle proprietà di un componente del flusso di dati

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Per impostare le proprietà dei componenti flusso di dati, tra cui origini, destinazioni e trasformazioni, utilizzare una delle funzionalità seguenti:  
  
-   Editor dei componenti forniti da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Gli editor includono solo le proprietà personalizzate di ogni componente flusso di dati.  
  
-   Nella finestra **Proprietà** sono elencate sia le proprietà personalizzate a livello di componente per ogni elemento, sia le proprietà comuni a tutti gli elementi del flusso di dati.  
  
-   La finestra di dialogo **Editor avanzato** consente l'accesso alle proprietà personalizzate di ciascun componente. La finestra di dialogo **Editor avanzato** consente anche di accedere alle proprietà comuni a tutti i componenti flusso di dati, ossia le proprietà degli input, degli output, degli output degli errori, delle colonne e delle colonne esterne.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-a-component-editor"></a>Impostare le proprietà di un componente flusso di dati usando un editor del componente  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** , quindi fare doppio clic sull'attività Flusso di dati che contiene il flusso di dati con il componente di cui si desidera visualizzare e modificare le proprietà.  
  
4.  Fare doppio clic sul componente del flusso di dati.  
  
5.  Nell'editor del componente visualizzare o modificare i valori delle proprietà e quindi chiudere l'editor.  
  
6.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
## <a name="set-the-properties-of-a-data-flow-component-in-the-properties-window"></a>Impostare le proprietà di un componente flusso di dati nella finestra Proprietà  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** , quindi fare doppio clic sull'attività Flusso di dati che contiene il componente di cui si desidera visualizzare e modificare le proprietà.  
  
4.  Fare clic con il pulsante destro del mouse sul componente flusso di dati, quindi scegliere **Proprietà**.  
  
5.  Visualizzare o modificare i valori delle proprietà, quindi chiudere la finestra **Proprietà** .  
  
    > [!NOTE]  
    >  Molte proprietà sono in sola lettura e non possono essere modificate.  
  
6.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-the-advanced-editor"></a>Impostare le proprietà di un componente flusso di dati usando l'Editor avanzato  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** , quindi fare doppio clic sull'attività Flusso di dati che contiene il componente che si desidera visualizzare o modificare.  
  
4.  Nella finestra di progettazione del flusso di dati fare clic con il pulsante destro del mouse sul componente flusso di dati, quindi scegliere **Visualizza editor avanzato**.  
  
    > [!NOTE]  
    >  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]non è possibile utilizzare la finestra di dialogo **Editor avanzato**per i componenti flusso di dati che supportano più input.  
  
5.  Nella finestra di dialogo **Editor avanzato** eseguire una delle operazioni seguenti:  
  
    -   Fare clic sulla scheda **Gestioni connessioni** per visualizzare e specificare la connessione usata dal componente.  
  
        > [!NOTE]  
        >  La scheda **Gestioni connessioni** è disponibile solo per i componenti flusso di dati che utilizzano gestioni connessioni per connettersi a origini dati quali file e database.  
  
    -   Fare clic sulla scheda **Proprietà componente** per visualizzare e modificare le proprietà a livello di componente.  
  
    -   Fare clic sulla scheda **Mapping colonne** per visualizzare e modificare i mapping tra le colonne esterne e l'output disponibile.  
  
        > [!NOTE]  
        >  La scheda **Mapping colonne** è disponibile solo durante la visualizzazione o la modifica di origini o destinazioni.  
  
    -   Per visualizzare un elenco delle colonne di input disponibili e aggiornare i nomi delle colonne di output, fare clic sulla scheda **Colonne di input** .  
  
        > [!NOTE]  
        >  La scheda Colonne di input è disponibile solo quando si utilizzano trasformazioni o destinazioni. Per altre informazioni, vedere [Trasformazioni di Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md).  
  
    -   Fare clic sulla scheda **Proprietà input e output** per visualizzare e modificare le proprietà degli input, degli output e degli output degli errori, nonché le proprietà delle colonne che contengono.  
  
        > [!NOTE]  
        >  Le origini non includono input, mentre le destinazioni non includono output, ad eccezione di un output degli errori facoltativo.  
  
6.  Visualizzare o modificare i valori delle proprietà.  
  
7.  Fare clic su **OK**.  
  
8.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  

## <a name="common-properties-of-data-flow-components"></a>Proprietà comuni dei componenti flusso di dati
Gli oggetti del flusso di dati nel modello a oggetti [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] hanno proprietà comuni e proprietà personalizzate a livello di componente, input e output, colonne di input e colonne di output. Molte proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
 In questo argomento vengono elencate e descritte le proprietà comuni degli oggetti del flusso di dati.  
  
-   [Componenti](#components)  
  
-   [Input](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [Output](#outputs)  
  
-   [Colonne di output](#outputcolumns)  
  
 
###  <a name="components"></a> Component properties  
 Nel modello a oggetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] un componente nel flusso di dati implementa l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 Nella tabella seguente vengono descritte le proprietà dei componenti in un flusso di dati. Alcune proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ComponentClassID|string|Valore CLSID del componente.|  
|ContactInfo|string|Informazioni di contatto dello sviluppatore di un componente.|  
|Descrizione|string|Descrizione del componente flusso di dati. Il valore predefinito di questa proprietà è il nome del componente flusso di dati.|  
|ID|Integer|Valore che identifica in modo univoco questa istanza del componente.|  
|IdentificationString|string|Identifica il componente.|  
|IsDefaultLocale|Boolean|Indica se il componente utilizza le impostazioni locali dell'attività Flusso di dati alla quale appartiene.|  
|LocaleID|Integer|Impostazioni locali che il componente flusso di dati utilizza durante l'esecuzione del pacchetto. Tutte le impostazioni locali di Windows sono disponibili per l'utilizzo nei componenti flusso di dati.|  
|Nome|string|Nome del componente del flusso di dati.|  
|PipelineVersion|Integer|Versione dell'attività Flusso di dati nella quale il componente è progettato per l'esecuzione.|  
|UsesDispositions|Boolean|Indica se un componente ha un output degli errori.|  
|ValidateExternalMetadata|Boolean|Indica se i metadati delle colonne esterne sono convalidati. Il valore predefinito di questa proprietà è **True**.|  
|Versione|Integer|Versione di un componente.|  
  
###  <a name="inputs"></a> Proprietà degli input  
 Nel modello a oggetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , le trasformazioni e le destinazioni includono input. L'input di un componente nel flusso di dati implementa l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>.  
  
 Nella tabella seguente vengono descritte le proprietà degli input dei componenti in un flusso di dati. Alcune proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|Descrizione|string|Descrizione dell'input.|  
|ErrorOrTruncationOperation|string|Stringa facoltativa che specifica i tipi di errori o troncamenti che possono verificarsi durante l'elaborazione di una riga.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valore che specifica la gestione degli errori. I valori sono **Interrompi componente**, **Ignora errore**e **Reindirizza riga**.|  
|HasSideEffects|Boolean|Indica se un componente può essere rimosso dal piano di esecuzione del flusso di dati se non è collegato a un componente a valle e se la proprietà **RunInOptimizedMode** è impostata su **true**.|  
|ID|Integer|Valore che identifica l'input in modo univoco.|  
|IdentificationString|string|Stringa che identifica l'input.|  
|IsSorted|Boolean|Indica se i dati nell'input sono ordinati.|  
|Nome|string|Nome dell'input.|  
|SourceLocale|Integer|ID delle impostazioni locali (LCID) dei dati di input.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valore che determina la gestione dei troncamenti da parte del componente durante l'elaborazione delle righe. . I valori sono **Interrompi componente**, **Ignora errore**e **Reindirizza riga**.|  
  
 Le destinazioni e alcune trasformazioni non supportano gli output degli errori e le proprietà ErrorRowDisposition e TruncationRowDisposition di questi componenti sono di sola lettura.  
  
###  <a name="inputcolumns"></a> Proprietà delle colonne di input  
 Nel modello a oggetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un input contiene una raccolta di colonne di input. Una colonna di input di un componente nel flusso di dati implementa l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100>.  
  
 Nella tabella seguente vengono descritte le proprietà delle colonne di input dei componenti in un flusso di dati. Alcune proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Set di flag che specificano il confronto di colonne che hanno un tipo di dati character. Per altre informazioni, vedere [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).|  
|Descrizione|string|Descrive la colonna di input.|  
|ErrorOrTruncationOperation|string|Stringa facoltativa che specifica i tipi di errori o troncamenti che possono verificarsi durante l'elaborazione di una riga.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valore che specifica la gestione degli errori. I valori sono **Interrompi componente**, **Ignora errore**e **Reindirizza riga**.|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|ID della colonna di metadati esterna assegnato a una colonna di input.|  
|ID|Integer|Valore che identifica la colonna di input in modo univoco.|  
|IdentificationString|string|Stringa che identifica la colonna di input.|  
|LineageID|Integer|ID della colonna a monte.|  
|LineageIdentificationString|string|Stringa di identificazione che include il nome della colonna a monte.|  
|Nome|string|Nome della colonna di input.|  
|SortKeyPosition|Integer|Valore che indica se una colonna è ordinata, l'ordinamento e la sequenza di ordinamento di più colonne. Il valore **0** indica che la colonna non è ordinata.  Per altre informazioni, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valore che determina la gestione dei troncamenti da parte del componente durante l'elaborazione delle righe. I valori sono **Interrompi componente**, **Ignora errore**e **Reindirizza riga**.|  
|UpstreamComponentName|string|Nome del componente a monte.|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|Valore che determina come una colonna di input viene utilizzata dal componente.|  
  
 Le colonne di input includono anche le proprietà del tipo di dati descritte in "Proprietà del tipo di dati".  
  
###  <a name="outputs"></a> Proprietà degli output  
 Nel modello a oggetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , le origini e le trasformazioni includono output. L'output di un componente nel flusso di dati implementa l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>.  
  
 Nella tabella seguente vengono descritte le proprietà degli output dei componenti in un flusso di dati. Alcune proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Boolean|Valore che determina se il motore del flusso di dati elimina l'output quando viene scollegato da un percorso.|  
|Descrizione|string|Descrive l'output.|  
|ErrorOrTruncationOperation|string|Stringa facoltativa che specifica i tipi di errori o troncamenti che possono verificarsi durante l'elaborazione di una riga.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valore che specifica la gestione degli errori. I valori sono **Interrompi componente**, **Ignora errore**e **Reindirizza riga**.|  
|ExclusionGroup|Integer|Valore che identifica un gruppo di output che si escludono a vicenda.|  
|HasSideEffects|Boolean|Valore che indica se un componente può essere rimosso dal piano di esecuzione del flusso di dati se non è collegato a un componente a monte e se la proprietà **RunInOptimizedMode** è impostata su **true**.|  
|ID|Integer|Valore che identifica l'output in modo univoco.|  
|IdentificationString|string|Stringa che identifica l'output.|  
|IsErrorOut|Boolean|Indica se l'output è un output degli errori.|  
|IsSorted|Boolean|Indica se l'output è ordinato. Il valore predefinito è **False**.<br /><br /> **\*\* Importante \*\*** L'impostazione del valore della proprietà **IsSorted** su **True** non determina l'ordinamento dei dati. Questa proprietà fornisce solo un hint ai componenti a valle in relazione all'ordinamento precedente dei dati. Per altre informazioni, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|Nome|string|Nome dell'output.|  
|SynchronousInputID|Integer|ID di un input sincrono all'output.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valore che determina la gestione dei troncamenti da parte del componente durante l'elaborazione delle righe. I valori sono **Interrompi componente**, **Ignora errore**e **Reindirizza riga**.|  
  
###  <a name="outputcolumns"></a> Proprietà delle colonne di output  
 Nel modello a oggetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un output contiene una raccolta di colonne di output. Una colonna di output di un componente nel flusso di dati implementa l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100>.  
  
 Nella tabella seguente vengono descritte le proprietà delle colonne di output dei componenti in un flusso di dati. Alcune proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Set di flag che specificano il confronto di colonne che hanno un tipo di dati character. Per altre informazioni, vedere [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).|  
|Descrizione|string|Descrive la colonna di output.|  
|ErrorOrTruncationOperation|string|Stringa facoltativa che specifica i tipi di errori o troncamenti che possono verificarsi durante l'elaborazione di una riga.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valore che specifica la gestione degli errori. I valori sono **Interrompi componente**, **Ignora errore**e **Reindirizza riga**. Il valore predefinito è **Interrompi componente**.|  
|ExternalMetadataColumnID|Integer|ID della colonna di metadati esterna assegnato a una colonna di input.|  
|ID|Integer|Valore che identifica la colonna di output in modo univoco.|  
|IdentificationString|string|Stringa che identifica la colonna di output.|  
|LineageID|Integer|ID della colonna di output. I componenti a valle fanno riferimento alla colonna utilizzando questo valore.|  
|LineageIdentificationString|string|Stringa di identificazione che include il nome della colonna.|  
|Nome|string|Nome della colonna di output.|  
|SortKeyPosition|Integer|Valore che indica se una colonna è ordinata, l'ordinamento e la sequenza di ordinamento di più colonne. Il valore **0** indica che la colonna non è ordinata. Per altre informazioni, vedere [Ordinamento dei dati per le trasformazioni Unione e Merge Join](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|SpecialFlags|Integer|Valore che contiene i flag speciali della colonna di output.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valore che determina la gestione dei troncamenti da parte del componente durante l'elaborazione delle righe. I valori sono **Interrompi componente**, **Ignora errore**e **Reindirizza riga**. Il valore predefinito è **Interrompi componente**.|  
  
 Le colonne di output includono anche un set di proprietà del tipo di dati.  
  
### <a name="external-metadata-column-properties"></a>Proprietà delle colonne di metadati esterne  
 Nel modello a oggetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , input e output possono contenere un insieme di colonne di metadati esterne. Una colonna di metadati esterna di un componente nel flusso di dati implementa l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>.  
  
 Nella tabella seguente vengono descritte le proprietà delle colonne di metadati esterne dei componenti in un flusso di dati. Alcune proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|Descrizione|string|Descrive la colonna esterna.|  
|ID|Integer|Valore che identifica la colonna in modo univoco.|  
|IdentificationString|string|Stringa che identifica la colonna.|  
|Nome|string|Nome della colonna esterna.|  
  
 Le colonne di metadati esterne includono anche un set di proprietà del tipo di dati.  
  
### <a name="data-type-properties"></a>Proprietà del tipo di dati  
 Le colonne di metadati esterne e le colonne di output includono anche un set di proprietà del tipo di dati. A seconda del tipo di dati della colonna, le proprietà possono essere di lettura/scrittura o di sola lettura.  
  
 Nella tabella seguente vengono descritte le proprietà del tipo di dati delle colonne di metadati esterne e delle colonne di output.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|CodePage|Integer|Specifica la tabella codici per i dati stringa non Unicode.|  
|DataType|Integer (enumerazione)|Tipo di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] della colonna. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).|  
|Length|Integer|Lunghezza della colonna in caratteri.|  
|Precision|Integer|Precisione di una colonna numerica.|  
|Scalabilità|Integer|Scala di una colonna numerica.|  

## <a name="custom-properties-of-data-flow-components"></a>Proprietà personalizzate dei componenti flusso di dati
Per informazioni sulle proprietà personalizzate, vedere gli argomenti seguenti  
  
-   [Proprietà personalizzate ADO NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
-   [Proprietà personalizzate dell'attività di controllo CDC](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
-   [Proprietà personalizzate dell'origine CDC](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [Proprietà personalizzate della destinazione Training modello di data mining](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [Proprietà personalizzate della destinazione DataReader](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
-   [Proprietà personalizzate della destinazione elaborazione dimensione](../../integration-services/data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Proprietà personalizzate di Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
-   [Proprietà personalizzate del file flat](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
-   [Proprietà personalizzate della destinazione ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
-   [Proprietà personalizzate dell'origine ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
-   [Proprietà personalizzate OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)Proprietà personalizzate OLE DB  
  
-   [Proprietà personalizzate della destinazione elaborazione partizione](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
-   [Proprietà personalizzate del file non elaborato](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
-   [Proprietà personalizzate della destinazione recordset](../../integration-services/data-flow/recordset-destination-custom-properties.md)  
  
-   [Proprietà personalizzate della destinazione SQL Server Compact Edition](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [Proprietà personalizzate della destinazione SQL Server](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
-   [Proprietà personalizzate dell'origine XML](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
## <a name="use-an-expression-in-a-data-flow-component"></a>Usare un'espressione in un componente flusso di dati
In questo argomento viene descritta la procedura per l'aggiunta di un'espressione nella trasformazione Suddivisione condizionale o Colonna derivata. La trasformazione Suddivisione condizionale utilizza espressioni per definire le condizioni che dirigono le righe di dati all'output della trasformazione, mentre la trasformazione Colonna derivata utilizza espressioni per definire i valori assegnati alle colonne.  
  
 Per implementare un'espressione in una trasformazione, è necessario che il pacchetto includa almeno un'attività Flusso di dati e un'origine. 
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo** e quindi sull'attività Flusso di dati contenente il flusso di dati in cui si vuole implementare un'espressione.  
  
4.  Fare clic sulla scheda **Flusso di dati** e trascinare una trasformazione Suddivisione condizionale o Colonna derivata dalla **casella degli strumenti** all'area di progettazione.  
  
5.  Trascinare il connettore verde dall'origine o trasformazione alla trasformazione Suddivisione condizionale o Colonna derivata.  
  
6.  Fare doppio clic sulla trasformazione. Verrà visualizzata la finestra di dialogo corrispondente.  
  
7.  Nel riquadro di sinistra espandere il nodo **Variabili** in modo da visualizzare le variabili definite dall'utente e di sistema. Espandere anche il nodo **Colonne** in modo da visualizzare le colonne di input della trasformazione.  
  
8.  Nel riquadro di destra espandere i nodi **Funzioni matematiche**, **Funzioni per i valori stringa**, **Funzioni di data/ora**, **Funzioni NULL**, **Cast di tipo**e **Operatori** per accedere alle funzioni, ai cast e agli operatori del linguaggio delle espressioni.  
  
9. A seconda della trasformazione, compilare un'espressione in uno dei modi seguenti:  
  
    -   Nella finestra di dialogo **Editor trasformazione Suddivisione condizionale** trascinare variabili, colonne, funzioni, operatori e cast nella colonna **Condizione** . In alternativa, è possibile digitare l'espressione direttamente nella colonna **Condizione** .  
  
    -   Nella finestra di dialogo **Editor trasformazione Colonna derivata** trascinare variabili, colonne, funzioni, operatori e cast nella colonna **Espressione** . In alternativa, è possibile digitare l'espressione direttamente nella colonna **Espressione** .  
  
        > [!NOTE]  
        >  Quando lo stato attivo viene rimosso dalla colonna **Condizione** o **Espressione** , il testo dell'espressione potrebbe essere evidenziato per indicare che la sintassi dell'espressione non è corretta.  
  
10. Fare clic su **OK** per chiudere la finestra di dialogo.  
  
    > [!NOTE]  
    >  Se l'espressione non è valida, viene visualizzato un avviso che evidenzia gli errori di sintassi.  

## <a name="data-flow-properties-that-you-can-set-with-an-expression"></a>Proprietà del flusso di dati che è possibile impostare con un'espressione
I valori di determinate proprietà di oggetti del flusso di dati possono essere specificati utilizzando espressioni di proprietà disponibili nel contenitore dell'attività Flusso di dati.  
  
 Per informazioni sull'utilizzo delle espressioni di proprietà, vedere [utilizzo delle espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 È possibile utilizzare espressioni di proprietà per personalizzare la configurazione di ogni istanza di pacchetto distribuita. È anche possibile usare espressioni di proprietà per specificare i vincoli in fase di esecuzione per un pacchetto tramite l'opzione **/set** con l'utilità del prompt dei comandi **dtexec** . Ad esempio, è possibile vincolare il **MaximumThreads** usato dalla trasformazione dell'ordinamento o il **MaxMemoryUsage** delle trasformazioni del raggruppamento fuzzy e della ricerca fuzzy. Se non vincolate, queste trasformazioni possono memorizzare nella cache grandi quantità di dati.  
  
 Per specificare un'espressione di proprietà per una delle proprietà degli oggetti del flusso di dati elencate in questo argomento, visualizzare la finestra **Proprietà** per l'attività flusso di dati selezionando l'attività flusso di dati nell'area di progettazione **Flusso di controllo** o selezionando la scheda **Flusso di dati** della finestra di progettazione senza selezionare componenti o percorsi singoli. Selezionare la proprietà **Espressioni** e fare clic sui puntini di sospensione per visualizzare la finestra di dialogo **Editor espressioni di proprietà** . Visualizzare l'elenco a discesa **Proprietà** per selezionare una proprietà, quindi digitare un'espressione nella casella di testo **Espressione** o fare clic sui puntini di sospensione per visualizzare la finestra di dialogo **Generatore di espressioni** .  
  
 Nell'elenco **Proprietà** vengono visualizzate le proprietà disponibili per gli oggetti del flusso di dati già posizionati nell'area di progettazione **Flusso di dati** . Pertanto, non è possibile usare l'elenco **Proprietà** per visualizzare tutte le possibili proprietà degli oggetti del flusso di dati che supportano le espressioni di proprietà. Ad esempio, se è stata posizionata un'origine ADO NET nell'area di progettazione, l'elenco **Proprietà** contiene una voce per la proprietà **[ADO NET Source].[SqlCommand]** . Nell'elenco vengono anche visualizzate molte proprietà dell'attività Flusso di dati.  
 
 È possibile specificare i valori delle proprietà del seguente elenco utilizzando le espressioni di proprietà.  
  
### <a name="data-flow-sources"></a>Origini del flusso di dati  
  
|Oggetto del flusso di dati|Proprietà|  
|----------------------|--------------|  
|Origine ADO NET|Proprietà TableOrViewName<br /><br /> Proprietà SqlCommand|  
|Origine XML|Proprietà XMLData<br /><br /> Proprietà XMLSchemaDefinition|  
  
### <a name="data-flow-transformations"></a>Trasformazioni del flusso di dati  
 Per altre informazioni su queste proprietà personalizzate, vedere [proprietà personalizzate della trasformazione](../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
|Oggetto del flusso di dati|Proprietà|  
|----------------------|--------------|  
|Suddivisione condizionale - trasformazione|Proprietà FriendlyExpression|  
|Trasformazione Colonna derivata|Proprietà FriendlyExpression|  
|Raggruppamento fuzzy - trasformazione|Proprietà MaxMemoryUsage|  
|Ricerca fuzzy - trasformazione|Proprietà MaxMemoryUsage|  
|Trasformazione Ricerca|Proprietà SqlCommand<br /><br /> Proprietà SqlCommandParam|  
|Comando OLE DB - trasformazione|Proprietà SqlCommand|  
|Campionamento percentuale - trasformazione|Proprietà SamplingValue|  
|Pivot - trasformazione|Proprietà PivotKeyValue|  
|Campionamento righe - trasformazione|Proprietà SamplingValue|  
|Ordinamento - trasformazione|Proprietà MaximumThreads|  
|UnPivot - trasformazione|Proprietà PivotKeyValue|  
  
### <a name="data-flow-destinations"></a>Destinazioni del flusso di dati  
  
|Oggetto del flusso di dati|Proprietà|  
|----------------------|--------------|  
|Destinazione ADO NET|Proprietà TableOrViewName<br /><br /> Proprietà BatchSize<br /><br /> Proprietà CommandTimeout|  
|file flat - destinazione|Proprietà dell'intestazione|  
|Destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact|Proprietà TableName|  
|Destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Proprietà BulkInsertTableName<br /><br /> Proprietà BulkInsertFirstRow<br /><br /> Proprietà BulkInsertLastRow<br /><br /> Proprietà BulkInsertOrder<br /><br /> Proprietà Timeout|  

