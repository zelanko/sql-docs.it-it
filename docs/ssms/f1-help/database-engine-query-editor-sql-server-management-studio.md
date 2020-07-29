---
title: editor di query del Motore di database
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/03/2020
ms.openlocfilehash: 9e90e4596c3d78f48b8ecc4a5af4741ea1f5949d
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2020
ms.locfileid: "87123042"
---
# <a name="ssms-query-editor"></a>Editor di query SSMS

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

L'editor di query del motore di database è uno dei quattro editor implementati in SQL Server Management Studio (SSMS).

Usare l'editor di query per creare ed eseguire script contenenti istruzioni Transact-SQL. L'editor supporta anche l'esecuzione di script contenenti comandi **sqlcmd** .

Per una descrizione della funzionalità implementata nell'editor di query e delle attività principali che è possibile eseguire usando l'editor, vedere [Editor di query e testo](../scripting/query-and-text-editors-sql-server-management-studio.md).

![Nuova query](media/database-engine-query-editor-sql-server-management-studio/new-query.png)

## <a name="transact-sql-f1-help"></a>Guida di Transact-SQL

L'editor di query supporta il collegamento all'argomento di riferimento per un'istruzione Transact-SQL specifica quando si seleziona F1. A tale scopo, evidenziare il nome di un'istruzione Transact-SQL, quindi selezionare F1. Il motore di ricerca della Guida cerca un argomento che dispone di un attributo della Guida corrispondente alla stringa evidenziata.

Se non vengono trovati argomenti con una parola chiave della Guida che corrisponde esattamente alla stringa evidenziata, viene visualizzato questo argomento. In tal caso esistono due approcci per trovare le informazioni che si stanno cercando:

- Copiare e incollare la stringa dell'editor evidenziata nella scheda di ricerca della documentazione online di SQL Server o effettuare una ricerca.

- Evidenziare solo la parte dell'istruzione Transact-SQL con maggiori probabilità di corrispondenza a una parola chiave della Guida applicata a un argomento e selezionare di nuovo F1. Il motore di ricerca richiede una corrispondenza esatta tra la stringa evidenziata e una parola chiave della Guida assegnata a un argomento. Se la stringa evidenziata contiene elementi univoci dell'ambiente, ad esempio nomi di colonna o di parametro, il motore di ricerca non restituisce corrispondenze. Di seguito sono riportati alcuni esempi di stringhe evidenziabili:

  - Nome dell'istruzione Transact-SQL, ad esempio SELECT, CREATE DATABASE o BEGIN TRANSACTION.

  - Nome di una funzione predefinita, ad esempio SERVERPROPERTY o @@VERSION.

  - Nome di una tabella di stored procedure di sistema o di una vista, ad esempio sys.data_spaces o sp_tableoption.

## <a name="sql-editor-toolbar"></a>Barra degli strumenti Editor SQL

Quando l'editor di query è aperto, la barra degli strumenti Editor SQL visualizza i pulsanti seguenti.

È anche possibile aggiungere la barra degli strumenti Editor SQL selezionando il menu **Visualizza** , **Barre degli strumenti**, quindi **Editor SQL**. Se la barra degli strumenti Editor SQL viene aggiunta quando non sono aperte finestre dell'editor di query, non è disponibile nessun pulsante.

![Barra degli strumenti dell'editor](media/database-engine-query-editor-sql-server-management-studio/editor-toolbar.png)

### <a name="connect-using-the-editor-toolbar"></a>Connetti - Barra degli strumenti dell'editor

Apre la finestra di dialogo **[Connetti al server](connect-to-server-database-engine.md)** . Utilizzare questa finestra di dialogo per stabilire una connessione a un server.

È anche possibile connettersi al database usando il [menu di scelta rapida](#connection-using-the-context-menu).

### <a name="change-connection-using-the-editor-toolbar"></a>Cambia connessione - Barra degli strumenti dell'editor

Consente di aprire la finestra di dialogo **Connetti al server** . Usare questa finestra di dialogo per stabilire una [connessione a un altro server](f1-help-for-server-connections-sql-server-management-studio.md).

È anche possibile cambiare connessione usando il [menu di scelta rapida](#connection-using-the-context-menu).

### <a name="available-databases-using-the-editor-toolbar"></a>Database disponibili - Barra degli strumenti dell'editor

Consente di passare a un database diverso sullo stesso server.

### <a name="execute-using-the-editor-toolbar"></a>Esegui - Barra degli strumenti dell'editor

Consente di eseguire il codice selezionato o, se non è selezionata alcuna parte del codice, di eseguire tutto il codice incluso nell'editor di query.

È anche possibile attivare il comando **Esegui** per una query selezionando F5 o usando il [menu di scelta rapida](#execute-using-the-context-menu).

### <a name="cancel-executing-query-using-the-editor-toolbar"></a>Annulla esecuzione query - Barra degli strumenti dell'editor

Consente di inviare una richiesta di annullamento al server. Alcune query non possono essere annullate immediatamente, ma devono attendere una condizione di annullamento adatta. Quando le transazioni vengono annullate, è possibile che si verifichino ritardi durante il rollback delle transazioni.

È anche possibile annullare una query in esecuzione selezionando ALT+INTERR.

### <a name="parse-using-the-editor-toolbar"></a>Analizza - Barra degli strumenti dell'editor

Consente di controllare la sintassi del codice selezionato. Se non è selezionato nessun codice, viene controllata la sintassi di tutto il codice incluso nella finestra dell'editor di query.

Per controllare il codice nell'editor di query è anche possibile selezionare CTRL+F5.

### <a name="display-estimated-execution-plan-using-the-editor-toolbar"></a>Visualizza piano di esecuzione stimato - Barra degli strumenti dell'editor

Richiede un piano di esecuzione query a Query Processor senza eseguire effettivamente la query e visualizza il piano nella finestra **Piano di esecuzione** . In tale piano vengono utilizzate statistiche dell'indice per stimare il numero di righe restituite previste durante ogni parte dell'esecuzione della query. Il piano di query effettivo utilizzato può differire dal piano di esecuzione stimato. Ciò si verifica in presenza di una differenza significativa tra il numero di righe restituite e quelle stimate. In questo caso, Query Processor modifica il piano per renderlo più efficiente.

È anche possibile visualizzare un piano di esecuzione stimato premendo CTRL+L o usando il [menu di scelta rapida](#display-estimated-execution-plan-using-the-context-menu).

### <a name="query-options-using-the-editor-toolbar"></a>Opzioni query - Barra degli strumenti dell'editor

Consente di aprire la finestra di dialogo **Opzioni query** . Utilizzare questa finestra di dialogo per configurare le opzioni predefinite per l'esecuzione della query e per i relativi risultati.

In alternativa è possibile selezionare **Opzioni query** dal [menu di scelta rapida](#query-options-using-the-context-menu).

### <a name="intellisense-enabled-using-the-editor-toolbar"></a>IntelliSense abilitato - Barra degli strumenti dell'editor

Consente di specificare se la funzionalità IntelliSense è disponibile o meno nell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Questa opzione è selezionata per impostazione predefinita.

È anche possibile selezionare **IntelliSense abilitato** premendo CTRL+B e quindi CTRL+I oppure usando il [menu di scelta rapida](#intellisense-enabled-using-the-context-menu).

### <a name="include-actual-execution-plan-using-the-editor-toolbar"></a>Includi piano di esecuzione effettivo - Barra degli strumenti dell'editor

Consente di eseguire la query e di restituirne i risultati insieme al piano di esecuzione utilizzato per la query. Questi elementi vengono visualizzati come piano di query grafico nella finestra **Piano di esecuzione** .

È anche possibile selezionare **Includi piano di esecuzione effettivo stimato** premendo CTRL+M o usando il [menu di scelta rapida](#include-actual-execution-plan-using-the-context-menu).

### <a name="include-live-query-statistics-using-the-editor-toolbar"></a>Includi statistiche query dinamiche - Barra degli strumenti dell'editor

Offre informazioni approfondite in tempo reale sul processo di esecuzione della query, man mano che i controlli passano da un operatore del piano di query a un altro.

È anche possibile selezionare **Includi statistiche query dinamiche** dal [menu di scelta rapida](#include-live-query-statistics-using-the-context-menu).

### <a name="include-client-statistics-using-the-editor-toolbar"></a>Includi statistiche client - Barra degli strumenti dell'editor

Include una finestra **Statistiche client** contenente statistiche relative alla query e ai pacchetti di rete, nonché al tempo trascorso dall'inizio della query.

È anche possibile selezionare **Includi statistiche client** premendo MAIUSC+ALT+S o usando il [menu di scelta rapida](#include-client-statistics-using-the-context-menu).

### <a name="results-to-text-using-the-editor-toolbar"></a>Risultati in formato testo - Barra degli strumenti dell'editor

Restituisce i risultati della query in formato testo nella finestra **Risultati** .

È anche possibile restituire i risultati in formato testo premendo CTRL+T o usando il [menu di scelta rapida](#results-using-the-context-menu).

### <a name="results-to-grid-using-the-editor-toolbar"></a>Risultati in formato griglia - Barra degli strumenti dell'editor

Restituisce i risultati della query sotto forma di una o più griglie nella finestra **Risultati** . Questa opzione è in genere abilitata per impostazione predefinita.

È anche possibile restituire i risultati in formato griglia premendo CTRL+D o usando [menu di scelta rapida](#results-using-the-context-menu).

### <a name="results-to-file-using-the-editor-toolbar"></a>Risultati in un file - Barra degli strumenti dell'editor

All'esecuzione della query viene visualizzata la finestra di dialogo **Salva risultati** . In **Salva in**selezionare la cartella in cui si desidera salvare il file. In **Nome file** digitare il nome del file e quindi selezionare **Salva** per salvare i risultati della query come file **Report** con estensione rpt. Per visualizzare le opzioni avanzate, fare clic sulla freccia giù del pulsante **Salva** e quindi selezionare **Salva con codifica**.

È anche possibile restituire i risultati in un file premendo CTRL+MAIUSC+F o usando [menu di scelta rapida](#results-using-the-context-menu).

### <a name="comment-out-the-selected-lines-using-the-editor-toolbar"></a>Imposta le righe selezionate come commento - Barra degli strumenti dell'editor

Consente di contrassegnare la riga corrente come commento tramite l'aggiunta di un operatore di commento (--) all'inizio della riga.

È anche possibile contrassegnare una riga come commento premendo CTRL+K e quindi CTRL+C.

### <a name="uncomment-the-selected-lines-using-the-editor-toolbar"></a>Rimuovi simboli di commento dalle righe selezionate - Barra degli strumenti dell'editor

Consente di modificare la riga corrente in istruzione di origine attiva rimuovendo eventuali operatori di commento (--) presenti all'inizio della riga.

È anche possibile rimuovere i simboli di commento da una riga premendo CTRL+K e quindi CTRL+U.

### <a name="decrease-indent-using-the-editor-toolbar"></a>Riduci rientro - Barra degli strumenti dell'editor

Consente di spostare a sinistra il testo della riga rimuovendo spazi vuoti all'inizio della riga.

### <a name="increase-line-indent-using-the-editor-toolbar"></a>Aumenta rientro riga - Barra degli strumenti dell'editor

Consente di spostare a destra il testo della riga aggiungendo spazi vuoti all'inizio della riga.

### <a name="specify-values-for-template-parameters-using-the-editor-toolbar"></a>Imposta valori per parametri modello - Barra degli strumenti dell'editor

Consente di aprire una finestra di dialogo in cui è possibile specificare valori per i parametri inclusi in stored procedure e funzioni.

## <a name="context-menu"></a>Menu di scelta rapida

È possibile accedere al menu di scelta rapida *facendo clic con il pulsante destro del mouse* in qualsiasi punto dell'editor di query. Le opzioni del menu di scelta rapida sono simili a quelle della barra degli strumenti dell'editor SQL. Il menu di scelta rapida visualizza le stesse opzioni della barra, ad esempio **Connetti** ed **Esegui**, ma anche altre opzioni come **Inserisci frammento** e **Racchiudi tra**.

![Opzioni del menu di scelta rapida](media/database-engine-query-editor-sql-server-management-studio/context-menu.png)

### <a name="insert-snippet-using-the-context-menu"></a>Inserisci frammento - Menu di scelta rapida

Un frammento di codice Transact-SQL è un modello che può essere usato come punto di partenza per la scrittura di nuove istruzioni Transact-SQL nell'editor di query.

### <a name="surround-with-using-the-context-menu"></a>Racchiudi tra - Menu di scelta rapida

Un frammento di inclusione è un modello che può essere usato come punto di partenza per includere un set di istruzioni Transact-SQL in un blocco BEGIN, IF o WHILE.

### <a name="connection-using-the-context-menu"></a>Connessione - Menu di scelta rapida

![Opzioni del menu di scelta rapida](media/database-engine-query-editor-sql-server-management-studio/context-menu-connections.png)

Nel menu di scelta rapida di SSMS sono disponibili più opzioni **Connessione** rispetto a quelle della barra degli strumenti.

- **Connetti**: apre la finestra di dialogo Connetti al server. Utilizzare questa finestra di dialogo per stabilire una connessione a un server.

- **Disconnetti**: disconnette l'editor di query corrente dal server.

- **Disconnetti tutte le query**: disconnette tutte le connessioni a query.

- **Cambia connessione**: apre la finestra di dialogo Connetti al server. Utilizzare questa finestra di dialogo per stabilire una connessione a un server diverso.

### <a name="open-server-in-object-explorer-using-the-context-menu"></a>Apri server in Esplora oggetti - Menu di scelta rapida

Esplora oggetti offre un'interfaccia utente gerarchica per visualizzare e gestire gli oggetti in ogni istanza di SQL Server. Il riquadro Dettagli Esplora oggetti presenta una vista tabulare di oggetti istanza e la funzionalità per cercare oggetti specifici. Le funzionalità di Esplora oggetti variano leggermente in base al tipo di server ma in genere comprendono le caratteristiche di sviluppo per i database e di gestione per tutti i tipi di server.

### <a name="execute-using-the-context-menu"></a>Esegui - Menu di scelta rapida

Consente di eseguire il codice selezionato o, se non è selezionata alcuna parte del codice, di eseguire tutto il codice incluso nell'editor di query.

### <a name="display-estimated-execution-plan-using-the-context-menu"></a>Visualizza piano di esecuzione stimato - Menu di scelta rapida

Richiede un piano di esecuzione query a Query Processor senza eseguire effettivamente la query e visualizza il piano nella finestra **Piano di esecuzione** . In tale piano vengono utilizzate statistiche dell'indice per stimare il numero di righe restituite previste durante ogni parte dell'esecuzione della query. Il piano di query effettivo utilizzato può differire dal piano di esecuzione stimato. Ciò si verifica in presenza di una differenza significativa tra il numero di righe restituite e quelle stimate. In questo caso, Query Processor modifica il piano per renderlo più efficiente.

### <a name="intellisense-enabled-using-the-context-menu"></a>IntelliSense abilitato - Menu di scelta rapida

Consente di specificare se la funzionalità IntelliSense è disponibile o meno nell'editor di query del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Questa opzione è selezionata per impostazione predefinita.

### <a name="trace-query-in-sql-server-profiler-using-the-context-menu"></a>Traccia query in SQL Server Profiler - Menu di scelta rapida

SQL Server Profiler è un'interfaccia per la creazione e la gestione di tracce e per l'analisi e la riproduzione dei risultati di tali tracce. Gli eventi vengono salvati in un file di traccia che può essere analizzato o usato successivamente per riprodurre una serie specifica di passaggi allo scopo di diagnosticare un problema.

### <a name="analyze-query-in-database-engine-tuning-advisor-using-the-context-menu"></a>Analizza query in Ottimizzazione guidata motore di database - Menu di scelta rapida

Ottimizzazione guidata motore di database di Microsoft analizza i database e offre raccomandazioni per ottimizzare le prestazioni delle query. È possibile usare Ottimizzazione guidata motore di database per selezionare e creare un set ottimale di indici, viste indicizzate e partizioni di tabella anche senza conoscere in modo approfondito la struttura del database o le caratteristiche interne di SQL Server. Con DTA, è possibile eseguire le attività seguenti.

### <a name="design-query-in-editor-using-the-context-menu"></a>Progetta query nell'editor - Menu di scelta rapida

Progettazione query e Progettazione viste viene aperto quando si apre la definizione di una vista, si visualizzano i risultati di una query o di una vista oppure si crea o si apre una query.

### <a name="include-actual-execution-plan-using-the-context-menu"></a>Includi piano di esecuzione effettivo - Menu di scelta rapida

Consente di eseguire la query e di restituirne i risultati insieme al piano di esecuzione utilizzato per la query. Questi elementi vengono visualizzati come piano di query grafico nella finestra **Piano di esecuzione** .

### <a name="include-live-query-statistics-using-the-context-menu"></a>Includi statistiche query dinamiche - Menu di scelta rapida

Offre informazioni approfondite in tempo reale sul processo di esecuzione della query, man mano che i controlli passano da un operatore del piano di query a un altro.

### <a name="include-client-statistics-using-the-context-menu"></a>Includi statistiche client - Menu di scelta rapida

Include una finestra **Statistiche client** contenente statistiche relative alla query e ai pacchetti di rete, nonché al tempo trascorso dall'inizio della query.

### <a name="results-using-the-context-menu"></a>Risultati - Menu di scelta rapida

![Opzioni per i risultati](media/database-engine-query-editor-sql-server-management-studio/context-menu-results.png)

È possibile scegliere l'opzione *Risultati* desiderata nel menu di scelta rapida.

- **Risultati in formato testo**: restituisce i risultati della query in formato testo nella finestra **Risultati**.

- **Risultati in formato griglia**: restituisce i risultati della query come una o più griglie nella finestra **Risultati**.

- **Risultati in un file**: all'esecuzione della query viene visualizzata la finestra di dialogo **Salva risultati**. In **Salva in**selezionare la cartella in cui si desidera salvare il file. In **Nome file** digitare il nome del file e quindi selezionare **Salva** per salvare i risultati della query come file **Report** con estensione rpt. Per visualizzare le opzioni avanzate, fare clic sulla freccia giù del pulsante **Salva** e quindi selezionare **Salva con codifica**.

### <a name="properties-window-using-the-context-menu"></a>Finestra Proprietà - Menu di scelta rapida

La [finestra Proprietà](../menu-help/properties-window-f1-help-management-studio.md) visualizza lo stato di un elemento in SQL Server Management Studio, ad esempio una connessione o un operatore Showplan, e riporta informazioni su oggetti di database come tabelle, visualizzazioni e finestre di progettazione.

È possibile utilizzare la finestra Proprietà per visualizzare le proprietà della connessione corrente. In questa finestra molte proprietà sono di sola lettura, ma è possibile modificarle altrove in Management Studio. La proprietà Database di una query, ad esempio, è di sola lettura nella finestra Proprietà ma può essere modificata sulla barra degli strumenti.

### <a name="query-options-using-the-context-menu"></a>Opzioni query - Menu di scelta rapida

Consente di aprire la finestra di dialogo **Opzioni query** . Utilizzare questa finestra di dialogo per configurare le opzioni predefinite per l'esecuzione della query e per i relativi risultati.

## <a name="see-also"></a>Vedere anche

- [Personalizzare i menu e i tasti di scelta rapida](../customize-menus-and-shortcut-keys.md)

- [Tasti di scelta rapida di SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)
