---
title: Architettura di estendibilità
description: Questo articolo descrive l'architettura del framework di estendibilità per l'esecuzione di uno script esterno, ad esempio R o Python, su SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fcdb92f92ffb8239a6cf20b0f39dfb8f546b521a
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727685"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Architettura di estendibilità in SQL Server Machine Learning Services 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server ha un framework di estendibilità per l'esecuzione di uno script esterno, ad esempio R o Python, nel server. Lo script viene eseguito in un ambiente di runtime del linguaggio come estensione del motore di database principale.

## <a name="background"></a>Informazioni preliminari

Il framework di estendibilità è stato introdotto in SQL Server 2016 per supportare il runtime R. In SQL Server 2017 e versioni successive è incluso il supporto per Python.

Lo scopo del framework di estendibilità è fornire un'interfaccia tra SQL Server e i linguaggi di data science, ad esempio R e Python. L'obiettivo è ridurre l'attrito durante il trasferimento delle soluzioni di data science all'ambiente di produzione e proteggere i dati esposti durante il processo di sviluppo. Eseguendo un linguaggio di scripting attendibile all'interno di un framework protetto gestito da SQL Server, gli amministratori di database possono mantenere la sicurezza consentendo ai data scientist di accedere ai dati aziendali.

Il diagramma seguente illustra graficamente le opportunità e i vantaggi dell'architettura estendibile.

  ![Obiettivi dell'integrazione con SQL Server](../media/ml-service-value-add.png "Valore aggiunto di Machine Learning Services")

Qualsiasi script esterno può essere eseguito chiamando una stored procedure e i risultati vengono restituiti sotto forma tabulare direttamente a SQL Server. Ciò semplifica la generazione o l'utilizzo di dati di Machine Learning da qualsiasi applicazione in grado di inviare una query SQL e gestire i risultati.

+ L'esecuzione di script esterni è soggetta alle regole di sicurezza dei dati di SQL Server. Un utente che esegue uno script esterno può accedere solo ai dati che sarebbero disponibili usando una query SQL. Se una query ha esito negativo per autorizzazioni insufficienti, anche uno script eseguito dallo stesso utente avrà esito negativo per lo stesso motivo. La sicurezza di SQL Server viene applicata a livello di tabella, database e istanza. Gli amministratori di database possono gestire l'accesso degli utenti, le risorse usate dagli script esterni e le librerie di codice esterno aggiunte al server.  

+ Le opportunità di scalabilità e ottimizzazione hanno una doppia base: i vantaggi che è possibile ottenere tramite la piattaforma di database (indici ColumnStore e [governance delle risorse](../../advanced-analytics/r/resource-governance-for-r-services.md)) e i miglioramenti specifici di un'estensione, ad esempio quando vengono usate le librerie Microsoft per R e Python per i modelli di data science. Le funzioni R sono a thread singolo, ma la funzioni RevoScaleR sono multithread e consentono la distribuzione di un carico di lavoro su più core.

+ La distribuzione è basata sulle metodologie di SQL Server. Possono ad esempio essere usate stored procedure che eseguono il wrapping di uno script esterno, di codice SQL incorporato o di query T-SQL che chiamano funzioni come PREDICT per restituire i risultati dei modelli di previsione salvati in modo permanente nel server.

+ Gli sviluppatori con competenze consolidate nell'uso di strumenti e IDE specifici possono scrivere codice usando questi strumenti e quindi trasferire il codice in SQL Server.

## <a name="architecture-diagram"></a>Diagramma dell'architettura

L'architettura è progettata in modo che gli script esterni vengano eseguiti in un processo separato da SQL Server, ma con componenti che gestiscono internamente la catena di richieste di dati e operazioni in SQL Server. A seconda della versione di SQL Server, le estensioni del linguaggio supportate includono [R](extension-r.md), [Python](extension-python.md) e linguaggi di terze parti, come Java e .NET.

  ***Architettura dei componenti in Windows:***
  
  ![Architettura dei componenti in Windows](../media/generic-architecture-windows.png "Architettura dei componenti")
  
  ***Architettura dei componenti in Linux:***

  ![Architettura dei componenti in Linux](../media/generic-architecture-linux.png "Architettura dei componenti")
  
I componenti includono un servizio **launchpad** usato per richiamare i runtime esterni e la logica specifica della libreria per il caricamento di interpreti e librerie. L'utilità di avvio carica un runtime del linguaggio ed eventuali moduli proprietari. Se ad esempio il codice include funzioni RevoScaleR, viene caricato un interprete RevoScaleR. **BxlServer** e **SQL Satellite** gestiscono le comunicazioni e il trasferimento dei dati con SQL Server. 

In Linux, SQL usa un servizio **launchpadd** per comunicare con un processo launchpad separato per ogni utente.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] è un servizio che gestisce ed esegue script esterni, in modo analogo a come il servizio di indicizzazione e query full-text avvia un host separato per l'elaborazione delle query full-text. Il servizio launchpad può avviare solo utilità di avvio attendibili pubblicate da Microsoft o che Microsoft ha certificato come conformi ai requisiti di prestazioni e gestione delle risorse.

| Utilità di avvio attendibili | Estensione | Versioni di SQL Server |
|-------------------|-----------|---------------------|
| RLauncher.dll per il linguaggio R per Windows | [Estensione di R](extension-r.md) | SQL Server 2016 e versioni successive |
| Pythonlauncher.dll per Python 3.5 per Windows | [Estensione di Python](extension-python.md) | SQL Server 2017 e versioni successive |
| RLauncher.so per il linguaggio R per Linux | [Estensione di R](extension-r.md) | SQL Server 2019 e versioni successive |
| Pythonlauncher.so per Python 3.5 per Linux | [Estensione di Python](extension-python.md) | SQL Server 2019 e versioni successive |

Il servizio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] viene eseguito con il relativo account utente. Se si modifica l'account che esegue launchpad, usare Gestione configurazione SQL Server per assicurarsi che le modifiche vengano scritte nei file correlati.

In Windows viene creato un servizio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] separato per ogni istanza del motore di database a cui è stato aggiunto SQL Server Machine Learning Services. È disponibile un servizio launchpad per ogni istanza del motore di database, quindi se si hanno più istanze con supporto per gli script esterni, si avrà un servizio launchpad per ciascuna di esse. Un'istanza del motore di database è associata al servizio launchpad creato per tale istanza. Per tutte le chiamate di script esterni in una stored procedure o in T-SQL, il servizio SQL Server chiama il servizio launchpad creato per la stessa istanza.

Per eseguire attività in un linguaggio supportato specifico, il servizio launchpad ottiene un account di lavoro protetto dal pool e avvia un processo satellite per gestire il runtime esterno. Ogni processo satellite eredita l'account utente del servizio launchpad e usa tale account di lavoro per la durata dell'esecuzione dello script. Se lo script usa processi paralleli, questi vengono creati con lo stesso account di lavoro singolo.

In Linux è supportata una sola istanza del motore di database e all'istanza è associato un solo servizio launchpadd. Quando viene eseguito uno script, il servizio launchpadd avvia un processo launchpad separato con l'account utente **mssql_satellite** che dispone di privilegi limitati. Ogni processo satellite eredita l'account utente mssql_satellite di launchpad e usa tale account per la durata dell'esecuzione dello script.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer e SQL Satellite

**BxlServer** è un eseguibile fornito da Microsoft che gestisce le comunicazioni tra SQL Server e il runtime del linguaggio. Crea gli oggetti processo di Windows per Windows, o gli spazi dei nomi per Linux, che vengono usati per contenere sessioni di script esterni. Effettua inoltre il provisioning di cartelle di lavoro sicure per ogni processo di script esterno e usa SQL satellite per gestire il trasferimento dei dati tra il runtime esterno e SQL Server. Se si esegue [Esplora processi](https://technet.microsoft.com/sysinternals/processexplorer.aspx) mentre un processo è in esecuzione, è possibile che vengano visualizzate istanze di BxlServer.

Di fatto, BxlServer è un ambiente di runtime del linguaggio che funziona con SQL Server per trasferire i dati e gestire le attività. BXL è l'acronimo di Binary Exchange Language e fa riferimento al formato di dati usato per spostare i dati in modo efficiente tra SQL Server e i processi esterni. BxlServer è anche una parte importante dei prodotti correlati, come Microsoft R Client e Microsoft R Server.

**SQL Satellite** è un'API di estendibilità, inclusa nel motore di database, che supporta il codice esterno o i runtime esterni implementati usando C o C++.

BxlServer usa SQL Satellite per queste attività:

+ Lettura dei dati di input
+ Scrittura dei dati di output
+ Recupero degli argomenti di input
+ Scrittura degli argomenti di output
+ Gestione degli errori
+ Scrittura di STDOUT e STDERR nel client

SQL Satellite usa un formato di dati personalizzato, ottimizzato per il trasferimento rapido dei dati tra SQL Server e i linguaggi di script esterni. Esegue le conversioni dei tipi e definisce gli schemi dei set di dati di input e output durante le comunicazioni tra SQL Server e il runtime dello script esterno.

SQL Satellite può essere monitorato usando gli eventi estesi di Windows (xEvents). Per altre informazioni, vedere [Eventi estesi per R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) ed [Eventi estesi per Python](../../advanced-analytics/python/extended-events-for-python.md).

## <a name="communication-channels-between-components"></a>Canali di comunicazione tra componenti

In questa sezione vengono descritti i protocolli di comunicazione tra i componenti e le piattaforme dati.

+ **TCP/IP**

  Per impostazione predefinita, le comunicazioni interne tra SQL Server e SQL Satellite usano TCP/IP.

+ **Named Pipe**

  Il trasporto dei dati interni tra BxlServer e SQL Server tramite SQL Satellite usa un formato di dati compresso proprietario per migliorare le prestazioni. Tra i runtime di linguaggio e BxlServer i dati vengono scambiati in formato BXL, tramite named pipe.

+ **ODBC**

  Le comunicazioni tra i client di data science esterni e un'istanza remota di SQL Server usano ODBC. L'account che invia i processi di script a SQL Server deve avere entrambe le autorizzazioni per connettersi all'istanza ed eseguire gli script esterni.

  Inoltre, a seconda dell'attività, per l'account potrebbero essere necessarie le autorizzazioni seguenti:

  + Lettura dei dati usati dal processo
  + Scrittura dei dati nelle tabelle: ad esempio, quando si salvano i risultati in una tabella
  + Creazione di oggetti di database: ad esempio, se si salva uno script esterno come parte di una nuova stored procedure.

  Quando si usa SQL Server come contesto di calcolo per uno script eseguito da un client remoto e l'eseguibile deve recuperare i dati da un'origine esterna, viene usato ODBC per il writeback. SQL Server mappa l'identità dell'utente che invia il comando remoto all'identità dell'utente dell'istanza corrente ed esegue il comando ODBC usando le credenziali di tale utente. La stringa di connessione necessaria per eseguire questa chiamata a ODBC viene ottenuta dal codice client.

+ **RODBC (solo R)** 

  Possono essere effettuate altre chiamate ODBC nello script tramite **RODBC**. RODBC è un pacchetto R molto diffuso usato per accedere ai dati nei database relazionali. Le sue prestazioni sono tuttavia generalmente più lente di quelle di provider analoghi usati da SQL Server. Molti script R usano le chiamate incorporate a RODBC come modo per recuperare set di dati "secondari" da usare nelle analisi. La stored procedure che esegue il training di un modello potrebbe ad esempio definire una query SQL per ottenere i dati per il training di un modello, ma usare una chiamata a RODBC incorporata per ottenere fattori aggiuntivi, eseguire ricerche o ottenere nuovi dati da origini esterne, come file di testo o Excel.

  Il codice seguente illustra una chiamata a RODBC incorporata in uno script R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Altri protocolli**

  I processi che potrebbero dover funzionare in "blocchi" o ritrasferire i dati a un client remoto possono anche usare il [formato di file XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). L'effettivo trasferimento dei dati avviene tramite BLOB codificati.

## <a name="see-also"></a>Vedere anche

+ [Estensione R in SQL Server](extension-r.md)
+ [Estensione Python in SQL Server](extension-python.md)