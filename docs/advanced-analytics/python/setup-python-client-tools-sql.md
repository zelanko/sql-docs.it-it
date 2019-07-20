---
title: Configurare un client data science per lo sviluppo in Python
description: Configurare un ambiente locale Python (Jupyter Notebook o PyCharm) per le connessioni remote a SQL Server Machine Learning Services con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 399aab131a30560ac3305b0cac678cd9e0d18553
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344804"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>Configurare un client data science per lo sviluppo Python in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

L'integrazione di Python è disponibile a partire da SQL Server 2017 o versione successiva quando si include l'opzione Python in un' [installazione di Machine Learning Services (in-database)](../install/sql-machine-learning-services-windows-install.md). 

Per sviluppare e distribuire soluzioni Python per SQL Server, installare [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) di Microsoft e altre librerie Python nella workstation di sviluppo. La libreria revoscalepy, che si trova anche sull'istanza di SQL Server remota, coordina le richieste di elaborazione tra entrambi i sistemi. 

Questo articolo illustra come configurare una workstation di sviluppo Python per poter interagire con una SQL Server remota abilitata per l'integrazione di machine learning e Python. Dopo aver completato i passaggi descritti in questo articolo, si avranno le stesse librerie Python di quelle presenti in SQL Server. Si saprà anche come eseguire il push di calcoli da una sessione Python locale a una sessione Python remota in SQL Server.

![Componenti client-server](media/sqlmls-python-client-revo.png "Sessioni e librerie Python locali e remote")

Per convalidare l'installazione, è possibile usare i notebook di Jupyter predefiniti, come descritto in questo articolo, oppure [collegare le librerie](#install-ide) a PyCharm o a qualsiasi altro IDE usato in genere.

> [!Tip]
> Per una dimostrazione video di questi esercizi, vedere [eseguire R e Python in remoto in SQL Server da notebook di Jupyter](https://youtu.be/D5erljpJDjE).

> [!Note]
> Un'alternativa all'installazione della libreria client consiste nell'utilizzo di un [server autonomo](../install/sql-machine-learning-standalone-windows-install.md) come rich client, che alcuni clienti preferiscono per lavorare in uno scenario più approfondito. Un server autonomo è completamente separato dal SQL Server, ma poiché ha le stesse librerie Python, è possibile usarlo come client per SQL Server analisi nel database. È anche possibile usarlo per il lavoro non correlato a SQL, inclusa la possibilità di importare e modellare i dati da altre piattaforme di dati. Se si installa un server autonomo, è possibile trovare il file eseguibile di Python `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`in questo percorso:. Per convalidare l'installazione, [aprire un notebook di Jupyter](#python-tools) per eseguire i comandi con Python. exe in quel percorso.

## <a name="commonly-used-tools"></a>Strumenti di uso comune

Che tu sia uno sviluppatore di Python nuovo a SQL o uno sviluppatore SQL nuovo per Python e analisi nel database, ti servirà sia uno strumento di sviluppo Python sia un editor di query T-SQL, ad esempio [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) , per esercitare tutte le funzionalità di analisi nel database.

Per lo sviluppo in Python, è possibile usare Jupyter Notebooks, fornito in bundle nella distribuzione anaconda installata da SQL Server. Questo articolo illustra come avviare notebook di Jupyter in modo che sia possibile eseguire il codice Python in locale e in remoto in SQL Server.

SSMS è un download separato, utile per la creazione e l'esecuzione di stored procedure su SQL Server, inclusi quelli che contengono codice Python. Quasi tutti i codici Python scritti in notebook di Jupyter possono essere incorporati in un stored procedure. È possibile eseguire altre guide introduttive per informazioni su [SSMS e Python incorporato](../tutorials/quickstart-python-verify.md).

## <a name="1---install-python-packages"></a>1-installare i pacchetti Python

Le workstation locali devono avere le stesse versioni del pacchetto python di quelle SQL Server, tra cui il 4.2.0 Anaconda di base con la distribuzione 3.5.2 di Python e i pacchetti specifici di Microsoft.

Uno script di installazione aggiunge tre librerie specifiche di Microsoft al client Python. Lo script installa [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), usato per definire gli oggetti origine dati e il contesto di calcolo. Installa [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) fornendo algoritmi di machine learning. Viene installato anche il pacchetto [azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) , ma si applica alle attività di operatività associate a un contesto di Machine Learning server autonomo (non di istanza) e può essere usato in modo limitato per l'analisi nel database.

1. Scaricare uno script di installazione.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py)installa la versione 9.2.1 dei pacchetti Microsoft Python. Questa versione corrisponde a un'istanza predefinita di SQL Server 2017. 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py)installa la versione 9,3 dei pacchetti Microsoft Python. Questa versione è la scelta migliore se l'istanza di SQL Server 2017 remota è [associata a Machine Learning Server 9,3](../install/upgrade-r-and-python.md).

2. Aprire una finestra di PowerShell con autorizzazioni di amministratore con privilegi elevati, facendo clic con il pulsante destro del mouse su **Esegui come amministratore**.

3. Passare alla cartella in cui è stato scaricato il programma di installazione ed eseguire lo script. Aggiungere l' `-InstallFolder` argomento della riga di comando per specificare il percorso di una cartella per le librerie. Ad esempio: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

Se si omette la cartella di installazione, il valore predefinito è C:\Program Files\Microsoft\PyForMLS.

Il completamento dell'installazione richiede del tempo. È possibile monitorare lo stato di avanzamento nella finestra di PowerShell. Al termine dell'installazione, sarà presente un set completo di pacchetti. 

> [!Tip] 
> Per informazioni generali su purppose sull'esecuzione di programmi Python in Windows, è consigliabile usare le [domande frequenti su Python per Windows](https://docs.python.org/3/faq/windows.html) .

## <a name="2---locate-executables"></a>2-individuare i file eseguibili

Sempre in PowerShell, elencare il contenuto della cartella di installazione per confermare che Python. exe, gli script e gli altri pacchetti siano installati. 

1. Immettere `cd \` per passare all'unità radice, quindi immettere il percorso specificato per `-InstallFolder` nel passaggio precedente. Se questo parametro è stato omesso durante l'installazione, il `cd C:\Program Files\Microsoft\PyForMLS`valore predefinito è.

2. Immettere `dir *.exe` per elencare i file eseguibili. Verranno visualizzati **Python. exe**, **pythonw. exe**e **Uninstall-Anaconda. exe**.

  ![Elenco di file eseguibili Python](media/powershell-python-exe.png)
   
Nei sistemi con più versioni di Python, ricordarsi di usare questo particolare Python. exe se si vuole caricare **revoscalepy** e altri pacchetti Microsoft.

> [!Note] 
> Lo script di installazione non modifica la variabile di ambiente PATH nel computer, il che significa che il nuovo interprete Python e i moduli appena installati non sono automaticamente disponibili per altri strumenti. Per informazioni sul collegamento dell'interprete Python e delle librerie agli strumenti, vedere [installare un IDE](#install-ide).

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-aprire notebook Jupyter

Anaconda include Jupyter notebook. Come passaggio successivo, creare un notebook ed eseguire codice Python contenente le librerie appena installate.

1. Al prompt di PowerShell, ancora nella directory C:\Program Files\Microsoft\PyForMLS, aprire notebook di Jupyter dalla cartella Scripts:

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  Un notebook verrà aperto nel browser predefinito all'indirizzo `https://localhost:8889/tree`.

  Un altro modo per iniziare è fare doppio clic su **jupyter-notebook. exe**. 

2. Fare clic su **nuovo** e quindi su **Python 3**.

  ![jupyter notebook con nuova selezione di Python 3](media/jupyter-notebook-new-p3.png)

3. Immettere `import revoscalepy` ed eseguire il comando per caricare una delle librerie specifiche di Microsoft.

4. Immettere ed eseguire `print(revoscalepy.__version__)` per restituire le informazioni sulla versione. Verrà visualizzato 9.2.1 o 9.3.0. È possibile usare una di queste versioni con [revoscalepy nel server](../package-management/installed-package-information.md). 

4. Immettere una serie di istruzioni più complesse. Questo esempio genera statistiche di riepilogo usando [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) su un set di dati locale. Altre funzioni ottengono il percorso dei dati di esempio e creano un oggetto origine dati per un file XDF locale.

  ```python
  import os
  from revoscalepy import rx_summary
  from revoscalepy import RxXdfData
  from revoscalepy import RxOptions
  sample_data_path = RxOptions.get_option("sampleDataDir")
  print(sample_data_path)
  ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
  summary = rx_summary("ArrDelay+DayOfWeek", ds)
  print(summary)
  ```

Lo screenshot seguente mostra l'input e una parte dell'output, tagliati per brevità.

  ![jupyter notebook che Mostra gli input e l'output di revoscalepy](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-ottenere le autorizzazioni SQL

Per connettersi a un'istanza di SQL Server per eseguire gli script e caricare i dati, è necessario disporre di un account di accesso valido nel server di database. È possibile usare un account di accesso SQL o un'autenticazione integrata di Windows. È in genere consigliabile usare l'autenticazione integrata di Windows, ma l'uso dell'account di accesso SQL è più semplice per alcuni scenari, in particolare quando lo script contiene stringhe di connessione a dati esterni.

Come minimo, l'account utilizzato per eseguire il codice deve disporre dell'autorizzazione di lettura dai database utilizzati, oltre all'autorizzazione speciale per l'esecuzione di qualsiasi SCRIPT esterno. La maggior parte degli sviluppatori richiede anche le autorizzazioni per la creazione di stored procedure e per la scrittura di dati in tabelle contenenti dati di training o dati con punteggio. 

Chiedere all'amministratore del database di [configurare le autorizzazioni seguenti per l'account](../security/user-permission.md)nel database in cui si usa Python:

+ **Eseguire qualsiasi script esterno** per eseguire python nel server.
+ privilegi **db_datareader** per eseguire le query utilizzate per il training del modello.
+ **db_datawriter** scrivere dati di training o dati con punteggio.
+ **db_owner** per la creazione di oggetti quali stored procedure, tabelle, funzioni. 
  È inoltre necessario che **db_owner** crei database di esempio e di test. 

Se per il codice sono necessari pacchetti non installati per impostazione predefinita con SQL Server, disporre con l'amministratore del database in modo che i pacchetti siano installati con l'istanza di. SQL Server è un ambiente protetto e sono presenti restrizioni per la posizione in cui è possibile installare i pacchetti. L'installazione ad hoc di pacchetti come parte del codice non è consigliata, anche se si dispone di diritti. Inoltre, valutare sempre attentamente le implicazioni di sicurezza prima di installare nuovi pacchetti nella libreria server.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-creare dati di test

Se si hanno le autorizzazioni per creare un database nel server remoto, è possibile eseguire il codice seguente per creare il database demo Iris usato per i passaggi rimanenti di questo articolo.

### <a name="1---create-the-irissql-database-remotely"></a>1-creare il database irissql in modalità remota

```python
import pyodbc

# creating a new db to load Iris sample in
new_db_name = "irissql"
connection_string = "Driver=SQL Server;Server=localhost;Database={0};Trusted_Connection=Yes;" 
                        # you can also swap Trusted_Connection for UID={your username};PWD={your password}
cnxn = pyodbc.connect(connection_string.format("master"), autocommit=True)
cnxn.cursor().execute("IF EXISTS(SELECT * FROM sys.databases WHERE [name] = '{0}') DROP DATABASE {0}".format(new_db_name))
cnxn.cursor().execute("CREATE DATABASE " + new_db_name)
cnxn.close()

print("Database created")
```

### <a name="2---import-iris-sample-from-sklearn"></a>2-importare l'esempio di Iris da SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-usare le API Revoscalepy per creare una tabella e caricare i dati Iris

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6-testare la connessione remota

Prima di provare il passaggio successivo, assicurarsi di disporre delle autorizzazioni per l'istanza SQL Server e una stringa di connessione al [database di esempio Iris](../tutorials/demo-data-iris-in-sql.md). Se il database non esiste e si dispone di autorizzazioni sufficienti, è possibile [creare un database utilizzando queste istruzioni inline](#create-iris-remotely).

Sostituire la stringa di connessione con i valori validi. Il codice di esempio `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` utilizza, ma il codice deve specificare un server remoto, possibilmente con un nome di istanza, e un'opzione di credenziale che esegue il mapping all'account di accesso dell'utente del database.

### <a name="define-a-function"></a>Definisci una funzione

Il codice seguente definisce una funzione che si invierà a SQL Server in un passaggio successivo. Quando viene eseguito, USA i dati e le librerie (revoscalepy, Pandas, matplotlib) nel server remoto per creare grafici a dispersione del set di dati Iris. Restituisce il ByteStream del. png a Jupyter Notebooks per eseguire il rendering nel browser.

```python
def send_this_func_to_sql():
    from revoscalepy import RxSqlServerData, rx_import
    from pandas.tools.plotting import scatter_matrix
    import matplotlib.pyplot as plt
    import io
    
    # remember the scope of the variables in this func are within our SQL Server Python Runtime
    connection_string = "Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"
    
    # specify a query and load into pandas dataframe df
    sql_query = RxSqlServerData(connection_string=connection_string, sql_query = "select * from iris_data")
    df = rx_import(sql_query)
    
    scatter_matrix(df)
    
    # return bytestream of image created by scatter_matrix
    buf = io.BytesIO()
    plt.savefig(buf, format="png")
    buf.seek(0)
    
    return buf.getvalue()
```

### <a name="send-the-function-to-sql-server"></a>Inviare la funzione a SQL Server

In questo esempio, creare il contesto di calcolo remoto e quindi inviare l'esecuzione della funzione a SQL Server con [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec). La funzione **rx_exec** è utile perché accetta un contesto di calcolo come argomento. Qualsiasi funzione che si vuole eseguire in modalità remota deve avere un argomento del contesto di calcolo. Alcune funzioni, ad esempio [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) supportano direttamente questo argomento. Per le operazioni che non sono, è possibile usare **rx_exec** per distribuire il codice in un contesto di calcolo remoto.

In questo esempio non è stato possibile trasferire dati non elaborati da SQL Server al Jupyter Notebook. Tutti i calcoli vengono eseguiti nel database Iris e al client viene restituito solo il file di immagine.

```python
from IPython import display
import matplotlib.pyplot as plt 
from revoscalepy import RxInSqlServer, rx_exec

# create a remote compute context with connection to SQL Server
sql_compute_context = RxInSqlServer(connection_string=connection_string.format(new_db_name))

# use rx_exec to send the function execution to SQL Server
image = rx_exec(send_this_func_to_sql, compute_context=sql_compute_context)[0]

# only an image was returned to my jupyter client. All data remained secure and was manipulated in my db.
display.Image(data=image)
```

Lo screenshot seguente mostra l'output del grafico di input e dispersione.

  ![jupyter notebook che mostra l'output del grafico a dispersione](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7-avviare Python dagli strumenti

Poiché gli sviluppatori lavorano spesso con più versioni di Python, il programma di installazione non aggiunge Python al percorso. Per usare il file eseguibile e le librerie di Python installati dal programma di installazione, collegare l'IDE a **Python. exe** nel percorso che fornisce anche **revoscalepy** e **microsoftml**. 

### <a name="command-line"></a>Riga di comando

Quando si esegue **Python. exe** da C:\Program Files\Microsoft\PyForMLS (o qualsiasi percorso specificato per l'installazione della libreria client Python), è possibile accedere alla distribuzione anaconda completa oltre ai moduli Microsoft Python, **revoscalepy** e **microsoftml**.

1. Passare a C:\Program Files\Microsoft\PyForMLS e fare doppio clic su **Python. exe**.
2. Aprire la guida interattiva:`help()`
3. Digitare il nome di un modulo al prompt della guida: `help> revoscalepy`. La Guida restituisce il nome, il contenuto del pacchetto, la versione e il percorso del file.
4. Restituire le informazioni sulla versione e sul pacchetto nel prompt > `revoscalepy`della **Guida** :. Premere INVIO alcune volte per uscire dalla guida.
5. Importare un modulo:`import revoscalepy`


### <a name="jupyter-notebooks"></a>Notebook di Jupyter

Questo articolo usa notebook Jupyter predefiniti per illustrare le chiamate di funzione a **revoscalepy**. Se non si ha familiarità con questo strumento, nello screenshot seguente viene illustrato il modo in cui i componenti si adattano e il motivo per cui tutto funziona. 

La cartella padre C:\Program Files\Microsoft\PyForMLS contiene Anaconda più i pacchetti Microsoft. I notebook di Jupyter sono inclusi in Anaconda, nella cartella Scripts e i file eseguibili Python vengono registrati automaticamente con i notebook di Jupyter. I pacchetti disponibili in site-packages possono essere importati in un notebook, inclusi i tre pacchetti Microsoft usati per data science e machine learning.

  ![File eseguibili e librerie](media/jupyter-notebook-python-registration.png)

Se si usa un altro IDE, sarà necessario collegare gli eseguibili e le librerie di funzioni di Python allo strumento. Nelle sezioni seguenti vengono fornite le istruzioni per gli strumenti di uso comune.

### <a name="visual-studio"></a>Visual Studio

Se si dispone di [Python in Visual Studio](https://code.visualstudio.com/docs/languages/python), usare le opzioni di configurazione seguenti per creare un ambiente Python che includa i pacchetti Microsoft Python.

| Impostazione di configurazione | Valore |
|-----------------------|-------|
| **Percorso prefisso** | C:\Programmi\Microsoft Files\Microsoft\PyForMLS |
| **Percorso dell'interprete** | C:\Programmi\Microsoft Files\Microsoft\PyForMLS\python.exe |
| **Interprete con finestra** | C:\Programmi\Microsoft Files\Microsoft\PyForMLS\pythonw.exe |

Per informazioni sulla configurazione di un ambiente Python, vedere [gestione degli ambienti Python in Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

### <a name="pycharm"></a>PyCharm

In PyCharm impostare l'interprete sull'eseguibile di Python installato da Machine Learning Server.

1. In un nuovo progetto, in impostazioni, fare clic su **Aggiungi localmente**.

2. Immettere `C:\Program Files\Microsoft\PyForMLS\`.

È ora possibile importare i moduli **revoscalepy**, **microsoftml**o **azureml** . È anche possibile scegliere **strumenti** > **console Python** per aprire una finestra interattiva.

## <a name="next-steps"></a>Passaggi successivi

Ora che sono disponibili strumenti e una connessione funzionante a SQL Server, espandere le proprie competenze eseguendo le guide introduttive di Python con [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

> [!div class="nextstepaction"]
> [Avvio rapido: Verificare che Python esista in SQL Server](../tutorials/quickstart-python-verify.md)