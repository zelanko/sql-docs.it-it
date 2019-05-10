---
title: Estensione di SQL Server 2019 (anteprima)
titleSuffix: Azure Data Studio
description: Estensione di anteprima di SQL Server 2019 per Data Studio di Azure
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 72ba0ed0ba190f390f355b9a7fcf823b3d99d766
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775363"
---
# <a name="sql-server-2019-extension-preview"></a>Estensione di SQL Server 2019 (anteprima)

L'estensione di SQL Server 2019 (anteprima) offre supporto in anteprima per nuove funzionalità e strumenti di spedizione supportare [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Ciò include il supporto di anteprima per [i cluster di SQL Server 2019 dei big data](../big-data-cluster/big-data-cluster-overview.md), un integrata [esperienza notebook](../big-data-cluster/notebooks-guidance.md)e un PolyBase [guidata Create External Table](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json).

## <a name="install-the-sql-server-2019-extension-preview"></a>Installare l'estensione di SQL Server 2019 (anteprima)

Per installare l'estensione di SQL Server 2019 (anteprima), scaricare e installare il file VSIX associato.

1. Scaricare il file VSIX di SQL Server 2019 estensione (anteprima) in una directory locale:

   |Piattaforma|Scarica|Data di rilascio|Versione
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2087443)|18 aprile 2019 |0.12.1
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2087442)|18 aprile 2019 |0.12.1
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2087441)|18 aprile 2019 |0.12.1

1. In Azure Data Studio scegliere **installare l'estensione dal pacchetto VSIX** dalle **File** menu e selezionare il file VSIX scaricato.

1. Scegli **Sì** quando viene richiesto di confermare l'installazione e attendere la notifica che l'installazione ha avuto esito positivo.

1. Selezionare **Ricarica** per abilitare l'estensione (richiesto solo la prima volta in cui l'estensione viene installata).

1. Dopo il ricaricamento, l'estensione installerà le dipendenze. È possibile visualizzare lo stato di avanzamento nella finestra di Output e che potrebbe richiedere alcuni minuti.

1. Dopo le dipendenze completato l'installazione, chiudere e riaprire Data Studio di Azure. Il **cluster di big data di SQL Server** tipo di connessione non è disponibile solo dopo il riavvio Data Studio di Azure.

## <a name="changes-in-release-0121"></a>Modifiche nella versione 0.12.1

* Il **cluster di big data di SQL Server** tipo di connessione è stata rimossa in questa versione. Tutte le funzionalità disponibili in precedenza dalla connessione di cluster di SQL Server i big data sono ora disponibile nella connessione di SQL Server.
* Esplorazione di HDFS sono disponibili nel **Data Services** cartella
* Per i notebook del kernel PySpark e altri dati di lavoro quando si è connessi all'istanza master di SQL Server nel cluster di big data di SQL Server.
* Creazione guidata tabella esterna:
  * Supporto per la creazione di tabella esterna usando l'origine dati esterna esistente.
  * Miglioramenti delle prestazioni attraverso la procedura guidata.
  * Gestione migliorata dei nomi degli oggetti con caratteri speciali. In alcuni casi questi errori causati la procedura guidata non
  * Miglioramenti dell'affidabilità per la pagina Mapping di oggetto.
  * Rimosso database di sistema - 'DWConfiguration', 'Delle DWDiagnostics', 'DWQueue' - dall'elenco a discesa database.
  * Supporto per l'impostazione del nome dell'oggetto External File Format **Create External Table dai file CSV** procedura guidata.
  * Aggiungere un pulsante di aggiornamento per la prima pagina della **Create External Table dai file CSV** procedura guidata.

## <a name="release-notes-v0110"></a>Note sulla versione (v0.11.0)

* Supporto per Notebook di Jupyter, in particolare il supporto per i kernel Spark e Python3, è stato spostato in Azure Data Studio. Questa estensione non è più necessaria per usare i notebook.
* Più correzioni di bug nelle procedure guidate di dati esterni:
  * Mapping dei tipi Oracle sono stati aggiornati per riflettere le modifiche disponibile in versione CTP 2.3 di SQL Server 2019.
  * Risolto un problema in cui sono stati perditi nuovi schemi tipizzati nei controlli di mapping della tabella.
  * Risolto un problema in cui il controllo di un nodo del Database nei mapping di tabella non ha restituito tutte le tabelle e visualizzazioni in fase di verifica.


## <a name="release-notes-v0102"></a>Note sulla versione (v0.10.2)
### <a name="sql-server-2019-support"></a>Supporto di SQL Server 2019
Supporto per SQL Server 2019 è stato aggiornato. Sulla connessione a un Cluster di dati Big data di SQL Server dell'istanza una nuova _Data Services_ cartella viene visualizzata nell'albero di Esplora. Si dispone di punti di avvio per le azioni, ad esempio l'apertura di un nuovo Notebook con la connessione, invio di processi di Spark e l'utilizzo con HDFS. Si noti che per alcune azioni, ad esempio _Create External Data_ tramite una file/cartella HDFS, il _anteprima di SQL Server 2019_ necessario installare l'estensione.

### <a name="notebook-support"></a>Supporto per notebook
Sono stati apportati aggiornamenti significativi per l'interfaccia utente del blocco appunti in questa versione. L'obiettivo è stato in rendendo più semplice leggere i blocchi appunti che vengono condivisi con l'utente. Ciò significava rimuovendo tutte definite dalle caselle attorno alle celle a meno che non selezionato o al passaggio del mouse, aggiunta del supporto al passaggio del mouse per semplici azioni a livello di cella senza dovranno selezionare una cella e chiarire dello stato di esecuzione mediante l'aggiunta di conteggio delle esecuzioni, un oggetto animato _eseguire di significative_ pulsante e altro ancora. Sono stati aggiunti anche i tasti di scelta rapida per _nuovo Notebook_ (`Ctrl+Shift+N`), _eseguire cella_ (`F5`), _nuova cella di codice_ (`Ctrl+Shift+C`),  _Nuova cella di testo_ (`Ctrl+Shift+T`). Per il futuro che sarà l'obiettivo è avere tutte le azioni chiave avviabili da collegamento così Fateci sapere gli elementi desiderati.

Altri miglioramenti e correzioni includono:
* Il _SQL Server 2019 Preview_ estensione ora prompt viene utilizzato per selezionare una directory di installazione per le dipendenze di Python. Non è più include anche Python nel `.vsix file`, la riduzione delle dimensioni complessive dell'estensione. Le dipendenze di Python necessari per supportare i kernel Spark e Python3, in modo da installare questa estensione è necessaria per usare questi.
* È stato aggiunto il supporto per l'avvio di un nuovo notebook dalla riga di comando. Avviare con gli argomenti `--command=notebook.command.new --server=myservername` deve aprire un nuovo notebook e connettersi a questo server.
* Correzioni alle prestazioni per i notebook con una lunghezza di codice di grandi dimensioni nelle celle. Se le celle di codice sono più di 250 righe ha una barra di scorrimento aggiunto.
* Migliorato il supporto di file con estensione ipynb. Versione 3 o versione successiva è ora supportato. Si noti che nel salvataggio di file verrà aggiornato alla versione 4 o versione successiva.
* Il `notebook.enabled` impostazione utente è stato rimosso a questo punto che incorporato nel Notebook è stabile Visualizzatore
* Tema a contrasto elevato è ora supportato con numerose correzioni di layout degli oggetti in questo caso.
* Corretto #3680 in cui gli output illustrato a volte un numero di `,,,` caratteri in modo non corretto
* Editor fisse di #3602 scompare per le celle dopo lo spostamento da studio dei dati di azure
* È stato aggiunto il supporto per usare le visualizzazioni griglia per il `application/vnd.dataresource+json` tipo MIME di output. Ciò significa che molti notebook che utilizzano questo (ad esempio impostando `pd.options.display.html.table_schema` in un notebook di Python) avranno coloro output tabulare fisso & 3959 Azure i dati si tenta di chiusura del server notebook due volte dopo la chiusura del blocco appunti

#### <a name="known-issues"></a>Problemi noti
* All'apertura di un blocco appunti verrà visualizzata la finestra di dialogo install python. Annullamento di questa installazione verificherà i kernel e allega a elenchi a discesa non vengono visualizzati valori previsti. La soluzione alternativa consiste nel completare l'installazione di Python.
* Quando viene aperto un notebook con un kernel non supportato, i kernel e _Collega a_ elenchi a discesa provocherà Studio di Azure Data bloccarsi. È necessario chiudere Data Studio di Azure e assicurarsi di usare un kernel che è supportato (Python3, Spark | Spark, R | Scala, PySpark, PySpark3)
* Collegamento di interfaccia utente di Spark non riesce quando si usa PySpark3 o altri kernel Spark per l'endpoint di SQL Server. In alternativa, fare clic sull'interfaccia utente di Spark nel dashboard o connettersi utilizzando il tipo di connessione del cluster di SQL Server i big data, perché ciò avrà il collegamento corretto dell'interfaccia utente di Spark

### <a name="extensibility-improvements"></a>Miglioramenti di estendibilità
In questa versione sono stati aggiunti numerosi miglioramenti che consentono di Extender
* Un nuovo `ObjectExplorerNodeProvider` API consente alle estensioni di contribuire con le cartelle in SQL Server o altri nodi di connessione. Questo è il modo in `Data Services` nodo viene aggiunto sotto le istanze di SQL Server 2019 ma può essere usato per aggiungere facilmente monitoraggio o altre cartelle per l'interfaccia utente.
* Due nuovi valori di chiave contesto sono disponibili per i contributi Mostra/Nascondi al dashboard.
  * `mssql:iscluster` indica se si tratta di un Cluster di dati grande SQL Server 2019
  * `mssql:servermajorversion` ha la versione del server (15 per SQL Server 2019, 14 per SQL Server 2017 e così via). Può essere utile funzionalità dovrebbero essere visualizzate solo per SQL Server 2017 o versione successiva, ad esempio.


## <a name="release-notes-v080"></a>Note sulla versione (v0.8.0)
*I notebook*:
* Aggiunta di celle prima / dopo esistente facendo clic sul pulsante "Altre azioni" cella è ora supportato celle
* **Aggiungi nuova connessione** aggiunta l'opzione per le connessioni nell'elenco a discesa "Allega a"
* Oggetto **reinstallare le dipendenze di Notebook** comando è stato aggiunto supporto per gli aggiornamenti dei pacchetti Python e risolvere i casi in cui installazione è stata interrotta ferma chiudendo l'applicazione. Può essere eseguito dal riquadro comandi (usare `Ctrl/Cmd+Shift+P` e il tipo `Reinstall Notebook Dependencies`)
* Il pacchetto python PROSE è stato aggiornato alla versione 1.1.0 e include una serie di correzioni di bug. Usare la **reinstallare le dipendenze di Notebook** comando per aggiornare il pacchetto
* Oggetto **Cancella Output** comando è ora supportato facendo le **altre azioni** pulsante della cella
* Risolto seguenti problemi segnalati dai clienti:
  * Sessione di notebook non è stato possibile avviare in Windows a causa di problemi di percorso
  * Non è stato possibile avviare Blocco note dalla cartella radice di un'unità, ad esempio C:\ o D:\
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) non è possibile modificare i notebook creati da annunci pubblicitari in Visual Studio Code
  * Collegamento di interfaccia utente di Spark funziona ora quando si esegue un kernel Spark
  * Rinominare "Managed Package" a "Installa pacchetti"

*Creare dati esterni*:

* Messaggi di errore sono copiabili e sono stati separati in una vista di riepilogo e dettagliata per la più semplice
* Layout dell'interfaccia utente migliorato e in modo significativo miglioramento dell'affidabilità e la gestione degli errori
* Risolto seguenti problemi segnalati dai clienti:
  * Le tabelle con il mapping delle colonne non valide vengono visualizzate come disabilitato e un messaggio di avviso viene illustrato l'errore

## <a name="release-notes-v072"></a>Note sulla versione (v0.7.2)
* Esplora risorse di Azure è ora incorporato in Azure Data Studio ed è stata rimossa da questa estensione. Grazie per i tuoi commenti su questo.
* Miglioramento delle prestazioni di notebook con numero di celle Markdown.
* Celle di codice il ridimensionamento automatico in Notebook. Questo ha ancora una dimensione minima basata sulla barra degli strumenti di cella.
* Avvisa utente quando l'installazione delle dipendenze di Notebook. In Windows in particolare l'operazione può richiedere un molto tempo, in modo che le notifiche vengono ora visualizzate nella visualizzazione attività.
* Supporto per reinstallare le dipendenze di Notebook. Ciò è utile se l'utente precedentemente chiuso Studio di Azure Data introdursi nell'installazione.
* Supporto per l'annullamento dell'esecuzione di celle nel Notebook.
* Maggiore affidabilità quando si utilizza Create External Data guidata, in particolare quando connessione si verificano errori.
* Blocca l'uso della procedura guidata Create External Data se PolyBase non è abilitato o è in esecuzione nel server di destinazione.
* Controllo ortografia e la denominazione correzioni relative a SQL Server 2019 e creare dati esterni.
* Rimosso un numero elevato di errori dalla console di debug di Studio dei dati di Azure.

##  <a name="sql-server-2019-big-data-cluster-support"></a>Supporto di SQL Server 2019 Big Data Cluster

* Fare clic su **Aggiungi connessione** nelle *Esplora oggetti* e scegliere **cluster di big data di SQL Server** come tipo di connessione.

   > [!TIP]
   > Se non viene visualizzato il **cluster di big data di SQL Server** tipo di connessione, riavviare Azure Studio dei dati.

* Immettere il nome host o indirizzo IP dell'endpoint del cluster più il nome utente e password utilizzata per la connessione.
* Facoltativamente, includere un nome descrittivo visualizzato nei **nome** campo.
* Fare clic su **Connect** e quindi è possibile avviare attività comuni nel dashboard, esplorare **HDFS** in Esplora oggetti ed esecuzione di attività nel contesto da tale posizione.
* Per inviare un processo Spark nel cluster, fare doppio clic sul nodo del server nella *Esplora oggetti* e scegliere **Submit Spark Job** per visualizzare la finestra di dialogo di invio.
* Per aprire un Notebook, vedere la sezione successiva.

Per informazioni dettagliate, vedere [i cluster di Big Data](../big-data-cluster/big-data-cluster-overview.md).


## <a name="azure-data-studio-notebooks"></a>Notebook di Studio dei dati di Azure

* Aprire un notebook in uno dei modi seguenti:
  * Aprire un nuovo notebook dal *comandi*.
  * Aprire l'albero di Esplora oggetti di HDFS per un cluster di big data 2019 di SQL Server e uno:
    * Fare clic con il pulsante destro sul nodo del server e scegliere **nuovo Jupyter Notebook**.
    * Fare clic con il pulsante destro su un file CSV e scegliere **analizza in Notebook**.
  * Aprire un file con estensione ipynb esistente dal **File** dal menu o Esplora file *(file con estensione ipynb devono essere aggiornati alla versione 4 o versione successiva per caricare correttamente)*
* Scegliere un kernel. Per l'esecuzione di notebook locale, scegliere Python 3. Per l'esecuzione remota, scegliere PySpark o Spark | Scala.
* Scegliere un endpoint del cluster SQL Server i big data a cui connettersi se l'esecuzione in modalità remota (non necessario per lo sviluppo locale con Python 3).
* Aggiunta di celle di codice o markdown tramite i pulsanti nell'intestazione del notebook. Rimuovere le celle con l'icona del Cestino a sinistra di ciascuna cella.
* Eseguire le celle con il pulsante play per le celle di codice e attivare la modifica di markdown e visualizzare in anteprima con l'icona sotto controllo

## <a name="polybase-create-external-table-wizard"></a>PolyBase Creazione guidata tabella esterna

* Da un'istanza di SQL Server 2019 il *Creazione guidata tabella esterna* possono essere aperti in tre modi:
  * Fare clic con il pulsante destro su un server, scegliere **Manage**, fare clic sulla scheda per SQL Server 2019 (anteprima) e scegliere **Create External Table**.
  * Con un'istanza di SQL Server 2019 selezionata in *Esplora oggetti*, visualizziamo *Creazione guidata esterno* tramite il *comandi*.
  * Fare clic con il pulsante destro su un database di SQL Server 2019 *Esplora oggetti* e scegliere **Create External Table**.
* In questa versione dell'estensione, è possibile creare tabelle esterne per accedere a tabelle remote di SQL Server e Oracle.

  > [!NOTE]
  > Mentre la funzionalità tabella esterna è una funzionalità 2019 SQL, il Server SQL remoto potrebbe essere in esecuzione una versione precedente di SQL Server.

* Scegliere se accede a SQL Server o Oracle nella prima pagina della procedura guidata e continuare.
* Verrà richiesto di creare una chiave Master del Database se non ne è stato creato (verranno bloccate le password di complessità insufficiente).
* Creare una connessione all'origine dati e denominato di credenziali per il server remoto.
* Scegliere quali oggetti per eseguire il mapping alla nuova tabella esterna.
* Scegli **genera Script** oppure **crea** per completare la procedura guidata.
* Dopo la creazione della tabella esterna, viene immediatamente visualizzato nell'albero degli oggetti del database in cui è stato creato.


## <a name="known-issues"></a>Problemi noti

* Se la password non viene salvata quando si crea una connessione, alcune azioni, ad esempio l'invio del processo Spark potrebbero non riuscire.
* I notebook con estensione ipynb esistente devono essere aggiornati alla versione 4 o versione successiva per caricare contenuto nel Visualizzatore.
* In esecuzione la **reinstallare le dipendenze di Notebook** 2 attività potrebbe visualizzare nella visualizzazione attività, uno dei quali ha esito negativo. Questo non prevede l'esito negativo dell'installazione
* Scelta **Aggiungi nuova connessione** in un Notebook e fare clic su Annulla causerà **Seleziona connessione** vengano visualizzati, anche se sono stati già connessi.
