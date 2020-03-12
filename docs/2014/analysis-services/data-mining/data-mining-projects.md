---
title: Progetti di data mining | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 543d70fc-34d2-42dd-8d6d-0543109f94d0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e107dde8a3f811cbc1a24533705863c954dd85c4
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112159"
---
# <a name="data-mining-projects"></a>Progetti di data mining
  Un progetto di data mining è parte di una soluzione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Durante il processo di progettazione, gli oggetti creati nel progetto sono disponibili per l'esecuzione di test e query come parte di un database dell'area di lavoro. Per consentire agli utenti di eseguire query o esplorare gli oggetti nel progetto, è necessario distribuire il progetto in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità multidimensionale.  
  
 In questo argomento vengono fornite informazioni di base necessarie per comprendere e creare i progetti di data mining.  
  
 
##  <a name="bkmk_Overview"></a>Creazione di progetti di data mining  
 In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]per compilare i progetti di data mining è possibile usare il modello **Progetto OLAP e data mining**. È inoltre possibile creare progetti di data mining a livello di codice tramite AMO. È possibile generare script dei singoli oggetti di data mining tramite ASSL (Analysis Services Scripting Language). Per altre informazioni, vedere [Accesso ai dati di modelli multidimensionali &#40;Analysis Services - Dati multidimensionali&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md).  
  
 Se si crea un progetto di data mining all'interno di una soluzione esistente, per impostazione predefinita gli oggetti di data mining saranno distribuiti in un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con lo stesso nome del file della soluzione. È possibile modificare il nome e il server di destinazione usando la finestra di dialogo **Proprietà progetto** . Per altre informazioni, vedere [Configurare proprietà di progetti di Analysis Services &#40;SSDT&#41;](../multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
> [!WARNING]  
>  Per compilare e distribuire correttamente il progetto, è necessario avere accesso a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in esecuzione in modalità OLAP/data mining. Non è possibile sviluppare o distribuire soluzioni di data mining in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che supporta modelli tabulari, né è possibile utilizzare direttamente i dati da una cartella di lavoro di PowerPivot o da un modello tabulare che utilizza l'archivio dati in memoria. Per determinare se l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponibile supporta il data mining, vedere [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 In ogni progetto di data mining creato si effettueranno i passaggi riportati di seguito:  
  
1.  Scegliere un' *origine dati*, ad esempio un cubo, un database o un file di Excel o di testo, che contiene i dati non elaborati da usare per la compilazione dei modelli.  
  
2.  Definire un subset dei dati nell'origine dati da usare per l'analisi e salvarlo come *vista origine dati*.  
  
3.  Definire una *struttura di data mining* per supportare la modellazione.  
  
4.  Aggiungere *modelli di data mining* alla struttura di data mining, scegliendo un *algoritmo* e specificando la modalità in cui i dati verranno gestiti dall'algoritmo.  
  
5.  Eseguire il training dei modelli popolandoli con i dati selezionati o un subset filtrato dei dati.  
  
6.  Esplorare, eseguire test e ricompilare i modelli.  
  
 Al completamento del progetto, è possibile distribuirlo per consentire agli utenti di esplorarlo o eseguire query oppure fornire l'accesso a livello di codice ai modelli di data mining in un'applicazione per supportare stime e analisi.  
  

  
##  <a name="bkmk_Objects"></a>Oggetti nei progetti di data mining  
 Tutti i progetti di data mining contengono i quattro tipi di oggetti seguenti. È possibile disporre di più oggetti di tutti i tipi.  
  
-   Origini dati  
  
-   Viste origine dati  
  
-   Strutture di data mining  
  
-   Modelli di data mining  
  
 Ad esempio, un solo progetto di data mining può contenere un riferimento a più origini dati, ciascuna delle quali supporta più viste origine dati. A sua volta, ogni vista origine dati può supportare più strutture di data mining, ciascuna con molti modelli di data mining correlati.  
  
 Inoltre, il progetto potrebbe includere algoritmi plug-in, assembly personalizzati o stored procedure personalizzate; questi oggetti tuttavia non vengono descritti in questo argomento. Per ulteriori informazioni, vedere [la guida per gli sviluppatori &#40;Analysis Services&#41;](../analysis-services-developer-documentation.md).  
 
  
###  <a name="bkmk_DataSources"></a>Origini dati  
 L'origine dati definisce la stringa di connessione e le informazioni di autenticazione utilizzate dal server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per connettersi all'origine dati. L'origine dati può contenere più tabelle o viste; può trattarsi semplicemente di una sola cartella di lavoro di Excel o un file di testo oppure essere più complessa, come un database OLAP (Online Analytical Processing, elaborazione analitica in linea) o un database relazionale di grandi dimensioni.  
  
 Un progetto di data mining può fare riferimento a più origini dati. Anche se un modello di data mining può utilizzare una sola origine dati alla volta, il progetto può avere più modelli tratti da origini dati diverse.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono supportati dati da più provider esterni e nel data mining di SQL Server è possibile utilizzare sia dati relazionali sia dati del cubo come origine dati. Tuttavia, se si sviluppano entrambi i tipi di progetti (modelli basati su origini relazionali e modelli basati su cubi OLAP), potrebbe essere necessario svilupparli e gestirli in progetti distinti.  
  
-   In genere i modelli basati su un cubo OLAP devono essere sviluppati all'interno della soluzione di progettazione OLAP. Ciò è dovuto al fatto che i modelli basati su un cubo devono elaborare il cubo per aggiornare i dati. In genere è necessario utilizzare dati del cubo solo quando si tratta del mezzo principale di archiviazione dati e accesso o quando si richiedono le aggregazioni, le dimensioni e gli attributi creati dal progetto multidimensionale.  
  
-   Se nel progetto si utilizzano solo dati relazionali, è necessario creare i modelli relazionali all'interno di un progetto separato, in modo da evitare di rielaborare inutilmente altri oggetti. In molti casi, il database di gestione temporanea o il data warehouse utilizzato per supportare la creazione del cubo contiene già le viste necessarie per eseguire il data mining ed è possibile utilizzare tali viste per il data mining anziché utilizzare le aggregazioni e le dimensioni nel cubo.  
  
-   Non è possibile utilizzare direttamente dati in memoria o PowerPivot per compilare i modelli di data mining.  
  
 L'origine dati identifica solo il server o il provider e il tipo di dati generale. Se è necessario modificare la formattazione dei dati e le aggregazioni, utilizzare l'oggetto vista origine dati.  
  
 Per controllare la modalità di gestione dei dati dall'origine dati, è possibile aggiungere colonne derivate o calcoli, modificare le aggregazioni o rinominare le colonne nei dati della vista origine dati. È inoltre possibile utilizzare anche i dati a valle, modificando le colonne della struttura di data mining o utilizzando flag di modellazione e filtri al livello della colonna del modello di data mining.  
  
 Se è necessario pulire i dati o modificare i dati nel data warehouse per creare variabili aggiuntive, modificare tipi di dati o creare un'aggregazione alternativa, potrebbe essere necessario creare tipi di progetto aggiuntivi a supporto del data mining. Per altre informazioni su questi progetti correlati, vedere [Progetti correlati per soluzioni di data mining](data-mining-solutions.md).  
  

  
###  <a name="bkmk_DSV"></a>Viste origine dati  
 Dopo avere definito la connessione a un'origine dati, viene creata una vista che individua i dati specifici rilevanti per il modello.  
  
 La vista origine dati consente inoltre di personalizzare la modalità in cui i dati nell'origine dati vengono forniti al modello di data mining. È possibile modificare la struttura dei dati in modo da renderla più rilevante per il progetto oppure scegliere solo determinati tipi di dati.  
  
 Ad esempio, tramite Editor vista origine dati è possibile:  
  
-   Creare colonne derivate, ad esempio datepart, sottostringhe e così via.  
  
-   Aggregare valori utilizzando istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] come GROUP BY  
  
-   Limitare temporaneamente i dati o i dati di esempio  
  
 Per altre informazioni sulla modifica di dati all'interno di una vista origine dati, vedere [Viste origine dati in modelli multidimensionali](../multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
> [!WARNING]  
>  Se si desidera filtrare i dati, è possibile eseguire questa operazione nella vista origine dati, ma anche creare filtri sui dati a livello del modello di data mining. Poiché la definizione del filtro è archiviata con il modello di data mining, l'utilizzo di filtri modello semplifica la determinazione dei dati utilizzati per il training del modello. Inoltre, è possibile creare più modelli correlati, con criteri di filtro diversi. Per altre informazioni, vedere [Filtri per i modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-models-analysis-services-data-mining.md).  
  
 Si noti che la vista origine dati creata può contenere dati aggiuntivi non utilizzati direttamente per l'analisi. Ad esempio, è possibile aggiungere alla vista origine dati altri dati utilizzati per test, stime o drill-through. Per altre informazioni su questi usi, vedere [Test e convalida &#40;Data mining&#41;](testing-and-validation-data-mining.md) e [Query drill-through (Data mining)](drillthrough-queries-data-mining.md).  
  

  
###  <a name="bkmk_Structures"></a>Strutture di data mining  
 Dopo aver creato l'origine dati e la vista origine dati, è necessario selezionare le colonne di dati più rilevanti per le esigenze aziendali, definendo *strutture di data mining* all'interno del progetto. Con una struttura di data mining si indica al progetto quali colonne di dati della vista origine dati devono effettivamente essere utilizzate nella modellazione, nel training e nei test.  
  
 Per aggiungere una nuova struttura di data mining, avviare la Creazione guidata modello di data mining. Con la procedura guidata viene automaticamente definita una struttura di data mining, viene avviato il processo di scelta dei dati e, facoltativamente, di aggiunta di un modello di data mining alla struttura. In una struttura di data mining si scelgono le tabelle e le colonne dalla vista origine dati o da un cubo OLAP e si definiscono le relazioni tra le tabelle, se i dati includono tabelle nidificate.  
  
 La scelta dei dati sarà molto diversa nella Creazione guidata modello di data mining, a seconda che si utilizzino origini dati relazionali o OLAP.  
  
-   Quando si scelgono dati da un'origine dati relazionale, l'impostazione di una struttura di data mining è semplice: si scelgono le colonne dai dati nella vista origine dati e si impostano personalizzazioni aggiuntive, quali gli alias, o si definisce in che modo raggruppare o suddividere in contenitori i valori nella colonna. Per altre informazioni, vedere [Creare una struttura di data mining relazionale](create-a-relational-mining-structure.md).  
  
-   Quando si utilizzano dati da un cubo OLAP, la struttura di data mining deve trovarsi nello stesso database della soluzione OLAP.  Per creare una struttura di data mining, selezionare gli attributi dalle dimensioni e le misure correlate nella soluzione OLAP. I valori numerici sono in genere presenti nelle misure e le variabili di categoria nelle dimensioni. Per altre informazioni, vedere [Creare una struttura di data mining OLAP](create-an-olap-mining-structure.md).  
  
-   Per definire le strutture di data mining è inoltre possibile utilizzare DMX. Per altre informazioni, vedere [Istruzioni DMX &#40;Data Mining Extensions&#41; per la definizione dei dati](/sql/dmx/dmx-statements-data-definition).  
  
 Dopo avere creato la struttura di data mining iniziale, è possibile copiare, modificare e creare alias delle colonne della struttura.  
  
 Ogni struttura di data mining può contenere più modelli di data mining. Pertanto, al termine dell'operazione è possibile aprire nuovamente la struttura di data mining e utilizzare [Data Mining Designer](data-mining-designer.md) per aggiungere altri modelli di data mining alla stessa.  
  
 È inoltre possibile separare i dati in un training set, utilizzato per la compilazione di modelli, e in un set di dati di controllo da utilizzare nei test o nella convalida dei modelli di data mining.  
  
> [!WARNING]  
>  Alcuni tipi di modelli, ad esempio i modelli Time Series, non supportano la creazione di set di dati di controllo perché richiedono una serie continua di dati per il training. Per altre informazioni, vedere [Training and Testing Data Sets](training-and-testing-data-sets.md).  
  
  
  
###  <a name="bkmk_Models"></a>Modelli di data mining  
 Il modello di data mining definisce l'algoritmo o il metodo di analisi che verrà utilizzato per i dati. A ogni struttura di data mining si aggiunge uno o più modelli di data mining.  
  
 A seconda delle esigenze, è possibile combinare più modelli in un solo progetto o creare progetti separati per ogni tipo di modello o attività analitica.  
  
 Dopo aver creato una struttura e un modello, ciascun modello viene *elaborato* eseguendo i dati dalla vista origine dati tramite l'algoritmo, che genera un modello matematico dei dati. Questo processo è noto anche come *training del modello*. Per altre informazioni, vedere [Requisiti e considerazioni sull'elaborazione &#40;data mining&#41;](processing-requirements-and-considerations-data-mining.md).  
  
 Dopo l'elaborazione del modello, è possibile esplorare visivamente il modello di data mining e creare query di stima basate su di esso. Se i dati ottenuti dal processo di training sono stati memorizzati nella cache, è possibile usare query *drill-through* per restituire informazioni dettagliate sui case usati nel modello.  
  
 Quando si desidera utilizzare un modello per la produzione (ad esempio per l'utilizzo nell'esecuzione di stime o per l'esplorazione da parte di utenti generici), è possibile distribuirlo in un server diverso. Se è necessario rielaborare il modello in futuro, occorre esportare anche la definizione della struttura di data mining sottostante (e necessariamente la definizione dell'origine dati e della vista origine dati).  
  
 Quando si distribuisce un modello, è necessario inoltre assicurarsi che siano impostate le opzioni di elaborazione corrette nella struttura e nel modello e che i potenziali utenti dispongano delle autorizzazioni necessarie per eseguire query, visualizzare modelli o eseguire il drill-through sulla struttura o i dati del modello. Per altre informazioni, vedere [Panoramica della sicurezza &#40;data mining&#41;](security-overview-data-mining.md).  
  
 
  
##  <a name="bkmk_Complete"></a>Utilizzo del progetto di data mining completato  
 In questa sezione vengono riepilogate le modalità di utilizzo del progetto di data mining completato. È possibile creare grafici di accuratezza, esplorare e convalidare i dati e rendere disponibili agli utenti i modelli di data mining.  
  
> [!WARNING]  
>  I grafici, le query e le visualizzazioni che si utilizzano con i modelli di data mining non vengono salvati come parte del progetto di data mining e non possono essere distribuiti. Se è necessario rendere persistenti tali oggetti, è necessario salvare il contenuto presentato o crearne uno script come descritto per ogni oggetto.  
  
 
  
###  <a name="bkmk_ViewExplore"></a>Visualizzare ed esplorare i modelli  
 Dopo avere creato un modello, è possibile utilizzare query e strumenti visivi per esplorare i modelli che contiene e acquisire ulteriori informazioni sui modelli e le statistiche sottostanti. Nella scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] offre visualizzatori per ogni tipo di modello di data mining che è possibile usare per esplorare i modelli di data mining.  
  
 Queste visualizzazioni sono temporanee e vengono chiuse senza essere salvate quando si esce dalla sessione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Pertanto, se è necessario esportare tali visualizzazioni in un'altra applicazione per una presentazione o un'ulteriore analisi, usare i comandi **Copia** forniti in ogni scheda o riquadro dell'interfaccia del visualizzatore.  
  
 I componenti aggiuntivi Data mining per Excel forniscono inoltre un modello di Visio che è possibile utilizzare per rappresentare i modelli in un diagramma di Visio e annotare e modificare il diagramma utilizzando gli strumenti di Visio. Per altre informazioni, vedere [Componenti aggiuntivi Data mining di Microsoft SQL Server 2008 SP2 per Microsoft Office 2007](https://www.microsoft.com/download/details.aspx?id=8569).
  
###  <a name="bkmk_Validate"></a>Test e convalida di modelli  
 Dopo avere creato un modello, è possibile analizzare i risultati e decidere quali modelli offrono prestazioni ottimali.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono disponibili diversi grafici che è possibile utilizzare per fornire strumenti che consentono di confrontare direttamente i modelli di data mining e di scegliere quello più accurato o più utile. Tra questi strumenti sono inclusi un grafico di accuratezza, un grafico dei profitti e una matrice di classificazione. È possibile generare tali grafici usando la scheda **Grafico accuratezza modello di data mining** di Progettazione modelli di data mining.  
  
 È anche possibile utilizzare il report convalida incrociata per eseguire il campionamento secondario iterativo dei dati per determinare se il modello è influenzato da un determinato set di dati. Le statistiche fornite dal report possono essere utilizzate per confrontare in modo obiettivo i modelli e per valutare la qualità dei dati di training.  
  
 Si noti che questi report e grafici non sono archiviati con il progetto o nel database di ssASnoversion, pertanto se è necessario conservare o duplicare i risultati, è necessario salvarli o creare script degli oggetti tramite DMX o AMO. È inoltre possibile utilizzare stored procedure per la convalida incrociata.  
  
 Per altre informazioni, vedere [Test e convalida &#40;Data mining&#41;](testing-and-validation-data-mining.md).  
  

  
###  <a name="bkmk_Predict"></a>Creazione di stime  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornisce un linguaggio di query denominato DMX (Data Mining Extension) che costituisce la base per la creazione di stime ed è facilmente gestibile tramite script. Per agevolare la compilazione di query di stima DMX, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile un generatore query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]sono inoltre presenti molti modelli DMX per l'editor di query. Se non si ha esperienza nelle query di stima, è consigliabile utilizzare il generatore query fornito sia in Progettazione modello di data mining sia in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Data Mining Tools](data-mining-tools.md).  
  
 Le stime create in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] non sono persistenti, pertanto se le query sono complesse o è necessario riprodurre i risultati, è consigliabile salvare le query di stima in file di query DMX, generarne script o incorporarle come parte di un pacchetto di Integration Services.  
  
 
  
##  <a name="bkmk_API"></a>Accesso a livello di codice agli oggetti di data mining  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] offre diversi strumenti per l'utilizzo a livello di codice dei progetti di data mining e dei relativi oggetti. Il linguaggio DMX offre istruzioni che è possibile utilizzare per creare origini dati e viste origine dati, nonché per creare, eseguire il training e utilizzare strutture e modelli di data mining. Per altre informazioni, vedere [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
 È inoltre possibile eseguire tali attività tramite ASSL (Analysis Services Scripting Language) oppure mediante AMO (Analysis Management Objects). Per altre informazioni, vedere [Sviluppo con XMLA in Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).  
  
  
  
## <a name="related-tasks"></a>Attività correlate  
 Negli argomenti seguenti viene descritto l'utilizzo della Creazione guidata modello di data mining per creare un progetto di data mining e gli oggetti associati.  
  
|Attività|Argomenti|  
|-----------|------------|  
|Viene descritto come utilizzare colonne della struttura di data mining|[Creare una struttura di data mining relazionale](create-a-relational-mining-structure.md)|  
|Vengono fornite ulteriori informazioni sull'aggiunta di nuovi modelli di data mining e sull'elaborazione di una struttura e dei relativi modelli|[Aggiunta di modelli di data mining a una struttura &#40;Analysis Services-Data mining&#41;](add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|Vengono forniti collegamenti a risorse utili per personalizzare gli algoritmi per la compilazione di modelli di data mining|[Personalizzare struttura e modelli di data mining](customize-mining-models-and-structure.md)|  
|Vengono forniti collegamenti alle informazioni su ciascuno dei visualizzatori dei modelli di data mining|[Visualizzatori modello di data mining](data-mining-model-viewers.md)|  
|Vengono fornite informazioni sulla creazione di un grafico di accuratezza, un grafico dei profitti o una matrice di classificazione o sul test di una struttura di data mining|[Test e convalida &#40;&#41;di data mining](testing-and-validation-data-mining.md)|  
|Vengono fornite informazioni sulle opzioni di elaborazione e sulle autorizzazioni|[Elaborazione di oggetti di data mining](processing-data-mining-objects.md)|  
|Vengono fornite ulteriori informazioni su Analysis Services|[Database modello multidimensionale &#40;SSAS&#41;](../multidimensional-models/multidimensional-model-databases-ssas.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione modelli di data mining](data-mining-designer.md)   
 [Creazione di modelli multidimensionali tramite SQL Server Data Tools &#40;SSDT&#41;](../multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [Database dell'area di lavoro &#40;SSAS tabulare&#41;](../tabular-models/workspace-database-ssas-tabular.md)  
  
  
