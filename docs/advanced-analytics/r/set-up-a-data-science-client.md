---
title: Configurare un client di analisi scientifica dei dati per lo sviluppo R - servizi di SQL Server Machine Learning
description: Installare gli strumenti e librerie di R locale in una workstation di sviluppo per le connessioni remote a SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/17/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 86b2ba305263b4699a3fe85328e854ba3105e4ab
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645512"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>Configurare un client di analisi scientifica dei dati per lo sviluppo di R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integrazione di R è disponibile in SQL Server 2016 o versioni successive quando si include l'opzione di linguaggio R in un' [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) oppure [SQL Server 2017 Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md) installazione. 

Per sviluppare e distribuire soluzioni R per SQL Server, installare [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) nella workstation di sviluppo per ottenere [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e altre librerie di R. La libreria RevoScaleR, che è necessario anche per l'istanza di SQL Server remota, coordina le richieste di elaborazione tra i due sistemi. 

In questo articolo, informazioni su come configurare una workstation di sviluppo R client in modo che sia possibile interagire con un Server SQL remoto abilitata per l'integrazione di R e apprendimento automatico. Dopo aver completato i passaggi descritti in questo articolo, si avranno le stesse librerie R come quelli in SQL Server. Inoltre, si saprà come trasferire i calcoli da una sessione R locale a una sessione remota di R in SQL Server.

![Componenti client-server](media/sqlmls-r-client-revo.png "librerie e le sessioni di R locali e remote")

Per convalidare l'installazione, è possibile utilizzare predefinito **RGUI** dello strumento come descritto in questo articolo, o [collegare le librerie](#install-ide) RStudio o qualsiasi altro IDE che in genere si usa.

> [!Tip]
> Per una dimostrazione video di questi esercizi, vedere [eseguire R e Python in modalità remota in Server SQL da notebook di Jupyter](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/).

> [!Note]
> Un'alternativa all'installazione della libreria client usa un [server autonomo](../install/sql-machine-learning-standalone-windows-install.md) come un rich client, alcuni clienti preferiscono per lavoro scenario più approfondita. Un server autonomo è completamente separato da SQL Server, ma perché contiene le stesse librerie di R, è possibile utilizzarlo come un client per analitica nel database di SQL Server. È anche possibile usarlo per lavoro non correlate a SQL, inclusa la possibilità di importare e modellare i dati da altre piattaforme di dati. Se si installa un server autonomo, è possibile trovare l'eseguibile di R in questa posizione: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. Per convalidare l'installazione [apre un'app console di R](#R-tools) per eseguire i comandi usando il R.exe in quella posizione.

## <a name="commonly-used-tools"></a>In genere utilizzato gli strumenti

Se sei uno sviluppatore di R per SQL o dagli sviluppatori SQL familiarità con R e analitica nel database, è necessario uno strumento di sviluppo R sia un editor di query T-SQL, ad esempio [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tenta di eseguire tutti i funzionalità di analitica nel database.

Per semplici scenari di sviluppo R, è possibile usare l'eseguibile, RGUI in bundle nella distribuzione base di R in MRO e SQL Server. Questo articolo illustra come usare RGUI per le sessioni di R locali e remote. Per una maggiore produttività, è consigliabile usare un IDE completo, ad esempio [RStudio o in Visual Studio](#install-ide).

SSMS è un download separato, utile per la creazione ed esecuzione di stored procedure in SQL Server, inclusi quelli contenenti codice R. Quasi qualsiasi codice R che si scrive in un ambiente di sviluppo può essere incorporato in una stored procedure. È possibile eseguire le altre esercitazioni per apprendere [SQL Server Management Studio e R incorporato](../tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="1---install-r-packages"></a>1: installare pacchetti R

I pacchetti R di Microsoft sono disponibili in più prodotti e servizi. In una workstation locale, è consigliabile installare Microsoft R Client. R Client offre [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)e altri pacchetti R.

1. [Scaricare Microsoft R Client](https://aka.ms/rclient/download).

2. Nell'installazione guidata, accettare o modificare il percorso di installazione predefinito, accettare o modificare l'elenco dei componenti e accettare le condizioni di licenza di Microsoft R Client.

  Al termine dell'installazione, una schermata iniziale viene presentata la documentazione e il prodotto.

3. Creare una variabile di ambiente di sistema MKL_CBWR per garantire coerenti con l'output su calcoli Intel Math Kernel Library (MKL).

  + Nel Pannello di controllo, fare clic su **sistema e sicurezza** > **System** > **impostazioni di sistema avanzate**  >   **Le variabili di ambiente**.
  + Creare una nuova variabile di sistema denominata **MKL_CBWR**, con un valore impostato **AUTO**.

## <a name="2---locate-executables"></a>2 - individuare i file eseguibili

Individuare ed elencare il contenuto della cartella di installazione per verificare che siano installati R.exe RGUI e altri pacchetti. 

1. In Esplora File aprire la cartella c:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\bin per verificare il percorso dei R.exe.

2. Sottocartella Open x64 per confermare **RGUI**. Questo strumento si userà nel passaggio successivo.

3. Aprire c:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\library per esaminare l'elenco dei pacchetti installati con R Client, tra cui RevoScaleR, MicrosoftML e altri.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3 - avviare RGUI

Quando si installa R con SQL Server, si ottengono gli stessi strumenti R standard per le installazioni di base di R, ad esempio RGui e Rterm così via. Questi strumenti sono leggeri, utile per controllo delle informazioni del pacchetto e di libreria, l'esecuzione di comandi ad hoc o uno script o avanzando istruzione per le esercitazioni. È possibile utilizzare questi strumenti per ottenere informazioni sulla versione di R e verificare la connettività.

1. Aprire c:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\bin\x64 e fare doppio clic su **RGui** per avviare una sessione di R con un prompt dei comandi di R.

  Quando si avvia una sessione di R da una cartella di programma Microsoft, diversi pacchetti, tra cui RevoScaleR, caricato automaticamente. 

2. Immettere `print(Revo.version)` al prompt dei comandi per RevoScaleR restituire le informazioni sulla versione del pacchetto. Deve avere la versione 9.2.1 o 9.3.0 per RevoScaleR.

3. Immettere **Search ()** al prompt di R per un elenco dei pacchetti installati.

   ![Informazioni sulla versione durante il caricamento di R](../install/media/rclient-rgui-r-prompt.png "aprire un prompt dei comandi di R")


## <a name="4---get-sql-permissions"></a>4 - ottenere le autorizzazioni di SQL

In R Client, l'elaborazione di R prevede un limite di due thread e i dati in memoria. Per l'elaborazione scalabile con più core e grandi set di dati, è possibile spostare l'esecuzione (detta *contesto di calcolo*) per il set di dati e la potenza di elaborazione di un'istanza remota di SQL Server. Questo è l'approccio consigliato per l'integrazione client con un'istanza di SQL Server di produzione è necessario disporre delle autorizzazioni e le informazioni di connessione per consentire il funzionamento.

Per connettersi a un'istanza di SQL Server per eseguire gli script e caricare i dati, è necessario un account di accesso valido nel server di database. È possibile usare un account di accesso SQL o un'autenticazione integrata di Windows. È consigliabile in genere si utilizza l'autenticazione integrata di Windows, ma utilizzando l'account di accesso SQL è più semplice per alcuni scenari, in particolare quando lo script contiene le stringhe di connessione ai dati esterni.

Come minimo, l'account usato per eseguire il codice deve disporre dell'autorizzazione di lettura da database si lavora con più di un'autorizzazione speciale EXECUTE ANY EXTERNAL SCRIPT. La maggior parte degli sviluppatori, inoltre, richiedono le autorizzazioni per creare le stored procedure e scrivere dati in tabelle contenenti dati di training o assegnare un punteggio dei dati. 

Chiedere all'amministratore di database di [configurare le autorizzazioni seguenti per l'account](../security/user-permission.md), nel database in cui si usa r:

+ **EXECUTE ANY EXTERNAL SCRIPT** per eseguire script R nel server.
+ **db_datareader** privilegi per eseguire le query usate per il training del modello.
+ **db_datawriter** per scrivere dati con punteggi o dati di training.
+ **db_owner** per creare oggetti quali stored procedure, tabelle, le funzioni. 
  È anche necessario **db_owner** per creare i database di esempio e test. 

Se il codice richiede i pacchetti non installati per impostazione predefinita con SQL Server, disporre con l'amministratore del database per i pacchetti installati con l'istanza. SQL Server è un ambiente protetto ed esistono restrizioni in cui i pacchetti possono essere installati. Per altre informazioni, vedere [installare nuovi pacchetti R in SQL Server](install-additional-r-packages-on-sql-server.md).

## <a name="5---test-connections"></a>5: verificare le connessioni

 Come passaggio di verifica, usare **RGUI** e RevoScaleR per confermare la connettività al server remoto. SQL Server deve essere abilitata per [le connessioni remote](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) ed è necessario disporre delle autorizzazioni, tra cui un account di accesso e un database a cui connettersi. 

I passaggi seguenti presuppongono il database, demo [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)e l'autenticazione di Windows.

1. Aprire **RGUI** sulla workstation client. Ad esempio, passare a `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` e fare doppio clic **RGui.exe** per avviarla.

2. RevoScaleR carica automaticamente. Verificare che sia operativo RevoScaleR eseguendo questo comando: `print(Revo.version)`

3. Immettere lo script di demo che viene eseguito nel server remoto. È necessario modificare il seguente script di esempio per includere un nome valido per un'istanza remota di SQL Server. In questa sessione viene avviata una sessione locale, ma il **rxSummary** funzione viene eseguita nell'istanza remota di SQL Server.

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

  Questo script si connette a un database nel server remoto, fornisce una query, crea un contesto di calcolo `cc` istruzioni per l'esecuzione remota del codice, offre quindi la funzione RevoScaleR **rxSummary** per restituire una statistica riepilogo dei risultati della query.

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

4. Ottenere e impostare il contesto di calcolo. Dopo aver impostato un contesto di calcolo, rimane attiva per la durata della sessione. Se non si è certi se calcolo è locale o remoto, eseguire il comando seguente per scoprire. I risultati che specificano una stringa di connessione indicano un contesto di calcolo remoto.

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

5. Restituisce informazioni sulle variabili nell'origine dati, inclusi nome e tipo.

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  I risultati includono le variabili di 23.


6. Generare un grafico a dispersione per esplorare se esistono dipendenze tra due variabili. 

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

  Lo screenshot seguente mostra l'output di tracciato di input e a dispersione.

   ![Grafico a dispersione in RGUI](media/rclient-setup-scatterplot.png "dispersione sui dati di demo dei Taxi di NYC")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6 - strumenti di link a R.exe

Per i progetti di sviluppo prolungato e grave, è necessario installare un ambiente di sviluppo integrato (IDE). Strumenti di SQL Server e gli strumenti R incorporati sono dotati di non per lo sviluppo R pesante. Dopo aver creato codice funzionante, è possibile distribuirlo come una stored procedure per l'esecuzione in SQL Server.

Scegliere l'ambiente IDE per le librerie R locale: di base R, RevoScaleR e così via. Esecuzione di carichi di lavoro in un Server SQL remoto si verifica durante l'esecuzione di script, quando lo script richiama un contesto di calcolo remota in SQL Server, l'accesso ai dati e le operazioni su tale server.

### <a name="rstudio"></a>RStudio

Quando si usa [RStudio](https://www.rstudio.com/), è possibile configurare l'ambiente per usare le librerie di R e i file eseguibili che corrispondono a quelle in un Server SQL remoto.

1. Controllare le versioni dei pacchetti R installate in SQL Server. Per altre informazioni, vedere [informazioni sui pacchetti R di ottenere](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location).

1. Installare Microsoft R Client o una delle opzioni server autonomo per l'aggiunta di RevoScaleR e altri pacchetti R, tra cui distribuzione base di R usata dall'istanza di SQL Server. Scegliere una versione allo stesso o un livello inferiore (i pacchetti sono compatibili con le versioni precedenti) che fornisce le stesse versioni del pacchetto al server. Per informazioni sulla versione, vedere la versione di eseguire il mapping in questo articolo: [Aggiornare i componenti di R e Python](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

1. In RStudio [aggiornare il percorso di R](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) in modo che punti all'ambiente R fornendo RevoScaleR, Microsoft R Open e altri pacchetti Microsoft. 

  + Per un'installazione di R Client, cercare c:\Programmi\Microsoft Files\Microsoft\R Client\R_SERVER\bin\x64
  + Per un server autonomo, cercare C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library o C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library

2. Chiudere e riaprire RStudio.

Quando si riapre RStudio, R eseguibile dal Client R (o server autonomo) è il motore R predefinita.


### <a name="r-tools-for-visual-studio-rtvs"></a>R Tools per Visual Studio (RTVS)

Se si ha già un IDE preferito per R, è consigliabile **R Tools per Visual Studio**.

+ [Scarica gli strumenti R per Visual Studio (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [Le istruzioni di installazione](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) -RTVS è disponibile in diverse versioni di Visual Studio.
+ [Introduzione a R Tools per Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>Connettersi a SQL Server da RTVS

Questo esempio Usa Visual Studio 2017 Community Edition, con il carico di lavoro analisi scientifica dei dati installato.

1. Dal **File** dal menu **New** e quindi selezionare **progetto**.

2. Nel riquadro a sinistra contiene un elenco di modelli preinstallati. Fare clic su **R**e selezionare **progetto R**. Nel **Name** , digitare `dbtest` e fare clic su **OK**. 

  Visual Studio crea una nuova cartella di progetto e un file di script predefinito, `Script.R`. 

3. Tipo `.libPaths()` sulla prima riga dello script di file e quindi premere CTRL + INVIO.

  Il percorso della libreria R corrente deve essere visualizzato nei **R interattivo** finestra. 

4. Scegliere il **R Tools** dal menu **Windows** per visualizzare un elenco di altre finestre specifici di R che è possibile visualizzare nell'area di lavoro.
 
  + Visualizzare la Guida per i pacchetti nella libreria corrente, premere CTRL + 3.
  + Vedere le variabili R nel **Esplora variabili**, premendo CTRL + 8.

## <a name="next-steps"></a>Passaggi successivi

Due diverse esercitazioni includono gli esercizi in modo da consentire l'esercitazione cambiato il contesto di calcolo da locale a un'istanza remota di SQL Server.

+ [Esercitazione: Usare funzioni RevoScaleR R con dati di SQL Server](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [Procedura dettagliata end-to-end per l'analisi scientifica dei dati](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)