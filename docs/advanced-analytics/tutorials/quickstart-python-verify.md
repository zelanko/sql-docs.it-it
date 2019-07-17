---
title: Guida introduttiva per la verifica per determinare se Python è presente in SQL Server
description: Guida introduttiva per la verifica dell'esistenza Python e Machine Learning Services in SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0a2c525c89a70f4a36749d7b9c6fb769362d517b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962048"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>Avvio rapido: Verificare la presenza di Python in SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server include il supporto Python per analitica di analisi scientifica dei dati residenti in dati di SQL Server. L'esecuzione dello script è tramite le stored procedure, usando uno degli approcci seguenti:

+ Incorporati [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure, il passaggio di script di Python in come parametro di input.
+ Eseguire il wrapping dello script di Python in un [stored procedure di custom](sqldev-in-database-r-for-sql-developers.md) creato.

In questa Guida introduttiva, si verificherà [Machine Learning Services di SQL Server 2017](../what-is-sql-server-machine-learning.md) viene installato e configurato.

## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione, è necessario accedere a un'istanza di SQL Server con [Machine Learning Services di SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) installato.

Istanza di SQL Server può essere in una macchina virtuale di Azure o in locale. Tieni presente che la funzionalità di script esterna è disabilitata per impostazione predefinita, pertanto potrebbe essere necessario [abilita la creazione di script esterni](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificare che **Launchpad di SQL Server service** è in esecuzione prima di iniziare.

È anche necessario uno strumento per l'esecuzione di query SQL. È possibile eseguire gli script di Python con qualsiasi gestione del database o eseguire una query dello strumento, purché possa connettersi a un'istanza di SQL Server ed eseguire una query T-SQL o una stored procedure. Questa Guida introduttiva Usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-python-exists"></a>Verificare il che esistenza di Python

È possibile verificare che servizi di Machine Learning (è abilitata per l'istanza di SQL Server e la versione di Python installata. Attenersi alla procedura seguente.

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server.

2. Eseguire il codice riportato di seguito. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. Script Python `print` funzione restituisce la versione per il **messaggi** finestra. Nell'output di esempio seguente, si noterà che in questo caso SQL Server hanno Python versione 3.5.2 installato.

    **Risultati**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

Se si verificano errori, sono disponibili un'ampia gamma di operazioni che è possibile eseguire per assicurarsi che l'istanza e Python possono comunicare.

Regola in primo luogo, gli eventuali problemi di installazione. Configurazione dopo l'installazione è necessaria per abilitare l'uso delle librerie di codice esterno. Visualizzare [installare SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). Analogamente, assicurarsi che il servizio Launchpad sia in esecuzione.

È inoltre necessario aggiungere il gruppo di utenti Windows `SQLRUserGroup` come account di accesso nell'istanza, per assicurarsi che Launchpad può fornire la comunicazione tra codice Python e SQL Server. (Lo stesso gruppo viene usato per entrambi R e l'esecuzione di codice Python). Per altre informazioni, vedere [creare un account di accesso per SQLRUserGroup](../security/create-a-login-for-sqlrusergroup.md).

Inoltre, è necessario abilitare i protocolli di rete che sono stati disabilitati o aprire il firewall in modo che SQL Server può comunicare con client esterni. Per altre informazioni, vedere [risoluzione dei problemi di installazione](../common-issues-external-script-execution.md).

## <a name="call-revoscalepy-functions"></a>Chiamare funzioni revoscalepy

Per verificare che **revoscalepy** è disponibile, eseguire uno script di esempio che include [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) che produce un riepilogo di dati statistici. Lo script seguente viene illustrato come recuperare un file di dati di esempio con estensione xdf da incorporati negli esempi inclusi in revoscalepy. La funzione RxOptions fornisce il **sampleDataDir** parametro che restituisce il percorso del file di esempio.

Poiché rx_summary restituisce un oggetto di tipo `class revoscalepy.functions.RxSummary.RxSummaryResults`, che contiene più elementi, è possibile usare pandas per estrarre solo il frame di dati in un formato tabulare.

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

## <a name="list-python-packages"></a>Elencare i pacchetti Python

Microsoft fornisce una serie di pacchetti Python pre-installati con i servizi di Machine Learning nell'istanza di SQL Server. Per visualizzare un elenco di Python vengono installati i pacchetti, inclusi versione, seguire questa procedura.

1. Eseguire lo script seguente nell'istanza di SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. L'output è tratto dal `pip.get_installed_distributions()` in Python e restituiti come `STDOUT` messaggi.

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

Ora che hai confermato che l'istanza è pronta per funzionare con Python, esaminiamo più da vicino un'interazione di Python di base.

> [!div class="nextstepaction"]
> [Avvio rapido: Script di Python "Hello world" in SQL Server](quickstart-python-run-using-t-sql.md)
