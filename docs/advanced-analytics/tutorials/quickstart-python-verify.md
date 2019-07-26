---
title: Guida introduttiva per la verifica dell'esistenza di Python in SQL Server
description: Guida introduttiva per la verifica dell'esistenza di Python e Machine Learning Services in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0dd5714f47c90c0091daacbd792b80c05ec68675
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469692"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>Avvio rapido: Verificare la presenza di Python in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server include il supporto del linguaggio Python per data science Analytics sui dati SQL Server residenti. L'esecuzione di script avviene tramite stored procedure, usando uno degli approcci seguenti:

+ [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) incorporato stored procedure, passando lo script Python in come parametro di input.
+ Eseguire il wrapping dello script Python in un [stored procedure personalizzato](sqldev-in-database-r-for-sql-developers.md) creato dall'utente.

In questa Guida introduttiva verrà verificato che sia installato e configurato [SQL Server 2017 Machine Learning Services](../what-is-sql-server-machine-learning.md) .

## <a name="prerequisites"></a>Prerequisiti

Questo esercizio richiede l'accesso a un'istanza di SQL Server con [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) installato.

L'istanza di SQL Server può trovarsi in una macchina virtuale di Azure o in locale. È sufficiente tenere presente che la funzionalità di scripting esterno è disabilitata per impostazione predefinita, pertanto potrebbe essere necessario abilitare l'esecuzione di [script esterni](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che **launchpad di SQL Server servizio** sia in esecuzione prima di iniziare.

È anche necessario uno strumento per l'esecuzione di query SQL. È possibile eseguire gli script Python usando qualsiasi strumento di gestione del database o query, purché sia in grado di connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o stored procedure. Questa Guida introduttiva usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-python-exists"></a>Verificare che Python esista

È possibile confermare che Machine Learning Services (è abilitato per l'istanza di SQL Server e la versione di Python installata. Attenersi alla procedura riportata di seguito.

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server.

2. Eseguire il codice riportato di seguito. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. La funzione `print` Python restituisce la versione alla finestra **messages** . Nell'output di esempio seguente si noterà che SQL Server in questo caso è installato Python versione 3.5.2.

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

Se si verificano errori, è possibile eseguire una serie di operazioni per garantire che l'istanza e Python possano comunicare.

Prima di tutto, escludere eventuali problemi di installazione. La configurazione post-installazione è necessaria per consentire l'uso di librerie di codice esterno. Vedere [Install SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). Analogamente, assicurarsi che il servizio Launchpad sia in esecuzione.

È inoltre necessario aggiungere il gruppo `SQLRUserGroup` di utenti Windows come account di accesso per l'istanza di, per assicurarsi che Launchpad possa fornire la comunicazione tra Python e SQL Server. (Lo stesso gruppo viene usato per l'esecuzione del codice R e Python). Per ulteriori informazioni, vedere la pagina relativa alla [creazione di un account di accesso per SQLRUserGroup](../security/create-a-login-for-sqlrusergroup.md).

Potrebbe inoltre essere necessario abilitare i protocolli di rete disabilitati o aprire il firewall in modo che SQL Server possa comunicare con client esterni. Per ulteriori informazioni, vedere [risoluzione dei problemi di installazione](../common-issues-external-script-execution.md).

## <a name="call-revoscalepy-functions"></a>Chiama funzioni revoscalepy

Per verificare che **revoscalepy** sia disponibile, eseguire uno script di esempio che include [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) che produce dati di riepilogo statistici. Lo script seguente illustra come recuperare un file di dati Sample. XDF da esempi predefiniti inclusi in revoscalepy. La funzione RxOptions fornisce il parametro **sampleDataDir** che restituisce il percorso dei file di esempio.

Poiché rx_summary restituisce un oggetto di tipo `class revoscalepy.functions.RxSummary.RxSummaryResults`, che contiene più elementi, è possibile usare i Panda per estrarre solo il frame di dati in formato tabulare.

```sql
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="list-python-packages"></a>Elenca pacchetti Python

Microsoft fornisce una serie di pacchetti Python pre-installati con Machine Learning Services nell'istanza di SQL Server. Per visualizzare un elenco dei pacchetti Python installati, inclusa la versione, seguire questa procedura.

1. Eseguire lo script seguente nell'istanza di SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. L'output è da `pip.get_installed_distributions()` in Python e restituito come `STDOUT` messaggi.

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    xlwt 1.2.0
    XlsxWriter 0.9.6
    xlrd 1.0.0
    win-unicode-console 0.5
    widgetsnbextension 2.0.0
    wheel 0.29.0
    Werkzeug 0.12.1
    wcwidth 0.1.7
    unicodecsv 0.14.1
    traitlets 4.3.2
    tornado 4.4.2
    toolz 0.8.2
    testpath 0.3
    tables 3.2.2
    sympy 1.0
    statsmodels 0.8.0
    sqlparse 0.1.19
    SQLAlchemy 1.1.9
    snowballstemmer 1.2.1
    six 1.10.0
    simplegeneric 0.8.1
    seaborn 0.7.1
    scipy 0.19.0
    scikit-learn 0.18.1
    ...
    ```

## <a name="next-steps"></a>Passaggi successivi

A questo punto, dopo aver verificato che l'istanza è pronta per l'uso con Python, esaminare in dettaglio un'interazione Python di base.

> [!div class="nextstepaction"]
> [Avvio rapido: Script Python "Hello World" in SQL Server](quickstart-python-run-using-t-sql.md)
