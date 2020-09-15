---
title: Configurare un client di data science R
description: Installare le librerie e gli strumenti R locali in una workstation di sviluppo per le connessioni remote a SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 95390a1eb5418a43883a9605c7498e6a86876e7e
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178898"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurare un client di data science per lo sviluppo in R in SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

L'integrazione di R è disponibile in SQL Server 2016 o versione successiva quando si include l'opzione del linguaggio R in un'installazione di [R Services per SQL Server 2016](../install/sql-r-services-windows-install.md) o [Machine Learning Services per SQL Server (In-Database)](../install/sql-machine-learning-services-windows-install.md). 

Per sviluppare e distribuire soluzioni R per SQL Server, installare [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) nella workstation di sviluppo per ottenere [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e altre librerie R. La libreria RevoScaleR, richiesta anche nell'istanza di SQL Server remota, coordina le richieste di calcolo tra i due sistemi. 

Questo articolo illustra come configurare una workstation di sviluppo R Client per poter interagire con un'istanza remota di SQL Server abilitata per l'integrazione di R e Machine Learning. Dopo aver completato i passaggi descritti in questo articolo, si disporrà delle stesse librerie R presenti in SQL Server. Si saprà anche come eseguire il push dei calcoli da una sessione di R locale a una sessione di R remota in SQL Server.

![Componenti client-server](media/sqlmls-r-client-revo.png "Sessioni e librerie R locali e remote")

Per convalidare l'installazione, è possibile usare lo strumento **RGUI** predefinito, come descritto in questo articolo, oppure [collegare le librerie](#install-ide) a RStudio o a qualsiasi altro ambiente di sviluppo integrato (IDE) usato in genere.

> [!Note]
> Un'alternativa all'installazione delle librerie client consiste nell'usare un [server autonomo](../install/sql-machine-learning-standalone-windows-install.md) come rich client, che alcuni clienti preferiscono per lavorare in uno scenario più ampio. Un server autonomo è completamente separato da SQL Server, ma poiché ha le stesse librerie R, è possibile usarlo come client per l'analisi nel database di SQL Server. È anche possibile usarlo per attività non correlate a SQL, inclusa la possibilità di importare e modellare i dati da altre piattaforme di dati. Se si installa un server autonomo, è possibile trovare l'eseguibile R in questo percorso: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. Per convalidare l'installazione, [aprire un'app console R](#R-tools) per eseguire i comandi usando R.exe in quel percorso.

## <a name="commonly-used-tools"></a>Strumenti di uso comune

Che si sia uno sviluppatore R che inizia a usare SQL o uno sviluppatore SQL che inizia a usare R e l'analisi nel database, sono necessari sia uno strumento di sviluppo R sia un editor di query T-SQL, ad esempio [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), per sfruttare tutte le funzionalità di analisi nel database.

Per gli scenari di sviluppo R semplici, è possibile usare il file eseguibile RGUI, incluso nella distribuzione R di base in MRO e SQL Server. Questo articolo illustra come usare RGUI per sessioni R locali e remote. Per migliorare la produttività, è consigliabile usare un IDE completo, ad esempio [RStudio o Visual Studio](#install-ide).

SSMS è una soluzione scaricabile separatamente, utile per la creazione e l'esecuzione di stored procedure in SQL Server, incluse quelle contenenti codice R. Quasi tutto il codice R scritto in un ambiente di sviluppo può essere incorporato in una stored procedure. È possibile eseguire altre esercitazioni per scoprire di più su [SSMS e R incorporato](../tutorials/r-taxi-classification-introduction.md).

## <a name="1---install-r-packages"></a>1 - Installare i pacchetti R

I pacchetti R di Microsoft sono disponibili in più prodotti e servizi. In una workstation locale è consigliabile installare Microsoft R Client. R Client include [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) e altri pacchetti R.

1. [Scaricare Microsoft R Client](https://aka.ms/rclient/download).

2. Nell'installazione guidata accettare o modificare il percorso di installazione predefinito, accettare o modificare l'elenco dei componenti e accettare le condizioni di licenza di Microsoft R Client.

   Al termine dell'installazione, una schermata iniziale presenta il prodotto e la documentazione.

3. Creare una variabile di ambiente di sistema MKL_CBWR per garantire l'output coerente per i calcoli MKL (Math Kernel Library) di Intel.

   + Nel Pannello di controllo fare clic su **Sistema e sicurezza** > **Sistema** > **Impostazioni di sistema avanzate** > **Variabili d'ambiente**.
   + Creare una nuova variabile di sistema denominata **MKL_CBWR**, con un valore impostato su **AUTO**.

## <a name="2---locate-executables"></a>2 - Individuare gli eseguibili

Individuare ed elencare il contenuto della cartella di installazione per verificare che siano installati R.exe, RGUI e gli altri pacchetti. 

1. In Esplora file aprire la cartella C:\Programmi\Microsoft\R Client\R_SERVER\bin per confermare il percorso di R.exe.

2. Aprire la sottocartella x64 per confermare **RGUI**. Questo strumento verrà usato nel passaggio successivo.

3. Aprire C:\Programmi\Microsoft\R Client\R_SERVER\library per controllare l'elenco dei pacchetti installati con R Client, inclusi RevoScaleR, MicrosoftML e altri.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3 - Avviare RGUI

Quando si installa R con SQL Server, si ottengono gli stessi strumenti R standard per qualsiasi installazione di base di R, ad esempio RGui, Rterm e così via. Questi strumenti sono leggeri, utili per verificare le informazioni relative a pacchetti e librerie, per eseguire comandi o script ad hoc o per seguire le esercitazioni. È possibile usare questi strumenti per ottenere informazioni sulla versione di R e confermare la connettività.

1. Aprire C:\Programmi\Microsoft\R Client\R_SERVER\bin\x64 e fare doppio clic su **RGui** per avviare una sessione di R con un prompt dei comandi di R.

   Quando si avvia una sessione di R da una cartella di programma Microsoft, vengono caricati automaticamente diversi pacchetti, tra cui RevoScaleR. 

2. Immettere `print(Revo.version)` al prompt dei comandi per restituire le informazioni sulla versione del pacchetto RevoScaleR. È necessario avere la versione 9.2.1 o 9.3.0 per RevoScaleR.

3. Immettere **search()** al prompt di R per un elenco dei pacchetti installati.

   ![Informazioni sulla versione durante il caricamento di R](../install/media/rclient-rgui-r-prompt.png "Aprire un prompt di R")


## <a name="4---get-sql-permissions"></a>4 - Ottenere le autorizzazioni SQL

In R Client l'elaborazione R è limitata a due thread e ai dati in memoria. Per l'elaborazione scalabile con più core e set di dati di grandi dimensioni, è possibile spostare l'esecuzione (definita *contesto di calcolo*) sui set di dati e la potenza di calcolo di un'istanza di SQL Server remota. Si tratta dell'approccio consigliato per l'integrazione del client con un'istanza di SQL Server di produzione e per poterlo applicare sono necessarie autorizzazioni e informazioni di connessione.

Per connettersi a un'istanza di SQL Server per eseguire gli script e caricare i dati, è necessario disporre di un account di accesso valido nel server di database. È possibile usare un account di accesso SQL o un'autenticazione integrata di Windows. In genere è consigliabile usare l'autenticazione integrata di Windows, ma l'uso dell'account di accesso SQL è più semplice per alcuni scenari, in particolare quando lo script contiene stringhe di connessione ai dati esterni.

L'account usato per eseguire il codice deve disporre almeno dell'autorizzazione di lettura dai database usati, oltre che dell'autorizzazione speciale EXECUTE ANY EXTERNAL SCRIPT. La maggior parte degli sviluppatori richiede anche le autorizzazioni per la creazione di stored procedure e per la scrittura dei dati in tabelle contenenti dati di training o dati con punteggio. 

Chiedere all'amministratore del database di [configurare le autorizzazioni seguenti per l'account](../security/user-permission.md) nel database in cui si usa R:

+ **EXECUTE ANY EXTERNAL SCRIPT** per eseguire script R nel server.
+ Privilegi **db_datareader** per eseguire le query usate per il training del modello.
+ **db_datawriter** per scrivere i dati di training o i dati con punteggio.
+ **db_owner** per creare oggetti come stored procedure, tabelle e funzioni. 
  Il ruolo **db_owner** è anche necessario per creare database di esempio e di test. 

Se il codice richiede pacchetti non installati per impostazione predefinita con SQL Server, chiedere all'amministratore del database di installare i pacchetti con l'istanza. SQL Server è un ambiente sicuro e prevede restrizioni relative alla posizione in cui è possibile installare i pacchetti. Per altre informazioni, vedere [Installare nuovi pacchetti R in SQL Server](../package-management/install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5 - Testare le connessioni

Come passaggio di verifica, usare **RGUI** e RevoScaleR per verificare la connettività al server remoto. SQL Server deve essere abilitato per le [connessioni remote](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) ed è necessario avere le autorizzazioni appropriate, tra cui un account di accesso utente e un database a cui connettersi. 

I passaggi seguenti presuppongono l'uso del database di esempio [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md) e dell'autenticazione di Windows.

1. Aprire **RGUI** nella workstation client. Ad esempio, passare a `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` e fare doppio clic su **RGui.exe** per avviarlo.

2. RevoScaleR viene caricato automaticamente. Verificare che RevoScaleR sia operativo eseguendo questo comando: `print(Revo.version)`

3. Immettere lo script demo eseguito nel server remoto. È necessario modificare lo script di esempio seguente per includere un nome valido per un'istanza di SQL Server remota. Questa sessione inizia come sessione locale, ma la funzione **rxSummary** viene eseguita nell'istanza di SQL Server remota.

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

   Questo script si connette a un database nel server remoto, fornisce una query, crea un'istruzione `cc` del contesto di calcolo per l'esecuzione remota del codice, quindi fornisce la funzione RevoScaleR **rxSummary** per restituire un riepilogo statistico dei risultati della query.

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

4. Ottenere e impostare il contesto di calcolo. Una volta impostato, il contesto di calcolo rimane attivo per la durata della sessione. Se non si è certi se i calcoli vengono eseguiti in locale o in remoto, eseguire il comando seguente per scoprirlo. I risultati che specificano una stringa di connessione indicano un contesto di calcolo remoto.

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

5. Restituire informazioni sulle variabili nell'origine dati, inclusi il nome e il tipo.

   ```R
   rxGetVarInfo(data = inDataSource)
   ```
   I risultati includono 23 variabili.


6. Generare un grafico a dispersione per appurare se sono presenti dipendenze tra due variabili. 

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

   Lo screenshot seguente mostra l'input e il grafico a dispersione di output.

   ![Grafico a dispersione in RGUI](media/rclient-setup-scatterplot.png "Grafico a dispersione dei dati demo di NYC Taxi")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6 - Collegare gli strumenti a R.exe

Per i progetti di sviluppo seri e duraturi, è necessario installare un ambiente di sviluppo integrato (IDE). Gli strumenti di SQL Server e gli strumenti R predefiniti non sono attrezzati per attività di sviluppo impegnative con R. Dopo aver creato il codice operativo, è possibile distribuirlo come stored procedure per l'esecuzione in SQL Server.

Puntare l'IDE alle librerie R locali: R di base, RevoScaleR e così via. L'esecuzione di carichi di lavoro in un'istanza remota di SQL Server si verifica durante l'esecuzione dello script, quando lo script richiama un contesto di calcolo remoto in SQL Server, accedendo a dati e operazioni in tale server.

### <a name="rstudio"></a>RStudio

Quando si usa [RStudio](https://www.rstudio.com/), è possibile configurare l'ambiente in modo da usare le librerie R e gli eseguibili che corrispondono a quelli in un'istanza di SQL Server remota.

1. Controllare le versioni del pacchetto R installate in SQL Server. Per altre informazioni, vedere [Ottenere informazioni sui pacchetti R](../package-management/r-package-information.md).

1. Installare Microsoft R Client o una delle opzioni di server autonomo per aggiungere RevoScaleR e altri pacchetti R, inclusa la distribuzione R di base usata dall'istanza di SQL Server. Scegliere una versione allo stesso livello o inferiore (i pacchetti sono compatibili con le versioni precedenti) che fornisce le stesse versioni del pacchetto del server. Per informazioni sulla versione, vedere la mappa delle versioni in questo articolo: [Aggiornare i componenti R e Python](../install/upgrade-r-and-python.md).

1. In RStudio [aggiornare il percorso di R](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) in modo che punti all'ambiente R che offre RevoScaleR, Microsoft R Open e altri pacchetti Microsoft. 

   + Per un'installazione di R Client, cercare C:\Programmi\Microsoft\R Client\R_SERVER\bin\x64
   + Per un server autonomo, cercare C:\Programmi\Microsoft SQL Server\140\R_SERVER\Library o C:\Programmi\Microsoft SQL Server\130\R_SERVER\Library

1. Chiudere e quindi aprire RStudio.

Quando si riapre RStudio, il file eseguibile R da R Client (o dal server autonomo) è il motore R predefinito.


### <a name="r-tools-for-visual-studio-rtvs"></a>R Tools per Visual Studio (RTVS)

Se non è già disponibile un IDE preferito per R, è consigliabile usare **R Tools per Visual Studio**.

+ [Scaricare R Tools per Visual Studio (RTVS)](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019)
+ [Istruzioni di installazione](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) - RTVS è disponibile in diverse versioni di Visual Studio.
+ [Introduzione a R Tools per Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Connettersi a SQL Server da RTVS

Questo esempio usa Visual Studio 2017 Community Edition con il carico di lavoro data science installato.

1. Scegliere **Nuovo** dal menu **File** e quindi selezionare **Progetto**.

2. Il riquadro a sinistra contiene un elenco dei modelli preinstallati. Fare clic su **R** e selezionare **Progetto R**. Digitare `dbtest` nella casella **Nome** e quindi fare clic su **OK**. 

   Visual Studio crea una nuova cartella di progetto e un file di script predefinito, `Script.R`. 

3. Digitare `.libPaths()` nella prima riga del file di script e quindi premere CTRL+INVIO.

   Il percorso corrente della libreria R deve essere visualizzato nella finestra di **R interattivo**. 

4. Fare clic sul menu **R Tools** e selezionare **Finestre** per visualizzare un elenco di altre finestre specifiche di R che è possibile visualizzare nell'area di lavoro.
 
   + Per visualizzare la Guida sui pacchetti nella libreria corrente, premere CTRL+3.
   + Vedere le variabili R in **Esplora variabili** premendo CTRL+8.

## <a name="next-steps"></a>Passaggi successivi

Due esercitazioni diverse includono esercizi che consentono di sperimentare il cambio del contesto di calcolo da locale a un'istanza di SQL Server remota.

+ [Esercitazione: Usare le funzioni R RevoScaleR con i dati di SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Procedura dettagliata end-to-end per l'analisi scientifica dei dati](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
