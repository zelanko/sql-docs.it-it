---
title: Estensione SQL Server 2019 (anteprima)
titleSuffix: Azure Data Studio
description: Estensione SQL Server 2019 (anteprima) per Azure Data Studio
ms.custom: seodec18
ms.date: 09/11/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: fffd79a18ca839816105242c054e74031828274f
ms.sourcegitcommit: 5d9ce5c98c23301c5914f142671516b2195f9018
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71961955"
---
# <a name="sql-server-2019-extension-for-azure-data-studio-preview"></a>Estensione SQL Server 2019 per Azure Data Studio (anteprima)

L'estensione SQL Server 2019 per Azure Data Studio (anteprima) fornisce supporto in anteprima per le funzionalità e gli strumenti nuovi disponibili per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Questo include il supporto in anteprima per i [cluster Big Data di SQL Server 2019](../big-data-cluster/big-data-cluster-overview.md), un'[esperienza di tipo notebook integrata](../big-data-cluster/notebooks-guidance.md) e una [procedura guidata di creazione tabella esterna](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json) PolyBase.

## <a name="install-the-sql-server-2019-extension-preview"></a>Installare l'estensione SQL Server 2019 (anteprima)

Per installare l'estensione SQL Server 2019 (anteprima), scaricare e installare il file VSIX associato.

1. Scaricare il file VSIX dell'estensione SQL Server 2019 (anteprima) in una directory locale:

   |Piattaforma|Scarica|Data di rilascio|Versione
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103613)|11 settembre 2019 |0.16.0
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103612)|11 settembre 2019 |0.16.0
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103709)|11 settembre 2019 |0.16.0

1. In Azure Data Studio scegliere **Install Extension from VSIX Package** (Installa estensione da pacchetto VSIX) dal menu **File** e selezionare il file con estensione vsix scaricato.

1. Scegliere **Sì** quando viene richiesto di confermare l'installazione e attendere la notifica di esito positivo dell'installazione.

1. Selezionare **Ricarica** per abilitare l'estensione (necessario solo la prima volta che si installa un'estensione).

1. Dopo il ricaricamento, l'estensione installerà le dipendenze. È possibile visualizzare lo stato di avanzamento nella finestra di output e l'operazione potrebbe richiedere alcuni minuti.

1. Al termine dell'installazione delle dipendenze, chiudere e riaprire Azure Data Studio. Il tipo di connessione **cluster Big Data di SQL Server** non è disponibile finché non si riavvia Azure Data Studio.

## <a name="changes-in-release-016"></a>Modifiche nella versione 0.16
* Procedura guidata di creazione tabella esterna:
  * Miglioramento della gestione degli errori durante il caricamento di tabelle e viste nella pagina di mapping degli oggetti.

## <a name="changes-in-release-015"></a>Modifiche nella versione 0.15
* Procedura guidata di creazione tabella esterna:
  * Riduzione del tempo necessario per caricare le informazioni relative a tabelle e colonne nella pagina di mapping degli oggetti.
  * Correzione di un bug relativo al caricamento delle credenziali con ambito database esistenti nella pagina Dettagli connessione.
* Procedura guidata per la creazione di una tabella esterna da file CSV:
  * Aumento delle dimensioni predefinite del campione usato per l'analisi PROSE.

## <a name="changes-in-release-0141"></a>Modifiche nella versione 0.14.1
* Supporto per l'origine dati CTP 3.1

## <a name="changes-in-release-0121"></a>Modifiche nella versione 0.12.1

* Il tipo di connessione **cluster Big Data di SQL Server** è stato rimosso in questa versione. Tutte le funzionalità precedentemente disponibili dalla connessione cluster Big Data di SQL Server sono ora disponibili nella connessione SQL Server.
* L'esplorazione HDFS è disponibile nella cartella **Servizi dati**
* Per i notebook, PySpark e altri kernel Big Data funzionano quando si è connessi all'istanza master di SQL Server nel cluster Big Data di SQL Server.
* Procedura guidata di creazione tabella esterna:
  * Supporto per la creazione di una tabella esterna mediante un'origine dati esterna esistente.
  * Miglioramenti delle prestazioni nella procedura guidata.
  * Gestione migliorata dei nomi degli oggetti con caratteri speciali. In alcuni casi questi causavano l'esito negativo della procedura guidata.
  * Miglioramenti dell'affidabilità per la pagina del mapping oggetti.
  * Rimozione dei database di sistema 'DWConfiguration', 'DWDiagnostics', 'DWQueue' dall'elenco a discesa dei database.
  * Supporto per l'impostazione del nome dell'oggetto Formato di file esterno nella procedura guidata **Create External Table from CSV Files** (Crea tabella esterna da file CSV).
  * È stato aggiunto un pulsante di aggiornamento alla prima pagina della procedura guidata **Create External Table from CSV Files** (Crea tabella esterna da file CSV).

## <a name="release-notes-v0110"></a>Note sulla versione (v0.11.0)

* Il supporto di Jupyter Notebook, in particolare il supporto per i kernel Python3 e Spark, è stato spostato in Azure Data Studio. Questa estensione non è più necessaria per poter usare i notebook.
* Più correzioni di bug nelle procedure guidate per i dati esterni:
  * I mapping dei tipi Oracle sono stati aggiornati in modo da corrispondere alle modifiche incluse in SQL Server 2019 CTP 2.3.
  * È stato risolto un problema per cui i nuovi schemi digitati nei controlli di mapping delle tabelle andavano persi.
  * È stato risolto un problema per cui il controllo di un nodo di database nei mapping di tabella non comportava il controllo di tutte le tabelle e le viste.


## <a name="release-notes-v0102"></a>Note sulla versione (v 0.10.2)
### <a name="sql-server-2019-support"></a>Supporto di SQL Server 2019
Il supporto per SQL Server 2019 è stato aggiornato. Dopo la connessione a un'istanza del cluster Big Data di SQL Server, nell'albero di esplorazione viene visualizzata una nuova cartella _Servizi dati_. Questa offre punti di avvio per azioni quali l'apertura di un nuovo notebook sulla connessione, l'invio di processi Spark e l'uso di HDFS. Si noti che per alcune azioni, ad esempio _creare dati esterni_ su un file o una cartella HDFS, è necessario installare l'estensione _SQL Server 2019 Preview_.

### <a name="notebook-support"></a>Supporto di notebook
In questa versione sono stati apportati aggiornamenti significativi all'interfaccia utente per i notebook. L'obiettivo è quello di semplificare la lettura dei notebook condivisi con l'utente. Sono state rimosse tutte le caselle di contorno intorno alle celle, a meno che non siano selezionate o evidenziate con il mouse, aggiungendo il supporto del passaggio del mouse per semplificare le azioni a livello di cella senza bisogno di selezionare una cella. Lo stato di esecuzione è ora più chiaro grazie all'aggiunta del conteggio delle esecuzioni, di un pulsante _Arresta esecuzione_ animato e altro ancora. Sono state aggiunge scelte rapide da tastiera per _New Notebook_ (Nuovo notebook) (`Ctrl+Shift+N`), _Run Cell_ (Esegui cella) (`F5`), _New Code Cell_ (Nuova cella di codice) (`Ctrl+Shift+C`), _New Text Cell_ (Nuova cella di testo) (`Ctrl+Shift+T`). In futuro, cercheremo di fare in modo che tutte le azioni chiave si possano lanciare tramite scelta rapida da tastiera, quindi ogni suggerimento sulle combinazioni mancanti è il benvenuto.

Altri miglioramenti e correzioni includono:
* L'estensione _SQL Server 2019 Preview_ ora richiede agli utenti di selezionare una directory di installazione per le dipendenze Python. Non include più Python nel `.vsix file`, riducendo così le dimensioni complessive dell'estensione. Le dipendenze Python supportano i kernel Spark e Python3.
* È stato aggiunto il supporto per l'avvio di un nuovo notebook dalla riga di comando. L'avvio con gli argomenti `--command=notebook.command.new --server=myservername` dovrebbe aprire un nuovo notebook e connettersi a questo server.
* Correzioni delle prestazioni per notebook con codice di lunghezza elevata nelle celle. Se le celle di codice sono lunghe più di 250 righe, viene aggiunta una barra di scorrimento.
* Miglioramento del supporto per i file con estensione ipynb. È ora supportata la versione 3 o successiva. Si noti che, al salvataggio, i file verranno aggiornati alla versione 4 o successiva.
* L'impostazione utente `notebook.enabled` è stata rimossa ora che il visualizzatore notebook predefinito è stabile
* È ora supportato il tema a contrasto elevato, con una serie di correzioni al layout degli oggetti.
* È stato corretto il problema 3680, per cui gli output talvolta mostravano erroneamente una serie di caratteri `,,,`
* È stato corretto il problema 3602, per cui uscendo dalla pagina di Azure Data Studio scompare l'editor per le celle
* È stato aggiunto il supporto per l'uso delle visualizzazioni griglia per il tipo MIME di output `application/vnd.dataresource+json`. Questo significa che molti notebook che lo usano, ad esempio impostando `pd.options.display.html.table_schema` in un notebook Python, avranno output tabulari migliore. È stato corretto il problema 3959, per cui Azure Data Studio tenta di arrestare il server notebook due volte dopo la chiusura del notebook

#### <a name="known-issues"></a>Problemi noti
* Quando si apre un notebook, viene visualizzata la finestra di dialogo per l'installazione di Python. Se si annulla questa installazione, i menu a discesa Kernels (Kernel) e Collega a non visualizzeranno i valori previsti. La soluzione alternativa consiste nel completare l'installazione di Python.
* Quando un notebook viene aperto con un kernel non supportato, i menu a discesa Kernels (Kernel) e _Collega a_ provocheranno il blocco delle risposte da parte di Azure Data Studio. Sarà necessario chiudere Azure Data Studio e assicurarsi di usare un kernel supportato (Python3, Spark | R, Spark | Scala, PySpark, PySpark3)
* Il collegamento all'interfaccia utente Spark ha esito negativo quando si usa PySpark3 o altri kernel Spark sull'endpoint SQL Server. Come soluzione alternativa, fare clic su Spark UI (Interfaccia utente Spark) dal dashboard o connettersi usando il tipo di connessione cluster Big Data di SQL Server, perché il collegamento ipertestuale all'interfaccia utente Spark sarà corretto

### <a name="extensibility-improvements"></a>Miglioramenti dell'estendibilità
In questa versione sono stati aggiunti alcuni miglioramenti utili per i controlli Extender
* Una nuova API `ObjectExplorerNodeProvider` consente alle estensioni di inserire cartelle in SQL Server o altri nodi di connessione. Questo è il modo in cui il nodo `Data Services` viene aggiunto nelle istanze di SQL Server 2019, ma l'API si può usare per aggiungere facilmente una cartella Monitoraggio o altre cartelle all'interfaccia utente.
* Sono disponibili due nuovi valori di chiave di contesto per visualizzare/nascondere i contributi al dashboard.
  * `mssql:iscluster` indica se si tratta di un cluster Big Data di SQL Server 2019
  * `mssql:servermajorversion` indica la versione del server (15 per SQL Server 2019, 14 per SQL Server 2017 e così via). Questo può essere utile se le funzionalità devono essere visualizzate, ad esempio, solo per SQL Server 2017 o versione successiva.


## <a name="release-notes-v080"></a>Note sulla versione (v0.8.0)
*Notebook*:
* L'aggiunta di celle prima/dopo le celle esistenti è ora supportata facendo clic sul pulsante della cella "Altre azioni"
* L'opzione **Aggiungi nuova connessione** è stata aggiunta alle connessioni nell'elenco a discesa "Collega a"
* È stato aggiunto un comando **Reinstall Notebook Dependencies** (Reinstalla dipendenze notebook) per facilitare gli aggiornamenti dei pacchetti Python e risolvere i casi in cui l'installazione è stata interrotta chiudendo l'applicazione. Può essere eseguito dal riquadro comandi (usare `Ctrl/Cmd+Shift+P` e digitare `Reinstall Notebook Dependencies`)
* Il pacchetto Python PROSE è stato aggiornato alla versione 1.1.0 e include una serie di correzioni di bug. Usare il comando **Reinstall Notebook Dependencies** (Reinstalla dipendenze notebook) per aggiornare questo pacchetto
* È ora supportato un comando **Cancella output** facendo clic sul pulsante della cella **Altre azioni**
* Sono stati corretti i seguenti problemi segnalati dai clienti:
  * Non è stato possibile avviare la sessione del notebook in Windows a causa di problemi di percorso
  * Non è stato possibile avviare il notebook dalla cartella radice di un'unità, ad esempio C:\ o D:\
  * [2820](https://github.com/Microsoft/azuredatastudio/issues/2820) Non è possibile modificare i notebook creati da ADS in VS Code
  * Il collegamento all'interfaccia utente Spark ora funziona quando si esegue un kernel Spark
  * Managed Packages (Pacchetti gestiti) è stato rinominato in "Installa pacchetti"

*Creazione di dati esterni*:

* I messaggi di errore sono copiabili e sono stati separati in un riepilogo e una visualizzazione dettagliata per semplificare la lettura
* Miglioramento del layout dell'interfaccia utente, affidabilità e gestione degli errori notevolmente migliorati
* Sono stati corretti i seguenti problemi segnalati dai clienti:
  * Le tabelle con mapping di colonna non validi vengono visualizzate come disabilitate e un avviso spiega l'errore

## <a name="release-notes-v072"></a>Note sulla versione (v0.7.2)
* Azure Resource Explorer ora è incorporata in Azure Data Studio ed è stato rimosso da questa estensione. Grazie per i commenti e suggerimenti inviati.
* Miglioramento delle prestazioni dei notebook con molte celle di markdown.
* Ridimensionamento automatico delle celle di codice nel notebook. Esiste ancora una dimensione minima in base alla barra degli strumenti della cella.
* Notifica all'utente durante l'installazione delle dipendenze del notebook. In Windows, in particolare, questa operazione può richiedere molto tempo, quindi le notifiche vengono ora mostrate nella visualizzazione Attività.
* Supporto per la reinstallazione delle dipendenze del notebook. Utile se in precedenza l'utente ha chiuso Azure Data Studio durante l'installazione.
* Supporto per l'annullamento dell'esecuzione di celle nel notebook.
* Maggiore affidabilità nell'uso della procedura guidata di creazione dati esterni, in particolare quando si verificano errori di connessione.
* Blocco dell'uso della procedura guidata di creazione dati esterni se PolyBase non è abilitato o non è in esecuzione nel server di destinazione.
* Correzioni di ortografia e di denominazione correlate a SQL Server 2019 e alla creazione dati esterni.
* Rimozione di un numero elevato di errori dalla console di debug di Azure Data Studio.
