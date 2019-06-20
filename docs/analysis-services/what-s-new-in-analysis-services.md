---
title: Che cosa sono le novità di SQL Server 2016 Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: de2ac80a10e66ed7673a65428c4bfa011d31b534
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263278"
---
# <a name="what39s-new-in-analysis-services"></a>Cosa&#39;s New in Analysis Services
[!INCLUDE[ssas-appliesto-sql2016](../includes/ssas-appliesto-sql2016.md)]

SQL Server 2016 Analysis Services include molti miglioramenti che prestazioni migliorate, più semplice la creazione di soluzioni, gestione automatizzate dei database, relazioni avanzate con, il filtro incrociato bidirezionale in parallelo l'elaborazione della partizione, e e altro ancora. L'elemento centrale per la maggior parte dei miglioramenti apportati in questa versione è il nuovo livello di compatibilità 1200 per i database modello tabulari.     

## <a name="azure-analysis-services"></a>Azure Analysis Services
Annunciato in occasione della 2016 SQL PASS Conference, Analysis Services è ora disponibile nel cloud come servizio di Azure. **Azure Analysis Services** supporta modelli tabulari a livello di compatibilità 1200 e versioni successive. DirectQuery, partizioni, sicurezza a livello di riga, relazioni bidirezionali e traduzioni sono tutte funzioni supportate. Per altre informazioni e per una prova gratuita, vedere [Azure Analysis Services](http://azure.microsoft.com/services/analysis-services/). 

## <a name="whats-new-in-sql-server-2016-service-pack-1-sp1-analysis-services"></a>Novità di SQL Server 2016 Service Pack 1 (SP1) Analysis Services

[Pagina di download di SQL Server 2016 SP1](http://www.microsoft.com/download/details.aspx?id=54276) 

SQL Server 2016 Service SP1 Analysis Services offre livelli più elevati di prestazioni e scalabilità grazie alla compatibilità NUMA (Non-Uniform Memory Access) e all'allocazione ottimizzata della memoria in base a **Intel Threading Building Blocks** (Intel TBB). Queste nuove funzionalità consentono di ridurre il costo totale di proprietà (TCO) fornendo il supporto di più utenti su un numero minore di server aziendali più potenti. 

In particolare, le funzionalità di SQL Server 2016 SP1 Analysis Services offrono miglioramenti in queste aree chiave:

-   **Compatibilità NUMA** : per un migliore supporto dell'architettura NUMA, il motore in memoria (VertiPaq) incluso in Analysis Services gestisce ora una coda di processi separata su ogni nodo NUMA. In questo modo, i processi di analisi dei segmenti vengono eseguiti sullo stesso nodo in cui è allocata la memoria per i dati dei segmenti. Si noti che la compatibilità NUMA è abilitata per impostazione predefinita solo nei sistemi con almeno quattro nodi NUMA. Nei sistemi a due nodi, i costi di accesso remoto allocati di memoria a livello generale non coprono l'overhead di gestione delle specifiche NUMA.
-   **Allocazione della memoria** : Analysis Services è stato accelerato con Intel Threading Building Blocks, un allocatore scalabile che fornisce pool di memoria separati per ogni core. Con l'aumento del numero di core, il sistema può essere scalato in modo quasi lineare.
-   **Frammentazione dell'heap** : l'allocatore scalabile basato su Intel TBB consente anche di attenuare i problemi di prestazioni dovuti alla frammentazione dell'heap che sono stati riscontrati per l'heap di Windows.

I test di prestazioni e scalabilità hanno mostrato miglioramenti significativi nella velocità di esecuzione delle query quando SQL Server 2016 SP1 Analysis Services viene eseguito su server aziendali di grandi dimensioni con più nodi.


## <a name="whats-new-in-sql-server-2016-analysis-services"></a>Che cosa sono le novità di SQL Server 2016 Analysis Services

Anche se la maggior parte dei miglioramenti presenti in questa versione sono specifici per i modelli tabulari, è stata apportata una serie di miglioramenti ai modelli multidimensionali: ottimizzazione ROLAP Distinct Count per origini dati quali DB2 e Oracle, supporto del drill-through con selezione multipla con Excel 2016 e ottimizzazioni per le query Excel.    

#### <a name="get-the-latest-tools"></a>Ottenere gli strumenti più recenti
Per poter sfruttare tutti i miglioramenti in questa versione, assicurarsi di installare le versioni più recenti di SSDT e SSMS.    
- [Scaricare SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)    
- [Scaricare SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)   

Se è disponibile un'applicazione personalizzata dipendente da AMO, potrebbe essere necessario installare una versione aggiornata della libreria AMO. Per istruzioni, vedere [Installare il provider di dati di Analysis Services &#40;AMO, ADOMD.NET, MSOLAP&#41;](../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md).    

## <a name="modeling"></a>Modellazione    
### <a name="improved-modeling-performance-for-tabular-1200-models"></a>Miglioramento delle prestazioni di modellazione per i modelli tabulari 1200    
Per i modelli tabulari 1200 le operazioni sui metadati in SSDT risultano molto più veloci rispetto ai modelli tabulari 1100 o 1103. A scopo di confronto, nello stesso hardware la creazione di una relazione in un modello impostato sul livello di compatibilità di SQL Server 2014 (1103) con 23 tabelle richiede 3 secondi, mentre la stessa relazione in un modello creato impostato sul livello di compatibilità 1200 richiede poco meno di un secondo.    
### <a name="project-templates-added-for-tabular-1200-models-in-ssdt"></a>Modelli di progetto aggiunti per i modelli tabulari 1200 in SSDT    
A partire da questa versione, non sono più necessarie due versioni di SSDT per la compilazione di progetti relazionali e di Business Intelligence. [SQL Server Data Tools per Visual Studio 2015](http://msdn.microsoft.com/library/mt204009.aspx) aggiunge modelli di progetto per le soluzioni di Analysis Services, inclusi i **progetti tabulari di Analysis Services** usati per la compilazione di modelli a livello di compatibilità 1200. Sono inclusi anche altri modelli di progetto di Analysis Services per soluzioni di data mining e multidimensionali, ma allo stesso livello di funzionalità 1100 o 1103 delle versioni precedenti.    
### <a name="display-folders"></a>Cartelle di visualizzazione
Ora sono disponibili le cartelle di visualizzazione per i modelli tabulari 1200. Le cartelle di visualizzazione, definite in SQL Server Data Tools e di cui viene eseguito il rendering in applicazioni client quali Excel o Power BI Desktop, consentono di organizzare un numero elevato di misure in singole cartelle, aggiungendo una gerarchia visiva per semplificare la navigazione tra gli elenchi di campi.
### <a name="bi-directional-cross-filtering"></a>Filtri incrociati bidirezionali
La novità di questa versione è un approccio predefinito per l'abilitazione dei filtri incrociati bidirezionali nei modelli tabulari, eliminando in questo modo la necessità di prevedere soluzioni DAX personalizzate per la propagazione del contesto di filtro nelle relazioni tra tabelle. I filtri vengono generati automaticamente solo quando è possibile stabilire la direzione con un livello di attendibilità elevato. In caso di ambiguità sotto forma di più percorsi di query tra le relazioni tra tabelle, i filtri non vengono creati automaticamente. Per informazioni dettagliate, vedere [Filtri incrociati bidirezionali per i modelli tabulari in SQL Server 2016 Analysis Services](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) .
 ### <a name="translations"></a>Traduzioni    
 È ora possibile archiviare metadati tradotti in un modello tabulare 1200. I metadati del modello includono campi per **Culture**e per didascalie e descrizioni tradotte. Per aggiungere traduzioni, usare il comando **Modello** > **Traduzioni** in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Per informazioni dettagliate, vedere [Traduzioni in modelli tabulari &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md).    
 ### <a name="pasted-tables"></a>Tabelle incollate    
 Ora è possibile eseguire l'aggiornamento di un modello tabulare 1100 o 1103 al livello 1200 quando il modello contiene tabelle incollate. È consigliabile usare [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. In SSDT impostare **CompatibilityLevel** su 1200 e distribuirlo in un'istanza di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per informazioni dettagliate, vedere [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) .    
 ### <a name="calculated-tables-in-ssdt"></a>Tabelle calcolate in SSDT    
Una *tabella calcolata* è una costruzione solo modello basata su una query o un'espressione DAX in SSDT. Quando viene distribuita in un database, una tabella calcolata non è distinguibile dalle tabelle normali.    

 Le tabelle calcolate possono essere usate per diversi scopi, inclusa la creazione di nuove tabelle per esporre una tabella esistente in un ruolo specifico. L'esempio tipico è una tabella data che opera in più contesti, ovvero data dell'ordine, data di spedizione e così via. La creazione di una colonna calcolata per un determinato ruolo permette ora di attivare una relazione tra tabelle per semplificare le query o l'interazione dei dati tramite la tabella calcolata. Le tabelle calcolate possono essere usate anche per combinare parti di tabelle esistenti in una tabella completamente nuova che esiste solo nel modello.  Visualizzare [creare una tabella calcolata](../analysis-services/tabular-models/create-a-calculated-table-ssas-tabular.md) per altre informazioni.    
 ### <a name="formula-fixup"></a>Correzione della formula    
 Con la correzione della formula in un modello tabulare 1200, SSDT aggiorna automaticamente qualsiasi misura che faccia riferimento a una colonna o una tabella che è stata rinominata.    
 ### <a name="support-for-visual-studio-configuration-manager"></a>Supporto per Gestione configurazione di Visual Studio    
 Per supportare più ambienti, ad esempio di testing e di preproduzione, Visual Studio consente agli sviluppatori di creare più configurazioni di progetto usando Gestione configurazione. È già usato nei modelli multidimensionali, ma non nei modelli tabulari. A partire da questa versione, è possibile usare Gestione configurazione per la distribuzione in server diversi.    

## <a name="instance-management"></a>Gestione di un'istanza    
 ### <a name="administer-tabular-1200-models-in-ssms"></a>È possibile amministrare i modelli tabulari 1200 in SSMS    
 In questa versione, un'istanza di Analysis Services in modalità server tabulare può eseguire modelli tabulari a qualsiasi livello di compatibilità (1100, 1103 o 1200). La versione più recente di [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) è stata aggiornata per la visualizzazione delle proprietà e l'amministrazione del modello di database per i modelli tabulari a livello di compatibilità 1200.    
 ### <a name="parallel-processing-for-multiple-table-partitions-in-tabular-models"></a>Elaborazione parallela per più partizioni di tabella nei modelli tabulari    
 Questa versione include una nuova funzionalità di elaborazione parallela per le tabelle con due o più partizioni e garantisce così un miglioramento delle prestazioni di elaborazione. Per questa funzionalità non sono previste impostazioni di configurazione. Per altre informazioni sulla configurazione di partizioni e l'elaborazione di tabelle, vedere [partizioni di modelli tabulari](../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md).    
 ### <a name="add-computer-accounts-as-administrators-in-ssms"></a>Aggiunta di account computer come amministratori in SSMS    
 Gli amministratori di[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] possono ora usare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per configurare gli account di computer come membri del gruppo Administrators di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Nella finestra di dialogo **Seleziona utenti o gruppi** impostare i **Percorsi** dei domini dei computer e quindi aggiungere il tipo di oggetto **Computers** . Per altre informazioni, vedere [Concedere i diritti di amministratore del server a un'istanza di Analysis Services](../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).    
 ### <a name="dbcc-for-analysis-services"></a>DBCC per Analysis Services    
 La verifica di coerenza del database (DBCC) viene eseguita internamente per rilevare possibili problemi di danneggiamento dei dati in fase di caricamento del database, ma può anche essere eseguita su richiesta, se si sospetta la presenza di problemi nei dati o nel modello. DBCC esegue controlli diversi a seconda che il modello sia tabulare o multidimensionale. Per informazioni dettagliate, vedere [Database Consistency Checker &#40;DBCC&#41; per i database tabulari e multidimensionali di Analysis Services](../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md).    
 ### <a name="extended-events-updates"></a>Aggiornamenti a Eventi estesi    
 Questa versione aggiunge un'interfaccia utente grafica a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per la configurazione e la gestione di Eventi estesi di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . È possibile impostare flussi di dati dinamici per monitorare l'attività del server in tempo reale, mantenere i dati di sessione caricati in memoria per analisi più veloci o salvare i flussi di dati in un file per l'analisi offline. Per altre informazioni, vedere [Monitorare Analysis Services con eventi estesi di SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) e il post di blog e il video di Guy in a Cube sull' [uso di Eventi estesi con Analysis Services](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx).    



## <a name="scripting"></a>Scripting
 ### <a name="powershell-for-tabular-models"></a>PowerShell per i modelli tabulari    
 Questa versione include miglioramenti di PowerShell per i modelli tabulari con livello di compatibilità 1200. È possibile usare tutti i cmdlet applicabili, nonché cmdlet specifici per la modalità tabulare: [Invoke-ProcessASDatabase](../analysis-services/powershell/invoke-processasdatabase.md) e [cmdlet Invoke-ProcessTable](../analysis-services/powershell/invoke-processtable-cmdlet.md).    
 ### <a name="ssms-scripting-database-operations"></a>Operazioni di scripting del database di SSMS    
 Nella [versione più recente di SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)è ora abilitato uno script per i comandi di database, tra cui quelli di creazione, modifica, eliminazione, backup, ripristino, collegamento e scollegamento. L'output è il linguaggio di scripting del modello tabulare (Tabular Model Scripting Language, TMSL) in JSON. Per altre informazioni, vedere [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Riferimento al linguaggio di scripting per modelli tabulari &#40;TMSL&#41;)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference).    
 ### <a name="analysis-services-execute-ddl-task"></a>Attività Esegui DDL Analysis Services    
 L'[Attività Esegui DDL Analysis Services](../integration-services/control-flow/analysis-services-execute-ddl-task.md) ora accetta i comandi TMSL (Tabular Model Scripting Language).     
 ### <a name="ssas-powershell-cmdlet"></a>cmdlet di PowerShell per SSAS    
 Il cmdlet di PowerShell per SSAS **Invoke-ASCmd** ora accetta i comandi TMSL (Tabular Model Scripting Language). Altri cmdlet di PowerShell per SSAS potrebbero essere aggiornati in una versione futura per l'uso dei nuovi metadati tabulari e le eccezioni verranno segnalate nelle note di rilascio.    
Per informazioni dettagliate, vedere [Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) .    
 ### <a name="tabular-model-scripting-language-tmsl-supported-in-ssms"></a>Supporto per TMSL (Tabular Model Scripting Language) in SSMS    
  Usando la [versione più recente di SSMS](http://msdn.microsoft.com/library/mt238290.aspx), è ora possibile creare script per automatizzare la maggior parte delle attività amministrative per i modelli tabulari 1200. Attualmente, è possibile creare le attività seguenti script: Processo in qualsiasi livello, oltre a CREATE, ALTER, eliminare a livello di database.    
    
 A livello funzionale, il linguaggio TMSL equivale all'estensione ASSL XMLA che fornisce le definizioni degli oggetti multidimensionali, ad eccezione del fatto che TMSL usa descrittori nativi come **model**, **table**e **relationship** per descrivere i metadati tabulari. Per informazioni dettagliate sullo schema, vedere [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Riferimento al linguaggio di scripting per modelli tabulari &#40;TMSL&#41;)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference).    
    
 Uno script generato basato su JSON per un modello tabulare avrà un aspetto simile al seguente:    
    
```    
{    
  "create": {    
    "database": { 
      "name": "AdventureWorksTabular1200",    
      "id": "AdventureWorksTabular1200",    
      "compatibilityLevel": 1200,    
      "readWriteMode": "readWrite",    
      "model": {}    
    }    
  }    
}    
```    

Il payload è un documento JSON che può essere minimo, come nell'esempio illustrato in precedenza, o dotato di un set completo di definizioni di oggetti. L'articolo [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Riferimento al linguaggio di scripting per modelli tabulari &#40;TMSL&#41;)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) descrive la sintassi.

A livello di database, i comandi CREATE, ALTER e DELETE restituiscono script TMSL nella finestra XMLA classica.  In questa versione è possibile generare script anche di altri comandi, ad esempio, Process. Per molte altre azioni il supporto per gli script potrebbe essere aggiunto in una versione futura.    

**Comandi gestibili tramite script** | **Descrizione**
--------------- | ----------------
create|Aggiunge un database, una connessione o una partizione. L'equivalente ASSL è CREATE.
createOrReplace|Aggiorna una definizione di oggetto esistente (database, connessione o partizione) sovrascrivendo una versione precedente. L'equivalente ASSL è ALTER con AllowOverwrite impostato su true e ObjectDefinition impostato su ExpandFull.
delete|Rimuove una definizione di oggetto. L'equivalente ASSL è DELETE.
refresh|Elabora l'oggetto. L'equivalente ASSL è PROCESS.

## <a name="dax"></a>DAX
### <a name="improved-dax-formula-editing"></a>Modifica migliorata della formula DAX
Gli aggiornamenti apportati alla barra della formula consentono di scrivere formule più facilmente differenziando le funzioni, i campi e le misure con la colorazione della sintassi. I suggerimenti intelligenti relativi a campi e funzioni segnalano le parti errate dell'espressione DAX con le *sottolineature*. Ora è anche possibile usare più righe (ALT+INVIO) e il rientro (TAB). La barra della formula ora consente inoltre di scrivere commenti come parte di misure, è sufficiente digitare "/ /" e tutto ciò che segue questi caratteri sulla stessa riga verranno considerati un commento.

### <a name="dax-variables"></a>Variabili DAX    
Questa versione ora include il supporto per le variabili in DAX. Ora le variabili possono archiviare il risultato di un'espressione come variabile denominata, che può essere passata come argomento ad altre espressioni di misura. Dopo aver calcolato i valori risultanti per un'espressione variabile, non tali valori non cambiano, anche se viene fatto riferimento alla variabile in un'altra espressione. Per altre informazioni, vedere la [funzione VAR](/dax/var-dax).    
### <a name="new-dax-functions"></a>Nuove funzioni DAX
Con questa versione, in DAX sono state introdotte più di cinquanta nuove funzioni per supportare calcoli più rapidi e visualizzazioni migliorate in Power BI. Per altre informazioni, vedere [Nuove funzioni DAX](/dax/new-dax-functions).
### <a name="save-incomplete-measures"></a>Salvataggio di misure incomplete
Ora è possibile salvare le misure DAX incomplete direttamente in un progetto di modello tabulare 1200 e riprenderle quando si è pronti per continuare.
### <a name="additional-dax-enhancements"></a>Altri miglioramenti di DAX
- Calcolo dei valori non vuoti - Riduce il numero di analisi necessarie per i valori non vuoti.
- Fusione delle misure - Più misure dalla stessa tabella vengono combinate in un singolo motore di archiviazione o una query.
- Set di raggruppamenti - Quando una query richiede misure con più granularità (totale/mese/anno), viene inviata una singola query al livello inferiore e il resto delle granularità viene derivato dal livello più basso.     
- Eliminazione di join ridondanti - Una singola query al motore di archiviazione restituisce le colonne della dimensione e i valori delle misure.
- Valutazione restrittiva di IF/SWITCH - Un ramo con una condizione false non comporterà più query del motore di archiviazione. In precedenza, i rami venivano valutati rapidamente ma i risultati erano scartati in un secondo momento.     
    
## <a name="developer"></a>Sviluppatore    
 ### <a name="microsoftanalysisservicestabular-namespace-for-tabular-1200-programmability-in-amo"></a>Spazio dei nomi Microsoft.AnalysisServices.Tabular per la programmabilità tabulare a livello 1200 in AMO
 Analysis Services Management Objects (AMO) viene aggiornato per includere un nuovo spazio dei nomi tabulare per la gestione di un'istanza in modalità tabulare di SQL Server 2016 Analysis Services e fornire il linguaggio DDL (Data Definition Language) per la creazione o la modifica di modelli tabulari 1200 a livello di codice. Per informazioni sull'API, vedere [Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) .    
 ### <a name="analysis-services-management-objects-amo-updates"></a>Aggiornamenti di Analysis Services Management Objects (AMO)
 È stato eseguito il refactoring di [Analysis Services Management Objects &#40;AMO&#41;](http://msdn.microsoft.com/library/mt436122.aspx) per includere un secondo assembly, Microsoft.AnalysisServices.Core.dll. Il nuovo assembly separa le classi comuni come Server, Database e Role che hanno un utilizzo diversificato in Analysis Services, indipendentemente dalla modalità del server.    
    
 Queste classi in precedenza facevano parte dell'assembly Microsoft.AnalysisServices originale. Lo spostamento in un nuovo assembly apre la strada a future estensioni di AMO, con una distinzione netta tra API generiche e API specifiche del contesto.    
    
 I nuovi assembly non influiscono sulle applicazioni esistenti. Tuttavia, se per qualsiasi motivo si sceglie di ricompilare le applicazioni usando il nuovo assembly AMO, assicurarsi di aggiungere un riferimento a Microsoft.AnalysisServices.Core.    
    
 Analogamente, gli script di PowerShell che chiamano AMO e vengono caricati al suo interno ora devono caricare Microsoft.AnalysisServices.Core.dll. Assicurarsi di aggiornare gli script.  

### <a name="json-editor-for-bim-files"></a>Editor JSON per file BIM
La vista Codice in Visual Studio 2015 ora esegue il rendering dei file BIM in formato JSON per i modelli tabulari 1200. La versione di Visual Studio determina il rendering del file BIM in JSON tramite l'editor JSON incorporato oppure come testo normale.

Per usare l'editor JSON, con la possibilità di espandere e comprimere le sezioni del modello, è necessaria la versione più recente di SQL Server Data Tools con una qualsiasi edizione di Visual Studio 2015, inclusa l'edizione Community gratuita. Per tutte le altre versioni di SSDT o Visual Studio, il file BIM viene visualizzato in JSON come testo normale.
Un modello vuoto contiene almeno il codice JSON seguente:

    ```    
    {    
      "name": "SemanticModel",
      "id": "SemanticModel",
      "compatibilityLevel": 1200,
      "readWriteMode": "readWrite",
      "model": {}
    }    
    ```    
    
> [!WARNING]
> Evitare di modificare direttamente il codice JSON, perché ciò può danneggiare il modello.    
>  ### <a name="new-elements-in-ms-csdlbi-20-schema"></a>Nuovi elementi nello schema MS-CSDLBI 2.0    
>  Gli elementi seguenti sono stati aggiunti al tipo complesso **TProperty** definito nello schema [MS-CSDLBI] 2.0:    
    
|Elemento|Definizione|    
|-------------|----------------|    
|DefaultValue|Proprietà che specifica il valore usato durante la valutazione della query. La proprietà DefaultValue è facoltativa, ma viene selezionata automaticamente se non è possibile aggregare i valori del membro.|    
|Statistiche|Set di statistiche dei dati sottostanti associati alla colonna. Le statistiche sono definite dal tipo complesso TPropertyStatistics e vengono fornite solo se la relativa generazione non risulta dispendiosa a livello di calcolo, come descritto nella sezione 2.1.13.5 del documento relativo al formato di file di Conceptual Schema Definition con annotazioni Business Intelligence.|    
    
## <a name="directquery"></a>DirectQuery    
### <a name="new-directquery-implementation"></a>Nuova implementazione di DirectQuery    
In questa versione sono stati apportati miglioramenti significativi a DirectQuery per i modelli tabulari 1200. Ecco un riepilogo:    
-   DirectQuery ora genera query più semplici che offrono prestazioni migliori.    
-   Maggiore controllo sulla definizione di set di dati di esempio usati per la progettazione e il testing dei modelli.    
-   La sicurezza a livello di riga è ora supportata per i modelli tabulari 1200 in modalità DirectQuery. In precedenza la presenza della sicurezza a livello di riga impediva di eseguire un modello tabulare in modalità DirectQuery.    
-   Le colonne calcolate non sono supportate per i modelli tabulari 1200 in modalità DirectQuery. In precedenza la presenza delle colonne calcolate impediva di distribuire un modello tabulare in modalità DirectQuery.    
-   Le ottimizzazioni delle prestazioni includono l'eliminazione di join ridondanti per VertiPaq e DirectQuery. 

### <a name="new-data-sources-for-directquery-mode"></a>Nuove origini dati per la modalità DirectQuery    
 Origini dati supportate per i modelli tabulari 1200 in modalità DirectQuery ora includono Oracle, Teradata e la piattaforma Analitica Microsoft (precedentemente noto come Parallel Data Warehouse).    
    
Per altre informazioni, vedere [la modalità DirectQuery](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).    

## <a name="see-also"></a>Vedere anche
[Blog del team di Analysis Services](http://blogs.msdn.microsoft.com/analysisservices/)    
[Novità di SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)    
     

