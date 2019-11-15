---
title: Pacchetto revoscalepy per Python
description: Introduzione al modulo revoscalepy in Machine Learning Services per SQL Server con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6de9072c32155446b3ff40df3f81af9073c1090
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706818"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (modulo Python in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy** è un modulo di Microsoft compatibile con Python35 che supporta processi di elaborazione distribuita, contesti di calcolo remoti e algoritmi di data science ad alte prestazioni. Questo modulo è basato sul pacchetto **RevoScaleR** per R (distribuito con Microsoft R Server e R Services per SQL Server), che offre funzionalità simili:

+ Contesti di calcolo locali e remoti in sistemi con la stessa versione di **revoscalepy**
+ Funzioni di visualizzazione e trasformazione dei dati
+ Funzioni di data science, scalabili tramite elaborazione distribuita o parallela
+ Prestazioni migliorate, incluso l'uso delle librerie Intel Math

Le origini dati e i contesti di calcolo creati in **revoscalepy** possono essere usati anche negli algoritmi di Machine Learning. Per un'introduzione a questi algoritmi, vedere [Modulo microsoftml per Python in SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentazione di riferimento completa

La libreria **revoscalepy** è distribuita in più prodotti Microsoft, ma l'utilizzo è lo stesso indipendentemente dal fatto che sia inclusa in SQL Server o in un altro prodotto. Poiché le funzioni sono le stesse, la [documentazione per le singole funzioni di revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) viene pubblicata in una sola posizione nelle [informazioni di riferimento per Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per Microsoft Machine Learning Server. In caso di comportamenti specifici per un prodotto, le discrepanze verranno indicate nella pagina della Guida delle funzioni in questione.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

Il modulo **revoscalepy** è basato su Python 3.5 ed è disponibile solo quando si installa uno dei prodotti o download Microsoft seguenti:

+ [Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Librerie client Python per un client di data science](setup-python-client-tools-sql.md)

> [!NOTE]
> Le versioni complete del prodotto sono solo per Windows in SQL Server 2017. Sia Windows che Linux sono supportati per **revoscalepy**in [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funzioni per categoria

Questa sezione elenca le funzioni per categoria per offrire un'idea di come vengono usate. È anche possibile usare il [sommario](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-data-source-and-compute"></a>1 - Origine dati e calcolo

**revoscalepy** include funzioni per la creazione di origini dati e l'impostazione della posizione, o *contesto di calcolo*, in cui vengono eseguiti i calcoli. Nella tabella seguente sono elencate le funzioni relative agli scenari con SQL Server.

In alcuni casi SQL Server e Python usano tipi di dati diversi. Per un elenco dei mapping tra i tipi di dati SQL e Python, vedere [Mapping dei tipi di dati tra Python e SQL](python-libraries-and-data-types.md).

| Funzione| Descrizione|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Crea un oggetto contesto di calcolo di SQL Server per eseguire il push dei calcoli in un'istanza remota. Diverse funzioni di **revoscalepy** accettano il contesto di calcolo come argomento. Per un esempio di cambio di contesto, vedere [Creare un modello usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Crea un oggetto dati basato su una query o una tabella SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Crea un'origine dati basata su una connessione ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Crea un'origine dati basata su un file XDF locale. I file XDF vengono spesso usati per l'offload dei dati in memoria su disco. Un file XDF può essere utile quando si usano più dati di quanti sia possibile trasferire dal database in un batch o più dati di quanti sia possibile archiviare in memoria. Se ad esempio si spostano regolarmente grandi quantità di dati da un database a una workstation locale, invece di eseguire ripetutamente query sul database per ogni operazione R, è possibile usare il file XDF come una sorta di cache per salvare i dati localmente e quindi lavorare nell'area di lavoro R. |

> [!TIP]
> Se non si ha familiarità con il concetto di origini dati o di contesti di calcolo, è consigliabile iniziare con il [calcolo distribuito](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) nella documentazione di Microsoft Machine Learning Server.

## <a name="2-data-manipulation-etl"></a>2 - Manipolazione dei dati (ETL)

| Funzione | Descrizione |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importa i dati in un file con estensione xdf o un frame di dati.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Trasforma i dati da un set di dati di input a un set di dati di output.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3 - Training e riepilogo

| Funzione| Descrizione|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Adatta gli alberi delle decisioni con boosting a gradienti stocastici|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Adatta le foreste delle decisioni di classificazione e regressione|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Adatta gli alberi di classificazione e regressione |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Creare un modello di regressione lineare|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Creare un modello di regressione logistica|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Genera riepiloghi univariati di oggetti in revoscalepy.|

Per altri approcci, è consigliabile vedere anche le funzioni di [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package).

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4 - Funzioni di assegnazione dei punteggi

| Funzione| Descrizione|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Genera stime da un modello sottoposto a training.|) | Genera stime da un modello sottoposto a training e può essere usata per l'assegnazione dei punteggi in tempo reale. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Calcola i valori stimati e i residui usando gli oggetti rx_lin_mod e rx_logit. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcola i valori stimati o adattati per un set di dati da un oggetto rx_dforest o rx_btrees. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcola i valori stimati o adattati per un set di dati da un oggetto rx_dtree. |

## <a name="how-to-work-with-revoscalepy"></a>Come utilizzare revoscalepy

Le funzioni di **revoscalepy** possono essere chiamate nel codice Python incapsulato nelle stored procedure. La maggior parte degli sviluppatori compila in locale le soluzioni **revoscalepy** e quindi esegue la migrazione del codice Python completato alle stored procedure, come esercizio di distribuzione.

Durante un'esecuzione locale, si esegue in genere uno script Python dalla riga di comando o da un ambiente di sviluppo Python e si specifica un contesto di calcolo di SQL Server usando una delle funzioni di **revoscalepy**. È possibile usare il contesto di calcolo remoto per l'intero codice o per singole funzioni. Ad esempio, potrebbe essere necessario eseguire l'offload del training del modello nel server per usare i dati più recenti ed evitare lo spostamento dati.

Quando si è pronti per incapsulare lo script Python all'interno di una stored procedure, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), è consigliabile riscrivere il codice come una singola funzione con input e output chiaramente definiti. 

Gli input e gli output devono essere frame di dati **pandas**. Al termine dell'operazione, sarà possibile chiamare la stored procedure da qualsiasi client con supporto per T-SQL, passare facilmente query SQL come input e salvare i risultati in tabelle SQL. Per un esempio, vedere l'esercitazione [Analisi dei dati Python nel database per sviluppatori SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Uso di revoscalepy con microsoftml

Le funzioni Python per [microsoftml](ref-py-microsoftml.md) sono integrate con i contesti di calcolo e le origini dati disponibili in revoscalepy. Quando si chiamano funzioni da microsoftml, ad esempio quando si esegue la definizione o il training di un modello, usare le funzioni revoscalepy per eseguire il codice Python in locale o in un contesto di calcolo remoto di SQL Server.

L'esempio seguente mostra la sintassi per l'importazione di moduli nel codice Python. È quindi possibile fare riferimento alle singole funzioni necessarie.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di Python](../tutorials/sql-server-python-tutorials.md)
+ [Esercitazione: Incorporare codice Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Informazioni di riferimento su Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
