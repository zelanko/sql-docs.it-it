---
title: Estensione del linguaggio di programmazione Python
description: Informazioni sull'esecuzione di codice Python e sulle librerie Python predefinite in SQL Server 2017 Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4e95fa47911b3942b44624a141a5c1c4c574b25a
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343382"
---
# <a name="python-language-extension-in-sql-server"></a>Estensione del linguaggio Python in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

L'estensione Python fa parte dell'SQL Server Machine Learning Services componente aggiuntivo per il motore di database relazionale. Aggiunge un ambiente di esecuzione Python, una distribuzione anaconda con il runtime e l'interprete Python 3,5, librerie e strumenti standard e le librerie di prodotti Microsoft per Python: [revoscalepy](../python/ref-py-revoscalepy.md) per l'analisi su larga scala e [microsoftml](../python/ref-py-microsoftml.md) per algoritmi di machine learning. 

L'integrazione di Python viene installata come [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

L'installazione del runtime e dell'interprete Python 3,5 garantisce la compatibilità quasi completa con le soluzioni Python standard. Python viene eseguito in un processo separato da SQL Server, per garantire che le operazioni di database non vengano compromesse.

## <a name="python-components"></a>Componenti Python

SQL Server include i pacchetti open source e proprietari. Il runtime di Python installato dal programma di installazione è Anaconda 4,2 con Python 3,5. Il runtime di Python viene installato indipendentemente dagli strumenti SQL e viene eseguito all'esterno dei processi del motore di base in Extensibility Framework. Nell'ambito dell'installazione di Machine Learning Services con Python, è necessario accettare i termini della licenza GNU Public. 

SQL Server non modifica i file eseguibili di Python, ma è necessario usare la versione di Python installata dal programma di installazione, perché tale versione è quella in cui vengono compilati e testati i pacchetti proprietari. Per un elenco dei pacchetti supportati dalla distribuzione anaconda, vedere il sito di analisi continua: [Elenco dei pacchetti Anaconda](https://docs.continuum.io/anaconda/packages/pkg-docs).

La distribuzione anaconda associata a un'istanza specifica del motore di database è reperibile nella cartella associata all'istanza. Se, ad esempio, è stato installato SQL Server motore di database 2017 con Machine Learning Services e Python nell'istanza predefinita, `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`cercare in.

I pacchetti Python aggiunti da Microsoft per i carichi di lavoro paralleli e distribuiti includono le librerie seguenti.

| Libreria | Descrizione |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Supporta oggetti origine dati e esplorazione, manipolazione, trasformazione e visualizzazione dei dati. Supporta la creazione di contesti di calcolo remoti, oltre a diversi modelli di apprendimento automatico scalabili, ad esempio **rxLinMod**. Per ulteriori informazioni, vedere il [modulo revoscalepy con SQL Server](../python/ref-py-revoscalepy.md).  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Contiene gli algoritmi di Machine Learning ottimizzati per la velocità e l'accuratezza, nonché le trasformazioni inline per l'utilizzo di testo e immagini. Per ulteriori informazioni, vedere il [modulo microsoftml con SQL Server](../python/ref-py-microsoftml.md). |

Microsoftml e revoscalepy sono strettamente collegati; le origini dati utilizzate in microsoftml sono definite come oggetti revoscalepy. Limitazioni del contesto di calcolo nel trasferimento di revoscalepy a microsoftml. In particolare, tutte le funzionalità sono disponibili per le operazioni locali, ma per passare a un contesto di calcolo remoto è necessario RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Uso di Python in SQL Server

Il modulo **revoscalepy** viene importato nel codice Python e quindi vengono chiamate funzioni dal modulo, come qualsiasi altra funzione di Python.

Le origini dati supportate includono i database ODBC, SQL Server e il formato di file XDF per lo scambio di dati con altre origini o con soluzioni R. I dati di input per Python devono essere tabulari. Tutti i risultati Python devono essere restituiti sotto forma di frame  di dati Pandas.

I contesti di calcolo supportati includono il contesto di calcolo locale o remoto SQL Server. Un contesto di calcolo remoto si riferisce all'esecuzione del codice che viene avviata in un computer, ad esempio una workstation, ma quindi passa l'esecuzione dello script a un computer remoto. Per cambiare il contesto di calcolo è necessario che entrambi i sistemi abbiano la stessa libreria revoscalepy.

Il contesto di calcolo locale, come ci si può aspettare, include l'esecuzione del codice Python nello stesso server dell'istanza del motore di database, con codice all'interno di T-SQL o incorporato in un stored procedure. È anche possibile eseguire il codice da un ambiente IDE di Python locale e far eseguire lo script nel computer SQL Server, definendo un contesto di calcolo remoto.

## <a name="execution-architecture"></a>Architettura di esecuzione

I diagrammi seguenti illustrano l'interazione dei componenti di SQL Server con il runtime di Python in ognuno degli scenari supportati: esecuzione di script nel database ed esecuzione remota da un terminale Python, usando un SQL Server contesto di calcolo.

### <a name="python-scripts-executed-in-database"></a>Script Python eseguiti nel database

Quando si esegue il SQL Server "interno" di Python, è necessario incapsulare lo script Python all'interno di uno Speciale stored procedure, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Dopo che lo script è stato incorporato nel stored procedure, qualsiasi applicazione che può effettuare una chiamata stored procedure può avviare l'esecuzione del codice Python.  Successivamente SQL Server gestisce l'esecuzione del codice come riepilogato nel diagramma seguente.

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Una richiesta per il runtime di Python è indicata dal parametro `@language='Python'` passato al stored procedure. SQL Server invia la richiesta al servizio launchpad.
2. Il servizio Launchpad avvia l'utilità di avvio appropriata; in questo caso, PythonLauncher.
3. PythonLauncher avvia il processo Python35 esterno.
4. BxlServer coordina con il runtime di Python per gestire lo scambio di dati e l'archiviazione dei risultati di lavoro.
5. Il satellite SQL gestisce le comunicazioni sulle attività e i processi correlati con SQL Server.
6. BxlServer usa SQL satellite per comunicare lo stato e i risultati a SQL Server.
7. SQL Server Ottiene i risultati e chiude le attività e i processi correlati.

### <a name="python-scripts-executed-from-a-remote-client"></a>Script Python eseguiti da un client remoto

È possibile eseguire script Python da un computer remoto, ad esempio un computer portatile, e fare in modo che vengano eseguiti nel contesto del computer SQl server, se vengono soddisfatte le condizioni seguenti:

+ Progettare gli script in modo appropriato
+ Il computer remoto ha installato le librerie di estensibilità utilizzate da Machine Learning Services. Il pacchetto [revoscalepy](../python/ref-py-revoscalepy.md) è necessario per usare i contesti di calcolo remoti.

Nel diagramma seguente viene riepilogato il flusso di lavoro complessivo quando gli script vengono inviati da un computer remoto.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. Per le funzioni supportate in **revoscalepy**, il runtime di Python chiama una funzione di collegamento, che a sua volta chiama BxlServer.
2. BxlServer è incluso in Machine Learning Services (in-database) e viene eseguito in un processo separato dal runtime di Python.
3. BxlServer determina la destinazione della connessione e avvia una connessione tramite ODBC, passando le credenziali fornite come parte della stringa di connessione nello script Python.
4. BxlServer apre una connessione all'istanza di SQL Server.
5. Quando viene chiamato un runtime di script esterno, viene richiamato il servizio Launchpad, che a sua volta avvia l'utilità di avvio appropriata: in questo caso, PythonLauncher. dll. Successivamente, l'elaborazione del codice Python viene gestita in un flusso di lavoro simile a quando il codice Python viene richiamato da un stored procedure in T-SQL.
6. PythonLauncher effettua una chiamata all'istanza di Python installata nel computer SQL Server.
7. I risultati vengono restituiti a BxlServer.
8. SQL satellite gestisce la comunicazione con SQL Server e la pulizia di oggetti processo correlati.
9. SQL Server passa nuovamente i risultati al client.

## <a name="see-also"></a>Vedere anche

+ [modulo revoscalepy in SQL Server](../python/ref-py-revoscalepy.md)
+ [riferimento alla funzione revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [Framework di estendibilità in SQL Server](extensibility-framework.md)
+ [Estensioni R e Machine Learning in SQL Server](extension-r.md)