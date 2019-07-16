---
title: Generare le previsioni e stime usando modelli di machine learning - SQL Server Machine Learning Services
description: Usare rxPredict o sp_rxPredict per l'assegnazione dei punteggi in tempo reale o prevedere T-SQL per le stime di assegnazione dei punteggi nativa e le previsioni in R e Pythin in SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4af5fff7581ae2ae8f74e09603b75bca620ca775
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962639"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>Come generare le previsioni e stime usando modelli di machine learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Usando un modello esistente per prevedere o prevedere risultati utili per nuovi input di dati è un'attività principale nell'apprendimento automatico. Questo articolo consente di enumerare gli approcci per la generazione di stime in SQL Server. Tra gli approcci vengono eseguite dipendenze in fase di elaborazione interna delle metodologie per stime ad alta velocità, in cui velocità si basa su incrementale riduzioni dei. Un minor numero di dipendenze significa che le stime più veloci.

Usando l'infrastruttura di elaborazione interna (punteggio in tempo reale o nativa) include requisiti della libreria. Le funzioni devono essere compresi le librerie di Microsoft. Codice R o Python che chiama funzioni open source o di terze parti non è supportato nelle estensioni CLR o C++.

La tabella seguente riepiloga i framework di assegnazione dei punteggi per la previsione e stime. 

| Metodologia           | Interfaccia         | Requisiti della libreria | Velocità di elaborazione |
|-----------------------|-------------------|----------------------|----------------------|
| Framework di estendibilità | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | No. I modelli possono essere basati su qualsiasi funzione R o Python | Centinaia di millisecondi. <br/>Il caricamento di un ambiente di runtime ha un costo fisso, il calcolo della media di tre a 600 millisecondi, prima di tutti i nuovi dati viene assegnato un punteggio. |
| [Estensione CLR assegnazione dei punteggi in tempo reale](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) su un modello serializzato | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | Decine di millisecondi, in Media. |
| [Estensione di C++ di assegnazione dei punteggi nativa](../sql-native-scoring.md) | [Funzione T-SQL stimare](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) su un modello serializzato | R: RevoScaleR <br/>Python: revoscalepy | Meno di 20 millisecondi, in Media. | 

Velocità di elaborazione e non sostanza dell'output è la funzionalità di differenziazione. Supponendo che le stesse funzioni e gli input, l'output con punteggio deve non variano in base utilizzato.

Il modello deve essere creato utilizzando una funzione supportata, quindi serializzato in un flusso di byte non elaborati salvato su disco o vengono archiviati in formato binario in un database. Usare una stored procedure o T-SQL, è possibile caricare e usare un modello binario senza l'overhead di un tempo di linguaggio eseguire R o Python, risultante in tempi più rapidi al completamento durante la generazione di punteggi di stima sui nuovi input.

L'importanza delle estensioni di C++ e CLR è prossimità al motore di database stesso. Il linguaggio nativo del motore di database è C++, ovvero estensioni scritte in C++ eseguito con un minor numero di dipendenze. Al contrario, le estensioni CLR dipendono da .NET Core. 

Come è prevedibile, supporto della piattaforma è stato interessato da questi ambienti di runtime. Estensioni del motore di database nativo esecuzione ovunque che è supportato nel database relazionale: Windows, Linux e Azure. Le estensioni CLR con il requisito di .NET Core attualmente è solo Windows.

## <a name="scoring-overview"></a>Panoramica di assegnazione dei punteggi

_Assegnazione dei punteggi_ è un processo in due passaggi. È possibile specificare un modello già sottoposto a training per caricare da una tabella. In secondo luogo, passare di nuovo i dati alla funzione, per generare i valori di stima di input (o _punteggi_). L'input è spesso una query T-SQL, che restituisce righe tabulari o singole. È possibile scegliere di generare un valore di colonna singola che rappresenta una probabilità o si potrebbero restituire valori diversi, ad esempio un intervallo di confidenza, errore o di altri complemento utile per la stima.

Un passo indietro, il processo complessivo di preparazione del modello e quindi la generazione di punteggi può essere riepilogata in questo modo:

1. Creare un modello usando un algoritmo supportato. Supporto varia in base alla metodologia di assegnazione dei punteggi che scelto.
2. Il training del modello.
3. Serializza il modello utilizzando un formato binario speciale.
3. Salvare il modello in SQL Server. In genere questo si intende archiviare il modello serializzato in una tabella di SQL Server.
4. Chiamare la funzione o una stored procedure, specifica il modello e i dati di input come parametri.

Quando l'input include molte righe di dati, è in genere più veloce per inserire i valori di stima in una tabella come parte del processo di assegnazione dei punteggi. La generazione di un singolo punteggio è più adatta in uno scenario in cui ottenere i valori di input da una richiesta di form o utente e restituire il punteggio a un'applicazione client. Per migliorare le prestazioni durante la generazione di punteggi successivi, SQL Server potrebbe memorizzare nella cache il modello in modo che possa essere ricaricato in memoria.

## <a name="compare-methods"></a>Confronto tra i metodi

Per mantenere l'integrità dei processi del motore di database base, il supporto per R e Python è abilitato in un'architettura a doppio che consente di isolare l'elaborazione del linguaggio dall'elaborazione RDBMS. A partire da SQL Server 2016, Microsoft ha aggiunto un framework di estensibilità che gli script R possono essere eseguite da T-SQL. In SQL Server 2017 è stata aggiunta l'integrazione di Python. 

Il framework di estendibilità supporta qualsiasi operazione che è possibile eseguire in R o Python, compreso tra le funzioni semplici e corsi di formazione complessi modelli di machine learning. Tuttavia, l'architettura dual-process richiede richiamo di un processo esterno di R o Python per ogni chiamata, indipendentemente dalla complessità dell'operazione. Quando il carico di lavoro comporta il caricamento di un modello con training preliminare da una tabella e di assegnazione dei punteggi contrastarla sui dati già in SQL Server, l'overhead della chiamata al metodo i processi esterni aggiunge latenza che può essere inaccettabile in determinate circostanze. Ad esempio, la rilevazione di frodi richiede redatto veloce di assegnazione dei punteggi.

Per aumentare la velocità di assegnazione dei punteggi per gli scenari di rilevamento di frodi, SQL Server aggiunta librerie di punteggio predefinite come estensioni di C++ e CLR che eliminano il sovraccarico dei processi di avvio R e Python.

[**Assegnazione dei punteggi in tempo reale** ](../real-time-scoring.md) era la prima soluzione di assegnazione dei punteggi a prestazioni elevate. Introdotta nelle prime versioni di SQL Server 2017 e versioni successive degli aggiornamenti per SQL Server 2016, assegnazione dei punteggi in tempo reale si basa sulle librerie di Common Language Runtime che ostacolano il settore per l'elaborazione su funzioni controllate da Microsoft in RevoScaleR, MicrosoftML (R), revoscalepy, Python e R e microsoftml (Python). Le librerie Common Language Runtime vengono richiamate utilizzando il **sp_rxPredict** stored procedure che genera l'errore punteggi da qualsiasi tipo di modello supportati, senza chiamare il runtime di R o Python.

[**Assegnazione dei punteggi nativa** ](../sql-native-scoring.md) è una funzionalità di SQL Server 2017, implementata come libreria di C++ nativa, ma solo per i modelli di RevoScaleR e revoscalepy. È l'approccio più rapido e più sicuro, ma supporta un set ridotto di funzioni rispetto ad altre metodologie.

## <a name="choose-a-scoring-method"></a>Scegliere un metodo di assegnazione dei punteggi

Requisiti di piattaforma spesso determinano quali metodologia di assegnazione dei punteggi da utilizzare.

| Piattaforma e versione del prodotto | Metodologia |
|------------------------------|-------------|
| SQL Server 2017 in Windows, SQL Server 2017 su Linux e il Database SQL di Azure | **Assegnazione dei punteggi nativa** con T-SQL prevedere |
| SQL Server 2017 (solo Windows), SQL Server 2016 R Services in SP1 o versione successiva | **Assegnazione dei punteggi in tempo reale** con Service Pack\_rxPredict stored procedure |

Si consiglia di assegnazione dei punteggi nativa con la funzione PREDICT. Con sp\_rxPredict richiede l'abilitazione integrazione SQLCLR. Prima di abilitare questa opzione, prendere in considerazione le implicazioni di sicurezza.

## <a name="serialization-and-storage"></a>Serializzazione e archiviazione

Per usare un modello con una delle opzioni di assegnazione dei punteggi veloce, salvare il modello usando un formato serializzato speciale, cui è stato ottimizzato per le dimensioni e l'efficienza di assegnazione dei punteggi.

+ Chiamare [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) scrivere un modello supportato per il **raw** formato.
+ Chiamare [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' per ricostituire il modello per l'uso in un altro codice R o per visualizzare il modello.

**Con SQL**

Dal codice SQL, è possibile eseguire il training usando il modello [sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)e inserire direttamente i modelli addestrati in una tabella, in una colonna di tipo **varbinary (max)** . Per un esempio semplice, vedere [creare un modello preditive in R](../tutorials/rtsql-create-a-predictive-model-r.md)

**Uso di R**

Dal codice R, chiamare il [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) funzione dal pacchetto RevoScaleR a scrivere il modello direttamente nel database. Il **rxWriteObject()** funzione può recuperare gli oggetti R da un'origine dati ODBC, ad esempio SQL Server, o scrivere gli oggetti di SQL Server. L'API viene modellato un semplice archivio chiave-valore.
  
Se si usa questa funzione, assicurarsi di serializzare il modello usando [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) prima. Quindi, impostare il *serializzare* nell'argomento **rxWriteObject** su FALSE, per evitare di ripetere il passaggio di serializzazione.

La serializzazione di un modello in un formato binario è utile, ma non è necessario se si assegna un punteggio stime usando R e Python esegue ambiente nel framework di estendibilità. È possibile salvare un modello in formato byte non elaborati in un file e quindi leggere dal file in SQL Server. Questa opzione potrebbe essere utile se si sta spostando o copia di modelli tra ambienti.

## <a name="scoring-in-related-products"></a>Assegnazione dei punteggi in prodotti correlati

Se si usa la [server autonomi](r-server-standalone.md) o una [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), sono disponibili altre opzioni oltre a stored procedure e funzioni T-SQL per la generazione di stime rapidamente. Il server autonomo e il Machine Learning Server supportano il concetto di una *servizio web* per la distribuzione di codice. È possibile aggregare una R o Python eseguito il training del modello come servizio web, chiamato in fase di esecuzione per valutare nuovi input di dati. Per altre informazioni, vedere questi articoli:

+ [Quali sono i servizi web in Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [Che cos'è messa in funzione?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Distribuire un modello Python come un servizio web con Azure ml-model-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Pubblicare un blocco di codice R o un modello in tempo reale come nuovo servizio web](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [pacchetto mrsdeploy per R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>Vedere anche

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREVEDERE T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)