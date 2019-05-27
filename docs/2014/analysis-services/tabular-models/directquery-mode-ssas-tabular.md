---
title: La modalità DirectQuery (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9ab544235e842e38024ce98763094c300bb06275
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067225"
---
# <a name="directquery-mode-ssas-tabular"></a>Modalità DirectQuery (SSAS tabulare)
  Analysis Services consente di recuperare i dati e creare report da un modello tabulare recuperando dati e aggregazioni direttamente da un sistema di database relazionali, usando *la modalità DirectQuery*. In questo argomento vengono illustrate le differenze tra i modelli tabulari standard residenti unicamente in memoria e i modelli tabulari in grado di eseguire query su un'origine dati relazionale. Viene inoltre descritto come creare e distribuire un modello destinato a essere utilizzato nella modalità DirectQuery.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi della modalità DirectQuery](#bkmk_Benefits)  
  
-   [Creazione di modelli per l'uso con la modalità DirectQuery](#bkmk_Design)  
  
    -   [Origini dati per i modelli DirectQuery](directquery-mode-ssas-tabular.md#bkmk_DataSources)  
  
    -   [Convalida e restrizioni della struttura per la modalità DirectQuery](#bkmk_Validation)  
  
    -   [Compatibilità delle formule per i modelli DirectQuery](#bkmk_FormulaCompat)  
  
    -   [Sicurezza in modalità DirectQuery](#bkmk_Security)  
  
    -   [Sicurezza in modalità DirectQuery](#bkmk_Security)  
  
-   [Proprietà di DirectQuery](#bkmk_PropertyList)  
  
-   [Attività e argomenti correlati](#bkmk_related_tasks)  
  
##  <a name="bkmk_Benefits"></a> Vantaggi della modalità DirectQuery  
 Per impostazione predefinita, i modelli tabulari utilizzano una cache in memoria per l'archiviazione dei dati e l'esecuzione di query. Poiché i modelli tabulari utilizzano dati residenti in memoria, anche le query più complesse possono essere molto veloci. Esistono tuttavia alcuni inconvenienti legati all'utilizzo dei dati memorizzati nella cache:  
  
-   I dati non vengono aggiornati quando i dati di origine cambiano. È necessario elaborare il modello per ottenere gli aggiornamenti ai dati.  
  
-   Quando si spegne il computer che ospita il modello, la cache viene salvata su disco e dovrà essere riaperta al caricamento del modello o all'apertura del file PowerPivot. Le operazioni di caricamento e salvataggio possono richiedere molto tempo.  
  
 Al contrario, la modalità DirectQuery prevede l'utilizzo dei dati archiviati in un database di SQL Server.  Quando si crea il modello, si importano nella cache tutti i dati o solo parte di essi e quando si distribuisce il modello, si specifica che per le query eseguite sul modello l'origine dati deve essere SQL Server, non i dati memorizzati nella cache. Qualsiasi query DAX sui dati verranno convertite da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in istruzioni SQL equivalenti sull'origine dati relazionale specificata.  
  
 La distribuzione di un modello tramite la modalità DirectQuery comporta molti vantaggi:  
  
-   È possibile disporre di un modello su set di dati troppo grandi per essere contenuti in memoria nel server Analysis Services.  
  
-   I dati sono sempre aggiornati e non si verifica alcun overhead di gestione supplementare legato alla necessità di conservare una copia separata dei dati. Le modifiche ai dati di origine sottostanti possono essere immediatamente riflesse nelle query sul modello di dati.  
  
-   La modalità DirectQuery può trarre vantaggio dall'accelerazione delle query lato provider, ad esempio quella fornita dagli indici di colonna con ottimizzazione per la memoria xVelocity.  
  
-   Qualsiasi livello di sicurezza applicato dal database back-end verrà sicuramente applicato, utilizzando la sicurezza a livello di riga. Al contrario, se si utilizzano i dati memorizzati nella cache, può essere difficile assicurarsi che la cache sia protetta esattamente come i dati nel server.  
  
-   Se il modello contiene formule complesse che potrebbero richiedere più query, Analysis Services consente di eseguire l'ottimizzazione per garantire che il piano relativo alla query eseguita sul database back-end sia il più efficiente possibile.  
  
##  <a name="bkmk_Design"></a> Creazione di modelli per l'uso con la modalità DirectQuery  
 I modelli tabulari vengono creati tramite Progettazione modelli [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Poiché in Progettazione modelli tutti i modelli vengono creati in memoria in fase di modellazione, se le dimensioni dei dati sono troppo elevate per la memoria, è opportuno importare solo un subset dei dati nella cache utilizzata dal database dell'area di lavoro.  
  
 Quando si è pronti a passare alla modalità DirectQuery, è possibile modificare una proprietà per abilitare la modalità DirectQuery. Per altre informazioni, vedere [abilitare la modalità DirectQuery &#40;modello tabulare di SSAS&#41;](enable-directquery-mode-in-ssdt.md).  
  
 Quando si esegue questa operazione, in Progettazione modelli viene automaticamente configurato il database dell'area di lavoro per l'esecuzione in una modalità ibrida che consente l'utilizzo dei dati memorizzati nella cache. Vengono inoltre segnalate all'utente le caratteristiche del modello non compatibili con la modalità DirectQuery. Di seguito sono elencati i requisiti principali da tenere presente:  
  
-   **Origini dati:** I modelli DirectQuery possono usare solo i dati da una sola origine dati SQL Server. Dopo avere attivato la modalità DirectQuery per un modello, non è possibile utilizzare altri tipi di dati in Progettazione modelli, incluse le tabelle aggiunte tramite operazioni di copia e incolla. Tutte le altre opzioni dell'importazione sono disabilitate. Eventuali tabelle incluse in una query devono appartenere all'origine dati di SQL Server. Visualizzare [origini dati per i modelli DirectQuery](directquery-mode-ssas-tabular.md#bkmk_DataSources)per altre informazioni.  
  
-   **Supporto per le colonne calcolate:** Le colonne calcolate non sono supportate per i modelli DirectQuery. È tuttavia possibile creare misure e indicatori di prestazioni chiave (KPI) utilizzabili sui set di dati. Vedere la sezione sulla [convalida](#bkmk_Validation) per altre informazioni.  
  
-   **Utilizzo limitato delle funzioni DAX:** Alcune funzioni DAX non possono essere utilizzati nella modalità DirectQuery, pertanto è necessario sostituirle con altre funzioni o creare i valori utilizzando colonne derivate nell'origine dati. In Progettazione modelli è possibile eseguire la convalida in fase di progettazione quando si verificano errori causati dalla creazione di formule incompatibili con la modalità DirectQuery. Vedere le sezioni seguenti per altre informazioni: [Convalida](#bkmk_Validation).  
  
-   **Compatibilità delle formule:** in alcuni casi noti, la stessa formula può restituire risultati diversi in un modello ibrido o memorizzato nella cache rispetto a un modello DirectQuery che usa unicamente l'archivio dati relazionale. Queste differenze sono una conseguenza delle differenze semantiche tra il motore di analisi in memoria xVelocity (VertiPaq) e SQL Server. Per altre informazioni su queste differenze, vedere la sezione: [Compatibilità delle formule](#bkmk_FormulaCompat).  
  
-   **Sicurezza:** È possibile usare diversi metodi per proteggere i modelli a seconda della modalità di distribuzione. I dati memorizzati nella cache per i modelli tabulari vengono protetti tramite il modello di sicurezza dell'istanza di Analysis Services. È possibile proteggere i modelli DirectQuery tramite i ruoli, ma anche utilizzando la sicurezza definita nell'archivio dati relazionale. È possibile configurare il modello in modo che gli utenti che aprono un report basato su un modello solo DirectQuery possono visualizzare solo i dati per cui dispongono delle autorizzazioni in SQL Server. Vedere la sezione per altre informazioni: [Sicurezza](#bkmk_Security).  
  
-   **Restrizioni client:** Quando un modello è in modalità DirectQuery, è possibile eseguire query solo tramite DAX. Non è possibile utilizzare MDX per creare query. Pertanto, non è possibile utilizzare Excel PivotClient, perché Excel utilizza MDX.  
  
     Tuttavia, è possibile creare query su un modello DirectQuery in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] se si usa una query di tabella DAX come parte di un'istruzione Execute XMLA, per altre informazioni, vedere [riferimento alla sintassi di Query DAX](https://msdn.microsoft.com/library/ee634217.aspx).  
  
 Dopo avere risolto tutti i problemi di progettazione e dopo avere testato il modello, è possibile procedere con la distribuzione. A questo punto, è possibile impostare il metodo preferito per rispondere alle query sul modello. Si desidera che gli utenti abbiano accesso alla cache o che utilizzino sempre e solo l'origine dati relazionale?  
  
 Se si distribuisce il modello in un *modalità ibrida*, la cache è ancora disponibile e può essere usata per le query. In una modalità ibrida sono disponibili molte opzioni:  
  
-   Quando la cache e l'origine dati relazionale sono entrambe disponibili, è possibile impostare il metodo di connessione preferito, ma sarà il client a stabilire in definitiva quale origine verrà utilizzata, tramite la proprietà della stringa di connessione DirectQueryMode.  
  
-   È inoltre possibile configurare le partizioni sulla cache in modo che la partizione primaria utilizzata per la modalità DirectQuery non venga mai elaborata e debba sempre fare riferimento all'origine relazionale. Sono disponibili molti modi per utilizzare le partizioni allo scopo di ottimizzare la progettazione dei modelli e la creazione di report. Per altre informazioni, vedere [partizioni e modalità DirectQuery &#40;modello tabulare di SSAS&#41;](define-partitions-in-directquery-models-ssas-tabular.md).  
  
-   Dopo avere distribuito il modello, è possibile modificare il metodo di connessione preferito. È ad esempio possibile utilizzare una modalità ibrida per i test e passare alla modalità **Solo DirectQuery** unicamente dopo avere testato accuratamente eventuali report o query che utilizzano il modello. Per altre informazioni, vedere [Impostare o modificare il metodo di connessione preferito per DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).  
  
###  <a name="bkmk_DataSources"></a> Origini dati per i modelli DirectQuery  
 Non appena si modifica l'ambiente di progettazione per abilitare la modalità DirectQuery, le origini dati per il database dell'area di lavoro vengono convalidate per assicurarsi che provengano da una sola origine dati SQL Server. Nei modelli DirectQuery non sono consentiti dati da altre origini, inclusi i dati incollati da un'operazione di copia.  
  
 Se si intende utilizzare il modello nella modalità DirectQuery, è necessario assicurarsi che tutti i dati necessari per il report che si desidera creare siano archiviati nel database di SQL Server specificato. Se i dati necessari per la modellazione non sono disponibili in questa origine, valutare la possibilità di utilizzare Integration Services o altri strumenti di data warehouse per importare i dati in un database di SQL Server utilizzato come origine dati DirectQuery.  
  
###  <a name="bkmk_Validation"></a> Convalida e restrizioni della struttura per la modalità DirectQuery  
 Quando si crea un modello da utilizzare nella modalità DirectQuery, è necessario caricare inizialmente una parte dei dati nella cache. Se i dati verranno utilizzati sono troppo grandi per rientrare nella memoria, è possibile usare la **Visualizza anteprima e filtro** opzione nell'Importazione guidata tabella per selezionare un subset di dati oppure scrivere uno script SQL per ottenere i dati desiderati.  
  
> [!WARNING]  
>  Poiché la modalità DirectQuery non supporta l'utilizzo delle colonne calcolate, se sono presenti colonne che si desidera combinare o su cui si desidera eseguire altre operazioni, è necessario prevederlo in anticipo e creare le definizioni delle colonne nello script o nella query di importazione dati.  
  
 Per visualizzare e risolvere gli errori di convalida, aprire l' **Elenco errori** in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Gli errori critici che impediscono l'utilizzo della modalità DirectQuery sono visualizzati nella scheda **Errori** . È necessario correggere questi errori prima di passare alla modalità DirectQuery. Gli errori di convalida più difficili da risolvere sono in genere correlati alle formule non supportate nella modalità DirectQuery. Vedere la sezione [compatibilità delle formule](#bkmk_FormulaCompat), per una panoramica degli errori correlati a formule e colonne calcolate.  
  
 Nell'elenco seguente sono riportate altre considerazioni da ricordare quando si crea un modello per l'accesso DirectQuery:  
  
-   In modalità *Solo DirectQuery* , i risultati di un report possono variare a seconda del contesto di sicurezza dell'utente che visualizza i risultati. È necessario testare i modelli con credenziali diverse per assicurarsi che gli utenti ottengano i risultati previsti.  
  
-   Se si configura un modello per la modalità ibrida, nella quale è possibile utilizzare la cache o i dati da SQL Server, esiste la possibilità che i client che si connettono a ogni origine possano ottenere risultati diversi, a seconda della modalità specificata nella stringa di connessione. Qualora sia necessario assicurarsi che gli utenti di report vedano solo i dati provenienti da SQL Server, è necessario cancellare la cache o impostare il modello su DirectQueryOnly.  
  
###  <a name="bkmk_FormulaCompat"></a> Compatibilità delle formule per i modelli DirectQuery  
 È possibile che alcuni modelli contengano formule non supportate nella modalità DirectQuery e che quindi debbano essere riprogettati per evitare errori di convalida. Di seguito sono riportate alcune limitazioni sulle formule supportate nella modalità DirectQuery:  
  
-   Le colonne calcolate non sono supportate nei modelli tabulari per cui è abilitata la modalità DirectQuery, nemmeno nei modelli ibridi. Se un modello richiede colonne calcolate, convertirle in colonne derivate tramite Transact-SQL nella definizione dell'importazione.  
  
-   I modelli DirectQuery supportano l'utilizzo delle formule DAX nelle misure, convertite in operazioni basate su set nell'archivio dati relazionale. Sono supportate tutte le misure create tramite misure implicite.  
  
-   Non tutte le funzioni sono supportate. Poiché [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] converte tutte le formule DAX e le definizioni di misure in istruzioni SQL quando si eseguono query su un modello DirectQuery, le formule che contengono elementi che non possono essere convertiti in Transact-SQL causeranno errori di convalida nel modello. Ad esempio, le funzioni di Business Intelligence per le gerarchie temporali non sono supportate. Anche le funzioni supportate, ad esempio le funzioni statistiche, possono assumere comportamenti diversi. Per un elenco completo dei problemi di compatibilità, vedere [compatibilità delle formule nella modalità DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md).  
  
-   Alcune formule del modello vengono convalidate quando si passa alla modalità DirectQuery, ma restituiscono risultati diversi a seconda che vengano eseguite nella cache o nell'archivio dati relazionale. Il motivo è che per i calcoli effettuati sulla cache viene utilizzata la semantica del motore di analisi in memoria xVelocity (VertiPaq) contenente molte funzionalità intese a emulare il comportamento di Excel, mentre per le query eseguite sui dati archiviati nell'archivio dati relazionale viene utilizzata necessariamente la semantica di SQL Server. Per un elenco delle funzioni DAX che potrebbero restituire risultati diversi quando il modello viene distribuito in tempo reale, vedere [compatibilità delle formule nella modalità DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md).  
  
###  <a name="bkmk_Connecting"></a> La connessione ai modelli DirectQuery  
 Non è possibile connettere i client che utilizzano MDX come linguaggio di query ai modelli che utilizzano la modalità DirectQuery. Se ad esempio si tenta di creare una query MDX su un modello DirectQuery, un errore indicherà che è impossibile trovare o elaborare il cubo. È possibile creare query sui modelli DirectQuery utilizzando [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], formule DAX o query XMLA. Per altre informazioni sul modo in cui è possibile eseguire query ad hoc sui modelli tabulari, vedere [Tabular Model Data Access](tabular-model-data-access.md).  
  
 Se si utilizza un modello ibrido, è possibile specificare se gli utenti si connettono alla cache o utilizzano dati DirectQuery specificando la proprietà della stringa di connessione, DirectQueryMode.  
  
###  <a name="bkmk_Security"></a> Sicurezza in modalità DirectQuery  
 Durante la creazione del modello si specificano le autorizzazioni utilizzate per recuperare i dati di origine. Si tratterà spesso delle proprie credenziali o di un account utilizzato per lo sviluppo. Tuttavia, quando si imposta il modello sulla modalità DirectQuery, il contesto di sicurezza è più complesso:  
  
-   Valutare se gli utenti dispongono del livello necessario di accesso ai dati nell'archivio dati relazionale.  
  
-   Gli utenti che visualizzano lo stesso modello o report potrebbero visualizzare dati diversi, a seconda del contesto di sicurezza dell'utente.  
  
-   Se la cache del modello è stata mantenuta, la cache è protetta tramite il modello di sicurezza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ruoli). La cache potrebbe contenere dati visualizzabili dal progettista del modello, ma non dall'utente. Il progettista di modelli e report ha la facoltà di cancellare la cache o di proteggere questi dati controllando l'accesso attraverso i ruoli.  
  
-   Un modello mediante il quale si risponde alle query dalla cache non può rappresentare l'utente corrente in caso di connessione all'origine dati. Se si desidera rappresentare l'utente corrente in caso di connessione all'origine dati, è necessario utilizzare la modalità DirectQuery.  
  
-   Se il modello di report richiede sicurezza, sono disponibili due opzioni: è possibile utilizzare i ruoli di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oppure impostare le autorizzazioni a livello di riga per l'origine dati. La sicurezza nell'origine dati relazionale viene utilizzata per controllare l'accesso alle tabelle e la sicurezza a livello di colonna non è supportata. Di conseguenza, se gli utenti di un'area non dispongono delle autorizzazioni per visualizzare le cifre sulle vendite di altre aree, un report che include una misura basata sulla tabella Sales restituirebbe spazi vuoti o un errore.  
  
 La proprietà delle impostazioni di rappresentazione consente di specificare le credenziali utilizzate per la connessione a un modello utilizzando DirectQuery, per un modello solo DirectQuery o per un modello ibrido che risponde alle query tramite DirectQuery. La proprietà presenta i valori seguenti:  
  
 **Default**  
 Vengono utilizzate le credenziali specificate nell'importazione guidata per connettersi all'origine dati. Può trattarsi di un utente di Windows specifico o dell'account di servizio.  
  
 `ImpersonateCurrentUser`  
 Consente di utilizzare le credenziali dell'utente corrente per connettersi all'origine dati.  
  
 Per informazioni su come impostare queste proprietà, vedere [scenari di distribuzione DirectQuery &#40;modello tabulare di SSAS&#41;](../directquery-deployment-scenarios-ssas-tabular.md).  
  
##  <a name="bkmk_PropertyList"></a> DirectQuery Properties  
 Nella tabella seguente sono elencate le proprietà che è possibile impostare in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] e in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per abilitare DirectQuery e controllare l'origine dei dati utilizzati per le query sul modello.  
  
|Nome proprietà|Descrizione|  
|-------------------|-----------------|  
|**Proprietà DirectQueryMode**|Questa proprietà consente l'utilizzo della modalità DirectQuery in Progettazione modelli. È necessario impostare questa proprietà su `On` per modificare qualsiasi altra proprietà DirectQuery.<br /><br /> Per altre informazioni, vedere [abilitare la modalità DirectQuery &#40;modello tabulare di SSAS&#41;](enable-directquery-mode-in-ssdt.md).|  
|**Proprietà QueryMode**|Questa proprietà specifica il metodo di query predefinito per un modello DirectQuery e può essere impostata in Progettazione modelli durante la distribuzione del modello. In seguito sarà comunque possibile eseguirne l'override. La proprietà presenta questi valori:<br /><br /> **DirectQuery** -specifica tutte le query sul modello devono utilizzare solo l'origine dati relazionale.<br /><br /> **DirectQuery con In memoria** : specifica che, per impostazione predefinita, le risposte alle query verranno fornite usando l'origine relazionale, salvo diversa indicazione nella stringa di connessione del client.<br /><br /> **In memoria** : specifica che le risposte alle query verranno fornite usando solo la cache.<br /><br /> **In memoria con DirectQuery** : specifica che, per impostazione predefinita, le risposte alle query verranno fornite utilizzando la cache, salvo diversa indicazione nella stringa di connessione del client.<br /><br /> <br /><br /> Per altre informazioni, vedere [Impostare o modificare il metodo di connessione preferito per DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).|  
|**Proprietà DirectQueryMode**|Dopo avere distribuito il modello, è possibile modificare l'origine dati delle query preferita per un modello DirectQuery, impostando questa proprietà in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]<br /><br /> Analogamente alla proprietà precedente, questa proprietà specifica l'origine dati predefinita per il modello e presenta questi valori:<br /><br /> **InMemory**: Le query possono utilizzare solo la cache.<br /><br /> **DirectQuerywithInMemory**: le query usano l'origine dati relazionale per impostazione predefinita, salvo diversa indicazione nella stringa di connessione del client.<br /><br /> **InMemorywithDirectQuery**: le query usano la cache per impostazione predefinita, salvo diversa indicazione nella stringa di connessione del client.<br /><br /> (**DirectQuery**: le query usano solo l'origine dati relazionale.<br /><br /> <br /><br /> Per altre informazioni, vedere [Impostare o modificare il metodo di connessione preferito per DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).|  
|**Proprietà delle impostazioni di rappresentazione**|Questa proprietà definisce le credenziali utilizzate per la connessione all'origine dati SQL Server in fase di esecuzione query. È possibile impostare questa proprietà in Progettazione modelli e modificarne in seguito il valore, dopo la distribuzione del modello.<br /><br /> Si noti che queste credenziali vengono utilizzate unicamente per rispondere alle query sull'archivio dati relazionale. Non corrispondono alle credenziali utilizzate per l'elaborazione della cache di un modello ibrido.<br /><br /> La rappresentazione non può essere utilizzata se il modello viene utilizzato solo in memoria. L'impostazione `ImpersonateCurrentUser` non è valida, a meno che il modello non utilizzi la modalità DirectQuery.|  
  
 Inoltre, se il modello include partizioni, è necessario scegliere una partizione da utilizzare come origine per le query in modalità DirectQuery. Per altre informazioni, vedere [partizioni e modalità DirectQuery &#40;modello tabulare di SSAS&#41;](define-partitions-in-directquery-models-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Attività e argomenti correlati  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Partizioni e modalità DirectQuery &#40;tabulare di SSAS&#41;](define-partitions-in-directquery-models-ssas-tabular.md)|Viene illustrato l'utilizzo delle partizioni nei modelli configurati per la modalità DirectQuery.|  
|[Compatibilità delle formule DAX in modalità DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|Vengono illustrati i requisiti di compatibilità e le restrizioni riguardanti le formule che è possibile utilizzare nei modelli configurati per la modalità DirectQuery.|  
|[Abilitare la modalità di progettazione DirectQuery &#40;tabulare di SSAS&#41;](enable-directquery-mode-in-ssdt.md)|Viene illustrato come modificare l'ambiente di progettazione in modo che supporti l'utilizzo della modalità DirectQuery.|  
|[Modificare la partizione DirectQuery &#40;tabulare di SSAS&#41;](../change-the-directquery-partition-ssas-tabular.md)|Viene illustrato come modificare la partizione DirectQuery.|  
|[Impostare o modificare il metodo di connessione preferito per DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md)|Viene illustrato come impostare o modificare il metodo di connessione per i modelli configurati per DirectQuery.|  
|[Scenari di distribuzione DirectQuery &#40;tabulare di SSAS&#41;](../directquery-deployment-scenarios-ssas-tabular.md)|Vengono illustrati gli scenari di distribuzione di DirectQuery|  
|[Configurare l'accesso in memoria o DirectQuery per un database di modello tabulare](enable-directquery-mode-in-ssms.md)|Esaminare le configurazioni di DirectQuery|  
|[Cancellare le cache di Analysis Services](../instances/clear-the-analysis-services-caches.md)|Cancellare la cache del modello tabulare|  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni &#40;SSAS tabulare&#41;](partitions-ssas-tabular.md)   
 [Progetti di modello tabulare &#40;SSAS tabulare&#41;](tabular-model-projects-ssas-tabular.md)   
 [Analizzare in Excel &#40;SSAS tabulare&#41;](analyze-in-excel-ssas-tabular.md)  
