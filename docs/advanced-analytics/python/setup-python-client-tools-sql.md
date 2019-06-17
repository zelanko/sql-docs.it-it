---
title: Configurare un client di analisi scientifica dei dati per lo sviluppo Python - SQL Server Machine Learning
description: Configurare un ambiente Python locale (Notebook di Jupyter o PyCharm) per le connessioni remote a servizi di SQL Server Machine Learning con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 448322fc79f4a85256b1d0b5b682fcc5147263c5
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140640"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>Configurare un client di analisi scientifica dei dati per lo sviluppo Python in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integrazione di Python è disponibile a partire da SQL Server 2017 o versioni successive quando si include l'opzione di Python in un [installazione di Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md). 

Per sviluppare e distribuire soluzioni Python per SQL Server, installare Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e altre librerie Python workstation di sviluppo. La libreria revoscalepy, che è anche nell'istanza del Server SQL remoto, coordina le richieste di elaborazione tra i due sistemi. 

In questo articolo, informazioni su come configurare una workstation di sviluppo Python in modo che sia possibile interagire con un Server SQL remoto abilitata per l'integrazione di Python e apprendimento automatico. Dopo aver completato i passaggi descritti in questo articolo, si avranno le stesse librerie di Python come quelli in SQL Server. Inoltre, si saprà come trasferire i calcoli da una sessione di Python locale a una sessione remota di Python in SQL Server.

![Componenti client-server](media/sqlmls-python-client-revo.png "sessioni locali che remote di Python e le librerie")

Per convalidare l'installazione, è possibile usare i notebook di Jupyter incorporato, come descritto in questo articolo, o [collegare le librerie](#install-ide) PyCharm o qualsiasi altro IDE che in genere si usa.

> [!Tip]
> Per una dimostrazione video di questi esercizi, vedere [eseguire R e Python in modalità remota in Server SQL da notebook di Jupyter](https://youtu.be/D5erljpJDjE).

> [!Note]
> Un'alternativa all'installazione della libreria client usa un [server autonomo](../install/sql-machine-learning-standalone-windows-install.md) come un rich client, alcuni clienti preferiscono per lavoro scenario più approfondita. Un server autonomo è completamente separato da SQL Server, ma perché contiene le stesse librerie di Python, è possibile utilizzarlo come un client per analitica nel database di SQL Server. È anche possibile usarlo per lavoro non correlate a SQL, inclusa la possibilità di importare e modellare i dati da altre piattaforme di dati. Se si installa un server autonomo, è possibile trovare l'eseguibile di Python in questa posizione: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Per convalidare l'installazione [apre un notebook di Jupyter](#python-tools) per eseguire i comandi usando il Python.exe in quella posizione.

## <a name="commonly-used-tools"></a>In genere utilizzato gli strumenti

Se sei uno sviluppatore di Python per SQL o dagli sviluppatori SQL familiarità con Python e analitica nel database, è necessario uno strumento di sviluppo Python sia un editor di query T-SQL, ad esempio [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tenta di eseguire tutti i le funzionalità di analitica nel database.

Per lo sviluppo Python, è possibile usare i notebook di Jupyter, che viene fornita in bundle nella distribuzione Anaconda installata tramite SQL Server. Questo articolo illustra come avviare i notebook di Jupyter in modo che sia possibile eseguire codice Python in locale e in modalità remota in SQL Server.

SSMS è un download separato, utile per la creazione ed esecuzione di stored procedure in SQL Server, inclusi quelli che contiene codice Python. Quasi qualsiasi codice Python che si scrive nel notebook di Jupyter può essere incorporato in una stored procedure. È possibile esaminare altre guide introduttive per conoscere [SQL Server Management Studio e Python incorporato](../tutorials/quickstart-python-verify.md).

## <a name="1---install-python-packages"></a>1: installare pacchetti Python

Workstation locale deve avere le stesse versioni di pacchetto di Python come quelli in SQL Server, tra cui la base Anaconda versione 4.2.0 con distribuzione di Python 3.5.2 e pacchetti di specifiche di Microsoft.

Uno script di installazione aggiunge tre librerie specifiche di Microsoft per il client Python. Lo script installa [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), usato per definire oggetti origine dei dati e il contesto di calcolo. Viene installato [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) fornendo algoritmi di machine learning. Il [azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) pacchetto viene installato anche, ma si applica alle attività di operazionalizzazione associata a un contesto di Machine Learning Server autonomo (non-istanza) e potrebbero essere limitate all'uso di analitica nel database.

1. Scaricare uno script di installazione.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) Installa versione 9.2.1 dei pacchetti Python di Microsoft. Questa versione corrisponde a un'istanza di SQL Server 2017 predefinita. 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) Installa versione 9.3 dei pacchetti Python di Microsoft. Questa versione è una scelta migliore se l'istanza remota di SQL Server 2017 [associato a Machine Learning Server 9.3](../install/upgrade-r-and-python.md).

2. Aprire una finestra di PowerShell con autorizzazioni di amministratore con privilegi elevati (fare doppio clic su **Esegui come amministratore**).

3. Passare alla cartella in cui è stato scaricato il programma di installazione ed eseguire lo script. Aggiungere il `-InstallFolder` argomento della riga di comando per specificare un percorso della cartella per le librerie. Ad esempio: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

Se si omette la cartella di installazione, il valore predefinito è c:\Programmi\Microsoft Files\Microsoft\PyForMLS.

Installazione richiede alcuni minuti. È possibile monitorare lo stato di avanzamento nella finestra di PowerShell. Al termine dell'installazione, si dispone di un set completo di pacchetti. 

> [!Tip] 
> È consigliabile la [Python per Windows domande frequenti su](https://docs.python.org/3/faq/windows.html) per informazioni generali purppose sull'esecuzione di programmi di Python in Windows.

## <a name="2---locate-executables"></a>2 - individuare i file eseguibili

Ancora in PowerShell, elencare il contenuto della cartella di installazione per verificare che siano installati Python.exe, script e altri pacchetti. 

1. Immettere `cd \` per passare all'unità radice e quindi immettere il percorso specificato per `-InstallFolder` nel passaggio precedente. Se si omette questo parametro durante l'installazione, il valore predefinito è `cd C:\Program Files\Microsoft\PyForMLS`.

2. Immettere `dir *.exe` per elencare i file eseguibili. Si noterà **python.exe**, **pythonw.exe**, e **anaconda.exe disinstallare**.

  ![Elenco di file eseguibili di Python](media/powershell-python-exe.png)
   
Nei sistemi con più versioni di Python, ricordarsi di usare questa particolare Python.exe se si desidera caricare **revoscalepy** e altri pacchetti Microsoft.

> [!Note] 
> Lo script di installazione non modifica la variabile di ambiente PATH nel computer, il che significa che il nuovo interprete python e i moduli che appena installato non sono automaticamente disponibili ad altri strumenti che è possibile. Per informazioni su come l'interprete Python e le librerie di collegamento agli strumenti, vedere [installare un IDE](#install-ide).

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3 - aprire Jupyter notebook

Anaconda include notebook di Jupyter. Come passaggio successivo, creare un notebook ed eseguire codice Python che contiene le librerie che appena installato.

1. Al prompt di Powershell, ancora nella directory c:\Programmi\Microsoft Files\Microsoft\PyForMLS, aprire Jupyter notebook dalla cartella degli script:

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  Un blocco appunti dovrebbe aprire nel browser predefinito in `https://localhost:8889/tree`.

  Un altro modo per iniziare è fare doppio clic su **jupyter notebook.exe**. 

2. Fare clic su **New** e quindi fare clic su **Python 3**.

  ![notebook di jupyter con Python 3 nuova selezione](media/jupyter-notebook-new-p3.png)

3. Immettere `import revoscalepy` ed eseguire il comando a uno carico delle librerie specifiche di Microsoft.

4. Immettere ed eseguire `print(revoscalepy.__version__)` per restituire le informazioni sulla versione. Dovrebbe essere 9.2.1 o 9.3.0. È possibile usare una di queste versioni con [revoscalepy sul server](../package-management/installed-package-information.md). 

4. Immettere una serie più complessa di istruzioni. Questo esempio genera le statistiche di riepilogo usando [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) su un set di dati locale. Altre funzioni di ottenere la posizione dei dati di esempio e creare un oggetto origine dati per un file con estensione xdf locale.

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

Lo screenshot seguente mostra l'input e una parte dell'output, tagliata per brevità.

  ![notebook di jupyter che mostra revoscalepy input e output](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4 - ottenere le autorizzazioni di SQL

Per connettersi a un'istanza di SQL Server per eseguire gli script e caricare i dati, è necessario un account di accesso valido nel server di database. È possibile usare un account di accesso SQL o un'autenticazione integrata di Windows. È consigliabile in genere si utilizza l'autenticazione integrata di Windows, ma utilizzando l'account di accesso SQL è più semplice per alcuni scenari, in particolare quando lo script contiene le stringhe di connessione ai dati esterni.

Come minimo, l'account usato per eseguire il codice deve disporre dell'autorizzazione di lettura da database si lavora con più di un'autorizzazione speciale EXECUTE ANY EXTERNAL SCRIPT. La maggior parte degli sviluppatori, inoltre, richiedono le autorizzazioni per creare le stored procedure e scrivere dati in tabelle contenenti dati di training o assegnare un punteggio dei dati. 

Chiedere all'amministratore di database di [configurare le autorizzazioni seguenti per l'account](../security/user-permission.md), nel database in cui si usano Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** per l'esecuzione di Python nel server.
+ **db_datareader** privilegi per eseguire le query usate per il training del modello.
+ **db_datawriter** per scrivere dati con punteggi o dati di training.
+ **db_owner** per creare oggetti quali stored procedure, tabelle, le funzioni. 
  È anche necessario **db_owner** per creare i database di esempio e test. 

Se il codice richiede i pacchetti non installati per impostazione predefinita con SQL Server, disporre con l'amministratore del database per i pacchetti installati con l'istanza. SQL Server è un ambiente protetto ed esistono restrizioni in cui i pacchetti possono essere installati. Installazione ad hoc dei pacchetti come parte del codice non è consigliabile, anche se si dispone di diritti. Inoltre, considerare sempre con attenzione le implicazioni di sicurezza prima di installare nuovi pacchetti nella raccolta di server.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5 - creare dati di test

Se si dispone delle autorizzazioni per creare un database nel server remoto, è possibile eseguire il codice seguente per creare il database di demo Iris utilizzato per i passaggi rimanenti in questo articolo.

### <a name="1---create-the-irissql-database-remotely"></a>1 - creare il database irissql in modalità remota

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

### <a name="2---import-iris-sample-from-sklearn"></a>2 - importare esempio Iris da SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3 - usare Revoscalepy APIs per creare una tabella e caricare i dati Iris

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6: test della connessione remota

Prima di tentare questo passaggio successivo, assicurarsi di avere le autorizzazioni per l'istanza di SQL Server e una stringa di connessione per il [database di esempio Iris](../tutorials/demo-data-iris-in-sql.md). Se il database non esiste e disporre di autorizzazioni sufficienti, è possibile [creare un database con queste istruzioni inline](#create-iris-remotely).

Sostituire la stringa di connessione con i valori validi. Il codice di esempio Usa `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` ma il codice deve specificare un server remoto, eventualmente con un nome di istanza e un'opzione delle credenziali che viene eseguito il mapping all'account di accesso di database utente.

### <a name="define-a-function"></a>Definire una funzione

Il codice seguente definisce una funzione che verrà inviata a SQL Server in un passaggio successivo. Quando viene eseguito, Usa i dati e le librerie (revoscalepy, pandas, matplotlib) nel server remoto per creare grafici a dispersione del set di dati iris. Restituisce il bytestream del PNG al notebook di Jupyter per eseguire il rendering nel browser.

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

### <a name="send-the-function-to-sql-server"></a>La funzione di invio a SQL Server

In questo esempio, creare il contesto di calcolo remoto e quindi inviare l'esecuzione della funzione a SQL Server con [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec). Il **rx_exec** funzione è utile in quanto accetta un contesto di calcolo come argomento. Qualsiasi funzione che si desidera eseguire in modalità remota deve avere un argomento di contesto di calcolo. Alcune funzioni, ad esempio [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) supportano direttamente in questo argomento. Per le operazioni che non, è possibile usare **rx_exec** per inviare il codice in un contesto di calcolo remoto.

In questo esempio, non i dati non elaborati dovevano essere trasferito da SQL Server per il Notebook di Jupyter. Tutti i calcoli avvengono all'interno del database di Iris e il client viene restituito solo il file di immagine.

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

Lo screenshot seguente mostra l'output di tracciato di input e a dispersione.

  ![notebook di jupyter che Mostra output di grafico a dispersione](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7 - avviare Python da strumenti

Poiché gli sviluppatori lavorano frequentemente con più versioni di Python, non il programma di installazione aggiunge al percorso di Python. Per utilizzare il file eseguibile di Python e librerie installate dal programma di installazione, IDE per il collegamento **Python.exe** nel percorso che offre anche **revoscalepy** e **microsoftml**. 

### <a name="command-line"></a>Riga di comando

Quando si esegue **Python.exe** dal c:\Programmi\Microsoft Files\Microsoft\PyForMLS (o qualsiasi percorso specificato per l'installazione della libreria client Python), è possibile utilizzare la distribuzione Anaconda completa oltre a Python di Microsoft moduli **revoscalepy** e **microsoftml**.

1. Passare a c:\Programmi\Microsoft Files\Microsoft\PyForMLS e fare doppio clic su **Python.exe**.
2. Aprire la Guida interattiva: `help()`
3. Digitare il nome di un modulo al prompt di Guida in linea: `help> revoscalepy`. Guida restituisce il nome, contenuto del pacchetto, versione e percorso del file.
4. Restituisce informazioni sulla versione e del pacchetto nel **aiutare >** prompt dei comandi: `revoscalepy`. Premere INVIO più volte per chiudere la Guida.
5. Importare un modulo: `import revoscalepy`


### <a name="jupyter-notebooks"></a>Notebook di Jupyter

Questo articolo usa i notebook di Jupyter incorporato per chiamate di funzione per illustrare **revoscalepy**. Se si ha familiarità con questo strumento, lo screenshot seguente illustra l'interazione di parti e il motivo per cui tutti gli elementi "funziona senza problemi". 

La cartella padre Files\Microsoft\PyForMLS c:\Programmi\Microsoft contiene Anaconda e i pacchetti Microsoft. I notebook di Jupyter è inclusi in Anaconda, nella cartella Scripts, e gli eseguibili di Python vengono registrati automaticamente con i notebook di Jupyter. I pacchetti disponibili nel sito di pacchetti possono essere importati in un notebook, inclusi i tre pacchetti Microsoft usati per l'analisi scientifica dei dati e machine learning.

  ![File eseguibili e librerie](media/jupyter-notebook-python-registration.png)

Se si usa un altro IDE, è necessario collegare le librerie di file eseguibili e la funzione Python per lo strumento. Le sezioni seguenti forniscono istruzioni per gli strumenti di usati comune.

### <a name="visual-studio"></a>Visual Studio

Se hai [Python in Visual Studio](https://code.visualstudio.com/docs/languages/python), usare le opzioni di configurazione seguenti per creare un ambiente di Python che include i pacchetti Python per Microsoft.

| Impostazione di configurazione | Valore |
|-----------------------|-------|
| **Prefisso percorso** | C:\Programmi\Microsoft Files\Microsoft\PyForMLS |
| **Cesta k interpretu** | C:\Programmi\Microsoft Files\Microsoft\PyForMLS\python.exe |
| **Interprete con finestra** | C:\Programmi\Microsoft Files\Microsoft\PyForMLS\pythonw.exe |

Per informazioni sulla configurazione di un ambiente di Python, vedere [gestione di ambienti Python in Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

### <a name="pycharm"></a>PyCharm

In PyCharm, impostare l'interprete Python eseguibile installato per Machine Learning Server.

1. In un nuovo progetto, in impostazioni, fare clic su **locale aggiungere**.

2. Immettere `C:\Program Files\Microsoft\PyForMLS\`.

È ora possibile importare **revoscalepy**, **microsoftml**, o **azureml** moduli. È anche possibile scegliere **degli strumenti** > **Console Python** per aprire una finestra interattiva.

## <a name="next-steps"></a>Passaggi successivi

Ora che si dispone di strumenti e una connessione attiva a SQL Server, espandere le tue competenze mediante l'esecuzione tramite le guide introduttive di Python usando [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

> [!div class="nextstepaction"]
> [Guida introduttiva: Verificare il che esistenza di Python in SQL Server](../tutorials/quickstart-python-verify.md)