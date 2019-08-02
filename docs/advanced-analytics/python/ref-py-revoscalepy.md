---
title: pacchetto python revoscalepy
description: Introduzione al modulo revoscalepy in SQL Server Machine Learning Services con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 76c68d0753c4ba29387b3378c1086ce9bce4f53b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715770"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (modulo Python in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy** è un modulo compatibile con Python35 di Microsoft che supporta l'elaborazione distribuita, i contesti di calcolo remoti e gli algoritmi a elevate prestazioni Data Science. Si basa sul pacchetto **RevoScaleR** per R (distribuito con Microsoft R Server e R Services per SQL Server), che offre funzionalità simili:

+ Contesti di calcolo locali e remoti in sistemi con la stessa versione di **revoscalepy**
+ Funzioni di visualizzazione e trasformazione dei dati
+ Funzioni di Data Science, scalabili tramite elaborazione distribuita o parallela
+ Miglioramento delle prestazioni, incluso l'uso di Intel Math Libraries

Le origini dati e i contesti di calcolo creati in **revoscalepy** possono essere usati anche negli algoritmi di machine learning. Per un'introduzione a questi algoritmi, vedere il [modulo Microsoftml Python in SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

La libreria **revoscalepy** viene distribuita in più prodotti Microsoft, ma l'utilizzo è lo stesso se si ottiene la libreria in SQL Server o in un altro prodotto. Poiché le funzioni sono uguali, la [documentazione per le singole funzioni revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) viene pubblicata in una sola posizione sotto il [riferimento Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per Microsoft Machine Learning server. Se sono presenti comportamenti specifici del prodotto, le discrepanze verranno indicate nella pagina della guida della funzione.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

Il modulo **revoscalepy** è basato su Python 3,5 ed è disponibile solo quando si installa uno dei seguenti prodotti o download Microsoft:

+ [Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Librerie client Python per un client data science](setup-python-client-tools-sql.md)

> [!NOTE]
> Le versioni di rilascio complete del prodotto sono solo Windows, a partire da SQL Server 2017. Il supporto Linux per **revoscalepy** è una novità di [SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funzioni per categoria

In questa sezione vengono elencate le funzioni per categoria per fornire un'idea del modo in cui vengono utilizzate. È anche possibile usare il [Sommario](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-data-source-and-compute"></a>1-origine dati e calcolo

**revoscalepy** include funzioni per la creazione di origini dati e l'impostazione della posizione o del *contesto di calcolo*in cui vengono eseguiti i calcoli. Nella tabella seguente sono elencate le funzioni rilevanti per gli scenari SQL Server.

In alcuni casi SQL Server e Python usano tipi di dati diversi. Per un elenco dei mapping tra i tipi di dati SQL e Python, vedere [tipi di dati Python-to-SQL](python-libraries-and-data-types.md).

| Funzione| Descrizione|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Creare un oggetto contesto di calcolo SQL Server per eseguire il push di calcoli in un'istanza remota. Diverse funzioni **revoscalepy** accettano il contesto di calcolo come argomento. Per un esempio di cambio di contesto, vedere [creare un modello con revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Creare un oggetto dati basato su una query o una tabella SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Creare un'origine dati basata su una connessione ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Creare un'origine dati basata su un file XDF locale. I file XDF vengono spesso usati per l'offload dei dati in memoria su disco. Un file XDF può essere utile quando si utilizzano più dati rispetto a quelli che possono essere trasferiti dal database in un unico batch o più dati di quelli che possono essere contenuti nella memoria. Se, ad esempio, si spostano regolarmente grandi quantità di dati da un database a una workstation locale, anziché eseguire ripetutamente query sul database per ogni operazione R, è possibile usare il file XDF come un tipo di cache per salvare i dati localmente e quindi usarli nell'area di lavoro di R. |

> [!TIP]
> Se non si ha familiarità con l'idea di origini dati o contesti di calcolo, è consigliabile iniziare con l' [elaborazione distribuita](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) nella documentazione di Microsoft Machine Learning server.

## <a name="2-data-manipulation-etl"></a>2-manipolazione dei dati (ETL)

| Funzione | Descrizione |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importa i dati in un file con estensione XDF o un frame di dati.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Trasformare i dati da un set di dati di input a un set di dati di output.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-training e riepilogo

| Funzione| Descrizione|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Adatta alberi delle decisioni con boosting a gradienti stocastici|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Adattare le foreste delle decisioni di classificazione e regressione|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Adatta alberi di classificazione e regressione |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Creare un modello di regressione lineare|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Creare un modello di regressione logistica|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Produrre riepiloghi univariati di oggetti in revoscalepy.|

Per ulteriori approcci, vedere anche le funzioni di [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) .

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4-funzioni di Punteggio

| Funzione| Descrizione|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Generare stime da un modello sottoposto a training|) | Genera stime da un modello sottoposto a training e può essere utilizzato per il punteggio in tempo reale. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Calcola i valori stimati e i residui usando gli oggetti rx_lin_mod e rx_logit. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcola i valori stimati o montati per un set di dati da un oggetto rx_dforest o rx_btrees. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcola i valori stimati o montati per un set di dati da un oggetto rx_dtree. |

## <a name="how-to-work-with-revoscalepy"></a>Come usare revoscalepy

Le funzioni in **revoscalepy** possono essere richiamate nel codice Python incapsulato nelle stored procedure. La maggior parte degli sviluppatori compila le soluzioni **revoscalepy** localmente e quindi esegue la migrazione del codice Python completato alle stored procedure come esercizio di distribuzione.

Quando si esegue localmente, in genere si esegue uno script Python dalla riga di comando o da un ambiente di sviluppo Python e si specifica un SQL Server contesto di calcolo usando una delle funzioni **revoscalepy** . È possibile usare il contesto di calcolo remoto per l'intero codice o per le singole funzioni. Ad esempio, potrebbe essere necessario eseguire l'offload del training del modello nel server per usare i dati più recenti ed evitare lo spostamento dei dati.

Quando si è pronti per incapsulare lo script Python all'interno di un stored procedure, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), è consigliabile riscrivere il codice come una singola funzione con input e output chiaramente definiti. 

Gli input e gli output devono essere frame di dati Pandas. Al termine di questa operazione, è possibile chiamare il stored procedure da qualsiasi client che supporta T-SQL, passare facilmente le query SQL come input e salvare i risultati nelle tabelle SQL. Per un esempio, vedere [informazioni sull'analisi Python nel database per sviluppatori SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Uso di revoscalepy con microsoftml

Le funzioni Python per [microsoftml](ref-py-microsoftml.md) sono integrate con i contesti di calcolo e le origini dati disponibili in revoscalepy. Quando si chiamano funzioni da microsoftml, ad esempio quando si definisce e si esegue il training di un modello, usare le funzioni revoscalepy per eseguire il codice Python localmente o in un contesto di calcolo remoto di SQl server.

Nell'esempio seguente viene illustrata la sintassi per l'importazione di moduli nel codice Python. È quindi possibile fare riferimento alle singole funzioni necessarie.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di Python](../tutorials/sql-server-python-tutorials.md)
+ [Esercitazione: Incorporare codice Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Guida di riferimento a Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
