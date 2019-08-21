---
title: Configurare un client di data science per lo sviluppo R
description: Installare le librerie e gli strumenti R locali in una workstation di sviluppo per le connessioni remote ai SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c81a69181d1bc723e622bac9ffeb5ff67fd0280
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633639"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurare un client data science per lo sviluppo R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

L'integrazione di r è disponibile in SQL Server 2016 o versione successiva quando si include l'opzione del linguaggio R in un'installazione di [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) o [SQL Server Machine Learning Services (in-database)](../install/sql-machine-learning-services-windows-install.md) . 

Per sviluppare e distribuire soluzioni R per SQL Server, installare [Microsoft R client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) nella workstation di sviluppo per ottenere [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e altre librerie r. La libreria RevoScaleR, necessaria anche per l'istanza di SQL Server remota, coordina le richieste di elaborazione tra entrambi i sistemi. 

Questo articolo illustra come configurare una workstation di sviluppo client R in modo che sia possibile interagire con una SQL Server remota abilitata per l'integrazione di machine learning e R. Dopo aver completato i passaggi descritti in questo articolo, si avranno le stesse librerie R disponibili in SQL Server. Si saprà anche come effettuare il push di calcoli da una sessione di R locale a una sessione di R remota in SQL Server.

![Componenti client-server](media/sqlmls-r-client-revo.png "Sessioni e librerie R locali e remote")

Per convalidare l'installazione, è possibile usare lo strumento **RGUI** incorporato, come descritto in questo articolo, oppure [collegare le librerie](#install-ide) a rstudio o a qualsiasi altro IDE usato in genere.

> [!Note]
> Un'alternativa all'installazione della libreria client consiste nell'utilizzo di un [server autonomo](../install/sql-machine-learning-standalone-windows-install.md) come rich client, che alcuni clienti preferiscono per lavorare in uno scenario più approfondito. Un server autonomo è completamente separato dal SQL Server, ma poiché ha le stesse librerie R, è possibile usarlo come client per SQL Server analisi nel database. È anche possibile usarlo per il lavoro non correlato a SQL, inclusa la possibilità di importare e modellare i dati da altre piattaforme di dati. Se si installa un server autonomo, è possibile trovare il file eseguibile R in `C:\Program Files\Microsoft SQL Server\140\R_SERVER`questo percorso:. Per convalidare l'installazione, [aprire un'app console r](#R-tools) per eseguire i comandi usando r. exe in quel percorso.

## <a name="commonly-used-tools"></a>Strumenti di uso comune

Che tu sia uno sviluppatore R nuovo a SQL o uno sviluppatore SQL nuovo a R e analisi nel database, ti servirà sia uno strumento di sviluppo R sia un editor di query T-SQL, ad esempio [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) , per esercitare tutte le funzionalità di nel database analisi.

Per gli scenari di sviluppo R semplici, è possibile usare il file eseguibile RGUI, incluso nella distribuzione R di base in riparazione e SQL Server. Questo articolo illustra come usare RGUI per sessioni R locali e remote. Per migliorare la produttività, è consigliabile usare un IDE completo, ad esempio [rstudio o Visual Studio](#install-ide).

SSMS è un download separato, utile per la creazione e l'esecuzione di stored procedure su SQL Server, inclusi quelli che contengono codice R. Quasi tutti i codici R scritti in un ambiente di sviluppo possono essere incorporati in un stored procedure. È possibile eseguire altre esercitazioni per ottenere informazioni su [SSMS e R Embedded](../tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="1---install-r-packages"></a>1-installare i pacchetti R

I pacchetti R Microsoft sono disponibili in più prodotti e servizi. In una workstation locale è consigliabile installare Microsoft R Client. R client fornisce [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)e altri pacchetti r.

1. [Scaricare Microsoft R client](https://aka.ms/rclient/download).

2. Nell'installazione guidata, accettare o modificare il percorso di installazione predefinito, accettare o modificare l'elenco dei componenti e accettare le condizioni di licenza Microsoft R Client.

  Al termine dell'installazione, una schermata iniziale presenta il prodotto e la documentazione.

3. Creare una variabile di ambiente di sistema MKL_CBWR per garantire l'output coerente sui calcoli di Intel Math Kernel Library (MKL).

  + Nel pannello di controllo fare clic su sistema **e sicurezza** > **sistema** > **Impostazioni** > di sistema avanzate**variabili di ambiente**.
  + Creare una nuova variabile di sistema denominata **MKL_CBWR**con un valore impostato su **auto**.

## <a name="2---locate-executables"></a>2-individuare i file eseguibili

Individuare ed elencare il contenuto della cartella di installazione per verificare che siano installati R. exe, RGUI e altri pacchetti. 

1. In Esplora file aprire la cartella C:\Program Files\Microsoft\R Client\R_SERVER\bin per confermare il percorso di R. exe.

2. Aprire la sottocartella x64 per confermare **RGUI**. Questo strumento verrà usato nel passaggio successivo.

3. Aprire C:\Program Files\Microsoft\R Client\R_SERVER\library per esaminare l'elenco dei pacchetti installati con R client, inclusi RevoScaleR, MicrosoftML e altri.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3-avviare RGUI

Quando si installa R con SQL Server, si ottengono gli stessi strumenti R standard per qualsiasi installazione di base di R, ad esempio RGui, Rterm e così via. Questi strumenti sono semplici, utili per verificare le informazioni relative a pacchetti e librerie, per eseguire comandi o script ad hoc o per esaminare le esercitazioni. È possibile usare questi strumenti per ottenere informazioni sulla versione di R e confermare la connettività.

1. Aprire C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 e fare doppio clic su **RGui** per avviare una sessione di r con un prompt dei comandi di r.

  Quando si avvia una sessione di R da una cartella del programma Microsoft, vengono caricati automaticamente diversi pacchetti, tra cui RevoScaleR. 

2. Immettere `print(Revo.version)` al prompt dei comandi per restituire le informazioni sulla versione del pacchetto RevoScaleR. È necessario avere la versione 9.2.1 o 9.3.0 per RevoScaleR.

3. Immettere **Search ()** al prompt di R per un elenco dei pacchetti installati.

   ![Informazioni sulla versione durante il caricamento di R](../install/media/rclient-rgui-r-prompt.png "Aprire un prompt di R")


## <a name="4---get-sql-permissions"></a>4-ottenere le autorizzazioni SQL

In R client l'elaborazione R è limitata a due thread e ai dati in memoria. Per l'elaborazione scalabile con più core e set di dati di grandi dimensioni, è possibile spostare l'esecuzione (denominata *contesto di calcolo*) per i set di dati e la potenza di calcolo di un'istanza di SQL Server remota. Si tratta dell'approccio consigliato per l'integrazione dei client con un'istanza di SQL Server di produzione e per renderlo funzionante sono necessarie le autorizzazioni e le informazioni di connessione.

Per connettersi a un'istanza di SQL Server per eseguire gli script e caricare i dati, è necessario disporre di un account di accesso valido nel server di database. È possibile usare un account di accesso SQL o un'autenticazione integrata di Windows. È in genere consigliabile usare l'autenticazione integrata di Windows, ma l'uso dell'account di accesso SQL è più semplice per alcuni scenari, in particolare quando lo script contiene stringhe di connessione a dati esterni.

Come minimo, l'account utilizzato per eseguire il codice deve disporre dell'autorizzazione di lettura dai database utilizzati, oltre all'autorizzazione speciale per l'esecuzione di qualsiasi SCRIPT esterno. La maggior parte degli sviluppatori richiede anche le autorizzazioni per la creazione di stored procedure e per la scrittura di dati in tabelle contenenti dati di training o dati con punteggio. 

Chiedere all'amministratore del database di [configurare le autorizzazioni seguenti per l'account](../security/user-permission.md)nel database in cui si usa R:

+ **Eseguire uno script esterno** per eseguire lo script R nel server.
+ privilegi **db_datareader** per eseguire le query utilizzate per il training del modello.
+ **db_datawriter** scrivere dati di training o dati con punteggio.
+ **db_owner** per la creazione di oggetti quali stored procedure, tabelle, funzioni. 
  È inoltre necessario che **db_owner** crei database di esempio e di test. 

Se per il codice sono necessari pacchetti non installati per impostazione predefinita con SQL Server, disporre con l'amministratore del database in modo che i pacchetti siano installati con l'istanza di. SQL Server è un ambiente protetto e sono presenti restrizioni per la posizione in cui è possibile installare i pacchetti. Per altre informazioni, vedere [Install New R packages on SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5-test delle connessioni

 Come passaggio di verifica, usare **RGUI** e RevoScaleR per confermare la connettività al server remoto. SQL Server deve essere abilitato per le [connessioni remote](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) ed è necessario disporre delle autorizzazioni, tra cui un account di accesso utente e un database a cui connettersi. 

I passaggi seguenti presuppongono il database demo, [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)e l'autenticazione di Windows.

1. Aprire **RGUI** nella workstation client. Ad esempio, passare a `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` e fare doppio clic su **RGui. exe** per avviarlo.

2. RevoScaleR viene caricato automaticamente. Verificare che RevoScaleR sia operativo eseguendo questo comando:`print(Revo.version)`

3. Immettere lo script demo eseguito sul server remoto. Per includere un nome valido per un'istanza di SQL Server remota, è necessario modificare lo script di esempio seguente. Questa sessione inizia come sessione locale, ma la funzione **rxSummary** viene eseguita nell'istanza di SQL Server remota.

  ```R
  # Define a connection. Replace server with a valid server name.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  
  # Specify the input data in a SQL query.
  sampleQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
  
  # Define a remote compute context based on the remote server.
  cc <-RxInSqlServer(connectionString=connStr)

  # Execute the function using the remote compute context.
  rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr), computeContext=cc)
  ```

  **Risultati:**

  Questo script si connette a un database nel server remoto, fornisce una query, crea un'istruzione del contesto `cc` di calcolo per l'esecuzione di codice in modalità remota, quindi fornisce la funzione RevoScaleR **rxSummary** per restituire un riepilogo statistico della query Risultati.

  ```R
    Call:
  rxSummary(formula = ~., data = RxSqlServerData(sqlQuery = sampleQuery, 
      connectionString = connStr), computeContext = cc)

  Summary Statistics Results for: ~.
  Data: RxSqlServerData(sqlQuery = sampleQuery, connectionString = connStr) (RxSqlServerData Data Source)
  Number of valid observations: 100 
  
  Name       Mean   StdDev   Min Max ValidObs MissingObs
  tip_amount 63.245 31.61087 36  180 100      0     
  ```

4. Ottenere e impostare il contesto di calcolo. Una volta impostato un contesto di calcolo, rimane attivo per la durata della sessione. Se non si è certi che il calcolo sia locale o remoto, eseguire il comando seguente per scoprirlo. I risultati che specificano una stringa di connessione indicano un contesto di calcolo remoto.

  ```R
  # Return the current compute context.
  rxGetComputeContext()

  # Revert to a local compute context.
  rxSetComputeContext("local")
  rxGetComputeContext()

  # Switch back to remote.
  connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  cc <-RxInSqlServer(connectionString=connStr)
  rxSetComputeContext(cc)
  rxGetComputeContext()
  ```  

5. Restituisce informazioni sulle variabili nell'origine dati, inclusi il nome e il tipo.

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  I risultati includono 23 variabili.


6. Generare un tracciato a dispersione per esplorare la presenza di dipendenze tra due variabili. 

  ```R
  # Set the connection string. Substitute a valid server name for the placeholder.
  connStr <- "Driver=SQL Server;Server=<your database name>;Database=NYCTaxi_Sample;Trusted_Connection=true"

  # Specify a query on the nyctaxi_sample table.
  # For variables on each axis, remove nulls. Use a WHERE clause and <> to do this.
  sampleQuery <-"SELECT DISTINCT TOP 100 * from [dbo].[nyctaxi_sample] WHERE fare_amount <> '' AND  tip_amount <> ''"
  cc <-RxInSqlServer(connectionString=connStr)

  # Generate a scatter plot.
  rxLinePlot(fare_amount ~ tip_amount, data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr, computeContext=cc), type="p")
  ```

  Lo screenshot seguente mostra l'output del grafico di input e dispersione.

   ![Grafico a dispersione in RGUI](media/rclient-setup-scatterplot.png "Grafico a dispersione sui dati demo di NYC Taxi")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6-Collegare gli strumenti a R. exe

Per i progetti di sviluppo gravi e continui, è necessario installare un Integrated Development Environment (IDE). Gli strumenti di SQL Server e gli strumenti R incorporati non sono attrezzati per uno sviluppo R intenso. Una volta creato il codice di lavoro, è possibile distribuirlo come stored procedure per l'esecuzione su SQL Server.

Puntare l'IDE alle librerie R locali: base R, RevoScaleR e così via. L'esecuzione di carichi di lavoro in una SQL Server remota si verifica durante l'esecuzione dello script, quando lo script richiama un contesto di calcolo remoto su SQL Server, accedendo ai dati e alle operazioni su tale server.

### <a name="rstudio"></a>RStudio

Quando si usa [rstudio](https://www.rstudio.com/), è possibile configurare l'ambiente in modo da usare le librerie R e gli eseguibili che corrispondono a quelli in una SQL Server remota.

1. Controllare le versioni del pacchetto R installate in SQL Server. Per altre informazioni, vedere [ottenere informazioni sul pacchetto R](../package-management/r-package-information.md).

1. Installare Microsoft R Client o una delle opzioni del server autonomo per aggiungere RevoScaleR e altri pacchetti R, inclusa la distribuzione R di base usata dall'istanza di SQL Server. Scegliere una versione allo stesso livello o inferiore (i pacchetti sono compatibili con le versioni precedenti) che fornisce le stesse versioni del pacchetto del server. Per informazioni sulla versione, vedere la mappa delle versioni in questo articolo: [Aggiornare i componenti di R e Python](../install/upgrade-r-and-python.md).

1. In RStudio [aggiornare il percorso di r](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) in modo che punti all'ambiente r che fornisce RevoScaleR, Microsoft R Open e altri pacchetti Microsoft. 

  + Per un'installazione client R, cercare C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64
  + Per un server autonomo, cercare C:\Programmi\Microsoft SQL Server\140\R_SERVER\Library o C:\Programmi\Microsoft SQL Server\130\R_SERVER\Library

2. Chiudere e quindi aprire RStudio.

Quando si riapre RStudio, il file eseguibile R da R client (o server autonomo) è il motore R predefinito.


### <a name="r-tools-for-visual-studio-rtvs"></a>R Tools per Visual Studio (RTVS)

Se non si dispone già di un IDE preferito per R, è consigliabile **R Tools per Visual Studio**.

+ [Scarica R Tools per Visual Studio (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [Istruzioni di installazione](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) : RTVS è disponibile in diverse versioni di Visual Studio.
+ [Inizia a usare R Tools per Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Connettersi a SQL Server da RTVS

Questo esempio usa Visual Studio 2017 Community Edition con il carico di lavoro data science installato.

1. Scegliere **nuovo** dal menu **file** e quindi selezionare **progetto**.

2. Il riquadro a sinistra contiene un elenco dei modelli preinstallati. Fare clic su **r**e selezionare **progetto r**. Nella casella **nome** Digitare `dbtest` e fare clic su **OK**. 

  Visual Studio crea una nuova cartella di progetto e un file `Script.R`di script predefinito. 

3. Digitare `.libPaths()` nella prima riga del file di script, quindi premere CTRL + INVIO.

  Il percorso della libreria R corrente dovrebbe essere visualizzato nella finestra **R interattivo** . 

4. Fare clic sul menu **r Tools** e selezionare **Windows** per visualizzare un elenco di altre finestre specifiche di r che è possibile visualizzare nell'area di lavoro.
 
  + Per visualizzare la guida sui pacchetti nella libreria corrente, premere CTRL + 3.
  + Vedere variabili R nel **Esplora variabili**, premendo CTRL + 8.

## <a name="next-steps"></a>Passaggi successivi

Due esercitazioni diverse includono esercizi che consentono di cambiare il contesto di calcolo da locale a un'istanza di SQL Server remota.

+ [Esercitazione: Usare le funzioni R RevoScaleR con i dati SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Procedura dettagliata end-to-end per l'analisi scientifica dei dati](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)