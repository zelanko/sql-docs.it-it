---
title: Estensione per il linguaggio R
description: Informazioni sull'estensione R per l'esecuzione di script R esterni con Machine Learning Services per SQL Server e R Services per SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e51e4121a7e941512a84e3acf577af0ff687f4d7
ms.sourcegitcommit: d1535944bff3f2580070cc036ece30f1d43ee2ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2020
ms.locfileid: "86406274"
---
# <a name="r-language-extension-in-sql-server-machine-learning-services"></a>Estensione del linguaggio R in Machine Learning Services per SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Questo articolo descrive l'estensione R per l'esecuzione di script Python esterni con [Machine Learning Services per SQL Server](../sql-server-machine-learning-services.md) e [R Services per SQL Server 2016](../r/sql-server-r-services.md). L'estensione aggiunge:

- Ambiente di esecuzione R
- Distribuzione R di base con librerie e strumenti standard
- Librerie R Microsoft:
  - [RevoScaleR](../r/ref-r-revoscaler.md) per l'analisi su larga scala
  - [MicrosoftML](../r/ref-r-microsoftml.md) per gli algoritmi di Machine Learning
  - Altre librerie per l'accesso ai dati o al codice R in SQL Server

## <a name="r-components"></a>Componenti R

SQL Server include pacchetti sia open source che proprietari. Le librerie R di base vengono installate tramite la distribuzione Microsoft di R open source: Microsoft R Open (MRO). Gli utenti correnti di R dovrebbero riuscire a trasferire il codice R ed eseguirlo come processo esterno su SQL Server con un numero limitato di modifiche o addirittura nessuna modifica. La distribuzione MRO viene installata indipendentemente dagli strumenti SQL e viene eseguita all'esterno dei processi del motore di base, nel framework di estendibilità. Durante l'installazione è necessario accettare le condizioni della licenza open source. Successivamente, è possibile eseguire i pacchetti R standard senza ulteriori modifiche, esattamente come per qualsiasi altra distribuzione open source di R. 

SQL Server non modifica i file eseguibili R di base, ma è necessario usare la versione di R installata dal programma di installazione perché è quella su cui vengono compilati e testati i pacchetti proprietari. Per altre informazioni sulle differenze tra MRO e una distribuzione di base di R che è possibile ottenere da CRAN, vedere [Interoperabilità con il linguaggio R e con i prodotti e le funzionalità Microsoft R](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

La distribuzione di base dei pacchetti R installata dal programma di installazione è disponibile nella cartella associata all'istanza. Se, ad esempio, è stato installato R Services in un'istanza predefinita di SQL Server, le librerie di R si trovano per impostazione predefinita in questa cartella: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`. Analogamente, gli strumenti per R associati all'istanza predefinita si troverebbero per impostazione predefinita in questa cartella: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`.

I pacchetti R aggiunti da Microsoft per i carichi di lavoro paralleli e distribuiti includono le librerie elencate di seguito.

| Libreria | Descrizione |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | Supporta gli oggetti origine dati e anche l'esplorazione, la manipolazione, la trasformazione e la visualizzazione dei dati. Supporta inoltre la creazione di contesti di calcolo remoti e diversi modelli di Machine Learning scalabili, ad esempio **rxLinMod**. Le API sono state ottimizzate per l'analisi dei set di dati troppo grandi per essere contenuti in memoria e per l'esecuzione di calcoli distribuiti su più core o processori. Il pacchetto RevoScaleR supporta anche il formato di file XDF per una maggiore rapidità di spostamento e archiviazione dei dati usati per l'analisi. Il formato XDF usa l'archiviazione a colonne, è portabile e può essere usato per caricare e quindi manipolare i dati da diverse origini, tra cui testo, SPSS o una connessione ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contiene gli algoritmi di Machine Learning ottimizzati per la velocità e l'accuratezza, nonché le trasformazioni inline per l'utilizzo di testo e immagini. Per altre informazioni, vedere [MicrosoftML in SQL Server](../r/ref-r-microsoftml.md). | 

## <a name="using-r-in-sql-server"></a>Uso di R in SQL Server

È possibile creare uno script R usando le funzioni di base, ma per trarre vantaggio dalla multielaborazione è necessario importare i moduli **RevoScaleR** e **MicrosoftML** nel codice R e quindi chiamare le relative funzioni per creare modelli da eseguire in parallelo. 
 
Le origini dati supportate includono i database ODBC, SQL Server e il formato di file XDF per lo scambio di dati con altre origini o con soluzioni R. I dati di input devono essere in formato tabulare. Tutti i risultati di R devono essere restituiti sotto forma di dataframe.

I contesti di calcolo supportati includono il contesto di calcolo di SQL Server, locale o remoto. Un contesto di calcolo remoto fa riferimento all'esecuzione del codice avviata in un computer, ad esempio una workstation, per poi passare l'esecuzione dello script a un computer remoto. Per cambiare il contesto di calcolo è necessario che entrambi i sistemi abbiano la stessa libreria RevoScaleR.

Il contesto di calcolo locale, come si può prevedere, include l'esecuzione del codice R sullo stesso server dell'istanza del motore di database, con il codice all'interno di T-SQL o incorporato in una stored procedure. È anche possibile eseguire il codice da un IDE di R locale e far eseguire lo script nel computer SQL Server, definendo un contesto di calcolo remoto.

## <a name="execution-architecture"></a>Architettura di esecuzione

I diagrammi seguenti illustrano l'interazione dei componenti di SQL Server con il runtime R in ognuno degli scenari supportati: esecuzione di script nel database ed esecuzione remota da una riga di comando R, usando un contesto di calcolo di SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Script R eseguiti da SQL Server (In-Database)

Dall'interno di SQL Server, il codice R viene eseguito chiamando una stored procedure. Qualsiasi applicazione in grado di eseguire una chiamata a una stored procedure può quindi avviare l'esecuzione del codice R.  Successivamente, SQL Server gestisce l'esecuzione del codice R, come riepilogato nel diagramma seguente.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Una richiesta per il runtime R è indicata dal parametro _@language='R'_ passato alla stored procedure, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). SQL Server invia la richiesta al servizio launchpad.
In Linux, SQL usa un servizio **launchpadd** per comunicare con un processo launchpad separato per ogni utente. Per informazioni dettagliate, vedere il [diagramma dell'architettura di estendibilità](extensibility-framework.md#architecture-diagram).
2. Il servizio launchpad avvia l'utilità di avvio appropriata, in questo caso RLauncher.
3. RLauncher avvia il processo R esterno.
4. BxlServer si coordina con il runtime R per gestire gli scambi di dati con SQL Server e l'archiviazione dei risultati.
5. SQL Satellite gestisce le comunicazioni relative ad attività e processi correlati con SQL Server.
6. BxlServer usa SQL Satellite per comunicare lo stato e i risultati a SQL Server.
7. SQL Server ottiene i risultati e chiude le attività e i processi correlati.

### <a name="r-scripts-executed-from-a-remote-client"></a>Script R eseguiti da un client remoto

Quando viene stabilita la connessione da un client di data science remoto che supporta Microsoft R, è possibile eseguire le funzioni R nel contesto di SQL Server usando le funzioni RevoScaleR. Si tratta di un flusso di lavoro diverso dal precedente, riepilogato nel diagramma seguente.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. Per le funzioni RevoScaleR, il runtime R chiama una funzione di collegamento che a sua volta chiama BxlServer.
2. BxlServer viene fornito con Microsoft R ed eseguito in un processo separato dal runtime R.
3. BxlServer determina la destinazione della connessione e avvia una connessione tramite ODBC, passando le credenziali fornite come parte della stringa di connessione nell'oggetto origine dati R.
4. BxlServer apre una connessione all'istanza di SQL Server.
5. Per una chiamata a R, viene richiamato il servizio launchpad, che a sua volta avvia l'utilità di avvio appropriata, in questo caso RLauncher. Da questo momento, l'elaborazione del codice R è simile al processo per l'esecuzione di codice R da T-SQL.
6. RLauncher effettua una chiamata all'istanza del runtime R installata nel computer SQL Server.
7. I risultati vengono restituiti a BxlServer.
8. SQL Satellite gestisce le comunicazioni con SQL Server e la pulizia degli oggetti processo correlati.
9. SQL Server passa i risultati al client.

## <a name="see-also"></a>Vedere anche

+ [Framework di estendibilità in SQL Server](extensibility-framework.md)
+ [Estensioni di Python e Machine Learning in SQL Server](extension-python.md)