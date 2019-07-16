---
title: Confronto dei modelli tabulari e multidimensionali di Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c1ca9d710ca0e87e69bcc237848c02b758c724cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210250"
---
# <a name="comparing-tabular-and-multidimensional-solutions"></a>Confronto tra soluzioni tabulari e multidimensionali
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  SQL Server Analysis Services fornisce diversi approcci per la creazione di un modello business intelligence Semantic Model: Tabulare, multidimensionale e PowerPivot per SharePoint.
  
 La disponibilità di più approcci consente esperienze di modellazione commisurate ai diversi requisiti di aziende e utenti. L'approccio multidimensionale è una tecnologia avanzata basata su standard aperti, adottato da numerosi fornitori di software di Business Intelligence, ma può essere difficile da gestire. L'approccio tabulare offre una modellazione relazionale che molti sviluppatori trovano più intuitiva. PowerPivot è ancora più semplice, poiché offre una modellazione dei dati visiva in Excel, con supporto server tramite SharePoint.  
  
 Tutti i modelli vengono distribuiti come database eseguiti in un'istanza di Analysis Services, a cui è possibile accedere con gli strumenti client usando un singolo set di provider di dati e possono essere visualizzati in report interattivi e statici tramite Excel, Reporting Services, Power BI e strumenti di Business Intelligence di altri fornitori.  
  
 Soluzioni tabulari e multidimensionali vengono create usando SSDT e devono essere usate per progetti di Business Intelligence aziendali che vengono eseguiti in un computer autonomo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dell'istanza in locale e per i modelli tabulari, un [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) server di cloud. Entrambe le soluzioni garantiscono database analitici a prestazioni elevate che si integrano facilmente con i client di Business Intelligence. Ogni soluzione tuttavia viene creata, utilizzata e distribuita in modo diverso. In questo argomento si mettono a confronto questi due tipi di modellazioni in modo da identificare l'approccio giusto per l'utente.  
  
 Per i nuovi progetti, è consigliabile in genere i modelli tabulari. I modelli tabulari sono più veloci per progettare, testare e distribuire; e verrà funzionano meglio con le applicazioni di Business Intelligence self-service più recenti e i servizi di Microsoft cloud.  
  
##  <a name="bkmk_overview"></a> Panoramica dei tipi di modellazione  
 Se non si ha familiarità con Analysis Services La tabella seguente elenca i diversi modelli, riepiloga l'approccio e identifica il veicolo della versione iniziale.  
 
 > [!NOTE]  
>  **Azure Analysis Services** supporta modelli tabulari a livello di compatibilità 1200 e versioni successive. Tuttavia, non tutte le funzionalità di modellazione tabulare descritte in questo argomento sono supportata in Azure Analysis Services. Durante la creazione e distribuzione di modelli tabulari in Azure Analysis Services è molto simile a quello in locale, è importante comprendere le differenze. Per altre informazioni, vedere [che cos'è Azure Analysis Services?](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)
  
||||  
|-|-|-|  
|**Tipo**|**Descrizione della modellazione**|**Rilasciato**|  
|Tabella|Costrutti di modellazione relazionale (modello, tabelle, colonne). Internamente, i metadati vengono ereditati dai costrutti di modellazione OLAP (cubi, dimensioni, misure). Codice e script usano i metadati OLAP.|SQL Server 2012 e versione successiva (livelli di compatibilità 1050 - 1103) <sup>1</sup>|  
|Tabulare in SQL Server 2016|Costrutti (modello, tabelle, colonne), articolati in definizioni di oggetti di metadati tabulari in di modellazione relazionale [TMSL Tabular Model Scripting Language ()](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) e [modello a oggetti tabulare (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) codice.|SQL Server 2016 (livello di compatibilità: 1200)| 
|Tabulare in SQL Server 2017|Costrutti (modello, tabelle, colonne), articolati in definizioni di oggetti di metadati tabulari in di modellazione relazionale [TMSL Tabular Model Scripting Language ()](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) e [modello a oggetti tabulare (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) codice.|SQL Server 2017 (livello di compatibilità 1400)| 
|Multidimensionale|Costrutti di modellazione OLAP (cubi, dimensioni, misure).|SQL Server 2000 e versioni successive|  
|Power Pivot|Inizialmente componente aggiuntivo, ma ora completamente integrato in Excel. Solo modellazione visiva attraverso un'infrastruttura tabulare interna. È possibile importare un modello PowerPivot in SSDT per creare un nuovo modello tabulare eseguibile su un'istanza di Analysis Services.|tramite Excel e PowerPivot BI Desktop|  
  
 <sup>1</sup> livelli di compatibilità sono importanti nella versione corrente a causa di un motore di metadati tabulari e al supporto per gli scenari e funzionalità disponibili solo a un livello superiore. Nelle versioni successive supportano livelli di compatibilità precedenti, ma si consiglia si creare nuovi modelli o aggiornano modelli esistenti con il massimo livello di compatibilità supportato dalla versione del server.
  
##  <a name="bkmk_models"></a> Funzionalità del modello  
  Nella tabella seguente viene riepilogata la disponibilità delle funzionalità al livello del modello. Consultare questo elenco per assicurarsi che la funzionalità che si desidera usare sia disponibile per il tipo di modello da compilare.  
  
|||| 
|-|-|-|
||Multidimensionale|Tabella|
|Azioni|Yes|No|
|Aggregations|Yes|No|
|Colonna calcolata|No|Yes|  
|Misure calcolate|Yes|Yes| 
|Tabelle calcolate|No|Sì<sup>1</sup>|  
|Assembly personalizzati|Yes|No|
|Rollup personalizzati|Yes|No| 
|Membro predefinito|Yes|No|  
|Cartelle di visualizzazione|Yes|Sì<sup>1</sup>|  
|Distinct Count|Yes|Sì (tramite DAX)|
|Drill-through|Yes|Sì (dipende dall'applicazione client)|
|Gerarchie|Yes|Yes|
|KPI|Yes|Yes| 
|Oggetti collegati|Yes|Sì (tabelle collegate)|
|Espressioni M|No|Sì<sup>1</sup>|
|Relazioni molti-a-molti|Yes|No (ma non esiste [filtri incrociati bidirezionali](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) livelli di compatibilità 1200 e versioni successive)| 
|Set denominati|Yes|No| 
|Gerarchie incomplete|Yes|Sì<sup>1</sup>|  
|Gerarchie padre-figlio|Yes|Sì (tramite DAX)|
|Partizioni|Yes|Yes| 
|Prospettive|Yes|Yes|
|Sicurezza a livello di riga|Yes|Yes| 
|Sicurezza a livello di oggetto|Yes|Sì<sup>1</sup>|
|Misure semiadditive|Yes|Yes| 
|Traduzioni|[Sì](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|Yes| 
|Gerarchie definite dall'utente|Yes|Yes|
|Writeback|Yes|No| 
  
 <sup>1</sup> visualizzare [Compatibility Level for Tabular modelli in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) per informazioni sulle differenze funzionali tra i livelli di compatibilità.  
  
##  <a name="bkmk_ds"></a> Considerazioni sui dati  
 I modelli tabulari e multidimensionali usano dati importati da origini esterne. La quantità e il tipo di dati da importare sono fattori di primaria importanza per decidere quale tipo di modello è più adatto ai dati in uso.  
  
 **Compressione**  
  
 Sia nelle soluzioni tabulari sia in quelle multidimensionali viene utilizzata la compressione dati che consente di ridurre le dimensioni del database di Analysis Services correlate al data warehouse da cui si importano i dati. Poiché la compressione effettiva varierà in base alle caratteristiche dei dati sottostanti, non vi è alcun modo per sapere con precisione la quantità di spazio su disco e di memoria che sarà richiesta da una soluzione una volta che i dati vengono elaborati e utilizzati nelle query.  
  
 Molti sviluppatori di Analysis Services stimano che le dimensioni dell'archiviazione primaria di un database multidimensionale saranno pari a circa un terzo rispetto a quelle dei dati iniziali. I database tabulari possono talvolta richiedere quantità di compressione maggiori, circa un decimo delle dimensioni, specialmente se la maggior parte dei dati viene importata dalle tabelle dei fatti.  
  
 **Dimensione del modello e distorsione delle risorse (in memoria o disco)**  
  
 La dimensione di un database di Analysis Services è limitata solo dalle risorse disponibili per l'esecuzione. Il tipo di modello e la modalità di archiviazione giocano un ruolo anche nel potenziale di crescita del database.  
  
 I database tabulari vengono eseguiti sia in modalità in memoria che tramite DirectQuery, che trasferisce l'esecuzione delle query a un database esterno. Per analitica in memoria tabulare, il database viene archiviato completamente nella memoria, il che significa che è necessario disporre di memoria sufficiente non solo caricare tutti i dati, ma anche le strutture di dati aggiuntivi create per supportare le query.  
  
 DirectQuery, rinnovato in SQL Server 2016, ha meno restrizioni rispetto a prima e prestazioni migliori. L'uso del database relazionale di back-end per l'archiviazione e l'esecuzione di query semplifica la compilazione di un modello tabulare su larga scala rispetto alle possibilità offerte dalla versione precedente.  
  
 In passato, i database più grandi nell'ambiente di produzione sono multidimensionali, con i carichi di lavoro elaborazione ed eseguire una query in esecuzione in modo indipendente su hardware dedicato, ognuno ottimizzato per il rispettivo uso.  I database tabulari stanno recuperando rapidamente e i nuovi miglioramenti di DirectQuery aiutano ancor di più a colmare il divario.  
  
 Per le query e archiviazione di dati multidimensionale offload esecuzione è disponibile tramite ROLAP.   In un server di query, i set di righe possono essere memorizzati nella cache e quelli obsoleti vengono scartati. Un uso efficiente ed equilibrato delle risorse di memoria e disco spesso conduce i clienti verso soluzioni multidimensionali.  
  
 In fase di caricamento, è possibile prevedere un aumento sia per i requisiti del disco sia per quelli della memoria di entrambi i tipi di soluzione quando tramite Analysis Services vengono memorizzati nella cache, archiviati, analizzati e sottoposti a query i dati. Per altre informazioni sulle opzioni di paging della memoria, vedere [Memory Properties](../analysis-services/server-properties/memory-properties.md). Per altre informazioni sulla scalabilità, vedere [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md).  
  
 PowerPivot per Excel dispone di un limite di dimensioni di file artificiale di 2 gigabyte, che viene imposto in modo che le cartelle di lavoro create in PowerPivot per Excel possano essere caricate in SharePoint, in cui vengono impostati i limiti massimi sulle dimensioni di caricamento del file. Uno dei motivi principali per l'esecuzione della migrazione di una cartella di lavoro di PowerPivot a una soluzione tabulare in un'istanza di Analysis Services autonoma è risolvere la limitazione delle dimensioni del file. Per altre informazioni sulla configurazione delle dimensioni massime di caricamento dei file, vedere [Configurare le dimensioni massime di caricamento dei file &#40;Power Pivot per SharePoint&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
 **Origini dati supportate**  
  
 I modelli tabulari possono importare dati da origini dati relazionali, feed di dati e alcuni formati del documento. È anche possibile usare OLE DB per i provider ODBC con modelli tabulari. I modelli tabulari a livello di compatibilità 1400 offrono un significativo aumento la varietà di origini dati da cui è possibile importare da. Ciò è dovuto l'introduzione dei moderni ottenere dati di query e funzionalità in SSDT che usano il linguaggio di query con formula M di importazione di dati.   

  Con le soluzioni multidimensionali è possibile importare i dati da origini dati relazionali usando provider gestiti e nativi OLE DB.  
  
 Per visualizzare l'elenco delle origini dati esterne che è possibile importare in ogni modello, vedere gli argomenti riportati di seguito.  
  
-   [Origini dati supportate](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  

-   [Origini dati supportate &#40;SSAS - multidimensionale&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  

  
##  <a name="bkmk_lang"></a> Supporto dei linguaggi di query e di scripting  
 Analysis Services include MDX, DMX, DAX, XML/A, ASSL e TMSL. Il supporto di tali linguaggi potrebbe variare in base al tipo di modello. Se i requisiti di linguaggi di query e di scripting sono una considerazione importante, esaminare l'elenco seguente.  

-   I database modello tabulare supportano calcoli DAX, query DAX e query MDX. Questo vale per tutti i livelli di compatibilità. I linguaggi di script sono ASSL (tramite XMLA) per i livelli di compatibilità: 1050-1103 e TMSL (tramite XMLA) per il livello di compatibilità 1200 o superiore. 

-   Le cartelle di lavoro di PowerPivot usano DAX per i calcoli e DAX o MDX per le query.  
  
-   Database modello multidimensionale supportano calcoli MDX, le query MDX, le query DAX e ASSL. 
  
-   I modelli di data mining supportano DMX e ASSL.  
  
-   PowerShell per Analysis Services è supportato per modelli e database tabulari e multidimensionali.  
  
 Tutti i database supportano XML/A. Vedere [Riferimento al linguaggio di query ed espressioni &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/9597533d-35f4-4742-9d8c-7af392163527) e [Guida per gli sviluppatori (Analysis Services)](../analysis-services/analysis-services-developer-documentation.md).  
  
##  <a name="bkmk_sec"></a> Funzionalità di sicurezza  
 Tutte le soluzioni di Analysis Services possono essere protette a livello di database. Opzioni di sicurezza più granulari variano in base alla modalità. Se le impostazioni di sicurezza granulari sono un requisito per la soluzione, esaminare l'elenco seguente per verificare che il livello di sicurezza desiderato sia supportato nel tipo di soluzione da compilare:  

  
-   Database modello tabulare è possono usare la sicurezza a livello di riga, usando autorizzazioni basate su ruolo.  
  
-   Database modello multidimensionale possono utilizzare dimensione e la sicurezza a livello di cella, usando autorizzazioni basate su ruolo.  

-   Le cartelle di lavoro di[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] sono protette a livello di file, mediante le autorizzazioni di SharePoint.  
  
 Le cartelle di lavoro di[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] possono essere ripristinate in un server in modalità tabulare. Una volta ripristinato, il file viene separato da SharePoint consentendo di usare tutte le funzionalità di modellazione tabulare, inclusa la sicurezza a livello di riga.  
  
##  <a name="bkmk_designer"></a> Strumenti di progettazione  
 Le competenze di modellazione dei dati e l'esperienza tecnica possono variare molto tra gli utenti che si occupano della compilazione di modelli analitici. Se in una soluzione la familiarità di uno strumento o l'esperienza degli utenti è una considerazione importante, confrontare le esperienze seguenti per la creazione del modello.  
  
|Strumento di modellazione|Modalità di utilizzo|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Consente di creare tabulari, multidimensionali e soluzioni di data mining. In questo ambiente di creazione viene utilizzata la shell di Visual Studio per fornire aree di lavoro, riquadri delle proprietà e navigazione degli oggetti. Gli utenti tecnici che già utilizzano Visual Studio preferiranno probabilmente questo strumento per la compilazione di applicazioni di Business Intelligence.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] per Excel|Usare per creare una cartella di lavoro di [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] da distribuire successivamente in una farm SharePoint in cui sia presente un'installazione di [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] per SharePoint. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] per Excel presenta un'area di lavoro dell'applicazione separata visualizzata sopra Excel. Vengono utilizzate le stesse metafore visive (pagine a schede, layout griglia e barra della formula) di Excel. Gli utenti con esperienza nell'utilizzo di Excel preferiranno questo strumento rispetto a [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].|  
  
##  <a name="bkmk_client"></a> Supporto delle applicazioni client  
 Le soluzioni in generale, tabulari e multidimensionali supportano le applicazioni client utilizzando una o più delle librerie client di Analysis Services (MSOLAP, adottano AMOMD, ADOMD). Ad esempio, Excel, Power BI Desktop e applicazioni personalizzate.   
 
 Se si utilizza Reporting Services, la disponibilità delle funzionalità di report varia tra le edizioni e le modalità server. Per questo motivo, il tipo di report che si desidera compilare potrebbe influire sulla modalità server che si sceglie di installare.  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], uno strumento di creazione di Reporting Services in esecuzione in SharePoint, è disponibile in un server di report distribuito in una farm di SharePoint 2010. L'unico tipo di origine dati che può essere usato con questo report è un database modello tabulare di Analysis Services o una cartella di lavoro di [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Ciò significa che è necessario disporre di un server in modalità tabulare o di un server [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] per SharePoint per ospitare l'origine dati usata da questo tipo di report. Non è possibile utilizzare un modello multidimensionale come origine dati per un report [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] . È necessario creare una connessione BISM [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] o un'origine dati condivisa di Reporting Services da usare come origine dati per un report [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] .  
  
 In Generatore report e Progettazione report è possibile usare qualsiasi database di Analysis Services, incluse le cartelle di lavoro di [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] ospitate in [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] per SharePoint.  
  
 I report Tabella pivot di Excel sono supportati da tutti i database di Analysis Services. Le funzionalità di Excel non cambiano se si usa un database tabulare, un database multidimensionale o una cartella di lavoro di [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , anche se la funzionalità writeback è supportata solo per i database multidimensionali.  
 
  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di un'istanza di Analysis Services](../analysis-services/instances/analysis-services-instance-management.md)   
 [Novità di Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)     

  
  
