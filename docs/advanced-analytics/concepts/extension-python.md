---
title: SQL Server Machine Learning - estensione del linguaggio di programmazione Python
description: Informazioni sull'esecuzione del codice Python e predefiniti delle librerie di Python in Machine Learning Services di SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c0284577d8e30871b354607cf9af978e6d53df63
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512218"
---
# <a name="python-language-extension-in-sql-server"></a>Estensione del linguaggio Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

L'estensione Python fa parte del componente aggiuntivo SQL Server Machine Learning Services al motore di database relazionale. Aggiunge un ambiente di esecuzione di Python, la distribuzione Anaconda con il runtime di Python 3.5 e dell'interprete, le librerie standard e gli strumenti e le librerie di prodotto Microsoft per Python: [revoscalepy](../python/ref-py-revoscalepy.md) per analitica in scala e a [microsoftml](../python/ref-py-microsoftml.md) per machine learning algoritmi. 

Integrazione di Python viene installato come [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

Installazione del runtime di Python 3.5 e dell'interprete assicura la compatibilità pressoché completa con le soluzioni di Python standard. Python viene eseguito in un processo separato da SQL Server, per garantire che le operazioni di database non vengano compromesse.

## <a name="python-components"></a>Componenti Python

SQL Server include pacchetti open source e proprietari. Il runtime di Python installato dal programma di installazione è 4.2 Anaconda con Python 3.5. Il runtime di Python viene installato indipendentemente da strumenti di SQL e viene eseguito all'esterno di processi del motore di base, nel framework di estendibilità. Come parte dell'installazione di servizi di Machine Learning con Python, è necessario accettare le condizioni della licenza GNU Public License. 

SQL Server non modifica gli eseguibili di Python, ma è necessario usare la versione di Python installata dal programma di installazione perché tale versione è quello che i pacchetti proprietari vengano compilati e testati in. Per un elenco dei pacchetti supportati per la distribuzione Anaconda, visitare il sito di analitica Continuum: [Elenco dei pacchetti anaconda](https://docs.continuum.io/anaconda/packages/pkg-docs).

La distribuzione Anaconda associata a un'istanza del motore di database specifico è reperibile nella cartella associata all'istanza. Ad esempio, se è installato il motore di database di SQL Server 2017 con Python e Machine Learning Services sull'istanza predefinita, cercarlo in `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

I pacchetti Python aggiunti per carichi di lavoro paralleli e distribuiti da Microsoft includono le librerie seguenti.

| Libreria | Descrizione |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Supporta gli oggetti origine dati ed esplorazione dei dati, manipolazione, trasformazione e la visualizzazione. Supporta la creazione di contesti di calcolo remoti, nonché un vari modelli scalabili di machine learning, ad esempio **rxLinMod**. Per altre informazioni, vedere [revoscalepy modulo con SQL Server](../python/ref-py-revoscalepy.md).  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Contiene algoritmi di machine learning che sono stati ottimizzati per la velocità e la precisione, nonché le trasformazioni per l'utilizzo di testo e immagini in linea. Per altre informazioni, vedere [modulo di microsoftml con SQL Server](../python/ref-py-microsoftml.md). |

Microsoftml e revoscalepy sono strettamente collegati; origini dati utilizzate nel microsoftml sono definite come oggetti revoscalepy. Limiti del contesto di trasferimento revoscalepy microsoftml di calcolo. Vale a dire, tutte le funzionalità sono disponibile per operazioni locali, ma il passaggio a un contesto di calcolo remoto richiede RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Uso di Python in SQL Server

Importare il **revoscalepy** modulo nel codice Python e quindi chiamano funzioni del modulo, come qualsiasi altra funzione di Python.

Origini dati supportate includono database ODBC, SQL Server e il formato di file XDF per lo scambio di dati con altre origini, o con soluzioni R. I dati di input per Python devono essere in formato tabulare. Tutti i risultati di Python devono essere restituiti sotto forma di una **pandas** frame di dati.

Contesti di calcolo supportati includono contesto di calcolo di SQL Server locale o remoto. Un contesto di calcolo remoto si riferisce all'esecuzione di codice che avvia in un computer, ad esempio una workstation, ma, commutatori lo script di esecuzione a un computer remoto. Passare il contesto di calcolo, è necessario che entrambi i sistemi abbiano la stessa libreria revoscalepy.

Contesto di calcolo locale, come è prevedibile, include l'esecuzione del codice Python nello stesso server come istanza del motore di database, con il codice all'interno di T-SQL o incorporato in una stored procedure. È possibile anche eseguire il codice da un ambiente IDE Python locale e lo script di esecuzione nel computer SQL Server, contesto di calcolo con la definizione di un server remoto.

## <a name="execution-architecture"></a>Architettura di esecuzione

Il diagramma seguente è illustrato l'interazione dei componenti di SQL Server con il runtime di Python in ognuno degli scenari supportati: in esecuzione l'esecuzione di script nel database e remoto da un terminale di Python, utilizzando un contesto di calcolo di SQL Server.

### <a name="python-scripts-executed-in-database"></a>Gli script Python eseguito nel database

Quando si esegue Python "all'interno di" SQL Server, lo script di Python all'interno di una stored procedure speciale, è necessario incapsulare [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Dopo che lo script è stato incorporato nella stored procedure, qualsiasi applicazione in grado di eseguire una stored procedure chiamata può avviare l'esecuzione del codice Python.  Successivamente, SQL Server gestisce l'esecuzione di codice come riepilogato nel diagramma seguente.

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Una richiesta per il runtime di Python è indicata dal parametro `@language='Python'` passato alla stored procedure. SQL Server invia la richiesta al servizio Launchpad.
2. Il servizio Launchpad avvia l'utilità di avvio appropriata; In questo caso, PythonLauncher.
3. PythonLauncher avvia il processo Python35 esterno.
4. BxlServer interagisce con il runtime di Python per gestire gli scambi di dati e archiviazione dei risultati.
5. SQL Satellite gestisce le comunicazioni sulle attività correlate e i processi con SQL Server.
6. BxlServer Usa SQL Satellite per comunicare lo stato e i risultati a SQL Server.
7. SQL Server Ottiene i risultati e chiude i processi e attività correlate.

### <a name="python-scripts-executed-from-a-remote-client"></a>Script Python eseguiti da un client remoto

È possibile eseguire gli script di Python da un computer remoto, ad esempio un computer portatile e li vengono eseguite nel contesto del computer SQl Server, se vengono soddisfatte queste condizioni:

+ Progettare in modo appropriato gli script
+ Nel computer remoto sia installato le librerie di estendibilità usati da servizi di Machine Learning. Il [revoscalepy](../python/ref-py-revoscalepy.md) pacchetto è necessario usare contesti di calcolo remoti.

Il diagramma seguente riepiloga il flusso di lavoro globale quando gli script vengono inviati da un computer remoto.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. Per le funzioni che sono supportate in **revoscalepy**, il runtime di Python chiama una funzione di collegamento, che a sua volta chiama BxlServer.
2. BxlServer è incluso in Machine Learning Services (In-Database) e viene eseguito in un processo separato dal runtime di Python.
3. BxlServer determina la destinazione della connessione e avvia una connessione tramite ODBC, passando le credenziali fornite come parte della stringa di connessione nello script Python.
4. BxlServer apre una connessione all'istanza di SQL Server.
5. Quando viene chiamato un tempo di esecuzione dello script esterno, viene richiamato il servizio Launchpad, che a sua volta avvia l'utilità di avvio appropriata: in questo caso, PythonLauncher.dll. Successivamente, l'elaborazione del codice Python viene gestita in un flusso di lavoro simile a quella quando codice Python viene richiamato da una stored procedure in T-SQL.
6. PythonLauncher effettua una chiamata all'istanza di Python installata nel computer SQL Server.
7. I risultati vengono restituiti a BxlServer.
8. SQL Satellite gestisce la comunicazione con SQL Server e la pulizia degli oggetti processo correlati.
9. SQL Server passa i risultati al client.

## <a name="see-also"></a>Vedere anche

+ [modulo revoscalepy in SQL Server](../python/ref-py-revoscalepy.md)
+ [riferimento a una funzione revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [Framework di estendibilità in SQL Server](extensibility-framework.md)
+ [R e machine learning le estensioni in SQL Server](extension-r.md)