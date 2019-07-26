---
title: Generare previsioni e stime usando modelli di apprendimento automatico
description: Usare rxPredict o sp_rxPredict per il punteggio in tempo reale oppure prevedere T-SQL per il Punteggio nativo per le stime e la previsione in R e in Pythin in SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 39edb40da1ebbddfff805aca321b99ea766f085c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470120"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>Come generare previsioni e stime usando modelli di Machine Learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

L'uso di un modello esistente per prevedere o stimare i risultati per i nuovi input di dati è un'attività fondamentale in Machine Learning. Questo articolo enumera gli approcci per la generazione di stime in SQL Server. Tra gli approcci sono disponibili metodologie di elaborazione interne per le stime ad alta velocità, in cui la velocità è basata sulle riduzioni incrementali delle dipendenze in fase di esecuzione. Meno dipendenze significano stime più veloci.

L'uso dell'infrastruttura di elaborazione interna (Punteggio in tempo reale o nativo) viene fornita con i requisiti della libreria. Le funzioni devono provenire da Microsoft Libraries. Il codice R o Python che chiama funzioni open source o di terze parti non è supportato in C++ CLR o nelle estensioni.

Nella tabella seguente sono riepilogati i Framework di assegnazione dei punteggi per la previsione e le stime. 

| Metodologia           | Interfaccia         | Requisiti della libreria | Velocità di elaborazione |
|-----------------------|-------------------|----------------------|----------------------|
| Framework di estendibilità | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | No. I modelli possono essere basati su qualsiasi funzione R o Python | Centinaia di millisecondi. <br/>Il caricamento di un ambiente di runtime comporta un costo fisso, con una media di tre a 600 millisecondi, prima di assegnare un punteggio ai nuovi dati. |
| [Estensione CLR di assegnazione dei punteggi in tempo reale](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) su un modello serializzato | R RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | In media, decine di millisecondi. |
| [Estensione per C++ il Punteggio nativo](../sql-native-scoring.md) | [Stimare la funzione T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) su un modello serializzato | R RevoScaleR <br/>Python: revoscalepy | Meno di 20 millisecondi, in media. | 

La velocità di elaborazione e non la sostanza dell'output è la funzionalità di differenziazione. Presumendo gli stessi input e funzioni, l'output con punteggio non dovrebbe variare a seconda dell'approccio usato.

Il modello deve essere creato utilizzando una funzione supportata, quindi serializzato in un flusso di byte non elaborati salvato su disco o archiviato in formato binario in un database. Usando un stored procedure o T-SQL, è possibile caricare e usare un modello binario senza l'overhead di un runtime del linguaggio R o Python, causando un tempo di completamento più rapido durante la generazione di punteggi di stima sui nuovi input.

Il significato di CLR ed C++ Extensions è la prossimità del motore di database stesso. La lingua nativa del motore di database è C++, il che significa che le C++ estensioni scritte in vengono eseguite con un minor numero di dipendenze. Al contrario, le estensioni CLR dipendono da .NET Core. 

Come ci si può aspettare, il supporto per la piattaforma è influenzato da questi ambienti di run-time. Le estensioni del motore di database native vengono eseguite ovunque sia supportato il database relazionale: Windows, Linux, Azure. Le estensioni CLR con il requisito di .NET Core sono attualmente solo Windows.

## <a name="scoring-overview"></a>Panoramica dei punteggi

Il _Punteggio_ è un processo in due passaggi. Per prima cosa, è necessario specificare un modello già sottoposto a training da caricare da una tabella. In secondo luogo, passare i nuovi dati di input alla funzione per generare valori di stima (o _punteggi_). L'input è spesso una query T-SQL, restituendo righe tabulari o singole. È possibile scegliere di restituire un valore di colonna singola che rappresenta una probabilità oppure è possibile che vengano restituiti diversi valori, ad esempio un intervallo di confidenza, un errore o un altro complemento utile alla stima.

Eseguendo un ulteriore passaggio, il processo complessivo di preparazione del modello e di generazione dei punteggi può essere riepilogato in questo modo:

1. Creare un modello usando un algoritmo supportato. Il supporto varia in base alla metodologia di assegnazione dei punteggi scelta.
2. Eseguire il training del modello.
3. Serializzare il modello utilizzando un formato binario speciale.
3. Salvare il modello in SQL Server. Ciò significa in genere archiviare il modello serializzato in una tabella SQL Server.
4. Chiamare la funzione o stored procedure, specificando gli input del modello e dei dati come parametri.

Quando l'input include molte righe di dati, in genere è più veloce inserire i valori di stima in una tabella come parte del processo di assegnazione dei punteggi. La generazione di un singolo punteggio è più tipica in uno scenario in cui si ottengono valori di input da un form o una richiesta utente e si restituisce il punteggio a un'applicazione client. Per migliorare le prestazioni durante la generazione di punteggi successivi, SQL Server possibile memorizzare nella cache il modello in modo che possa essere ricaricato in memoria.

## <a name="compare-methods"></a>Metodi di confronto

Per mantenere l'integrità dei processi del motore di database di base, il supporto per R e Python è abilitato in un'architettura doppia che isola l'elaborazione del linguaggio dall'elaborazione RDBMS. A partire da SQL Server 2016, Microsoft ha aggiunto un Framework di estendibilità che consente l'esecuzione di script R da T-SQL. In SQL Server 2017 è stata aggiunta l'integrazione con Python. 

Il Framework di estendibilità supporta qualsiasi operazione che può essere eseguita in R o Python, da semplici funzioni a training di modelli di apprendimento automatico complessi. Tuttavia, l'architettura a doppio processo richiede il richiamo di un processo R o Python esterno per ogni chiamata, indipendentemente dalla complessità dell'operazione. Quando il carico di lavoro comporta il caricamento di un modello con training preliminare da una tabella e l'assegnazione dei punteggi ai dati già presenti in SQL Server, l'overhead associato alla chiamata dei processi esterni aggiunge latenza che può essere inaccettabile in determinate circostanze. Il rilevamento delle frodi, ad esempio, richiede un punteggio rapido per essere pertinente.

Per aumentare le velocità di assegnazione dei punteggi per scenari come il rilevamento delle frodi, SQL Server aggiunte C++ librerie di Punteggio predefinite come e le estensioni CLR che eliminano il sovraccarico dei processi di avvio di R e Python.

Il [**punteggio in tempo reale**](../real-time-scoring.md) è stato la prima soluzione per il punteggio a prestazioni elevate. Introdotta nelle prime versioni di SQL Server 2017 e negli aggiornamenti successivi a SQL Server 2016, il punteggio in tempo reale si basa sulle librerie CLR che si trovano per l'elaborazione R e Python sulle funzioni controllate da Microsoft in RevoScaleR, MicrosoftML (R), revoscalepy e microsoftml (Python). Le librerie CLR vengono richiamate usando il stored procedure **sp_rxPredict** per generare i punteggi da qualsiasi tipo di modello supportato, senza chiamare il runtime di R o Python.

Il [**Punteggio nativo**](../sql-native-scoring.md) è una funzionalità di SQL Server 2017, implementata C++ come libreria nativa, ma solo per i modelli RevoScaleR e revoscalepy. Si tratta dell'approccio più veloce e più sicuro, ma supporta un set ridotto di funzioni rispetto ad altre metodologie.

## <a name="choose-a-scoring-method"></a>Scegliere un metodo di assegnazione dei punteggi

I requisiti della piattaforma spesso stabiliscono la metodologia di assegnazione dei punteggi da usare.

| Versione e piattaforma del prodotto | Metodologia |
|------------------------------|-------------|
| SQL Server 2017 in Windows, SQL Server 2017 Linux e database SQL di Azure | Assegnazione dei **punteggi nativi** con T-SQL Predict |
| SQL Server 2017 (solo Windows), SQL Server 2016 R Services a SP1 o versione successiva | Assegnazione di **punteggi in tempo reale** con SP\_rxPredict stored procedure |

È consigliabile assegnare punteggi nativi con la funzione PREDICT. Per usare\_SP rxPredict è necessario abilitare l'integrazione di SQLCLR. Prendere in considerazione le implicazioni di sicurezza prima di abilitare questa opzione.

## <a name="serialization-and-storage"></a>Serializzazione e archiviazione

Per utilizzare un modello con una delle opzioni di Punteggio rapido, salvare il modello utilizzando un formato speciale serializzato, ottimizzato per le dimensioni e l'efficienza dei punteggi.

+ Chiamare [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) per scrivere un modello supportato nel formato non **elaborato** .
+ Chiamare [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' per ricostituire il modello per l'uso in un altro codice R o per visualizzare il modello.

**Uso di SQL**

Dal codice SQL è possibile eseguire il training del modello usando [sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)e inserire direttamente i modelli sottoposti a training in una tabella, in una colonna di tipo **varbinary (max)** . Per un esempio semplice, vedere [creare un modello Preditive in R](../tutorials/rtsql-create-a-predictive-model-r.md)

**Uso di R**

Dal codice R, chiamare la funzione [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) dal pacchetto RevoScaleR per scrivere il modello direttamente nel database. La funzione **rxWriteObject ()** può recuperare oggetti R da un'origine dati ODBC, ad esempio SQL Server, oppure scrivere oggetti in SQL Server. L'API viene modellata dopo un semplice archivio chiave-valore.
  
Se si utilizza questa funzione, assicurarsi di serializzare il modello utilizzando prima [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) . Impostare quindi l'argomento *Serialize* in **rxWriteObject** su false per evitare di ripetere il passaggio di serializzazione.

La serializzazione di un modello in un formato binario è utile, ma non è necessaria se si assegna un punteggio alle stime usando R e l'ambiente di runtime Python in Extensibility Framework. È possibile salvare un modello in formato byte non elaborato in un file e quindi leggere dal file in SQL Server. Questa opzione può essere utile se si stanno muovendo o copiando modelli tra ambienti.

## <a name="scoring-in-related-products"></a>Assegnazione dei punteggi nei prodotti correlati

Se si utilizza il [server autonomo](r-server-standalone.md) o un [Microsoft Machine Learning server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), sono disponibili altre opzioni oltre alle stored procedure e alle funzioni T-SQL per la generazione rapida delle stime. Sia il server autonomo che Machine Learning Server supportano il concetto di *servizio Web* per la distribuzione del codice. È possibile aggregare un modello con training preliminare R o Python come servizio Web, chiamato in fase di esecuzione per valutare i nuovi input di dati. Per altre informazioni, vedere questi articoli:

+ [Che cosa sono i servizi Web in Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [Che cos'è la operatività?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Distribuire un modello Python come servizio Web con azureml-Model-Management-SDK](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Pubblicare un blocco di codice R o un modello in tempo reale come nuovo servizio Web](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [pacchetto mrsdeploy per R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>Vedere anche

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)