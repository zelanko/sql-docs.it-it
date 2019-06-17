---
title: Panoramica dell'architettura logica (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], examples
- cubes [Analysis Services], about cubes
ms.assetid: 1a547bce-dacf-4d32-bc0f-3829f4b026e1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27095834c7f3b863bbc1a4f330898790cf467ec6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62699197"
---
# <a name="logical-architecture-overview-analysis-services---multidimensional-data"></a>Panoramica dell'architettura logica (Analysis Services - Dati multidimensionali)
  Analysis Services viene eseguito in una modalità di distribuzione server che determina l'architettura di memoria e l'ambiente di runtime utilizzati dai diversi tipi di modelli di Analysis Services. La modalità server viene determinata durante l'installazione. **Modalità multidimensionale e Data Mining** supporta OLAP tradizionali e il data mining. **Modalità tabulare** supporta modelli tabulari. **La modalità integrata SharePoint** fa riferimento a un'istanza di Analysis Services installata come PowerPivot per SharePoint, utilizzato per il caricamento ed eseguire query sui modelli di dati di Excel o PowerPivot all'interno di una cartella di lavoro.  
  
 In questo argomento viene illustrata l'architettura di base di Analysis Services quando viene utilizzato nella modalità multidimensionale e di data mining. Per altre informazioni sulle altre modalità, vedere [modellazione tabulare &#40;modello tabulare di SSAS&#41; ](../../tabular-models/tabular-models-ssas.md) e [confronto tabulari e multidimensionali &#40;SSAS&#41;](../../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md).  
  
## <a name="basic-architecture"></a>Architettura di base  
 Un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] può contenere più database e un database può includere contemporaneamente oggetti OLAP e oggetti di data mining. Le applicazioni si connettono a un'istanza specifica di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e a un database specifico. Un computer server può ospitare più istanze di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Le istanze di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] indicato come "\<nomeserver >\\< NomeIstanza\>". La figura seguente mostra tutte le relazioni indicate tra [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oggetti.  
  
 ![Relazioni tra oggetti AMO in esecuzione](../../../analysis-services/dev-guide/media/amo-runningobjects.gif "relazioni tra oggetti AMO in esecuzione")  
  
 Le classi di base rappresentano il set di oggetti minimo richiesto per la compilazione di un cubo. Tale set di oggetti minimo è costituito da una dimensione, un gruppo di misure e una partizione. L'utilizzo di un'aggregazione è facoltativo.  
  
 Le dimensioni vengono compilate da attributi e gerarchie. Queste ultime sono formate da un set ordinato di attributi, dove ogni attributo del set corrisponde a un livello nella gerarchia.  
  
 I cubi sono compilati da dimensioni e gruppi di misure. Le dimensioni nella raccolta di dimensioni di un cubo appartengono alla raccolta di dimensioni del database. I gruppi di misure sono raccolte di misure che hanno la stessa vista origine dati e lo stesso subset di dimensioni del cubo. Un gruppo di misure dispone di una o più partizioni per la gestione dei dati fisici. Un gruppo di misure può avere una progettazione delle aggregazioni predefinita, la quale può essere utilizzata da tutte le partizioni nel gruppo di misure. Ogni partizione può inoltre disporre di una progettazione delle aggregazioni specifica.  
  
 Oggetti Server  
 Ciascuna istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] è considerata un oggetto server diverso in AMO. Ogni istanza è connessa a un oggetto <xref:Microsoft.AnalysisServices.Server> mediante una connessione diversa. In ogni oggetto server sono contenuti una o più origini dati, viste origine dati e oggetti di database, nonché assembly e ruoli di sicurezza.  
  
 Oggetti Dimension  
 Ogni oggetto di database contiene più oggetti dimensione, ciascuno dei quali contiene uno o più attributi organizzati in gerarchie.  
  
 Oggetti cubo  
 Ogni oggetto di database contiene uno o più oggetti cubo. Un cubo è definito dalle relative misure e dimensioni. Le misure e le dimensioni di un cubo derivano dalle tabelle e dalle viste della vista origine dati su cui il cubo si basa o che viene generata dalle definizioni delle misure e delle dimensioni.  
  
## <a name="object-inheritance"></a>Ereditarietà degli oggetti  
 Il modello a oggetti ASSL contiene molti gruppi di elementi ripetuti. Ad esempio, il gruppo di elementi "`Dimensions` contengono `Hierarchies`," definisce la gerarchia di dimensione di un elemento. `Cubes` e `MeasureGroups` contengono entrambi il gruppo di elementi "`Dimensions` contain `Hierarchies`".  
  
 Se non viene sottoposto a override in modo esplicito, un elemento eredita i dettagli di tali gruppi di elementi ripetuti dal livello più elevato. `Translations` per `CubeDimension` corrisponde ad esempio a `Translations` del relativo elemento predecessore `Cube`.  
  
 Per eseguire in modo esplicito l'override delle proprietà ereditate da un oggetto di livello superiore, non è necessario che un oggetto ripeta in modo esplicito l'intera struttura e le proprietà dell'oggetto di livello superiore. Un oggetto deve dichiarare in modo esplicito solo le proprietà di cui desidera eseguire l'override. Un oggetto `CubeDimension` può ad esempio elencare solo le proprietà `Hierarchies` da disabilitare in `Cube`, per le quali è necessario modificare la visibilità o per le quali non sono stati specificati alcuni dettagli di `Level` a livello di `Dimension`.  
  
 Alcune proprietà specificate per un oggetto forniscono i valori predefiniti per la stessa proprietà in un oggetto figlio o discendente. `Cube.StorageMode` fornisce ad esempio il valore predefinito per `Partition.StorageMode`. Per i valori predefiniti ereditati, in ASSL vengono applicate le regole per i valori predefiniti ereditati:  
  
-   Quando la proprietà per l'oggetto figlio è Null in XML, il valore ereditato viene utilizzato per impostazione predefinita. Se tuttavia si esegue una query relativa al valore nel server, viene restituito il valore Null dell'elemento XML.  
  
-   Non è possibile determinare a livello di programmazione se la proprietà di un oggetto figlio è stata impostata direttamente su tale oggetto oppure se è stata ereditata.  
  
## <a name="example"></a>Esempio  
 Il cubo Imports contiene due misure, Packages e Last, e tre dimensioni correlate, Route, Source e Time.  
  
 ![Esempio 1 di cubo](../../../analysis-services/dev-guide/media/cubeintro1.gif "cubo di esempio 1")  
  
 I valori alfanumerici più piccoli disposti intorno al cubo rappresentano i membri delle dimensioni. Ad esempio, ground, Africa e 1st quarter sono rispettivamente membri delle dimensioni Route, Source e Time.  
  
### <a name="measures"></a>Misure  
 I valori all'interno delle celle del cubo rappresentano le due misure Packages e Last. La misura Packages rappresenta il numero di confezioni importate. Per aggregare i fatti viene utilizzata la funzione `Sum`. La misura Last rappresenta la data di ricevimento. Per aggregare i fatti viene utilizzata la funzione `Max`.  
  
### <a name="dimensions"></a>Dimensioni  
 La dimensione Route rappresenta il mezzo di trasporto mediante il quale i beni importati giungono a destinazione. I membri di questa dimensione includono ground, nonground, air, sea, road e rail. La dimensione Source rappresenta le località in cui vengono prodotti i beni importati, ad esempio Africa o Asia. La dimensione Time rappresenta i trimestri e i semestri di un singolo anno.  
  
### <a name="aggregates"></a>Aggregazioni  
 Gli utenti aziendali di un cubo possono determinare il valore di qualsiasi misura per ogni membro di ogni dimensione, indipendentemente dal livello del membro all'interno della dimensione, perché in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] i valori vengono aggregati ai livelli superiori in base alle esigenze. I valori delle misure nella figura precedente, ad esempio, possono essere aggregati in base a una gerarchia con il calendario standard utilizzando la gerarchia Calendar Time della dimensione temporale, come illustrato nel diagramma seguente.  
  
 ![Diagramma delle misure organizzate lungo la dimensione temporale](../../../analysis-services/dev-guide/media/cubeintro2.gif "diagramma delle misure organizzate lungo la dimensione temporale")  
  
 Oltre che in base a un'unica dimensione, le misure possono essere aggregate utilizzando combinazioni di membri di dimensioni diverse. Ciò consente agli utenti aziendali di valutare le misure di più dimensioni contemporaneamente. Se, ad esempio, un utente aziendale desidera analizzare ogni trimestre le importazioni giunte per via aerea dagli emisferi orientale e occidentale, potrà eseguire una query sul cubo per recuperare il set di dati seguente.  
  
||||Pacchetti|||Ultimo|||  
|-|-|-|--------------|-|-|----------|-|-|  
||||All Sources|Eastern Hemisphere|Western Hemisphere|All Sources|Eastern Hemisphere|Western Hemisphere|  
|All Time|||25110|6547|18563|DEC-29-99|Dec-22-99|DEC-29-99|  
||1st half||11173|2977|8196|Jun-28-99|Jun-20-99|Jun-28-99|  
|||1st quarter|5108|1452|3656|Mar-30-99|Mar-19-99|Mar-30-99|  
|||2nd quarter|6065|1525|4540|Jun-28-99|Jun-20-99|Jun-28-99|  
||2nd half||13937|3570|10367|DEC-29-99|Dec-22-99|DEC-29-99|  
|||3rd quarter|6119|1444|4675|Sep-30-99|Sep-18-99|Sep-30-99|  
|||4th quarter|7818|2126|5692|DEC-29-99|Dec-22-99|DEC-29-99|  
  
 Dopo avere definito un cubo, è possibile creare nuove aggregazioni o modificare quelle esistenti in modo da impostare le opzioni per determinare, ad esempio, se le aggregazioni devono essere precalcolate durante la fase di elaborazione o calcolate durante l'esecuzione della query. **Argomento correlato:** [aggregazioni e progettazione di aggregazioni](../../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
### <a name="mapping-measures-attributes-and-hierarchies"></a>Mapping di misure, attributi e gerarchie  
 Le misure, gli attributi e le gerarchie del cubo di esempio derivano dalle colonne seguenti nelle tabelle dei fatti e delle dimensioni del cubo.  
  
|Misura o attributo (livello)|Membri|Tabella di origine|Colonna di origine|Valore della colonna di esempio|  
|------------------------------------|-------------|------------------|-------------------|-------------------------|  
|Misura Packages|Non applicabile|ImportsFactTable|Pacchetti|12|  
|Misura Last|Non applicabile|ImportsFactTable|Ultimo|May-03-99|  
|Livello Route Category nella dimensione Route|nonground,ground|RouteDimensionTable|Route_Category|Nonground|  
|Attributo Route nella dimensione Route|air,sea,road,rail|RouteDimensionTable|Route|Sea|  
|Attributo Hemisphere nella dimensione Source|Eastern Hemisphere,Western Hemisphere|SourceDimensionTable|Hemisphere|Eastern Hemisphere|  
|Attributo Continent nella dimensione Source|Africa,Asia,AustraliaEurope,N. America,S. America|SourceDimensionTable|Continent|Europe|  
|Attributo Half nella dimensione Time|1st half,2nd half|TimeDimensionTable|Half|2nd half|  
|Attributo Quarter nella dimensione Time|1st quarter,2nd quarter,3rd quarter,4th quarter|TimeDimensionTable|Quarter|3rd quarter|  
  
 I dati di una singola cella del cubo in genere derivano da più righe della tabella dei fatti. Ad esempio, la cella del cubo nel punto di intersezione tra il membro air, il membro Africa e il membro 1st quarter contiene un valore che deriva dall'aggregazione le seguenti righe di **ImportsFactTable** tabella dei fatti.  
  
|||||||  
|-|-|-|-|-|-|  
|Import_ReceiptKey|RouteKey|SourceKey|TimeKey|Pacchetti|Ultimo|  
|3516987|1|6|1|15|Gennaio-10-99|  
|3554790|1|6|1|40|Gennaio-19-99|  
|3572673|1|6|1|34|Jan-27-99|  
|3600974|1|6|1|45|Feb-02-99|  
|3645541|1|6|1|20|Feb-09-99|  
|3674906|1|6|1|36|Feb-17-99|  
  
 Nella tabella precedente, ogni riga dispone degli stessi valori per il **RouteKey**, **SourceKey**, e **TimeKey** colonne, che indica che queste righe contribuiscono alla cella del cubo stesso.  
  
 Nell'esempio illustrato di seguito viene rappresentato un cubo molto semplice, in quanto contiene un solo gruppo di misure, e tutte le tabelle delle dimensioni vengono unite in join alla tabella dei fatti in uno schema star. Un altro schema comune è quello snowflake, in cui una o più tabelle delle dimensioni sono unite in join a un'altra tabella delle dimensioni, anziché direttamente alla tabella dei fatti. **Argomento correlato:** [dimensioni &#40;Analysis Services - dati multidimensionali&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 Nell'esempio illustrato di seguito viene utilizzata una sola tabella dei fatti. Quando un cubo utilizza più tabelle dei fatti, le misure di ogni tabella dei fatti vengono organizzate in gruppi di misure, ognuno dei quali è correlato a un set di dimensioni specifico mediante le relazioni tra dimensioni definite. Queste relazioni vengono definite specificando le tabelle della vista origine dati coinvolte e il livello di granularità della relazione. **Argomento correlato:** [relazioni tra dimensioni](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Database modelli multidimensionali &#40;SSAS&#41;](../multidimensional-model-databases-ssas.md)  
  
  
