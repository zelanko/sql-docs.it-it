---
title: Estensione di SQL Server 2019 (anteprima)
titleSuffix: Azure Data Studio
description: Estensione di anteprima di SQL Server 2019 per Data Studio di Azure
ms.custom: seodec18
ms.date: 01/10/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c41c2a08f0b8d608ef21cd44a60a2d63cdeb5fed
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143314"
---
# <a name="sql-server-2019-extension-preview"></a>Estensione di SQL Server 2019 (anteprima)

L'estensione di SQL Server 2019 (anteprima) offre supporto in anteprima per nuove funzionalità e strumenti di spedizione supportare [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Ciò include il supporto di anteprima per [i cluster di SQL Server 2019 dei big data](../big-data-cluster/big-data-cluster-overview.md), un integrata [esperienza notebook](../big-data-cluster/notebooks-guidance.md), un PolyBase [guidata Create External Table](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json)e [Esplora risorse di azure](azure-resource-explorer.md).

## <a name="install-the-sql-server-2019-extension-preview"></a>Installare l'estensione di SQL Server 2019 (anteprima)

Per installare l'estensione di SQL Server 2019 (anteprima), scaricare e installare il file VSIX associato.

1. Scaricare il file VSIX di SQL Server 2019 estensione (anteprima) in una directory locale:

   |Piattaforma|Scarica|Data di rilascio|Versione
   |:---|:---|:---|:---|
   |WINDOWS|[VSIX](https://go.microsoft.com/fwlink/?linkid=2051167)|09 gennaio 2019 |0.9.1
   |macOS|[VSIX](https://go.microsoft.com/fwlink/?linkid=2051166)|09 gennaio 2019 |0.9.1
   |Linux|[VSIX](https://go.microsoft.com/fwlink/?linkid=2051165)|09 gennaio 2019 |0.9.1

1. In Azure Data Studio scegliere **installare l'estensione dal pacchetto VSIX** dalle **File** menu e selezionare il file VSIX scaricato.

1. Scegli **Sì** quando viene richiesto di confermare l'installazione e attendere la notifica che l'installazione ha avuto esito positivo.

1. Selezionare **Ricarica** per abilitare l'estensione (richiesto solo la prima volta in cui l'estensione viene installata).

1. Dopo il ricaricamento, l'estensione installerà le dipendenze. È possibile visualizzare lo stato di avanzamento nella finestra di Output e che potrebbe richiedere alcuni minuti.

1. Dopo le dipendenze completato l'installazione, chiudere e riaprire Data Studio di Azure. Il **cluster di big data di SQL Server** tipo di connessione non è disponibile solo dopo il riavvio Data Studio di Azure.

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