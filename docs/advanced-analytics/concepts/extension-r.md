---
title: SQL Server Machine Learning - estensione del linguaggio di programmazione R
description: Informazioni sull'esecuzione del codice R e librerie di R incorporate in SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cb9b710ca5ec06e05a93dbee5f22ee0860f7f4ca
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432764"
---
# <a name="r-language-extension-in-sql-server"></a>Estensione del linguaggio R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

L'estensione di R è parte del componente aggiuntivo SQL Server Machine Learning Services al motore di database relazionale. Aggiunge un ambiente di esecuzione di R, una distribuzione base di R con strumenti e librerie standard e le librerie di Microsoft R: [RevoScaleR](../r/ref-r-revoscaler.md) per su larga scala, analitica [MicrosoftML](../r/ref-r-microsoftml.md) per algoritmi di machine learning e altre librerie per l'accesso ai dati o del codice R in SQL Server.

Integrazione di R è disponibile in SQL Server in SQL Server 2016, a partire [R Services](../r/sql-server-r-services.md)e continuare come parte del rollforward [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

## <a name="r-components"></a>Componenti R

SQL Server include pacchetti open source e proprietari. Le librerie R di base vengono installate tramite distribuzione Microsoft di r open source: Microsoft R Open (MRO). Gli utenti correnti di R devono essere in grado di trasferire il proprio codice R ed eseguirlo come un processo esterno in SQL Server con le modifiche pochissime o addirittura nessuna. MRO è installata indipendentemente da strumenti di SQL e viene eseguito all'esterno di processi del motore di base, nel framework di estendibilità. Durante l'installazione, è necessario accettare le condizioni di licenza open source. Successivamente, è possibile eseguire pacchetti R standard senza ulteriori modifiche esattamente come farebbe in qualsiasi altra distribuzione open source di R. 

SQL Server non modifica i file eseguibili R di base, ma è necessario usare la versione di R installato dal programma di installazione perché tale versione è quello che i pacchetti proprietari vengano compilati e testati in. Per altre informazioni sulle differenze MRO tra una distribuzione di base di R che si potrebbero ottenere da CRAN, vedere [interoperabilità con linguaggio R e i prodotti Microsoft R e funzionalità](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

La distribuzione di base dei pacchetti R installata dal programma di installazione è reperibile nella cartella associata all'istanza. Ad esempio, se è installato R Services in un'istanza predefinita di SQL Server 2016, le librerie R si trovano in questa cartella per impostazione predefinita: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`. Analogamente, gli strumenti R associati all'istanza predefinita sono posizionati in questa cartella per impostazione predefinita: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`.

I pacchetti R aggiunti per carichi di lavoro paralleli e distribuiti da Microsoft includono le librerie seguenti.

| Libreria | Descrizione |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | Supporta gli oggetti origine dati ed esplorazione dei dati, manipolazione, trasformazione e la visualizzazione. Supporta la creazione di contesti di calcolo remoti, nonché un vari modelli scalabili di machine learning, ad esempio **rxLinMod**. Le API sono state ottimizzate per l'analisi dei set di dati troppo grandi per essere contenuti in memoria e per l'esecuzione di calcoli distribuiti su più core o processori. Il pacchetto RevoScaleR supporta anche il formato di file XDF per più rapido dello spostamento e l'archiviazione dei dati utilizzati per l'analisi. Il formato XDF usa l'archiviazione a colonne, è portabile e può essere usato per caricare e quindi manipolare i dati da diverse origini, tra cui testo, SPSS o una connessione ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contiene algoritmi di machine learning che sono stati ottimizzati per la velocità e la precisione, nonché le trasformazioni per l'utilizzo di testo e immagini in linea. Per altre informazioni, vedere [MicrosoftML in SQL Server](../r/ref-r-microsoftml.md). | 

## <a name="using-r-in-sql-server"></a>Uso di R in SQL Server

È possibile generare uno script R usando funzioni di base, ma per trarre vantaggio dall'elaborazione di più, è necessario importare il **RevoScaleR** e **MicrosoftML** moduli nel codice R e quindi chiamare le funzioni per creare i modelli che eseguire in parallelo. 
 
Origini dati supportate includono database ODBC, SQL Server e il formato di file XDF per lo scambio di dati con altre origini, o con soluzioni R. I dati di input devono essere in formato tabulare. Tutti i risultati di R devono essere restituiti in forma di un frame di dati.

Contesti di calcolo supportati includono contesto di calcolo di SQL Server locale o remoto. Un contesto di calcolo remoto si riferisce all'esecuzione di codice che avvia in un computer, ad esempio una workstation, ma, commutatori lo script di esecuzione a un computer remoto. Passare il contesto di calcolo, è necessario che entrambi i sistemi abbiano la stessa libreria RevoScaleR.

Contesto di calcolo locale, come è prevedibile, include l'esecuzione del codice R nello stesso server come istanza del motore di database, con il codice all'interno di T-SQL o incorporato in una stored procedure. È possibile anche eseguire il codice da un IDE R locale e lo script di esecuzione nel computer SQL Server, contesto di calcolo con la definizione di un server remoto.

## <a name="execution-architecture"></a>Architettura di esecuzione

Il diagramma seguente è illustrato l'interazione dei componenti di SQL Server con il runtime R in ognuno degli scenari supportati: in esecuzione l'esecuzione di script nel database e remoto da una riga di comando di R, usando un contesto di calcolo di SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Script R eseguiti da SQL Server nel database

Codice R eseguito da "inside" SQL Server viene eseguito chiamando una stored procedure. Qualsiasi applicazione in grado di eseguire una chiamata a una stored procedure può quindi avviare l'esecuzione del codice R.  Successivamente, SQL Server gestisce l'esecuzione del codice R, come riepilogato nel diagramma seguente.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Una richiesta per il runtime R è indicata dal parametro _@language='R'_ passato alla stored procedure, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). SQL Server invia la richiesta al servizio Launchpad.
2. Il servizio Launchpad avvia l'utilità di avvio appropriata, in questo caso, RLauncher.
3. RLauncher avvia il processo R esterno.
4. BxlServer interagisce con il runtime di R per gestire gli scambi di dati con SQL Server e archiviazione dei risultati.
5. SQL Satellite gestisce le comunicazioni sulle attività correlate e i processi con SQL Server.
6. BxlServer Usa SQL Satellite per comunicare lo stato e i risultati a SQL Server.
7. SQL Server Ottiene i risultati e chiude i processi e attività correlate.

### <a name="r-scripts-executed-from-a-remote-client"></a>Script R eseguiti da un client remoto

Quando ci si connette da un client di analisi scientifica dei dati remoti che supporta Microsoft R, è possibile eseguire funzioni R nel contesto di SQL Server usando le funzioni RevoScaleR. Si tratta di un flusso di lavoro diverso dal precedente, riepilogato nel diagramma seguente.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. Per le funzioni RevoScaleR, il runtime R chiama una funzione di collegamento che a sua volta chiama BxlServer.
2. BxlServer viene fornito con Microsoft R ed eseguito in un processo separato dal runtime R.
3. BxlServer determina la destinazione della connessione e avvia una connessione tramite ODBC, passando le credenziali fornite come parte della stringa di connessione nell'oggetto origine dati R.
4. BxlServer apre una connessione all'istanza di SQL Server.
5. Per una chiamata a R, la finestra di avvio di servizio viene richiamato, che a sua volta avvia l'utilità di avvio appropriata, RLauncher. Da questo momento, l'elaborazione del codice R è simile al processo per l'esecuzione di codice R da T-SQL.
6. RLauncher effettua una chiamata all'istanza del runtime R installato nel computer SQL Server.
7. I risultati vengono restituiti a BxlServer.
8. SQL Satellite gestisce la comunicazione con SQL Server e la pulizia degli oggetti processo correlati.
9. SQL Server passa i risultati al client.

## <a name="see-also"></a>Vedere anche

+ [Framework di estendibilità in SQL Server](extensibility-framework.md)
+ [Python e machine learning le estensioni in SQL Server](extension-python.md)