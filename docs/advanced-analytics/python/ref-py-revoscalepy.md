---
title: pacchetto Python revoscalepy - servizi di SQL Server Machine Learning
description: Introduzione al modulo revoscalepy in SQL Server 2017 Machine Learning Services con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3482a15392fa04f7f10d2acbb0843d124e27dc21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962742"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (modulo di Python in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy** è un modulo Python35 compatibile da Microsoft che supporta l'elaborazione distribuita, contesti di calcolo remoti e gli algoritmi di analisi scientifica dei dati ad alte prestazioni. Si basa il **RevoScaleR** pacchetto per R (distribuita con Microsoft R Server e SQL Server R Services), che offre funzionalità simili:

+ Nei sistemi con la stessa versione di contesti di calcolo di locale e remota **revoscalepy**
+ Funzioni di trasformazione e la visualizzazione dei dati
+ Funzioni di data science, scalabile tramite l'elaborazione distribuita o parallela
+ Miglioramento delle prestazioni, incluso l'uso delle librerie Intel math

Origini dati e contesti di calcolo creati in **revoscalepy** è anche utilizzabile in algoritmi di machine learning. Per un'introduzione a questi algoritmi, vedere [microsoftml modulo Python in SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentazione di riferimento complete

Il **revoscalepy** libreria distribuita in vari prodotti Microsoft, ma che utilizzo è lo stesso sia ottenere la libreria in SQL Server o un altro prodotto. Perché le funzioni sono gli stessi, [documentazione per le funzioni revoscalepy singoli](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) pubblicata in un'unica posizione sotto il [riferimento Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per Microsoft Machine Learning Server. Qualsiasi prodotto specifico deve comportamenti esistono, verranno indicate nella pagina della Guida funzione discrepanze.

## <a name="versions-and-platforms"></a>Versioni e piattaforme

Il **revoscalepy** modulo è basata su Python 3.5 e disponibile solo quando si installa uno dei seguenti prodotti Microsoft o download:

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o versione successiva](https://docs.microsoft.com/machine-learning-server/)
+ [Librerie client Python per un client di data science](setup-python-client-tools-sql.md)

> [!NOTE]
> Sono versioni di rilascio versione completa del prodotto Windows sola, a partire da SQL Server 2017. Il supporto per Linux **revoscalepy** sono le novità [anteprima di SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funzioni per categoria

In questa sezione elenca le funzioni in base alla categoria per farsi un'idea dell'utilizzo di ciascuna di esse. È anche possibile usare la [sommario](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) per trovare le funzioni in ordine alfabetico.

## <a name="1-data-source-and-compute"></a>Risorse di calcolo e di origine dati 1

**revoscalepy** include funzioni per la creazione di origini dati e impostazione del percorso, o *contesto di calcolo*, di cui vengono eseguiti i calcoli. Funzioni rilevanti per gli scenari di SQL Server sono elencate nella tabella seguente.

SQL Server e Python usare diversi tipi di dati in alcuni casi. Per un elenco dei mapping tra tipi di dati SQL e Python, vedere [tipi di dati Python-to-SQL](python-libraries-and-data-types.md).

| Funzione| Descrizione|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Creare un oggetto di contesto di calcolo di SQL Server per trasferire i calcoli a un'istanza remota. Numerosi **revoscalepy** funzioni accettano il contesto di calcolo come argomento. Per un esempio di cambio di contesto, vedere [creare un modello usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Creare un oggetto di dati basato su una query di SQL Server o una tabella. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Creare un'origine dati basata su una connessione ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Creare un'origine dati basata su un file XDF locale. I file XDF vengono spesso utilizzati per l'offload dei dati in memoria su disco. Un file XDF può essere utile quando si utilizzano più dati possono essere trasferiti dal database in un unico batch, o altri dati che possono adattarsi alla memoria. Ad esempio, se si spostano regolarmente grandi quantità di dati da un database in una workstation locale, invece di query del database più volte per ogni operazione R, è possibile utilizzare il file XDF come un tipo di cache per salvare i dati in locale e quindi lavorare nell'area di lavoro R. |

> [!TIP]
> Se si ha familiarità con l'idea di origini dati o contesti di calcolo, è consigliabile iniziare con [elaborazione distribuita](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) nella documentazione di Microsoft Machine Learning Server.

## <a name="2-data-manipulation-etl"></a>Manipolazione dei dati-2 (ETL)

| Funzione | Descrizione |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importare dati in un frame di dati o file con estensione xdf.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Trasformare i dati da un set di dati di input a un set di dati di output.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-formazione e attività di riepilogo

| Funzione| Descrizione|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Adattare gli alberi delle decisioni con Boosting a gradienti stocastica|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Adattare la classificazione e regressione foreste delle decisioni|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Alberi di classificazione e regressione appropriati |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Creare un modello di regressione lineare|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Creare un modello di regressione logistica|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Produrre riepiloghi univariata degli oggetti in revoscalepy.|

È consigliabile rivedere anche le funzioni [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) per altri approcci.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>Funzioni di assegnazione dei punteggi di 4

| Funzione| Descrizione|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Generare stime tramite un modello con training|) | Genera stime da un modello con training e può essere usato per l'assegnazione dei punteggi in tempo reale. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Calcolare i valori stimati e valori residui utilizzando oggetti rx_lin_mod e rx_logit. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcolare i valori stimati o adattati per un set di dati da un oggetto rx_dforest o rx_btrees. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcolare i valori stimati o adattati per un set di dati da un oggetto rx_dtree. |

## <a name="how-to-work-with-revoscalepy"></a>Come lavorare con revoscalepy

Le funzioni nello **revoscalepy** possono essere chiamati nel codice Python incapsulato nelle stored procedure. La maggior parte degli sviluppatori di compilare **revoscalepy** soluzioni in locale, e quindi eseguire la migrazione di codice Python alle stored procedure come un esercizio di distribuzione.

Quando si esegue localmente, in genere eseguire uno script di Python dalla riga di comando o da un ambiente di sviluppo Python e specificare un contesto di calcolo di SQL Server utilizzando uno dei **revoscalepy** funzioni. È possibile usare il contesto di calcolo remoto per tutto il codice o per le singole funzioni. Ad esempio, è possibile eseguire l'offload di training del modello per il server di usare i dati più recenti e di evitare lo spostamento dei dati.

Quando si è pronti per lo script di Python all'interno di una stored procedure di incapsulare [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), si consiglia di riscrivere il codice come una singola funzione che è chiaramente definito gli input e output. 

Input e output deve essere **pandas** frame di dati. Quando questa operazione, è possibile chiamare la stored procedure da qualsiasi client che supporta T-SQL, facilmente passare le query SQL come input e salvare i risultati in tabelle SQL. Per un esempio, vedere [altre analitica di Python nel database per sviluppatori SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Con revoscalepy microsoftml

Funzioni di script Python per [microsoftml](ref-py-microsoftml.md) sono integrati con le origini dati e contesti di calcolo sono disponibili in revoscalepy. Quando si chiamano funzioni di microsoftml, ad esempio quando la definizione e training di un modello Usa le funzioni revoscalepy per eseguire script Python code sia in locale o in un SQl Server remoto contesto di calcolo.

Nell'esempio seguente viene illustrata la sintassi per l'importazione di moduli nel codice Python. È quindi possibile fare riferimento a singole funzioni che è necessario.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vedere anche

+ [Esercitazioni di Python](../tutorials/sql-server-python-tutorials.md)
+ [Esercitazione: Incorporare il codice Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Riferimento di Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
