---
title: Architettura di estendibilità per il linguaggio R e lo script Python
description: Supporto del codice esterno per il motore di database SQL Server, con architettura doppia per l'esecuzione di script R e Python su dati relazionali.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a5c49172ed23867f95e383878f792092bd762177
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470453"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Architettura di estendibilità in SQL Server Machine Learning Services 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server dispone di un Framework di estendibilità per l'esecuzione di script esterni, ad esempio R o Python, nel server. Lo script viene eseguito in un ambiente di runtime del linguaggio come estensione del motore di database principale. 

## <a name="background"></a>Sfondo

Il Framework di estendibilità è stato introdotto in SQL Server 2016 per supportare il runtime di R. SQL Server 2017 aggiunge il supporto per Python

Lo scopo del Framework di estendibilità è fornire un'interfaccia tra SQL Server e linguaggi data science, ad esempio R e Python, riducendo l'attrito durante lo sviluppo di soluzioni data science in produzione e proteggendo i dati esposti durante lo sviluppo processo. Eseguendo un linguaggio di scripting attendibile all'interno di un Framework protetto gestito da SQL Server, gli amministratori di database possono mantenere la sicurezza consentendo ai data scientist di accedere ai dati aziendali.

Il diagramma seguente illustra visivamente le opportunità e i vantaggi dell'architettura estendibile.

  ![Obiettivi dell'integrazione con SQL Server](../media/ml-service-value-add.png "Aggiunta valore Machine Learning Services")

Qualsiasi script R o Python può essere eseguito chiamando un stored procedure e i risultati vengono restituiti come risultati tabulari direttamente a SQL Server, semplificando la generazione o l'utilizzo di machine learning da qualsiasi applicazione in grado di inviare una query SQL e gestire i risultati.

+ L'esecuzione di script esterni è soggetta a SQL Server sicurezza dei dati, in cui un utente che esegue uno script esterno può accedere solo ai dati che sono ugualmente disponibili in una query SQL. Se una query ha esito negativo a causa di autorizzazioni insufficienti, anche lo script eseguito dallo stesso utente avrà esito negativo per lo stesso motivo. SQL Server sicurezza viene applicata a livello di tabella, di database e di istanza. Gli amministratori di database possono gestire l'accesso utente, le risorse usate dagli script esterni e le librerie di codice esterno aggiunte al server.  

+ Le opportunità di scalabilità e ottimizzazione hanno una duplice base: i guadagni attraverso la piattaforma di database (indici columnstore, [governance delle risorse](../../advanced-analytics/r/resource-governance-for-r-services.md)) e i miglioramenti specifici dell'estensione quando si usano le librerie Microsoft per R e Python per i modelli di Data Science. Mentre R è a thread singolo, le funzioni RevoScaleR sono multithread, in grado di distribuire un carico di lavoro su più core.

+ La distribuzione usa SQL Server metodologie: stored procedure che eseguono il wrapping di script esterni, incorporate SQL o query T-SQL che chiamano funzioni come PREDICT per restituire i risultati dai modelli di previsione salvati in modo permanente nel server.

+ Gli sviluppatori R e Python con competenze stabilite in strumenti e IDE specifici possono scrivere codice in questi strumenti e quindi trasferire il codice per SQL Server.

## <a name="architecture-diagram"></a>Diagramma dell'architettura

L'architettura è progettata in modo che gli script esterni vengano eseguiti in un processo separato da SQL Server, ma con componenti che gestiscono internamente la catena di richieste di dati e operazioni su SQL Server. A seconda della versione di SQL Server, le estensioni del linguaggio supportate includono R e Python. 

  ![Architettura del componente](../media/generic-architecture.png "Architettura del componente")

I componenti includono un servizio **Launchpad** usato per richiamare i lanci specifici della lingua (R o Python), la logica specifica del linguaggio e della libreria per il caricamento di interpreti e librerie. L'utilità di avvio carica un tempo di esecuzione del linguaggio, oltre a qualsiasi modulo proprietario. Se, ad esempio, il codice include funzioni RevoScaleR, viene caricato un interprete RevoScaleR. **BxlServer** e **SQL satellite** gestiscono le comunicazioni e il trasferimento dei dati con SQL Server.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] È un servizio che gestisce ed esegue script esterni, in modo analogo al modo in cui il servizio di indicizzazione e query full-text avvia un host separato per l'elaborazione di query full-text. Il servizio Launchpad può avviare solo avvii attendibili pubblicati da Microsoft o certificati da Microsoft come requisiti per la gestione delle prestazioni e delle risorse.

| Avvii attendibili | Estensione | Versioni SQL Server |
|-------------------|-----------|---------------------|
| RLauncher. dll per il linguaggio R | [Estensione R](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| Pythonlauncher. dll per Python 3,5 | [Estensione Python](extension-python.md) | SQL Server 2017 |

Il servizio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] viene eseguito con il relativo account utente. Se si modifica l'account che esegue Launchpad, assicurarsi di usare Gestione configurazione SQL Server per assicurarsi che le modifiche vengano scritte nei file correlati.

Viene creato [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] un servizio separato per ogni istanza del motore di database a cui è stato aggiunto SQL Server Machine Learning Services. È disponibile un servizio Launchpad per ogni istanza del motore di database, pertanto se si dispone di più istanze con supporto per gli script esterni, sarà disponibile un servizio Launchpad per ciascuno di essi. Un'istanza del motore di database è associata al servizio Launchpad creato. Tutte le chiamate di script esterno in un stored procedure o in T-SQL generano il servizio SQL Server che chiama il servizio Launchpad creato per la stessa istanza.

Per eseguire attività in una lingua supportata specifica, la finestra di avvio ottiene un account di lavoro protetto dal pool e avvia un processo satellite per gestire il runtime esterno. Ogni processo satellite eredita l'account utente della finestra di avvio e utilizza tale account di lavoro per la durata dell'esecuzione dello script. Se lo script usa processi paralleli, vengono creati con lo stesso account di lavoro singolo.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer e SQL satellite

**BxlServer** è un eseguibile fornito da Microsoft che gestisce la comunicazione tra SQL Server e Python o R. Crea gli oggetti processo di Windows usati per contenere sessioni di script esterne, effettua il provisioning di cartelle di lavoro sicure per ogni processo di script esterno e usa SQL satellite per gestire il trasferimento dei dati tra il runtime esterno e SQL Server. Se si esegue [Esplora processi](https://technet.microsoft.com/sysinternals/processexplorer.aspx) mentre un processo è in esecuzione, è possibile che vengano visualizzate una o più istanze di BxlServer.

In effetti, BxlServer è un ambiente di runtime del linguaggio che funziona con SQL Server per trasferire i dati e gestire le attività. BXL si basa sul linguaggio di scambio binario e si riferisce al formato dati utilizzato per spostare i dati in modo efficiente tra SQL Server e processi esterni. BxlServer è anche una parte importante dei prodotti correlati, ad esempio Microsoft R Client e Microsoft R Server.

Il **satellite SQL** è un'API di estendibilità, inclusa nel motore di database a partire da SQL Server 2016, che supporta codice esterno o Runtime esterni implementato C++con C o.

BxlServer usa SQL Satellite per queste attività:

+ Lettura dei dati di input
+ Scrittura dei dati di output
+ Recupero degli argomenti di input
+ Scrittura degli argomenti di output
+ Gestione degli errori
+ Scrittura di STDOUT e STDERR nel client

SQL satellite usa un formato di dati personalizzato ottimizzato per il trasferimento rapido dei dati tra SQL Server e linguaggi di script esterni. Esegue conversioni di tipi e definisce gli schemi dei set di dati di input e di output durante le comunicazioni tra SQL Server e il runtime di script esterno.

Il satellite SQL può essere monitorato tramite gli eventi estesi di Windows (XEvent). Per altre informazioni, vedere [eventi estesi per R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) ed [eventi estesi per Python](../../advanced-analytics/python/extended-events-for-python.md).

## <a name="communication-channels-between-components"></a>Canali di comunicazione tra i componenti

In questa sezione vengono descritti i protocolli di comunicazione tra i componenti e le piattaforme di dati.

+ **TCP/IP**

  Per impostazione predefinita, le comunicazioni interne tra SQL Server e il satellite SQL usano TCP/IP.

+ **Named Pipe**

  Il trasporto di dati interni tra BxlServer e SQL Server tramite SQL satellite usa un formato di dati compresso e proprietario per migliorare le prestazioni. I dati vengono scambiati tra i tempi di esecuzione del linguaggio e BxlServer in formato BXL usando named pipe.

+ **ODBC**

  Le comunicazioni tra client di data science esterni e un'istanza di SQL Server remota utilizzano ODBC. L'account che invia i processi di script a SQL Server deve disporre di entrambe le autorizzazioni per la connessione all'istanza di e per l'esecuzione di script esterni.

  Inoltre, a seconda dell'attività, per l'account potrebbero essere necessarie le autorizzazioni seguenti:

  + Leggere i dati usati dal processo
  + Scrivere dati in tabelle: ad esempio, quando si salvano i risultati in una tabella
  + Creare oggetti di database: ad esempio, se si salva uno script esterno come parte di un nuovo stored procedure.

  Quando SQL Server viene utilizzato come contesto di calcolo per lo script eseguito da un client remoto e il file eseguibile deve recuperare i dati da un'origine esterna, per il writeback viene utilizzato ODBC. SQL Server esegue il mapping dell'identità dell'utente che ha emesso il comando remoto all'identità dell'utente nell'istanza corrente ed esegue il comando ODBC utilizzando le credenziali dell'utente. La stringa di connessione necessaria per eseguire questa chiamata a ODBC viene ottenuta dal codice client.

+ **RODBC (solo R)** 

  Possono essere effettuate altre chiamate ODBC nello script tramite **RODBC**. RODBC è un pacchetto R popolare usato per accedere ai dati nei database relazionali. Tuttavia, le prestazioni sono in genere più lente rispetto ai provider comparabili usati da SQL Server. Molti script R usano le chiamate incorporate a RODBC come modo per recuperare set di dati "secondari" da usare nelle analisi. La stored procedure che esegue il training di un modello potrebbe ad esempio definire una query SQL per ottenere i dati per il training di un modello, ma usare una chiamata a RODBC incorporata per ottenere fattori aggiuntivi, eseguire ricerche o ottenere nuovi dati da origini esterne, come file di testo o Excel.

  Il codice seguente illustra una chiamata a RODBC incorporata in uno script R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Altri protocolli**

  I processi che potrebbero dover funzionare in "blocchi" o trasferire i dati a un client remoto possono anche usare il [formato di file XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Il trasferimento effettivo dei dati avviene tramite BLOB codificati.

## <a name="see-also"></a>Vedere anche

+ [Estensione R in SQL Server](extension-r.md)
+ [Estensione Python in SQL Server](extension-python.md)