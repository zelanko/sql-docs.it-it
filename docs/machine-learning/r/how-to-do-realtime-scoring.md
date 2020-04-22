---
title: Generare previsioni e stime
description: Usare rxPredict o sp_rxPredict per l'assegnazione dei punteggi in tempo reale oppure PREDICT T-SQL per l'assegnazione dei punteggi nativa per eseguire stime e previsioni in R e Python in SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3f431d1598038d0789579697fccbaeffe5ef1fd0
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487840"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>Come generare previsioni e stime usando modelli di Machine Learning in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

L'uso di un modello esistente per prevedere o stimare i risultati per i nuovi input di dati è un'attività fondamentale nel Machine Learning. Questo articolo illustra gli approcci per la generazione di stime in SQL Server. Tra i vari approcci sono disponibili metodologie di elaborazione interne per stime ad alta velocità, in cui la velocità è basata sulla riduzione incrementale delle dipendenze in fase di esecuzione. Meno dipendenze vuol dire stime più veloci.

Per l'uso dell'infrastruttura di elaborazione interna (assegnazione dei punteggi in tempo reale o nativa) sono previsti requisiti in termini di librerie. Le funzioni devono provenire da librerie Microsoft. La chiamata di funzioni open source o di terze parti da parte del codice R o Python non è supportata nelle estensioni C++ o CLR.

Nella tabella seguente sono riepilogati i framework di assegnazione dei punteggi per la previsione e la stima. 

| Metodologia           | Interfaccia         | Requisiti di libreria | Velocità di elaborazione |
|-----------------------|-------------------|----------------------|----------------------|
| Framework di estendibilità | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | No. I modelli possono essere basati su qualsiasi funzione R o Python | Centinaia di millisecondi. <br/>Il caricamento di un ambiente di runtime ha un costo fisso, che va in media da 300 a 600 millisecondi, prima che vengano assegnati punteggi ai nuovi dati. |
| [Estensione CLR per punteggio in tempo reale](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) in un modello serializzato | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | In media, decine di millisecondi. |
| [Estensione C++ per assegnazione dei punteggi nativa](../sql-native-scoring.md) | [Funzione PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) in un modello serializzato | R: RevoScaleR <br/>Python: revoscalepy | In media, meno di 20 millisecondi. | 

La differenza sta nella velocità di elaborazione e non nella sostanza dell'output. Presumendo gli stessi input e funzioni, l'output con punteggio non dovrebbe variare a seconda dell'approccio usato.

Il modello deve essere creato usando una funzione supportata, quindi serializzato in un flusso di byte non elaborati salvato su disco o archiviato in formato binario in un database. Usando una stored procedure o T-SQL, è possibile caricare e usare un modello binario senza l'overhead di un runtime R o Python. Questo si traduce in tempi di completamento più rapidi quando si generano di punteggi di stima sui nuovi input.

La significatività delle estensioni CLR e C++ è la prossimità al motore di database stesso. Il linguaggio nativo del motore di database è C++, il che significa che le estensioni scritte in C++ vengono eseguite con un minor numero di dipendenze. Al contrario, le estensioni CLR dipendono da .NET Core. 

Come ci si può aspettare, il supporto della piattaforma è influenzato da questi ambienti di runtime. Le estensioni del motore di database native vengono eseguite ovunque sia supportato il database relazionale: Windows, Linux, Azure. Le estensioni CLR con il requisito .NET Core sono attualmente solo per Windows.

## <a name="scoring-overview"></a>Panoramica dell'assegnazione dei punteggi

Quello del _punteggio_ è un processo in due fasi. Per prima cosa, si specifica un modello già sottoposto a training da caricare da una tabella. In secondo luogo, si passano nuovi dati di input alla funzione, per generare valori stima (o _punteggi_). L'input è spesso una query T-SQL, che restituisce righe tabulari o singole. Si può scegliere di restituire come output un unico valore di colonna che rappresenta una probabilità oppure più valori, ad esempio un intervallo di confidenza, un errore o un altro complemento utile alla stima.

Il processo complessivo di preparazione del modello e di generazione dei punteggi può essere riepilogato in questo modo:

1. Creare un modello usando un algoritmo supportato. Il supporto varia in base alla metodologia di assegnazione dei punteggi scelta.
2. Eseguire il training del modello.
3. Serializzare il modello utilizzando un formato binario speciale.
3. Salvare il modello in SQL Server. In genere, questo significa archiviare il modello serializzato in una tabella di SQL Server.
4. Chiamare la funzione o la stored procedure, specificando il modello e gli input di dati come parametri.

Quando l'input include molte righe di dati, in genere è più veloce inserire i valori di stima in una tabella come parte del processo di assegnazione dei punteggi. La generazione di un unico punteggio è tipica in uno scenario in cui si ottengono valori di input da un modulo o una richiesta utente e si restituisce il punteggio a un'applicazione client. Per migliorare le prestazioni durante la generazione dei punteggi successivi, SQL Server potrebbe memorizzare nella cache il modello in modo che possa essere ricaricato in memoria.

## <a name="compare-methods"></a>Confronto dei metodi

Per preservare l'integrità dei processi del motore di database principale, il supporto per R e Python è abilitato in un'architettura doppia che isola l'elaborazione del linguaggio dall'elaborazione RDBMS. A partire da SQL Server 2016, Microsoft ha aggiunto un framework di estendibilità che consente l'esecuzione di script R da T-SQL. In SQL Server 2017 è stata aggiunta l'integrazione di Python. 

Il Framework di estendibilità supporta qualsiasi operazione che possa essere eseguita in R o Python, dalle funzioni più semplici al training di modelli di Machine Learning complessi. Tuttavia, l'architettura di elaborazione doppia prevede di richiamare un processo R o Python esterno per ogni chiamata, indipendentemente dalla complessità dell'operazione. Quando il carico di lavoro comporta il caricamento di un modello con training preliminare da una tabella e l'assegnazione dei punteggi sulla base di dati già presenti in SQL Server, l'overhead associato alla chiamata dei processi esterni aggiunge una latenza che in determinate circostanze può essere inaccettabile. Per il rilevamento delle frodi, ad esempio, l'assegnazione rapida dei punteggi è essenziale.

Per aumentare le velocità di assegnazione dei punteggi per scenari come il rilevamento delle frodi, in SQL Server sono state aggiunte librerie di punteggio predefinite come estensioni C++ e CLR, che eliminano il sovraccarico dei processi di avvio di R e Python.

L'[**assegnazione dei punteggi in tempo reale**](../real-time-scoring.md) è stata la prima soluzione per prestazioni elevate. Introdotta nelle prime versioni di SQL Server 2017 e negli aggiornamenti successivi a SQL Server 2016, l'assegnazione dei punteggi in tempo reale si basa sulle librerie CLR che sostituiscono l'elaborazione R e Python per le funzioni controllate da Microsoft in RevoScaleR, MicrosoftML (R), revoscalepy e Microsoftml (Python). Le librerie CLR vengono richiamate usando la stored procedure **sp_rxPredict** per generare punteggi da qualsiasi tipo di modello supportato, senza chiamare il runtime R o Python.

L'[**assegnazione dei punteggi nativa**](../sql-native-scoring.md) è una funzionalità di SQL Server 2017, implementata come libreria C++ nativa, ma solo per i modelli RevoScaleR e revoscalepy. Si tratta dell'approccio più veloce e più sicuro, ma supporta un set ridotto di funzioni rispetto ad altre metodologie.

## <a name="choose-a-scoring-method"></a>Scegliere un metodo di assegnazione dei punteggi

Spesso, la scelta della metodologia di assegnazione dei punteggi da usare è dettata dai requisiti della piattaforma.

| Versione del prodotto e piattaforma | Metodologia |
|------------------------------|-------------|
| SQL Server 2017 o versione successiva in Windows e Linux | **Assegnazione dei punteggi nativa** tramite T-SQL PREDICT |
| SQL Server 2017 (solo Windows), R Services per SQL Server 2016 SP1 o versione successiva | **Assegnazione dei punteggi in tempo reale** con la stored procedure SP\_rxPredict |

È consigliabile l'assegnazione dei punteggi nativa con la funzione PREDICT. Per l'uso di sp\_rxPredict è necessario abilitare l'integrazione di SQLCLR. Prima di abilitare questa opzione, valutare le implicazioni per la sicurezza.

## <a name="serialization-and-storage"></a>Serializzazione e archiviazione

Per usare un modello con una delle opzioni di assegnazione dei punteggi rapide, salvare il modello usando un formato serializzato speciale, ottimizzato per le dimensioni e per l'efficienza dell'assegnazione dei punteggi.

+ Chiamare [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) per scrivere un modello supportato nel formato **raw**.
+ Chiamare [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) per ricostituire il modello per l'uso in un altro codice R o per visualizzare il modello.

**Usando SQL**

Dal codice SQL è possibile eseguire il training del modello con [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) e inserire direttamente i modelli sottoposti a training in una tabella, in una colonna di tipo **varbinary (max)** . Per un esempio semplice, vedere [Creare un modello predittivo in R](../tutorials/quickstart-r-train-score-model.md)

**Usando R**

Dal codice R, chiamare la funzione [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) dal pacchetto RevoScaleR per scrivere il modello direttamente nel database. La funzione **rxWriteObject()** può recuperare oggetti R da un'origine dati ODBC, ad esempio SQL Server, oppure scrivere oggetti in SQL Server. L'API è modellata sulla base di un semplice archivio chiave-valore.
  
Se si utilizza questa funzione, assicurarsi di serializzare il modello usando prima [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel). Impostare quindi l'argomento *serialize* in **rxWriteObject** su FALSE, per evitare di ripetere il passaggio di serializzazione.

Serializzare un modello in un formato binario è utile, ma non è necessario se si stanno assegnando punteggi alle stime usando R e l'ambiente di runtime Python nel framework di estendibilità. È possibile salvare un modello in formato byte non elaborato in un file e quindi leggere dal file in SQL Server. Questa opzione può essere utile se si stanno spostando o copiando modelli tra ambienti.

## <a name="scoring-in-related-products"></a>Assegnazione dei punteggi nei prodotti correlati

Se si usa il [server autonomo](r-server-standalone.md) o [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), oltre alle stored procedure e alle funzioni T-SQL sono disponibili altre opzioni per la generazione rapida delle stime. Sia il server autonomo che Machine Learning Server supportano il concetto di *servizio Web* per la distribuzione del codice. È possibile distribuire un modello con training preliminare R o Python come servizio Web, chiamato in fase di esecuzione per valutare i nuovi input di dati. Per altre informazioni, vedere questi articoli:

+ [Cosa sono i servizi Web in Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [Cos'è l'operazionalizzazione?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Distribuire un modello Python come servizio Web con azureml-model-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Pubblicare un blocco di codice R o un modello in tempo reale come nuovo servizio Web](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [Pacchetto mrsdeploy per R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>Vedere anche

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)