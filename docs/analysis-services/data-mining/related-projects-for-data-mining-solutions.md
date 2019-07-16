---
title: Progetti correlati per soluzioni di Data Mining | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 103d0a724fa3abeae61441f64dd763424e9454e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68182427"
---
# <a name="related-projects-for-data-mining-solutions"></a>Progetti correlati per soluzioni di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Come minimo, per una soluzione di data mining è richiesto il progetto di data mining, in cui si definiscono origini dati, viste origine dati, strutture di data mining e modelli di data mining. Tuttavia, quando i modelli di data mining vengono utilizzati nei processi decisionali quotidiani, è importante che il data mining sia integrato con altre parti di una soluzione analitica predittiva, che può includere i seguenti processi e componenti:  
  
-   Preparazione e selezione di dati e variabili. Include pulizia dei dati, gestione di metadati e integrazione di più origini dati, nonché la conversione, l'unione e il caricamento di dati in un data warehouse.  
  
-   Report di analisi, presentazione di stime e controllo e rilevamento delle attività di data mining.  
  
-   Utilizzo di modelli multidimensionali o tabulari per esplorare i risultati.  
  
-   Perfezionamento della soluzione di data mining per supportare nuovi dati o modifiche nell'infrastruttura di supporto derivanti dall'analisi corrente.  
  
 In questo argomento vengono descritte le altre funzionalità di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] che fanno spesso parte di una soluzione analitica predittiva, per supportare i processi di preparazione dei dati e di data mining o assistere gli utenti fornendo strumenti per l'analisi e l'azione.  
  
 [Integration Services](#bkmk_SSIS)  
  
 [Reporting Services](#bkmk_SSRS)  
  
 [Data Quality Services](#bkmk_DQSetc)  
  
 [Ricerca full-text](#bkmk_FTSetc)  
  
 [Indicizzazione semantica](#bkmk_SemSearch)  
  
##  <a name="bkmk_SSIS"></a> SQL Server Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] vengono forniti componenti e funzionalità richiesti per le fasi di preparazione dei dati e di training di un progetto di data mining. Benché sia possibile eseguire molte attività di pulizia o preparazione dei dati tramite altri strumenti, ad esempio gli script, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] offre numerosi vantaggi per il data mining:  
  
-   Rappresenta le attività come parte di un flusso di lavoro che può essere ripetuto, automatizzato, ramificato ed esteso.  
  
-   Viene fornito ampio supporto per il controllo e diverse modalità di acquisizione degli errori e registrazione degli eventi.  
  
     Oltre all'acquisizione della derivazione dei dati, è possibile monitorare le modifiche apportate ai dati per l'intera pipeline per la trasformazione dei dati.  
  
     È inoltre possibile integrare i flussi di lavoro SSIS con le funzionalità che supportano la funzionalità Change Data Capture di SQL Server.  
  
-   È possibile incorporare il data mining nel flusso di lavoro di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , per separare in modo intelligente i dati in ingresso in più tabelle. Ad esempio, è possibile utilizzare una query di stima per suddividere i nuovi clienti in gruppi diversi come destinazione di una campagna di mailing.  
  
 Negli elenchi seguenti vengono forniti collegamenti ai componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizzati maggiormente a supporto del data mining.  
  
 **Componenti del flusso di controllo**  
  
-   [Attività Esegui DDL Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Attività Elaborazione Analysis Services](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [Attività di controllo CDC](../../integration-services/control-flow/cdc-control-task.md)  
  
-   [Pulizia dei dati](../../data-quality-services/data-cleansing.md)  
  
-   [Attività Query di data mining](../../integration-services/control-flow/data-mining-query-task.md)  
  
-   [Attività Profiling dati](../../integration-services/control-flow/data-profiling-task.md)  
  
 **Componenti del flusso di dati**  
  
-   [Componenti di flusso CDC](../../integration-services/data-flow/cdc-flow-components.md)  
  
-   [Trasformazione Suddivisione condizionale](../../integration-services/data-flow/transformations/conditional-split-transformation.md)  
  
-   [Trasformazione Conversione dati](../../integration-services/data-flow/transformations/data-conversion-transformation.md)  
  
-   [Destinazione Training modello di data mining](../../integration-services/data-flow/data-mining-model-training-destination.md)  
  
-   [Trasformazione Query di data mining](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)  
  
-   [Trasformazione Colonna derivata](../../integration-services/data-flow/transformations/derived-column-transformation.md)  
  
-   [Trasformazione Campionamento percentuale](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
-   [Trasformazione Estrazione termini](../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
-   [Trasformazione Ricerca termini](../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
##  <a name="bkmk_SSRS"></a> SQL Server Reporting Services  
 Benché [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non sia in genere considerato un componente critico delle soluzioni di data mining, fornisce le seguenti funzionalità utili per la presentazione di soluzioni di data mining.  
  
-   Integrazione di dati da più origini in report complessi. Creazione di query rispetto al contenuto del modello per gli analisti e di report che mostrano stime e tendenze per gli utenti finali.  
  
-   Possibilità di creare un report che consenta agli utenti di eseguire direttamente le query su un modello di data mining esistente.  
  
-   Integrazione con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]per supportare drill-through ed esplorazione di dimensioni di data mining e cubi di data mining creati da modelli OLAP.  
  
-   Parametrizzazione e funzionalità di formattazione disponibili in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Per ulteriori informazioni sull'utilizzo di Reporting Services con query DMX come origine dati, vedere i collegamenti seguenti:  
  
 [Recuperare i dati da un modello di data mining &#40;DMX&#41; &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)  
  
 [Interfaccia utente di Progettazione query DMX in Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
 [Tipo di connessione di Analysis Services per DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
 Tuttavia, non è necessario utilizzare DMX come origine dati. I componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per il data mining supportano inoltre il salvataggio dei risultati di una query di stima in un database relazionale. Se si dispone di un flusso di lavoro stabilito per l'aggiornamento di modelli tramite [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], l'impostazione della persistenza di stime e altri risultati di query di data mining in SQL Server consente di utilizzare [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] per la creazione di report, nonché altri strumenti non interfacciati con DMX.  
  
 Per ulteriori informazioni sull'utilizzo di Reporting Services come livello di presentazione per le origini dati, vedere [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md).  
  
##  <a name="bkmk_DQSetc"></a> Data Quality Services  
 Data Quality Services (DQS) è una novità in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Poiché i problemi relativi ai dati possono impedire il data mining, è probabile che i data miner che eseguono analisi ripetute o lavorano in organizzazioni di grandi dimensioni con origini dati complesse ritengano che un progetto di dati ben pianificato basato su DQS sia una soluzione di data mining più affidabile rispetto alla pulizia ad hoc dei dati tramite [!INCLUDE[tsql](../../includes/tsql-md.md)] o altri script.  
  
 È opportuno considerare le funzionalità seguenti di DQS per la preparazione e l'integrità dei dati in una soluzione di data mining.  
  
 **Processo di pulizia dei dati assistito da computer tramite cui vengono analizzati i dati di origine e proposte modifiche.**  
 Con DQS è possibile confrontare i dati di origine con dati di riferimento basati su cloud gestiti e garantiti da provider di qualità dei dati.  
  
 In DQS è inoltre possibile analizzare dati di origine non elaborati e creare una Knowledge Base dai dati dell'utente. I dati elaborati sono suddivisi in categorie, quindi visualizzati all'utente per ulteriore elaborazione. Il processo di pulizia è interattivo, pertanto l'amministratore dei dati può approvare, rifiutare o modificare i dati proposti dal processo di pulizia assistito da computer.  
  
 Il risultato del processo è una Knowledge Base che è possibile migliorare continuamente o riutilizzare in più fasi di miglioramento dei dati.  
  
 Per altre informazioni, vedere [Data Cleansing](../../data-quality-services/data-cleansing.md).  
  
 **Processo di individuazione delle corrispondenze assistito da computer tramite cui vengono analizzati i dati di origine e proposte modifiche.**  
 Per evitare la duplicazione dei dati, è possibile eseguire pulizie aggiuntive dell'origine dati per identificare corrispondenze esatte e approssimative. Questi componenti consentono di specificare le regole di corrispondenza e le soglie di applicazione.  
  
 L'individuazione delle corrispondenze di dati consente di rimuovere duplicati che possono costituire un problema per il data mining. La deduplicazione dei dati non è automatica; l'amministratore dei dati o un professionista IT deve verificare sia le informazioni della Knowledge Base sia le modifiche da apportare ai dati.  
  
 Dopo avere creato il progetto DQS iniziale, è possibile automatizzare molte attività tramite i componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Per altre informazioni, vedere [Data Matching](../../data-quality-services/data-matching.md).  
  
 Durante l'esecuzione delle attività di pulizia e corrispondenza in un progetto di qualità dei dati, è possibile ottenere statistiche e informazioni in tempo reale sui dati elaborati da DQS. Il profiling dati consente di valutare a che livello la qualità dei dati è stata migliorata grazie alla pulizia o all'individuazione di corrispondenze dei dati e comprendere le modifiche apportate. Per ulteriori informazioni sul profiling dati e le notifiche, vedere [Data Profiling and Notifications in DQS](../../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
 **Una Knowledge Base che rappresenta tre tipi di conoscenza: conoscenza pronta all'uso, conoscenza generata dal server DQS e conoscenza generata dall'utente.**  
 Una volta creata una Knowledge Base, è possibile utilizzarla in modo iterativo per pulire e verificare altri dati.  
  
 È possibile importare nuovi dati nella Knowledge Base da più origini, sia dati puliti da provider di riferimento o dati non elaborati corrispondenti ai dati esistenti nella Knowledge Base.  
  
 Per informazioni dettagliate sull'attività di pulizia in un progetto di qualità dei dati, vedere Pulizia dei dati (DQS).  
  
 È inoltre possibile applicare la conoscenza presente nella Knowledge Base ad altre origini, per eseguire la pulizia dei dati all'interno di altri processi. Con questa attività di pulizia dei dati è possibile individuare errori di immissione da parte dell'utente, danni subiti durante la trasmissione o l'archiviazione oppure definizioni del dizionario dei dati non corrispondenti.  
  
 Per altre informazioni, vedere [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
##  <a name="bkmk_FTSetc"></a> Ricerca full-text  
 In SQL Server la ricerca full-text consente ad applicazioni e utenti di eseguire query full-text su dati di tipo carattere in tabelle di SQL Server. Quando la ricerca full-text è abilitata, è possibile eseguire ricerche rispetto a dati di testo migliorati dalle regole specifiche della lingua relative alle diverse forme di una parola o di una frase. È inoltre possibile configurare condizioni di ricerca, ad esempio la distanza tra più termini, e utilizzare funzioni per vincolare i risultati restituiti in ordine di probabilità.  
  
 Poiché le query full-text sono una funzionalità fornita dal motore di SQL Server, è possibile creare query con parametri, generare set di dati personalizzati o vettori di termini tramite funzionalità di ricerca full-text in un'origine dati di testo e utilizzare tale origine nel data mining.  
  
 Per altre informazioni sull'interazione delle query full-text con l'indice full-text, vedere [Esecuzione della query con ricerca full-text](../../relational-databases/search/query-with-full-text-search.md).  
  
 Un vantaggio dell'utilizzo delle funzionalità della ricerca full-text di SQL Server è la possibilità di sfruttare l'intelligenza linguistica contenuta nei word breaker e negli stemmer forniti per tutte le lingue di SQL Server. Tramite i word breaker e gli stemmer forniti, è possibile verificare che le parole siano separate utilizzando i caratteri appropriati per ogni lingua e che i sinonimi basati su segni diacritici o variazioni ortografiche (ad esempio i diversi formati numerici in giapponese) non siano trascurati.  
  
 Oltre all'intelligenza linguistica che regola i confini di parola, tramite gli stemmer per ogni lingua è possibile ridurre le varianti di una parola a un solo termine, in base alla conoscenza delle regole di coniugazioni e variazioni ortografiche di tale lingua. Le regole per l'analisi linguistica sono diverse per ogni lingua e sono sviluppate sulla base di ricerche estese su raccolte di testi autentici.  
  
 Per altre informazioni, vedere [Configurare e gestire word breaker e stemmer per la ricerca](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
 La versione di una parola archiviata dopo l'indicizzazione full-text è un token in formato compresso. Le query successive nell'indice full-text generano più formati flessionali di una determinata parola basati sulle regole della lingua specifica, per garantire l'individuazione di tutte le corrispondenze probabili. Ad esempio, anche se il token archiviato può essere "Esegui", il motore di query vengono cercati anche i termini "acquario", "ran" e "runner", perché questi sono variazioni morfologiche derivate regolarmente della parola radice "Esegui".  
  
 È inoltre possibile creare e compilare un thesaurus dell'utente per archiviare sinonimi e migliorare i risultati della ricerca o la categorizzazione dei termini. Sviluppando un thesaurus basato sui dati full-text in uso, è possibile ampliare in modo efficace l'ambito delle query full-text su tali dati. Per altre informazioni, vedere [Configurare e gestire i file del thesaurus per la ricerca full-text](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
 Tra i requisiti per l'utilizzo della ricerca full-text sono inclusi:  
  
-   L'amministratore del database deve creare un indice full-text nella tabella.  
  
-   È consentito un solo indice full-text per tabella.  
  
-   Ogni colonna indicizzata deve disporre di una chiave univoca.  
  
-   L'indicizzazione full-text è supportata solo nelle colonne con i tipi di dati char, varchar, nchar, nvarchar, text, ntext, image, xml, varbinary e varbinary(max). Se la colonna è di tipo varbinary, varbinary(max), image o xml, è necessario specificare l'estensione di file del documento indicizzabile (doc, pdf, xls e così via) in una colonna di tipo separata.  
  
##  <a name="bkmk_SemSearch"></a> Indicizzazione semantica  
 La ricerca semantica è basata sulle funzionalità complete della ricerca full-text esistenti in SQL Server, ma utilizza funzionalità e statistiche aggiuntive per consentire scenari quali l'estrazione automatica di parole chiave e l'individuazione di documenti correlati. Ad esempio, è possibile utilizzare la ricerca semantica per compilare una tassonomia di base per un'organizzazione o per classificare una raccolta di documenti. Inoltre, è possibile utilizzare la combinazione di termini estratti e punteggi di somiglianza dei documenti nei modelli di clustering o albero delle decisioni.  
  
 Dopo avere abilitato correttamente la ricerca semantica e indicizzato le colonne di dati, è possibile utilizzare le funzioni fornite a livello nativo con l'indicizzazione semantica per eseguire le operazioni seguenti:  
  
-   Restituire frasi chiave composte da una singola parola con il relativo punteggio.  
  
-   Restituire documenti che contengono una frase chiave specificata.  
  
-   Restituire punteggi di somiglianza e termini che contribuiscono al punteggio.  
  
 Per altre informazioni, vedere [Trovare frasi chiave nei documenti mediante ricerca semantica](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) e [Trovare documenti simili e correlati tramite la ricerca semantica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
 Per altre informazioni sugli oggetti di database che supportano l'indicizzazione semantica, vedere [Abilitare la ricerca semantica in tabelle e colonne](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md).  
  
 Tra i requisiti per l'utilizzo della ricerca semantica sono inclusi:  
  
-   È necessario abilitare anche la ricerca full-text.  
  
-   L'installazione dei componenti della ricerca semantica crea inoltre un database di sistema speciale che non è possibile rinominare, modificare o sostituire.  
  
-   I documenti indicizzati tramite il servizio devono essere archiviati in SQL Server, in un qualsiasi oggetto di database supportato per l'indicizzazione full-text, incluse tabelle e viste indicizzate.  
  
-   Non tutte le lingue full-text supportano l'indicizzazione semantica. Per un elenco delle lingue supportate, vedere [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Soluzioni di modelli multidimensionali](../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [Soluzioni di modelli tabulari](../../analysis-services/tabular-models/tabular-models-ssas.md)  
  
  
