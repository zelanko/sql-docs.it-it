---
title: Origini dati e associazioni (SSAS multidimensionale) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data source views [Analysis Services], bindings
- DSO, bindings
- Analysis Services Scripting Language, data sources
- cubes [Analysis Services], bindings
- OLAP mining models [Analysis Services Scripting Language]
- bindings [Analysis Services Scripting Language]
- rebindings [Analysis Services Scripting Language]
- ASSL, bindings
- relational mining models [ASSL]
- data sources [Analysis Services Scripting Language]
- ASSL, data sources
- dimensions [Analysis Services], bindings
- measures [Analysis Services], bindings
- relational data sources [Analysis Services Scripting Language]
- Analysis Services Scripting Language, bindings
- chaptered rowsets
- granularity
- mining models [Analysis Services], data sources
- inline bindings [ASSL]
- out-of-line bindings
- measure groups [Analysis Services], bindings
- partitions [Analysis Services], bindings
ms.assetid: bc028030-dda2-4660-b818-c3160d79fd6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60b3e29ae94c4dcf5d136bcc01bf291a9a6118fe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62700089"
---
# <a name="data-sources-and-bindings-ssas-multidimensional"></a>Origini dati e associazioni (SSAS - multidimensionale)
  È possibile associare cubi, dimensioni e altri oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a un'origine dati. Un'origine dati può essere rappresentata da uno dei seguenti oggetti:  
  
-   Un'origine dati relazionale.  
  
-   Una pipeline di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che restituisce un set di righe o un set di righe inserito in un capitolo.  
  
 La modalità di espressione dell'origine dati varia in base al tipo di origine dati. Un'origine dati relazionale si distingue ad esempio per la stringa di connessione. Per altre informazioni sulle origini dati, vedere [Origini dati nei modelli multidimensionali](data-sources-in-multidimensional-models.md).  
  
 Indipendentemente dall'origine dati utilizzata, la vista origine dati contiene i metadati per l'origine dati. Le associazioni per un cubo o altri oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono pertanto espresse sotto forma di associazioni alla vista origine dati. Queste associazioni possono includere associazioni a oggetti di oggetti logici, ad esempio viste, colonne calcolate e relazioni che non esistono fisicamente nell'origine dati. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aggiunge una colonna calcolata che incapsula l'espressione nella vista origine dati, quindi associa la misura OLAP corrispondente a tale colonna nella vista origine dati. Per altre informazioni sulle viste origine dati, vedere [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md).  
  
 Ciascun oggetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene associato all'origine dati in modo specifico. Inoltre, le associazioni dati per tali oggetti e la definizione dell'origine dati possono essere fornite inline con la definizione dell'oggetto associato a dati, ad esempio la dimensione, oppure out-of-line come un set di definizioni distinto.  
  
## <a name="analysis-services-data-types"></a>Tipi di dati di Analysis Services  
 I tipi di dati usati nelle associazioni devono corrispondere ai tipi di dati supportati da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]sono definiti i tipi di dati seguenti:  
  
|Tipo di dati di Analysis Services|Descrizione|  
|---------------------------------|-----------------|  
|BigInt|Intero con segno a 64 bit. Per questo tipo di dati viene eseguito il mapping al tipo di dati Int64 in Microsoft [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_I8 in OLE DB.|  
|Bool|Valore booleano. Per questo tipo di dati viene eseguito il mapping al tipo di dati Boolean in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_BOOL in OLE DB.|  
|Currency|Valore di valuta compreso nell'intervallo tra -2 63 (o -922337.203.685.477,5808) e 2 63 -1 (o +922.337.203.685.477,5807) con un'approssimazione pari a dieci millesimi di unità di valuta. Per questo tipo di dati viene eseguito il mapping al tipo di dati Decimal in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_CY in OLE DB.|  
|date|Dati di data, archiviati come numero a virgola mobile a precisione doppia. La parte intera è il numero di giorni a partire dal 30 dicembre 1899 mentre la parte frazionaria rappresenta una frazione del giorno. Per questo tipo di dati viene eseguito il mapping al tipo di dati DateTime in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_DATE in OLE DB.|  
|Double|Numero a virgola mobile a precisione doppia compreso tra -1.79E +308 e 1.79E +308. Per questo tipo di dati viene eseguito il mapping al tipo di dati Double in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_R8 in OLE DB.|  
|Valore intero|Intero con segno a 32 bit. Per questo tipo di dati viene eseguito il mapping al tipo di dati Int32 in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_I4 in OLE DB.|  
|Single|Numero a virgola mobile a precisione singola compreso tra -3.40E +38 e 3.40E +38. Per questo tipo di dati viene eseguito il mapping al tipo di dati Single in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_R4 in OLE DB.|  
|SmallInt|Intero con segno a 16 bit. Per questo tipo di dati viene eseguito il mapping al tipo di dati Int16 in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_I2 in OLE DB.|  
|TinyInt|Numero intero con segno a 8 bit. Per questo tipo di dati viene eseguito il mapping al tipo di dati SByte in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_I1 in OLE DB.<br /><br /> Nota: Se un'origine dati contiene campi che sono di tipo tinyint e la proprietà AutoIncrement è impostata su True, verranno convertiti in numeri interi nella vista origine dati.|  
|UnsignedBigInt|Intero senza segno a 64 bit. Per questo tipo di dati viene eseguito il mapping al tipo di dati UInt64 in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_UI8 in OLE DB.|  
|UnsignedInt|Intero senza segno a 32 bit. Per questo tipo di dati viene eseguito il mapping al tipo di dati UInt32 in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_UI4 in OLE DB.|  
|UnsignedSmallInt|Numero intero non firmato a 16 bit. Per questo tipo di dati viene eseguito il mapping al tipo di dati UInt16 in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_UI2 in OLE DB.|  
|WChar|Flusso con terminazione Null di caratteri Unicode. Per questo tipo di dati viene eseguito il mapping al tipo di dati String in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e al tipo di dati DBTYPE_WSTR in OLE DB.|  
  
 Tutti dati ricevuti dall'origine dati vengono convertiti nel tipo [!INCLUDE[ssAS](../../includes/ssas-md.md)] specificato nell'associazione, in genere durante l'elaborazione. Viene generato un errore se non è possibile eseguire la conversione (ad esempio da String a Int). [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] imposta in genere il tipo di dati nell'associazione su quello che corrisponde meglio al tipo di origine nell'origine dati. Ad esempio, per i tipi di dati SQL Date, DateTime, SmallDateTime, DateTime2, DateTimeOffset viene eseguito il mapping a [!INCLUDE[ssAS](../../includes/ssas-md.md)] Date e il tipo SQL Time a String.  
  
## <a name="bindings-for-dimensions"></a>Associazioni per dimensioni  
 Ciascun attributo di una dimensione è associato a una colonna in una vista origine dati. Tutti gli attributi di una dimensione devono provenire da una singola origine dati. È tuttavia possibile associare gli attributi a colonne di diverse tabelle. Le relazioni tra le tabelle sono definite nella vista origine dati. Nel caso in cui è presente più di un set di relazioni alla stessa tabella, potrebbe essere necessario introdurre una query denominata nella vista origine dati come tabella di 'alias'. Le espressioni e i filtri sono definiti nella tabella origine dati mediante calcoli denominati e query denominate.  
  
## <a name="bindings-for-measuregroups-measures-and-partitions"></a>Associazioni per gruppi di misure, misure e partizioni  
 Ciascun gruppo di misure dispone delle seguenti associazioni predefinite:  
  
-   Il gruppo di misure è associato a una tabella in una vista origine dati, ad esempio `MeasureGroup.Source`.  
  
-   Ciascun gruppo di misure è associato a una colonna della tabella, ad esempio `Measure.ValueColumn.Source`.  
  
-   Ogni dimensione del gruppo di misure dispone di un set di *attributi di granularità* che definiscono la granularità del gruppo di misure. Ciascuno di tali attributi deve essere associato alla colonna o alle colonne della tabella dei fatti contenente la chiave dell'attributo. Per ulteriori informazioni sugli attributi di granularità, vedere "Attributi di granularità dei gruppi di misure" più avanti in questo argomento.  
  
 È possibile eseguire l'override di queste associazioni predefinite in modo selettivo per partizione. Ogni partizione può specificare un'origine dati, un nome di tabella o di query o un'espressione di filtro differente. La strategia di partizionamento più comune consiste nell'eseguire l'override della tabella per partizione, utilizzando la stessa origine dati. È anche possibile applicare un filtro diverso per partizione o modificare l'origine dati.  
  
 È necessario definire l'origine dati predefinita nella tabella origine dati, fornendo le informazioni sullo schema e includendo i dettagli delle relazioni. Sebbene le tabelle e le query aggiuntive specificate a livello di partizione non debbano essere elencate nella vista origine dati, devono avere lo stesso schema della tabella predefinita definita per il gruppo di misure o contenere almeno tutte le colonne utilizzate dalle misure o dagli attributi di granularità. Non è possibile eseguire l'override a livello di partizione delle associazioni dettagliate per misura e attributo di granularità. Si presuppone inoltre che si tratti delle stesse colonne definite per il gruppo di misure. Pertanto, se la partizione utilizza un'origine dati con uno schema diverso, la query `TableDefinition` definita per la partizione deve restituire lo stesso schema utilizzato dal gruppo di misure.  
  
### <a name="measuregroup-granularity-attributes"></a>Attributi di granularità dei gruppi di misure  
 Se la granularità di un gruppo di misure corrisponde alla granularità nota nel database ed esiste una relazione diretta tra la tabella dei fatti e la tabella delle dimensioni, l'attributo di granularità deve essere associato solo alla colonna chiave esterna appropriata o alle colonne nella tabella dei fatti. Si considerino ad esempio la tabella dei fatti e la tabella delle dimensioni seguenti:  
  
 `Sales(RequestedDate, OrderedProductID, ReplacementProductID, Qty)`  
  
 `Product(ProductID, ProductName,Category)`  
  
 ``  
  
 `Relation: Sales.OrderedProductID -> Product.ProductID`  
  
 `Relation: Sales.ReplacementProductID -> Product.ProductID`  
  
 ``  
  
 Se si esegue l'analisi in base al prodotto ordinato, l'attributo di granularità Product viene associato a Sales.OrderedProductID per il ruolo di dimensione Ordered Product on Sales.  
  
 In alcuni casi è tuttavia possibile che gli `GranularityAttributes` non esistano come colonne nella tabella dei fatti. Di seguito vengono riportati i casi in cui gli `GranularityAttributes` potrebbero non esistere come colonne:  
  
-   La granularità OLAP è più grossolana della granularità nell'origine.  
  
-   Una tabella intermedia si interpone tra la tabella dei fatti e la tabella delle dimensioni.  
  
-   La chiave della dimensione non corrisponde alla chiave primaria nella tabella delle dimensioni.  
  
 In tali casi, è necessario definire la vista origine dati in modo che siano presenti attributi di granularità nella tabella dei fatti. È ad esempio possibile introdurre una query denominata o una colonna calcolata.  
  
 In caso di granularità per categoria, nelle stesse tabelle di esempio indicate in precedenza è ad esempio possibile introdurre una vista delle vendite:  
  
 `SalesWithCategory(RequestedDate, OrderedProductID, ReplacementProductID, Qty, OrderedProductCategory)`  
  
 `SELECT Sales.*, Product.Category AS OrderedProductCategory`  
  
 `FROM Sales INNER JOIN Product`  
  
 `ON Sales.OrderedProductID = Product.ProductID`  
  
 ``  
  
 In questo caso, la categoria dell'attributo di granularità è associata a SalesWithCategory.OrderedProductCategory.  
  
### <a name="migrating-from-decision-support-objects"></a>Esecuzione della migrazione da DSO (Decision Support Objects)  
 DSO (Decision Support Objects) 8.0 consente di riassociare le `PartitionMeasures`. La strategia di migrazione in questi casi consiste pertanto nella costruzione della query appropriata.  
  
 In modo analogo, non è possibile riassociare gli attributi della dimensione all'interno di una partizione, sebbene DSO 8.0 supporti anche la riassociazione. In questi casi, la strategia di migrazione consiste nel definire le query denominate necessarie nella vista origine dati, in modo tale che nella vista origine dati della partizione esistano le stesse tabelle e colonne utilizzate per la dimensione. Potrebbe in tali casi essere necessario utilizzare la migrazione semplice, che prevede il mapping della clausola From/Join/Filter a una sola query denominata anziché a un set strutturato di tabelle correlate. Sebbene DSO 8.0 consenta la riassociazione delle dimensioni della partizione anche se la partizione utilizza la stessa origine dati, è possibile che la migrazione richieda più viste origine dati per la stessa origine dati.  
  
 In DSO 8.0 le associazioni corrispondenti possono essere espresse in due diversi modi, a seconda se vengono utilizzati schemi ottimizzati: associazione alla chiave primaria nella tabella delle dimensioni o alla chiave esterna nella tabella dei fatti. In ASSL non è possibile distinguere questi due modi.  
  
 Lo stesso approccio relativo alle associazioni è valido anche per una partizione che utilizza un'origine dati non contenente tabelle delle dimensioni, poiché viene effettuata l'associazione alla colonna chiave esterna nella tabella dei fatti, anziché alla colonna chiave primaria nella tabella delle dimensioni.  
  
## <a name="bindings-for-mining-models"></a>Associazioni per modelli di data mining  
 Un modello di data mining può essere relazionale oppure OLAP. Le associazioni dati per un modello di data mining relazionale sono molto diverse da quelle per un modello di data mining OLAP.  
  
### <a name="bindings-for-a-relational-mining-model"></a>Associazioni per un modello di data mining relazionale  
 Un modello di data mining relazionale si basa sulle relazioni definite nella vista origine dati per risolvere qualsiasi ambiguità relativa alle associazioni tra colonne e origini dati. In un modello di data mining relazionale, le associazioni dati sono basate sulle seguenti regole:  
  
-   Ciascuna colonna di tabella non nidificata è associata a una colonna nella tabella del case o a una tabella correlata alla tabella del case, in base a una relazione molti-a-uno o uno-a-uno. Le relazioni tra le tabelle sono definite nella vista origine dati.  
  
-   Ciascuna colonna di tabella nidificata è associata a una tabella di origine. Le colonne di proprietà della colonna di tabella nidificata vengono pertanto associate alle colonne della tabella di origine o di una tabella correlata alla tabella di origine. Anche in questo caso, l'associazione si basa su una relazione molti-a-uno o uno-a-uno. Le associazioni per il modello di data mining non forniscono il percorso di join della tabella nidificata. Tali informazioni vengono invece fornite dalle relazioni definite nella vista origine dati.  
  
### <a name="bindings-for-an-olap-mining-model"></a>Associazioni per un modello di data mining OLAP  
 I modelli di data mining OLAP non dispongono di un elemento equivalente a una vista origine dati. È pertanto necessario che le associazioni dati consentano la risoluzione di ambiguità tra colonne e origini dati. È ad esempio possibile che un modello di data mining sia basato sul cubo Sales e che le colonne siano basate su Qty, Amount e Product Name. In alternativa, è possibile che un modello di data mining sia basato su Product e che le colonne siano basate su Product Name, Product Color e su una tabella nidificata con Sales Qty.  
  
 In un modello di data mining OLAP, le associazioni dati sono basate sulle seguenti regole:  
  
-   Ciascuna colonna di tabella non nidificata è associata a una misura in un cubo, a un attributo in una dimensione del cubo (specificando `CubeDimension` per risolvere l'ambiguità nel caso dei ruoli di dimensione) o a un attributo in una dimensione.  
  
-   Ciascuna colonna di tabella nidificata è associata a `CubeDimension`. Definisce pertanto la modalità di navigazione da una dimensione a un cubo correlato o, nel caso meno comune di tabelle nidificate, da un cubo a una delle relative dimensioni.  
  
## <a name="out-of-line-bindings"></a>associazioni out-of-line  
 Le associazioni out-of-line consentono di modificare temporaneamente le associazioni dati esistenti per la durata di un comando. Le associazioni out-of-line si riferiscono ad associazioni incluse in un comando e non sono persistenti. Tali associazioni si applicano solo durante l'esecuzione del comando specifico. Le associazioni inline sono invece contenute in una definizione di oggetto ASSL e risultano persistenti con la definizione di oggetto nei metadati del server.  
  
 ASSL consente di specificare le associazioni out-of-line in un comando `Process`, se non è in un batch, o in un comando `Batch`. Se le associazioni out-of-line sono specificate nel comando `Batch`, tutte le associazioni specificate nel comando `Batch` creano un nuovo contesto di associazione in cui vengono eseguiti tutti i comandi `Process` del batch. Il nuovo contesto di associazione include oggetti elaborati indirettamente a causa del comando `Process`.  
  
 Quando vengono specificate in un comando, le associazioni out-of-line eseguono l'override delle associazioni inline contenute nell'istruzione DDL persistente per gli oggetti specificati. Tali oggetti elaborati possono includere l'oggetto denominato direttamente nel comando `Process` o altri oggetti la cui elaborazione viene inizializzata automaticamente come parte dell'elaborazione.  
  
 Le associazioni out-of-line vengono specificate includendo l'oggetto raccolta `Bindings` facoltativo nel comando di elaborazione. La raccolta `Bindings` facoltativa contiene i seguenti elementi.  
  
|Proprietà|Cardinalità|Tipo|Descrizione|  
|--------------|-----------------|----------|-----------------|  
|`Binding`|0-n|`Binding`|Fornisce una raccolta di nuove associazioni.|  
|`DataSource`|0-1|`DataSource`|Sostituisce `DataSource` dal server da utilizzare.|  
|`DataSourceView`|0-1|`DataSourceView`|Sostituisce `DataSourceView` dal<br /><br /> server da utilizzare.|  
  
 Tutti gli elementi che fanno riferimento alle associazioni out-of-line sono facoltativi. Per qualsiasi elemento non specificato, ASSL utilizza la specifica contenuta nell'istruzione DDL dell'oggetto persistente. La specifica di `DataSource` o `DataSourceView` nel comando `Process` è facoltativa. Se `DataSource` o `DataSourceView` è specificato, la relativa istanza non viene creata. Gli oggetti non risultano inoltre persistenti una volta completato il comando `Process`.  
  
### <a name="definition-of-the-out-of-line-binding-type"></a>Definizione del tipo di associazione out-of-line  
 Nella raccolta `Bindings` out-of-line, ASSL supporta una raccolta di associazioni per più oggetti, una per ciascuna proprietà `Binding`. Ciascuna proprietà `Binding` ha un riferimento all'oggetto esteso, che è simile al riferimento all'oggetto, ma può riferirsi anche a oggetti minori, ad esempio attributi della dimensione e attributi del gruppo di misure. Questo oggetto assume il formato flat tipico del `Object` nell'elemento `Process` comandi, a meno che il \< *oggetto*>\<*/oggetto*> i tag non sono presenti.  
  
 Ogni oggetto per cui è specificata l'associazione è identificato da un elemento XML nel formato \< *oggetto*> ID (ad esempio, `DimensionID`). Dopo aver identificato l'oggetto in modo specifico con il modulo \< *oggetto*> ID, si identifica l'elemento per cui è stata specificata l'associazione, ovvero in genere `Source`. Una situazione comune da tenere in considerazione è quella in cui `Source` è una proprietà in `DataItem`, come nel caso delle associazioni di colonna in un attributo. In questo caso, non specificare il tag `DataItem`. Specificare solo la proprietà `Source`, come se si trovasse direttamente nella colonna da associare.  
  
 L'identificazione di `KeyColumns` viene effettuata in base all'ordinamento nella raccolta `KeyColumns`. Non è possibile ad esempio specificare solo la prima e la terza colonna chiave di un attributo, perché non è possibile indicare di ignorare la seconda colonna chiave. Tutte le colonne chiave devono essere presenti nell'associazione out-of-line per un attributo della dimensione.  
  
 Sebbene non dispongano di un ID, le `Translations` sono identificate a livello semantico in base alla lingua. È pertanto necessario che le `Translations` in `Binding` includano l'identificatore di lingua.  
  
 All'interno di `Binding` è consentito un elemento aggiuntivo che non esiste direttamente nell'istruzione DDL denominato `ParentColumnID`, il quale è utilizzato per le tabelle nidificate per il data mining. In questo caso, è necessario identificare la colonna padre nella tabella nidificata per la quale è fornita l'associazione.  
  
  
