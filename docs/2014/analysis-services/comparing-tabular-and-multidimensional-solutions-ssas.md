---
title: Confronto tra soluzioni tabulari e multidimensionali (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5cb21b733fd1663f0e26c765f519544597aa9063
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527427"
---
# <a name="comparing-tabular-and-multidimensional-solutions-ssas"></a>Confronto tra soluzioni tabulari e multidimensionali (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]in sono disponibili due approcci distinti per la modellazione dei dati: tabulari e multidimensionali. Benché sia presente una sovrapposizione significativa dei due approcci, ci sono anche differenze importanti quali la decisione su come procedere. In questo argomento vengono confrontate le funzionalità e viene illustrato il modo in cui ogni approccio risolve i requisiti di progetto comuni. Ad esempio, se il supporto di un'origine dati specifica è di importanza fondamentale, la sezione sulle origini dati consente di facilitare la decisione su quale approccio di modellazione adottare.  
  
 Questo argomento include le sezioni seguenti:  
  
-   [Panoramica di modellazione in Analysis Services](#bkmk_overview)  
  
-   [Supporto delle origini dati in base al tipo di soluzione](#bkmk_ds)  
  
-   [Funzionalità del modello](#bkmk_models)  
  
-   [Dimensioni del modello](#bkmk_modelsize)  
  
-   [Programmabilità ed esperienza dello sviluppatore](#bkmk_ext)  
  
-   [Supporto dei linguaggi di query e di scripting](#bkmk_lang)  
  
-   [Supporto della funzionalità della sicurezza](#bkmk_sec)  
  
-   [Strumenti di progettazione](#bkmk_designer)  
  
-   [Client e applicazioni di creazione report](#bkmk_client)  
  
-   [Piattaforme di hosting](#bkmk_sharePoint)  
  
-   [Modalità di distribuzione di server per soluzioni multidimensionali e tabulari](#bkmk_deploymentmode)  
  
-   [Passaggio successivo: Compilare una soluzione](#bkmk_Next)  
  
 Altre informazioni sono disponibili in questo articolo tecnico su MSDN: [Scegliere un'esperienza di modellazione tabulare o multidimensionale in SQL Server 2012 Analysis Services](https://go.microsoft.com/fwlink/?LinkId=251588).  
  
##  <a name="overview-of-modeling-in-analysis-services"></a><a name="bkmk_overview"></a>Panoramica della modellazione in Analysis Services  
 Analysis Services offre un'esperienza di sviluppo del modello, nonché la distribuzione di modelli tramite l'hosting di database in un'istanza di Analysis Services. Tra i tipi di modello sono inclusi tabulari e multidimensionali. Come prevedibile, l'hosting di database supporta le soluzioni tabulari e multidimensionali create dall'utente, ma l'hosting del database include anche PowerPivot per SharePoint.  
  
 PowerPivot per SharePoint è *Analysis Services in modalità SharePoint*, dove Analysis Services viene eseguito come servizio supplementare in SharePoint, contribuendo a ospitare e gestire modelli di dati di Excel creati in precedenza in Excel e quindi salvati in SharePoint. Il ruolo di Analysis Services in questo contesto consiste nel caricare il modello di dati in memoria, aggiornare i dati da origini dati esterne ed eseguire query sul modello. In questa configurazione, Analysis Services viene eseguito in background. Tutte le connessioni e le richieste ad Analysis Services vengono effettuate da SharePoint e solo quando una cartella di lavoro di Excel contiene un modello di dati (i modelli di dati sono facoltativi nelle cartelle di lavoro di Excel). Se si compila un modello di dati in Excel e lo si ospita in SharePoint, è allineato ai requisiti del progetto, vedere [Power Pivot: potente strumento di analisi e modellazione dei dati in Excel](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b) e [PowerPivot per SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md) per altre informazioni.  
  
> [!NOTE]  
>  I modelli di dati di Excel e i modelli tabulari sono strutturalmente simili. Se è necessario supportare maggiori quantità di dati o usare altre funzionalità di modello non disponibili in Excel, è possibile importare un modello di dati di Excel in un modello tabulare.  
  
 Le soluzioni tabulare e multidimensionale vengono compilate mediante [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] e devono essere utilizzate per progetti di Business Intelligence aziendali che vengono eseguiti in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] autonoma. Con entrambe le soluzioni è possibile generare database analitici a prestazioni elevate che si integrano facilmente con Excel, con i report di Reporting Services, con altre applicazioni di Business Intelligence di Microsoft e con applicazioni di terze parti. Entrambe le soluzioni producono database autonomi che possono essere usati da qualsiasi applicazione client che supporta Analysis Services.  
  
 In generale, le differenze tra modelli tabulari e multidimensionali possono essere descritte come segue:  
  
-   Le soluzioni multidimensionali e di data mining usano costrutti di modellazione OLAP (cubi e dimensioni) e l'archiviazione MOLAP, ROLAP o HOLAP che usa il disco come archivio dati primario per i dati preaggregati.  
  
-   Con le soluzioni tabulari è possibile utilizzare costrutti di modellazione relazionali, quali tabelle e relazioni, per modellare i dati e il motore di analisi in memoria, per archiviare e calcolare i dati. La maggior parte dei modelli, se non tutti, viene archiviata nella RAM ed è spesso molto più veloce rispetto alla controparte multidimensionale.  
  
 In caso di nuovi progetti, si consideri prima l'approccio tabulare, con cui sarà possibile progettare, testare e distribuire più velocemente. Inoltre, consente prestazioni migliori con le applicazioni di Business Intelligence in modalità self-service più recenti di Microsoft.  
  
##  <a name="data-source-support-by-solution-type"></a><a name="bkmk_ds"></a>Supporto dell'origine dati in base al tipo di soluzione  
 I modelli multidimensionali e tabulari usano dati importati da origini esterne. La maggior parte degli sviluppatori usa un data warehouse, progettato per supportare strutture di dati del report, come l'origine dati primaria alla base di un modello. Il data warehouse è spesso basato su uno schema star o snowflake e SSIS viene usato per caricare dati da soluzioni OLTP nel data warehouse. La modellazione è più semplice quando si usa un data warehouse come origine dati back-end.  
  
|**Collegamento**|**Riepilogo delle opzioni supportate**|  
|--------------|--------------------------------------|  
|[Origini dati supportate &#40;SSAS multidimensionale&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)|I modelli multidimensionali usano dati da origini dati relazionali.|  
|[Origini dati supportate &#40;SSAS tabulare&#41;](tabular-models/data-sources-supported-ssas-tabular.md)|I modelli tabulari supportano una più ampia gamma di origini dati, inclusi file flat, feed di dati e origini dati che sono accessibili tramite provider di dati ODBC.|  
  
 Entrambi gli approcci di modellazione possono usare dati da più origini dati nello stesso modello.  
  
 Se la soluzione richiede l'archiviazione dei dati del modello all'esterno del modello nel database relazionale (una tecnica usata quando i requisiti di dimensione dati sono particolarmente grandi), il tipo di origine dati deve essere un database relazionale di SQL Server. Sia l'archiviazione ROLAP per i modelli multidimensionali sia DirectQuery per i modelli tabulari presentano questo requisito.  
  
 **Dimensioni dei dati**  
  
 Sia nelle soluzioni tabulari sia in quelle multidimensionali viene utilizzata la compressione dati che consente di ridurre le dimensioni del database di Analysis Services correlate al data warehouse da cui si importano i dati. Poiché la compressione effettiva varierà in base alle caratteristiche dei dati sottostanti, non vi è alcun modo per sapere con precisione la quantità di spazio su disco e di memoria che sarà richiesta da una soluzione una volta che i dati vengono elaborati e utilizzati nelle query. Molti sviluppatori di Analysis Services stimano che le dimensioni dell'archiviazione primaria di un database multidimensionale saranno pari a circa un terzo rispetto a quelle dei dati iniziali.  
  
 I database tabulari possono talvolta richiedere quantità di compressione maggiori, circa un decimo delle dimensioni, specialmente se la maggior parte dei dati viene importata dalle tabelle dei fatti. In caso di soluzione tabulare, i requisiti di memoria saranno maggiori delle dimensioni dei dati su disco, a causa di strutture dei dati aggiuntive create quando il database tabulare viene caricato in memoria. In fase di caricamento, è possibile prevedere un aumento sia per i requisiti del disco sia per quelli della memoria di entrambi i tipi di soluzione quando tramite Analysis Services vengono memorizzati nella cache, archiviati, analizzati e sottoposti a query i dati.  
  
 Per alcuni progetti, i requisiti dei dati potrebbero essere così importanti da diventare un fattore determinante nella scelta tra i tipi di modello. Se i dati da caricare sono costituiti da molti terabyte, una soluzione tabulare potrebbe non soddisfare i requisiti qualora la memoria disponibile non possa contenere i dati. È disponibile un'opzione di paging con cui è possibile eseguire lo swapping dei dati in memoria sul disco, ma quantità molto grandi di dati vengono gestite meglio nelle soluzioni multidimensionali. I database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] più grandi in produzione oggi sono multidimensionali. Per ulteriori informazioni sulle opzioni di paging della memoria per le soluzioni tabulari, vedere [Memory Properties](server-properties/memory-properties.md). Per ulteriori informazioni sulla scalabilità di una soluzione multidimensionale, vedere la pagina relativa alla [scalabilità orizzontale di query per Analysis Services con database di sola lettura](https://go.microsoft.com/fwlink/?LinkId=251711).  
  
##  <a name="model-features"></a><a name="bkmk_models"></a>Funzionalità del modello  
 Nella tabella seguente viene riepilogata la disponibilità delle funzionalità al livello del modello. Se si è già installato Analysis Services, è possibile utilizzare queste informazioni per capire le funzionalità della modalità server installata. Se si ha familiarità con le funzionalità del modello in Analysis Services e i requisiti aziendali includono una o più di tali funzionalità, è possibile esaminare questo elenco per assicurarsi che la funzionalità desiderata sia disponibile nel tipo di modello che si intende compilare.  
  
 Per ulteriori informazioni sulla modalità di confronto delle funzionalità in base all'approccio di modellazione, vedere l'articolo tecnico relativo alla [scelta di un modello tabulare o multidimensionale in SQL Server 2012 Analysis Services](https://go.microsoft.com/fwlink/?LinkId=251588) su MSDN.  
  
> [!NOTE]  
>  La modellazione tabulare è supportata in edizioni specifiche di SQL Server. Per ulteriori informazioni, vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
||||  
|-|-|-|  
||**Multidimensionale**|**Tabulare**|  
|Azioni|[Sì](multidimensional-models/actions-in-multidimensional-models.md)|No|  
|Oggetti Aggregation|[Sì](multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)|No|  
|Misure calcolate|[Sì](multidimensional-models/create-calculated-members.md)|Sì|  
|Assembly personalizzati|[Sì](multidimensional-models/multidimensional-model-assemblies-management.md)|No|  
|Rollup personalizzati|Sì|No|  
|Distinct Count|[Sì](multidimensional-models/use-aggregate-functions.md)|Sì (tramite DAX) *|  
|Drill-through|[Sì](multidimensional-models/actions-in-multidimensional-models.md)|Sì|  
|Gerarchie|[Sì](multidimensional-models/user-defined-hierarchies-create.md)|Sì|  
|KPI|[Sì](multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|Sì|  
|Gruppi di misure collegati|[Sì](multidimensional-models/linked-measure-groups.md)|No|  
|Relazioni molti-a-molti|[Sì](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)|No|  
|Gerarchie padre-figlio|[Sì](multidimensional-models/parent-child-dimension.md)|Sì (tramite DAX)|  
|Partizioni|[Sì](tabular-models/partitions-ssas-tabular.md)|  
|Prospettive|[Sì](multidimensional-models/perspectives-in-multidimensional-models.md)|[Sì](tabular-models/partitions-ssas-tabular.md)|  
|Misure semiadditive|[Sì](multidimensional-models/define-semiadditive-behavior.md)|Sì (tramite DAX)|  
|Traduzioni|[Sì](multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|No|  
|Gerarchie definite dall'utente|[Sì](multidimensional-models/user-defined-hierarchies-create.md)|Sì|  
|Writeback|[Sì](multidimensional-models/set-partition-writeback.md)|No|  
  
 * Se la soluzione deve supportare un numero molto elevato di conteggi distinti, ad esempio molti milioni di ID cliente, considerare prima tabulare. che risulta più efficiente in questo scenario. Vedere la sezione sui conteggi distinti nel white paper, [Case Study di Analysis Services: Uso di modelli tabulari in soluzioni commerciali su larga scala](https://msdn.microsoft.com/library/dn751533.aspx).  
  
##  <a name="model-size"></a><a name="bkmk_modelsize"></a>Dimensioni del modello  
 Le dimensioni del modello, in termini di numero totale di oggetti, non variano in base al tipo di soluzione. Tuttavia, gli strumenti di progettazione usati per compilare ciascuna soluzione variano in base alla capacità di supportare un gran numero di oggetti. La compilazione di un modello più grande è più semplice in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] perché fornisce più funzionalità per creare diagrammi ed elencare oggetti in base al tipo in Esplora oggetti ed Esplora soluzioni.  
  
 I modelli molto grandi, costituiti da molte centinaia di tabelle o dimensioni, sono spesso compilati a livello di codice in Visual Studio e non negli strumenti di progettazione. Per ulteriori informazioni sul numero massimo di oggetti in un modello, vedere la pagina relativa alle [specifiche di capacità massima &#40;Analysis Services&#41;](multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md).  
  
##  <a name="programmability-and-developer-experience"></a><a name="bkmk_ext"></a>Programmabilità e esperienza dello sviluppatore  
 Per i modelli tabulari e multidimensionali, è disponibile un modello a oggetti condiviso per entrambe le modalità. AMO e ADOMD.NET supportano entrambe le modalità. Nessuna delle librerie client è stata rivista relativamente ai costrutti tabulari, pertanto sarà necessario capire la modalità di correlazione tra i costrutti multidimensionali e tabulari e le convenzioni di denominazione. Esaminare innanzitutto l'esempio di programmazione da AMO a tabulare per comprendere la programmazione AMO rispetto a un modello tabulare. Per ulteriori informazioni, scaricare l'esempio dal [sito Web codeplex](https://go.microsoft.com/fwlink/?LinkID=221036).  
  
 Le soluzioni tabulari supportano solo un file model.bim per soluzione, pertanto tutto il lavoro deve essere eseguito in un singolo file. I team di sviluppo abituati all'utilizzo di più progetti in una sola soluzione potrebbero dover rivedere la modalità con cui operano quando si compila una soluzione tabulare condivisa.  
  
##  <a name="query-and-scripting-language-support"></a><a name="bkmk_lang"></a>Supporto del linguaggio di query e di scripting  
 Analysis Services include MDX, DMX, DAX XML/A e ASSL. Il supporto di tali linguaggi varia leggermente in base al tipo di modello. Se i requisiti di linguaggi di query e di scripting sono una considerazione importante, esaminare l'elenco seguente.  
  
-   I database modello tabulare supportano calcoli DAX, query DAX e query MDX.  
  
-   I database modello multidimensionale supportano calcoli MDX e query MDX, nonché ASSL.  
  
-   I modelli di data mining supportano DMX e ASSL.  
  
-   Analysis Services PowerShell è supportato per l'amministrazione di server e database. Il tipo di modello (o la modalità server) non è un fattore in uso dei cmdlet di PowerShell.  
  
 Tutti i database supportano XML/A.  
  
##  <a name="security-feature-support"></a><a name="bkmk_sec"></a>Supporto delle funzionalità di sicurezza  
 Tutte le soluzioni di Analysis Services possono essere protette a livello di database. Opzioni di sicurezza più granulari variano in base alla modalità. Se le impostazioni di sicurezza granulari sono un requisito per la soluzione, esaminare l'elenco seguente per verificare che il livello di sicurezza desiderato sia supportato nel tipo di soluzione da compilare:  
  
-   I database modello tabulare possono utilizzare la sicurezza a livello di riga, mediante le autorizzazioni basate sul ruolo in Analysis Services.  
  
-   I database modello multidimensionale possono utilizzare la sicurezza a livello di cella e di dimensione, mediante le autorizzazioni basate sui ruoli in Analysis Services.  
  
 È possibile ripristinare i modelli di dati di Excel in un server in modalità tabulare. Una volta ripristinato, il file viene separato da SharePoint (supponendo che sia stato ripristinato da un percorso di SharePoint) consentendo di usare quasi tutte le funzionalità della modellazione tabulare, inclusa la sicurezza a livello di riga. L'unica funzionalità di modellazione tabulare che non è possibile utilizzare in una cartella di lavoro ripristinata riguarda le tabelle collegate.  
  
##  <a name="design-tools"></a><a name="bkmk_designer"></a>Strumenti di progettazione  
 Le competenze di modellazione dei dati e l'esperienza tecnica possono variare molto tra gli utenti che si occupano della compilazione di modelli analitici. Se in una soluzione la familiarità di uno strumento o l'esperienza degli utenti è una considerazione importante, confrontare le esperienze seguenti per la creazione del modello.  
  
|**Strumento di modellazione**|**Modalità di utilizzo**|  
|-----------------------|------------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Utilizzare per creare soluzioni tabulari, multidimensionali e di data mining. In questo ambiente di creazione viene utilizzata la shell di Visual Studio per fornire aree di lavoro, riquadri delle proprietà e navigazione degli oggetti. Gli utenti tecnici che già utilizzano Visual Studio preferiranno probabilmente questo strumento per la compilazione di applicazioni di Business Intelligence. Per informazioni dettagliate, vedere [Tools and applications used in Analysis Services](tools-and-applications-used-in-analysis-services.md) .|  
|Excel 2013 e versioni successive con il componente aggiuntivo Power Pivot per Excel|PowerPivot per Excel è uno strumento usato per modificare e migliorare un modello di dati di Excel. È un'area di lavoro di applicazione separata visualizzata sopra Excel, ma che usa le stesse metafore visive (pagine a schede, layout di griglia e barra della formula) di Excel. Gli utenti con esperienza nell'utilizzo di Excel in genere preferiscono questo strumento rispetto a [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Vedere [Power Pivot: potente strumento di analisi e creazione di modelli di dati in Excel](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b).|  
  
##  <a name="client-and-reporting-applications"></a><a name="bkmk_client"></a>Applicazioni client e di Reporting  
 Nelle versioni precedenti, la scelta del tipo di modello aveva un impatto sulle applicazioni client che era possibile utilizzare, ma tale distinzione è diminuita nel tempo. I modelli tabulare e multidimensionale offrono per lo più un supporto equivalente per quanto riguarda le applicazioni client connesse ai dati di Analysis Services. Nella tabella seguente è riportato un elenco di applicazioni client Microsoft che possono essere usate con i modelli di dati di Analysis Services.  
  
|**Applicazione**|**Descrizione**|  
|---------------------|---------------------|  
|Rapporti PivotTable di Excel|La funzionalità di Excel è la stessa per i modelli tabulari e multidimensionali, sebbene Writeback (una funzionalità di Analysis Services implementata da Excel) è supportato solo per i modelli multidimensionali.|  
|Report RDL di Reporting Services|I report RDL, creati in Generatore Report o Progettazione report, possono usare qualsiasi modello di Analysis Services, nonché modelli di dati di Excel ospitati in PowerPivot per SharePoint.|  
|Dashboard di PerformancePoint|In SharePoint, i dashboard di PerformancePoint possono connettersi a tutti i database di Analysis Services, inclusi i modelli di dati di Excel. Per ulteriori informazioni, vedere la pagina relativa alla [creazione di connessioni dati (PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkdID=218155).|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]in Office 365 o Power BI siti|Solo modelli tabulari.|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] in SharePoint locale|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], come applicazione ClickOnce da SharePoint, possono usare un cubo di Analysis Services o un modello tabulare.|  
  
##  <a name="server-deployment-modes-for-multidimensional-and-tabular-solutions"></a><a name="bkmk_deploymentmode"></a>Modalità di distribuzione server per soluzioni multidimensionali e tabulari  
 Un'istanza di Analysis Services viene installata in una delle tre modalità che impostano il contesto operativo del server. La modalità server installata determinerà il tipo di soluzioni che è possibile distribuire in tale server. Archiviazione e architettura della memoria sono le differenze principali tra le modalità, ma ne esistono altre. Le tre modalità server disponibili sono descritte brevemente nella tabella riportata di seguito. Per altre informazioni, vedere [Determinare la modalità server di un'istanza di Analysis Services](instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
|Modalità di distribuzione|Descrizione|  
|---------------------|-----------------|  
|0 - Multidimensionale e data mining|Vengono eseguite soluzioni multidimensionali e di data mining che vengono distribuite in un'istanza predefinita di Analysis Services. La modalità di distribuzione 0 è l'impostazione predefinita per un'installazione di Analysis Services. Per ulteriori informazioni, vedere [Install Analysis Services in Multidimensional and Data Mining Mode](../../2014/sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md).|  
|1 - PowerPivot per SharePoint|Per l'accesso del modello di dati di Excel, Analysis Services è un componente interno di SharePoint. Analysis Services viene installato in modalità di distribuzione 1 e accetta le richieste solo da Excel Services in un ambiente SharePoint. Per ulteriori informazioni, vedere [PowerPivot for SharePoint 2010 Installation](../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md).|  
|2 - Tabulare|Vengono eseguite soluzioni tabulari in un'istanza autonoma di Analysis Services configurata per la modalità di distribuzione 2. Per ulteriori informazioni, vedere [Install Analysis Services in Tabular Mode](instances/install-windows/install-analysis-services.md).|  
  
 Si noti che i modelli di server non sono intercambiabili. Al momento dell'installazione, si sceglierà una modalità di funzionamento del server. È necessario installare più istanze, una per ogni modalità server, per supportare tutti i carichi di lavoro.  
  
##  <a name="hosting-platforms"></a><a name="bkmk_sharePoint"></a>Piattaforme di hosting  
 Microsoft offre diversi metodi per l'hosting di dati, applicazioni, rapporti e collaborazione. In questa sezione viene illustrata l'interoperabilità di Analysis Services per quanto riguarda ciascuna piattaforma di hosting.  
  
|**Platform**|**Descrizione**|  
|------------------|---------------------|  
|Microsoft Azure|È possibile eseguire qualsiasi versione ed edizione supportata di Analysis Services in una macchina virtuale di Azure. A differenza del Database SQL di Azure, che è un servizio in Azure che offre la stessa funzionalità di un motore di database relazionale locale, non esiste alcun equivalente di Analysis Services in Azure. L'installazione, la configurazione e l'esecuzione di Analysis Services in una macchina virtuale di Azure è l'unica opzione basata su Azure.|  
|Office 365|Excel Online in Office 365 supporta le connessioni remote a modelli tabulari e multidimensionali eseguiti in locale.|  
|Siti di Power BI in Office 365|In un sito di Power BI, i report Power View possono connettersi a modelli di dati tabulari in esecuzione in locale.|  
|Server locali (istanze di SQL Server e SharePoint)|Un server di database locale (ossia, un'istanza di SQL Server con Analysis Services installato) è ancora il mezzo principale per rendere disponibili i dati di Analysis Services per report e le applicazioni client. Le soluzioni tabulari, multidimensionali e di data mining vengono eseguite in istanze di Analysis Services su una rete, senza la dipendenza da SharePoint.<br /><br /> SQL Server si integra con SharePoint aggiungendo supporto per l'accesso ai dati PowerPivot e a quelli tabulari. L'investimento in termini di integrazione di SharePoint e SQL Server cresce all'aumentare del numero di funzionalità utilizzate da ciascun prodotto. Se si dispone di SharePoint, è possibile installare SQL Server PowerPivot per SharePoint per abilitare l'accesso ai dati PowerPivot e ottenere i file di connessione con estensione bism di PowerPivot utilizzati per accedere a database tabulari in esecuzione in un'istanza di Analysis Services esterna su un server di rete.<br /><br /> Se si dispone di SQL Server e SharePoint, è possibile supportare la seguente combinazione di servizi e applicazioni:<br /><br /> Modelli di Analysis Services (tabulari o multidimensionali)<br /><br /> Servizi di SharePoint di livello intermedio (ad esempio Excel Services, Reporting Services in SharePoint o servizi PerformancePoint)<br /><br /> Client del browser o rich client (Excel) per l'esplorazione e l'analisi più approfondita dei dati.|  
  
##  <a name="next-step-build-a-solution"></a><a name="bkmk_Next"></a>Passaggio successivo: compilare una soluzione  
 Dopo aver compreso come confrontare le soluzioni, provare le esercitazioni seguenti per apprendere i passaggi relativi alla creazione di ciascuna soluzione. Nei collegamenti seguenti sono disponibili le esercitazioni in cui vengono illustrati i passaggi.  
  
-   Compilare un modello tabulare usando [Modellazione tabulare &#40;esercitazione di AdventureWorks&#41;](tabular-modeling-adventure-works-tutorial.md).  
  
-   Compilare un modello tabulare usando [Modellazione multidimensionale &#40;esercitazione di AdventureWorks&#41;](multidimensional-modeling-adventure-works-tutorial.md).  
  
-   Compilazione di un modello di data mining utilizzando [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
-   Compilazione di un modello PowerPivot mediante l' [esercitazione su PowerPivot per Excel](https://go.microsoft.com/fwlink/?LinkId=251135).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione dell'istanza di Analysis Services](instances/analysis-services-instance-management.md)   
 [Novità di Analysis Services e Business Intelligence](what-s-new-in-analysis-services.md)   
 [Novità &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)   
 [Novità di PowerPivot](https://go.microsoft.com/fwlink/?LinkId=238141)   
 [Guida di PowerPivot per SQL Server 2012](https://go.microsoft.com/fwlink/?LinkID=220946)   
 [Connessione BI Semantic Model di PowerPivot &#40;. BISM&#41;](power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
  
