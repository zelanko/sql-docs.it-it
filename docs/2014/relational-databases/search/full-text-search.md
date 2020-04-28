---
title: Ricerca full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server]
ms.assetid: a0ce315d-f96d-4e5d-b4eb-ff76811cab75
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 61faaa7854aa362e7d269cf3f00911470126f42c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176841"
---
# <a name="full-text-search"></a>Ricerca full-text
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] la ricerca full-text consente a utenti e applicazioni di eseguire query full-text su dati di tipo carattere in tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Affinché le query full-text possano essere eseguite in una determinata tabella, l'amministratore del database deve prima creare un indice full-text nella tabella in questione. L'indice full-text include una o più colonne basate su caratteri nella tabella. In queste colonne possono essere presenti i seguenti tipi di dati: `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, o `varbinary(max)` e FILESTREAM. Ogni indice full-text consente di indicizzare una o più colonne della tabella e ciascuna colonna può essere utilizzata con una lingua specifica.

 Attraverso le query full-text è possibile eseguire ricerche linguistiche rispetto ai dati di testo contenuti negli indici full-text, utilizzando parole e frasi in base alle regole di una determinata lingua, come ad esempio l'inglese o il giapponese. Le query full-text possono contenere semplici parole e frasi oppure più forme di una parola o frase. Una query full-text restituisce qualsiasi documento contenente almeno una corrispondenza, nota anche come *riscontro*. Si ottiene una corrispondenza quando un documento di destinazione contiene tutti i termini specificati nella query full-text e soddisfa qualsiasi altra condizione di ricerca, come ad esempio la distanza entro i termini corrispondenti.

> [!NOTE]
>  La ricerca full-text è un componente facoltativo del Motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [Install SQL Server 2014](../../database-engine/install-windows/install-sql-server.md).

##  <a name="what-can-i-do-with-full-text-search"></a><a name="benefits"></a>Cosa è possibile fare con la ricerca full-text?
 La ricerca full-text è applicabile a un'ampia gamma di scenari aziendali, ad esempio e-business, per la ricerca di elementi in un sito Web; aziende legali: ricerca di cronologie di casi in un repository di dati legali; o reparti risorse umane: descrizioni dei processi corrispondenti con riavvii archiviati. Le attività di sviluppo e amministrazione di base della ricerca full-text sono equivalenti indipendentemente dagli scenari aziendali. In uno scenario aziendale, tuttavia, l'indice e le query full-text possono essere modificati in base agli obiettivi aziendali da raggiungere. È ad esempio probabile che per un'attività di commercio elettronico l'ottimizzazione delle prestazioni sia ritenuta più importante della classificazione dei risultati, dell'accuratezza delle chiamate (quante delle corrispondenze esistenti vengono effettivamente restituite da una query full-text) o del supporto di più lingue. Per un ufficio legale, invece, l'aspetto più importante potrebbe essere la restituzione di ogni possibile occorrenza (*richiamo totale* delle informazioni).

 [Contenuto dell'articolo](#top)

###  <a name="full-text-search-queries"></a><a name="queries"></a>Query di ricerca full-text
 Dopo l'aggiunta delle colonne a un indice full-text, gli utenti e le applicazioni possono eseguire query full-text sul testo contenuto all'interno delle colonne. Queste query possono consentire la ricerca degli elementi seguenti:

-   Una o più parole o frasi specifiche (*termine semplice*)

-   Parola o frase in cui le parole iniziano con il testo specificato (*termine di prefisso*)

-   Forme flessive di una parola specifica (*termine di generazione*)

-   Una parola o frase vicina a un'altra parola o frase (*termine di prossimità*)

-   Sinonimi di una parola specifica (*thesaurus*)

-   Parole o frasi che usano valori ponderati (*termine ponderato*)

 Per le query di ricerca full-text non viene fatta distinzione tra maiuscole e minuscole. Ad esempio, dalla ricerca di "Alluminio" o "alluminio" vengono restituiti gli stessi risultati.

 Nelle query full-text viene utilizzato un set ridotto di predicati (CONTAINS e FREETEXT) e funzioni (CONTAINSTABLE e FREETEXTTABLE) [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Tuttavia, gli obiettivi di ricerca di un determinato scenario aziendale influiscono sulla struttura delle query full-text. Ad esempio:

-   Commercio elettronico: ricerca di un prodotto in un sito Web

    ```
    SELECT product_id 
    FROM products 
    WHERE CONTAINS(product_description, "Snap Happy 100EZ"
        OR FORMSOF(THESAURUS,'Snap Happy')
        OR '100EZ') 
    AND product_cost < 200 ;
    ```

-   Assunzione di personale: ricerca di candidati con esperienza in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

    ```
    SELECT candidate_name,SSN 
    FROM candidates 
    WHERE CONTAINS(candidate_resume,"SQL Server") AND candidate_division = 'DBA';
    ```

 Per altre informazioni, vedere [Esecuzione della query con ricerca Full-Text](query-with-full-text-search.md).

 [Contenuto dell'articolo](#top)

###  <a name="comparing-like-to-full-text-search"></a><a name="like"></a>Confronto tra LIKE e la ricerca full-text
 Contrariamente alla ricerca full-text, il predicato [LIKE](/sql/t-sql/language-elements/like-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] funziona unicamente con i modelli di caratteri. Non è inoltre possibile utilizzare il predicato LIKE per eseguire query su dati binari formattati. Inoltre, l'esecuzione di una query LIKE su una grande quantità di dati di testo non strutturati è molto più lenta dell'esecuzione di una query full-text equivalente sugli stessi dati. Una query LIKE eseguita su milioni di righe di dati di testo può richiedere diversi minuti, mentre per una query full-text sugli stessi dati possono essere necessari al massimo pochi secondi, a seconda del numero di righe restituite.

 [Contenuto dell'articolo](#top)

##  <a name="components-and-architecture-of-full-text-search"></a><a name="architecture"></a>Componenti e architettura della ricerca full-text
 L'architettura della ricerca full-text è costituita dai processi seguenti:

-   Processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (sqlservr.exe).

-   Processo host del daemon di filtri (fdhost.exe).

     Ai fini della sicurezza, i filtri vengono caricati da processi separati definiti host del daemon di filtri. I processi fdhost.exe vengono creati da un servizio dell'utilità di avvio di FDHOST (MSSQLFDLauncher) e vengono eseguiti con le credenziali di sicurezza dell'account del servizio dell'utilità di avvio di FDHOST. Il funzionamento delle query e dell'indicizzazione full-text dipende quindi dall'esecuzione del servizio dell'utilità di avvio di FDHOST. Per informazioni sulla configurazione dell'account del servizio per questo servizio, vedere [Impostazione dell'account del servizio dell'Utilità di avvio del daemon di filtri full-text](set-the-service-account-for-the-full-text-filter-daemon-launcher.md).

 In questi due processi sono inclusi i componenti dell'architettura della ricerca full-text, riepilogati con le relative relazioni nell'illustrazione seguente. I componenti vengono descritti dopo l'illustrazione.

 ![architettura della ricerca full-text](../../database-engine/media/ifts-arch.gif "architettura della ricerca full-text")

 [Contenuto dell'articolo](#top)

###  <a name="sql-server-process"></a><a name="sqlprocess"></a>SQL Server processo
 Nel processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono utilizzati i componenti seguenti per la ricerca full-text:

-   **Tabelle utente.** In queste tabelle sono contenuti i dati da inserire nell'indice full-text.

-   **Gatherer full-text.** Il gatherer full-text funziona con i thread della ricerca per indicizzazione full-text e consente di pianificare e gestire il popolamento degli indici full-text, nonché di monitorare i cataloghi full-text.

-   **File del thesaurus.** In questi file sono contenuti i sinonimi dei termini da cercare. Per altre informazioni, vedere [Configurare e gestire i file del thesaurus per la ricerca full-text](configure-and-manage-thesaurus-files-for-full-text-search.md).

-   **Oggetti dell'elenco di parole non significative.** Negli oggetti dell'elenco di parole non significative sono inclusi un insieme di parole comuni che non risultano utili per la ricerca. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).

-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Query Processor.** Query Processor consente di compilare ed eseguire query SQL. Se in una query SQL è inclusa una query di ricerca full-text, la query viene inviata al motore di ricerca full-text sia durante la compilazione sia durante l'esecuzione. Il risultato della query viene messo a confronto con l'indice full-text.

-   **Motore di ricerca full-text.** Il motore di ricerca full-text in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è attualmente completamente integrato con Query Processor. Il motore di ricerca full-text compila ed esegue query full-text. Come parte dell'esecuzione di query, il motore di ricerca full-text può ricevere input dal thesaurus e dall'elenco di parole non significative.

-   **Writer di indici (indicizzatore).** Il writer di indici consente di compilare la struttura utilizzata per archiviare i token indicizzati.

-   **Strumento di gestione del daemon di filtri.** Lo strumento di gestione del daemon di filtri consente di monitorare lo stato dell'host del daemon di filtri per il motore di ricerca full-text.

 [Contenuto dell'articolo](#top)

###  <a name="filter-daemon-host-process"></a><a name="fdhostprocess"></a>Processo host del daemon di filtri
 L'host del daemon di filtri è un processo avviato dal motore di ricerca full-text e consente l'esecuzione dei componenti della ricerca full-text seguenti, responsabili dell'accesso, del filtraggio e del word breaking di dati dalle tabelle, nonché del word breaking e dello stemming dell'input della query.

 I componenti dell'host del daemon di filtri sono i seguenti:

-   **Protocol handler.** Questo componente consente di effettuare il pull dei dati dalla memoria per un'ulteriore elaborazione e di accedere ai dati da una tabella utente in un database specificato. È inoltre responsabile della raccolta dei dati dalle colonne oggetto dell'indicizzazione full-text e del loro passaggio all'host del daemon di filtri tramite il quale verrà applicato il filtro e il word breaker in base alle specifiche esigenze.

-   **Filtri.** Per alcuni tipi di dati è richiesta l'applicazione di un filtro prima che i dati di un documento possano essere sottoposti all'indicizzazione full-text, inclusi i dati nelle colonne `varbinary`, `varbinary(max)`, `image` o `xml`. Il filtro utilizzato per un documento dipende dal relativo tipo. Vengono infatti utilizzati filtri diversi per documenti di Microsoft Word (doc), documenti di Microsoft Excel (xls) e documenti XML (xml). Il filtro estrae blocchi di testo dal documento, rimuovendo la formattazione incorporata e mantenendo il testo e, potenzialmente, le informazioni sulla posizione del testo. Il risultato è un flusso di informazioni testuali. Per altre informazioni, vedere [Configurazione e gestione di filtri per la ricerca](configure-and-manage-filters-for-search.md).

-   **Word breaker e stemmer.** Un word breaker è un componente specifico della lingua che consente di trovare i delimitatori di parola in base alle regole lessicali di una determinata lingua (*word breaking*). Ogni word breaker è associato a uno stemmer specifico della lingua che coniuga i verbi ed esegue le espansioni flessionali. In fase di indicizzazione, l'host del daemon di filtri utilizza un word breaker e uno stemmer per eseguire l'analisi linguistica sui dati testuali di una colonna di tabella specificata. Il word breaker e lo stemmer utilizzati per l'indicizzazione della colonna sono determinati dalla lingua associata a una colonna di tabella nell'indice full-text. Per altre informazioni, vedere [Configurare e gestire word breaker e stemmer per la ricerca](configure-and-manage-word-breakers-and-stemmers-for-search.md).

 [Contenuto dell'articolo](#top)

##  <a name="full-text-search-processing"></a><a name="processing"></a>Elaborazione della ricerca full-text
 La ricerca full-text è supportata dal motore di ricerca full-text che svolge due ruoli, vale a dire il supporto per l'indicizzazione e quello per l'esecuzione di query.

###  <a name="full-text-indexing-process"></a><a name="indexing"></a>Processo di indicizzazione full-text
 Quando viene iniziato un popolamento full-text, noto anche come ricerca per indicizzazione, tramite il motore di ricerca full-text viene eseguito il push di batch di grandi dimensioni di dati in memoria e viene inviata una notifica all'host del daemon di filtri. L'host filtra ed esegue il word breaking dei dati ed esegue inoltre la conversione dei dati convertiti in elenchi di parole invertiti. La ricerca full-text effettua quindi il pull dei dati convertiti dagli elenchi di parole, elabora i dati per rimuovere le parole non significative e salva in modo permanente gli elenchi di parole per un batch in uno o più indici invertiti.

 Quando si indicizzano i dati archiviati `varbinary(max)` in `image` una colonna o, il filtro, che implementa l'interfaccia **IFilter** , estrae il testo in base al formato di file specificato per tali dati [!INCLUDE[msCoName](../../includes/msconame-md.md)] , ad esempio Word. In alcuni casi, i componenti filtro richiedono che `varbinary(max)`i dati `image` , o vengano scritti nella cartella FilterData, anziché essere inseriti in memoria.

 Nell'ambito dell'elaborazione, i dati di testo raccolti vengono sottoposti a un word breaker per separare il testo in singoli token o parole chiave. La lingua utilizzata per la suddivisione in token viene specificata a livello di colonna o può essere identificata all'interno dei dati `varbinary(max)`, `image` o `xml` dal componente filtro.

 È possibile eseguire un'ulteriore elaborazione per rimuovere le parole non significative e normalizzare i token prima di archiviarli nell'indice full-text o in un frammento di indice.

 Al termine di un popolamento, viene attivato un processo di unione conclusivo che associa i frammenti di indice in un singolo indice full-text master. Ciò consente prestazioni di query superiori poiché è necessario eseguire query solo sull'indice master anziché su alcuni frammenti di indice ed è possibile utilizzare statistiche di punteggio migliori per la classificazione della pertinenza.

 [Contenuto dell'articolo](#top)

###  <a name="full-text-querying-process"></a><a name="querying"></a>Processo di esecuzione di query full-text
 Query Processor consente di passare le parti full-text di una query al motore di ricerca full-text affinché vengano elaborate. Il motore di ricerca full-text esegue il word breaking e, facoltativamente, le espansioni del thesaurus, lo stemming e l'elaborazione delle parole non significative. Le parti full-text della query vengono rappresentate come operatori SQL, principalmente come funzioni di flusso con valori di tabella. Durante l'esecuzione della query, queste funzioni accedono all'indice invertito per recuperare i risultati corretti. I risultati vengono restituiti al client immediatamente oppure dopo essere stati ulteriormente elaborati.

 [Contenuto dell'articolo](#top)

##  <a name="linguistic-components-and-language-support-in-full-text-search"></a><a name="components"></a>Componenti linguistici e supporto per la lingua nella ricerca full-text
 La ricerca full-text supporta quasi 50 lingue, tra cui inglese, spagnolo, cinese, giapponese, arabo, bengali e hindi. Per un elenco completo delle lingue full-text supportate, vedere [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql). A ognuna delle colonne contenute nell'indice full-text è associato un identificatore delle impostazioni locali (LCID) di Microsoft Windows che corrisponde a una lingua supportata dalla ricerca full-text. L'identificatore LCID 1033, ad esempio, corrisponde all'inglese americano, mentre l'identificatore LCID 2057 corrisponde all'inglese britannico. Per ogni lingua full-text supportata, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono forniti componenti linguistici che supportano l'indicizzazione e l'esecuzione di query su dati full-text archiviati in quella lingua.

 Tra i componenti specifici della lingua sono inclusi gli elementi seguenti:

-   **Word breaker e stemmer.** Un word breaker consente di trovare i delimitatori di parola in base alle regole lessicali di una determinata lingua (*word breaking*). A ogni word breaker è associato uno stemmer tramite cui vengono coniugati i verbi per la stessa lingua. Per altre informazioni, vedere [Configurare e gestire word breaker e stemmer per la ricerca](configure-and-manage-word-breakers-and-stemmers-for-search.md).

-   **Elenchi di parole non significative.** Viene inoltre fornito un elenco di parole non significative di sistema. Per *parola non significativa* si intende una parola inutile ai fini della ricerca e quindi ignorata dalle query full-text. Ad esempio, nelle impostazioni locali della lingua italiana parole quali "circa", "con", "devo" e "cui" sono considerate non significative. In genere, è necessario configurare uno o più file del thesaurus ed elenchi di parole non significative. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).

-   **File del thesaurus.** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] installa anche un file del thesaurus per ogni lingua full-text e un file del thesaurus globale. I file del thesaurus installati sono praticamente vuoti, ma è possibile modificarli per definire sinonimi per una lingua o uno scenario aziendale specifico. Sviluppando un thesaurus basato sui dati full-text in uso, è possibile ampliare in modo efficace l'ambito delle query full-text su tali dati. Per altre informazioni, vedere [Configurare e gestire i file del thesaurus per la ricerca full-text](configure-and-manage-thesaurus-files-for-full-text-search.md).

-   **Filtri (iFilters).**  L'indicizzazione di un documento in una colonna con tipo di dati `varbinary(max)`, `image` o `xml` richiede l'applicazione di un filtro per eseguire ulteriori operazioni di elaborazione. Il filtro deve essere specifico del tipo di documento (doc, pdf, xls, xml e così via). Per altre informazioni, vedere [Configurazione e gestione di filtri per la ricerca](configure-and-manage-filters-for-search.md).

 I word breaker, gli stemmer e i filtri vengono eseguiti nel processo host del daemon di filtri (fdhost.exe).

 [Contenuto dell'articolo](#top)

##  <a name="related-tasks"></a><a name="reltasks"></a> Attività correlate

-   [Introduzione alla ricerca full-text](get-started-with-full-text-search.md)

-   Scrittura di query full-text

    -   [Eseguire query con ricerca full-text](query-with-full-text-search.md)

    -   [Ricerca di parole vicine a un'altra parola con NEAR](search-for-words-close-to-another-word-with-near.md)

    -   [Limitazione dei risultati della ricerca mediante RANK](limit-search-results-with-rank.md)

    -   [Migliorare le prestazioni delle query full-text](improve-the-performance-of-full-text-queries.md)

    -   [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](search-document-properties-with-search-property-lists.md)

    -   [Trovare GUID del set di proprietà e ID di tipo integer delle proprietà per le proprietà di ricerca](find-property-set-guids-and-property-integer-ids-for-search-properties.md)

-   Gestione di cataloghi e indici

    -   [Creare e gestire cataloghi full-text](create-and-manage-full-text-catalogs.md)

    -   [Creazione e gestione di indici full-text](create-and-manage-full-text-indexes.md)

    -   [Scelta di una lingua durante la creazione di un indice full-text](choose-a-language-when-creating-a-full-text-index.md)

    -   [Popolamento degli indici full-text](populate-full-text-indexes.md)

    -   [Gestione di indici full-text.](../../database-engine/manage-full-text-indexes.md)

    -   [Miglioramento delle prestazioni di indici full-text](improve-the-performance-of-full-text-indexes.md)

    -   [Risoluzione dei problemi nell'indicizzazione full-text](troubleshoot-full-text-indexing.md)

    -   [Backup e ripristino di indici e cataloghi full-text](back-up-and-restore-full-text-catalogs-and-indexes.md)

-   Gestione dei componenti linguistici

    -   [Configurazione e gestione di filtri per la ricerca](configure-and-manage-filters-for-search.md)

    -   [Configurazione e gestione di word breaker e stemmer per la ricerca](configure-and-manage-word-breakers-and-stemmers-for-search.md)

    -   [Visualizzazione o modifica di word breaker e filtri registrati](view-or-change-registered-filters-and-word-breakers.md)

    -   [Ripristinare i word breaker utilizzati dalla ricerca alla versione precedente](revert-the-word-breakers-used-by-search-to-the-previous-version.md)

    -   [Modifica del word breaker utilizzato per le lingue Inglese (Stati Uniti) e Inglese (Regno Unito)](change-the-word-breaker-used-for-us-english-and-uk-english.md)

    -   [Personalizzare Comportamento di word breaker con un dizionario personalizzato](customize-the-behavior-of-word-breakers-with-a-custom-dictionary.md)

    -   [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)

    -   [Configurare e gestire i file del thesaurus per la ricerca full-text](configure-and-manage-thesaurus-files-for-full-text-search.md)

-   Gestione della ricerca full-text

    -   [Gestione e monitoraggio della ricerca full-text per un'istanza del server](manage-and-monitor-full-text-search-for-a-server-instance.md)

    -   [Impostazione dell'account del servizio dell'Utilità di avvio del daemon di filtri full-text](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)

-   [Aggiornamento della ricerca full-text](upgrade-full-text-search.md)

 [Contenuto dell'articolo](#top)

##  <a name="related-content"></a><a name="relcontent"></a> Contenuto correlato

-   [DDL di ricerca full-text, funzioni, stored procedure e viste](../views/views.md)

 [Contenuto dell'articolo](#top)


