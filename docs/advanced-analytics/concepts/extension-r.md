---
title: Estensione del linguaggio di programmazione R
description: Informazioni sull'esecuzione di codice R e sulle librerie R predefinite in SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 300b5d25d62be24c1e5590f5cd9795d08da7f2c1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470493"
---
# <a name="r-language-extension-in-sql-server"></a>Estensione del linguaggio R in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

L'estensione R fa parte dell'SQL Server Machine Learning Services componente aggiuntivo per il motore di database relazionale. Aggiunge un ambiente di esecuzione R, una distribuzione R di base con librerie e strumenti standard e le librerie Microsoft R: [RevoScaleR](../r/ref-r-revoscaler.md) per l'analisi su larga scala, [MicrosoftML](../r/ref-r-microsoftml.md) per gli algoritmi di machine learning e altre librerie per accedere ai dati o al codice R in SQL Server.

L'integrazione di r è disponibile in SQL Server a partire da SQL Server 2016, con [R Services](../r/sql-server-r-services.md)e continuando come parte di [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

## <a name="r-components"></a>Componenti R

SQL Server include i pacchetti open source e proprietari. Le librerie R di base vengono installate tramite la distribuzione di Microsoft Open Source R: Microsoft R Open (riparazione). Gli utenti correnti di R devono essere in grado di trasferire il codice R ed eseguirlo come processo esterno su SQL Server con poche o nessuna modifica. Il processo di riparazione viene installato indipendentemente dagli strumenti SQL e viene eseguito all'esterno dei processi del motore di base in Extensibility Framework. Durante l'installazione è necessario accettare le condizioni della licenza open source. Successivamente, è possibile eseguire pacchetti R standard senza ulteriori modifiche come per qualsiasi altra distribuzione open source di R. 

SQL Server non modifica i file eseguibili R di base, ma è necessario usare la versione di R installata dal programma di installazione di, perché tale versione è quella in cui vengono compilati e testati i pacchetti proprietari. Per altre informazioni sulle differenze tra la modalità di distribuzione di base di R e la distribuzione di R da CRAN, vedere interoperabilità [con il linguaggio r e prodotti e funzionalità Microsoft r](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

La distribuzione del pacchetto di base R installata dal programma di installazione di si trova nella cartella associata all'istanza. Ad esempio, se R Services è stato installato in un'istanza predefinita di SQL Server 2016, le librerie R si trovano in questa cartella per `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`impostazione predefinita:. Analogamente, gli strumenti R associati all'istanza predefinita si trovano in questa cartella per impostazione predefinita: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`.

I pacchetti R aggiunti da Microsoft per i carichi di lavoro paralleli e distribuiti includono le librerie seguenti.

| Libreria | Descrizione |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | Supporta oggetti origine dati e esplorazione, manipolazione, trasformazione e visualizzazione dei dati. Supporta la creazione di contesti di calcolo remoti, oltre a diversi modelli di apprendimento automatico scalabili, ad esempio **rxLinMod**. Le API sono state ottimizzate per l'analisi dei set di dati troppo grandi per essere contenuti in memoria e per l'esecuzione di calcoli distribuiti su più core o processori. Il pacchetto RevoScaleR supporta anche il formato di file XDF per lo spostamento e l'archiviazione più veloci dei dati usati per l'analisi. Il formato XDF usa l'archiviazione a colonne, è portabile e può essere usato per caricare e quindi manipolare i dati da diverse origini, tra cui testo, SPSS o una connessione ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contiene gli algoritmi di Machine Learning ottimizzati per la velocità e l'accuratezza, nonché le trasformazioni inline per l'utilizzo di testo e immagini. Per ulteriori informazioni, vedere [MicrosoftML in SQL Server](../r/ref-r-microsoftml.md). | 

## <a name="using-r-in-sql-server"></a>Uso di R in SQL Server

È possibile creare uno script di R usando le funzioni di base, ma per trarre vantaggio dalla multielaborazione è necessario importare i moduli **RevoScaleR** e **MicrosoftML** nel codice r e quindi chiamare le relative funzioni per creare modelli eseguiti in parallelo. 
 
Le origini dati supportate includono i database ODBC, SQL Server e il formato di file XDF per lo scambio di dati con altre origini o con soluzioni R. I dati di input devono essere tabulari. Tutti i risultati di R devono essere restituiti sotto forma di frame di dati.

I contesti di calcolo supportati includono il contesto di calcolo locale o remoto SQL Server. Un contesto di calcolo remoto si riferisce all'esecuzione del codice che viene avviata in un computer, ad esempio una workstation, ma quindi passa l'esecuzione dello script a un computer remoto. Per cambiare il contesto di calcolo è necessario che entrambi i sistemi abbiano la stessa libreria RevoScaleR.

Il contesto di calcolo locale, come ci si può aspettare, include l'esecuzione del codice R sullo stesso server dell'istanza del motore di database, con codice all'interno di T-SQL o incorporato in un stored procedure. È anche possibile eseguire il codice da un IDE R locale e far eseguire lo script nel computer SQL Server, definendo un contesto di calcolo remoto.

## <a name="execution-architecture"></a>Architettura di esecuzione

I diagrammi seguenti illustrano l'interazione dei componenti di SQL Server con il runtime di R in ognuno degli scenari supportati: esecuzione di script nel database ed esecuzione remota da una riga di comando di R, usando un contesto di calcolo SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Script R eseguiti da SQL Server nel database

Il codice R che viene eseguito dal SQL Server "interno" viene eseguito chiamando una stored procedure. Qualsiasi applicazione in grado di eseguire una chiamata a una stored procedure può quindi avviare l'esecuzione del codice R.  In seguito SQL Server gestisce l'esecuzione del codice R come riepilogato nel diagramma seguente.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Una richiesta per il runtime R è indicata dal parametro _@language='R'_ passato alla stored procedure, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). SQL Server invia la richiesta al servizio launchpad.
2. Il servizio Launchpad avvia l'utilità di avvio appropriata, in questo caso, RLauncher.
3. RLauncher avvia il processo R esterno.
4. BxlServer coordina con il runtime di R per gestire lo scambio di dati con SQL Server e l'archiviazione dei risultati di lavoro.
5. Il satellite SQL gestisce le comunicazioni sulle attività e i processi correlati con SQL Server.
6. BxlServer usa SQL satellite per comunicare lo stato e i risultati a SQL Server.
7. SQL Server Ottiene i risultati e chiude le attività e i processi correlati.

### <a name="r-scripts-executed-from-a-remote-client"></a>Script R eseguiti da un client remoto

Quando ci si connette da un client data science remoto che supporta Microsoft R, è possibile eseguire funzioni R nel contesto di SQL Server usando le funzioni RevoScaleR. Si tratta di un flusso di lavoro diverso dal precedente, riepilogato nel diagramma seguente.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. Per le funzioni RevoScaleR, il runtime di R chiama una funzione di collegamento che a sua volta chiama BxlServer.
2. BxlServer viene fornito con Microsoft R ed eseguito in un processo separato dal runtime R.
3. BxlServer determina la destinazione della connessione e avvia una connessione tramite ODBC, passando le credenziali fornite come parte della stringa di connessione nell'oggetto origine dati R.
4. BxlServer apre una connessione all'istanza di SQL Server.
5. Per una chiamata R, viene richiamato il servizio Launchpad, che a sua volta avvia l'avvio appropriato, RLauncher. Da questo momento, l'elaborazione del codice R è simile al processo per l'esecuzione di codice R da T-SQL.
6. RLauncher effettua una chiamata all'istanza del runtime R installata nel computer SQL Server.
7. I risultati vengono restituiti a BxlServer.
8. SQL satellite gestisce la comunicazione con SQL Server e la pulizia di oggetti processo correlati.
9. SQL Server passa nuovamente i risultati al client.

## <a name="see-also"></a>Vedere anche

+ [Framework di estendibilità in SQL Server](extensibility-framework.md)
+ [Estensioni di Python e Machine Learning in SQL Server](extension-python.md)