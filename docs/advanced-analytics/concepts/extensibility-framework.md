---
title: Architettura di estendibilità per il linguaggio R e Python - script di SQL Server Machine Learning
description: Supporto del codice esterno per il motore di database di SQL Server, con architettura a doppio per l'esecuzione di script R e Python su dati relazionali.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3d4d8108fda500d48425abfb52fd9f72c6faa147
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963050"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Architettura di estendibilità in SQL Server Machine Learning Services 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server è un framework di estensibilità per l'esecuzione di script esterni, ad esempio R o Python nel server. Script viene eseguito in un ambiente di runtime del linguaggio come un'estensione per il motore di database principale. 

## <a name="background"></a>Sfondo

Il framework di estendibilità è stato introdotto in SQL Server 2016 per supportare il runtime di R. Aggiunge il supporto per Python per SQL Server 2017

Lo scopo del framework di estendibilità consiste nel fornire un'interfaccia tra SQL Server e i linguaggi di analisi scientifica dei dati, ad esempio R e Python, ridurre gli attriti durante lo spostamento di soluzioni di data science in produzione e proteggere i dati esposti durante lo sviluppo processo. Tramite l'esecuzione di un linguaggio di scripting attendibile all'interno di un'infrastruttura protetta gestita da SQL Server, gli amministratori di database possono gestire sicurezza, consentendo l'accesso ai dati aziendali ai data Scientist.

Il diagramma seguente illustra in modo visivo le opportunità e i vantaggi dell'architettura estendibile.

  ![Obiettivi dell'integrazione con SQL Server](../media/ml-service-value-add.png "valore aggiunto da Machine Learning Services")

Qualsiasi script R o Python può essere eseguito chiamando una stored procedure e i risultati vengono restituiti come risultati tabulari direttamente da SQL Server, rendendo più semplice generare o usare apprendimento automatico da qualsiasi applicazione che può inviare una query SQL e gestire i risultati.

+ L'esecuzione di script esterni è soggetto a protezione dei dati di SQL Server, in cui un utente che esegue script esterni possono solo accedere ai dati che è ugualmente disponibile in una query SQL. Se una query ha esito negativo a causa di autorizzazioni insufficienti, dello script eseguito dallo stesso utente potrebbe anche non riuscire per lo stesso motivo. Sicurezza di SQL Server viene applicata la tabella, database e a livello di istanza. Gli amministratori di database possono gestire l'accesso utente, le risorse usate dagli script esterni e le librerie di codice esterno aggiunte al server.  

+ Opportunità di scalabilità e ottimizzazione hanno una base di doppia: guadagni tramite la piattaforma di database (gli indici ColumnStore [governance delle risorse](../../advanced-analytics/r/resource-governance-for-r-services.md)) e specifiche dell'estensione utili quando le librerie di Microsoft per R e Python sono usate per i dati modelli di analisi scientifica. Mentre R è a thread singolo, le funzioni RevoScaleR sono in grado di distribuire un carico di lavoro su più core, a thread multipli.

+ La distribuzione Usa le metodologie di SQL Server: stored procedure il wrapping dello script esterno, embedded SQL o T-SQL esegue una query funzioni chiamanti come stima per restituire risultati da modelli di previsione vengono mantenuti nel server.

+ Gli sviluppatori di R e Python con stabilita competenze nell'IDE e strumenti specifici possono scrivere codice in questi strumenti e quindi convertire il codice per SQL Server.

## <a name="architecture-diagram"></a>Diagramma dell'architettura

L'architettura è progettata in modo che gli script esterni eseguiti in un processo separato da SQL Server, ma con i componenti che gestiscono internamente la catena di richieste di dati e le operazioni in SQL Server. A seconda della versione di SQL Server, le estensioni dei linguaggi supportati includono R e Python. 

  ![Architettura dei componenti](../media/generic-architecture.png "architettura dei componenti")

I componenti includono un' **Launchpad** servizio utilizzato per richiamare il linguaggio R o Python, specifici della lingua nelle schermate di avvio e la logica di libreria specifica per il caricamento di interpreti e librerie. L'utilità di avvio carica un tempo di linguaggio eseguito, oltre a tutti i moduli proprietari. Ad esempio, se il codice include funzioni RevoScaleR, potrebbe caricare un interprete di RevoScaleR. **BxlServer** e **SQL Satellite** gestire il trasferimento di dati e la comunicazione con SQL Server.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

Il [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] è un servizio che gestisce ed esegue script esterni, analogamente al modo in cui il servizio di indicizzazione e query full-text avvia un host separato per l'elaborazione delle query full-text. Il servizio Launchpad possa avviare solo utilità di avvio attendibili pubblicate da Microsoft o che sono stati certificati da Microsoft come conformi ai requisiti di prestazioni e gestione delle risorse.

| Utilità di avvio attendibili | Estensione | Versioni di SQL Server |
|-------------------|-----------|---------------------|
| Rlauncher. dll per il linguaggio R | [Estensione di R](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| Pythonlauncher.dll per Python 3.5 | [Estensione per Python](extension-python.md) | SQL Server 2017 |

Il servizio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] viene eseguito con il relativo account utente. Se si modifica l'account che esegue Launchpad, assicurarsi di eseguire questa operazione mediante Gestione configurazione SQL Server, per garantire che le modifiche vengono scritte per i relativi file.

Un oggetto separato [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servizio viene creato per ogni istanza del motore di database a cui si sono aggiunti servizi di SQL Server Machine Learning. È disponibile una finestra di avvio del servizio per ogni istanza del motore di database, pertanto se si dispone di più istanze con supporto per gli script esterni, è necessario un servizio Launchpad per ognuno di essi. Un'istanza del motore di database è associata al servizio Launchpad creato appositamente. Tutte le chiamate di script esterni in una stored procedure o il risultato di T-SQL nel servizio di SQL Server chiama il servizio Launchpad creato per la stessa istanza.

Per eseguire le attività in una determinata lingua supportata, la finestra di avvio Ottiene un account di lavoro protetti dal pool e avvia un processo satellite per gestire il runtime esterno. Ogni processo satellite eredita l'account utente del Launchpad e Usa l'account di lavoro per la durata dell'esecuzione dello script. Se lo script Usa processi paralleli, vengono create con l'account di lavoro stessa.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer e SQL Satellite

**BxlServer** è un eseguibile fornito da Microsoft che gestisce la comunicazione tra Server SQL e Python o R. Crea gli oggetti di processo di Windows vengono usati per contenere le sessioni di script esterni, effettua il provisioning sicuro le cartelle di lavoro per ogni processo di script esterni, che Usa SQL Satellite per gestire il trasferimento di dati tra i runtime esterni e SQL Server. Se si esegue [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) mentre è in esecuzione un processo, si potrebbero vedere una o più istanze di BxlServer.

In effetti, BxlServer è complementare a un linguaggio di ambiente di runtime che funziona con SQL Server per trasferire i dati e le attività di gestione. BXL è l'acronimo di Binary Exchange language e fa riferimento al formato dei dati consente di spostare i dati in modo efficiente tra SQL Server e i processi esterni. BxlServer è anche una parte importante di prodotti correlati, ad esempio Microsoft R Client e Microsoft R Server.

**SQL Satellite** è un'API di estendibilità, inclusi nel motore di database a partire da SQL Server 2016, che supporta codice esterno o un runtime esterni implementati usando C o C++.

BxlServer usa SQL Satellite per queste attività:

+ Lettura dei dati di input
+ Scrittura dei dati di output
+ Recupero degli argomenti di input
+ Scrittura degli argomenti di output
+ Gestione degli errori
+ Scrittura di STDOUT e STDERR nel client

SQL Satellite Usa un formato di dati personalizzato ottimizzato per il trasferimento rapido dei dati tra SQL Server e i linguaggi di script esterni. Esegue conversioni di tipi e definisce gli schemi dei set di dati di input e output durante le comunicazioni tra SQL Server e l'esecuzione dello script esterno.

È possibile monitorare SQL Satellite usando windows estesi (XEvent) di eventi. Per altre informazioni, vedere [degli eventi estesi per R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) e [eventi estesi per Python](../../advanced-analytics/python/extended-events-for-python.md).

## <a name="communication-channels-between-components"></a>Canali di comunicazione tra componenti

In questa sezione sono descritti i protocolli di comunicazione tra componenti e le piattaforme di dati.

+ **TCP/IP**

  Per impostazione predefinita, le comunicazioni interne tra SQL Server e SQL Satellite usano TCP/IP.

+ **Named Pipe**

  Trasporto dei dati interni tra BxlServer e SQL Server tramite SQL Satellite Usa un formato di dati compresso proprietario per migliorare le prestazioni. I dati vengono scambiati tra BxlServer e tempi di linguaggio eseguito nel formato BXL, tramite Named pipe.

+ **ODBC**

  Le comunicazioni tra i client di analisi scientifica dei dati esterna e un'istanza remota di SQL Server usano ODBC. L'account che invia i processi di script a SQL Server deve avere entrambe le autorizzazioni per connettersi all'istanza ed eseguire gli script esterni.

  Inoltre, a seconda dell'attività, l'account potrebbe essere necessario queste autorizzazioni:

  + Leggere i dati usati dal processo
  + Scrivere dati nelle tabelle: ad esempio, quando salvare i risultati a una tabella
  + Creare oggetti di database: ad esempio, se il salvataggio dello script esterno come parte di una nuova stored procedure.

  Quando SQL Server viene usato come contesto di calcolo per gli script eseguiti da un client remoto e il file eseguibile deve recuperare dati da un'origine esterna, viene usato ODBC per il writeback. SQL Server viene eseguito il mapping di identità dell'utente che invia il comando remoto all'identità dell'utente nell'istanza corrente e viene eseguito il comando ODBC usando le credenziali dell'utente. La stringa di connessione necessaria per eseguire questa chiamata a ODBC viene ottenuta dal codice client.

+ **RODBC (solo R)** 

  Possono essere effettuate altre chiamate ODBC nello script tramite **RODBC**. RODBC è un pacchetto R molto diffuso usato per accedere ai dati in database relazionali. Tuttavia, le prestazioni sono generalmente più lente di provider analoghi usati da SQL Server. Molti script R usano le chiamate incorporate a RODBC come modo per recuperare set di dati "secondari" da usare nelle analisi. La stored procedure che esegue il training di un modello potrebbe ad esempio definire una query SQL per ottenere i dati per il training di un modello, ma usare una chiamata a RODBC incorporata per ottenere fattori aggiuntivi, eseguire ricerche o ottenere nuovi dati da origini esterne, come file di testo o Excel.

  Il codice seguente illustra una chiamata a RODBC incorporata in uno script R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Altri protocolli**

  I processi che potrebbero dover funzionare in "blocchi" o trasferire i dati a un client remoto possono anche utilizzare il [formato di file con estensione XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Trasferimento di dati reali avviene tramite BLOB codificati.

## <a name="see-also"></a>Vedere anche

+ [Estensione di R in SQL Server](extension-r.md)
+ [Estensione di Python in SQL Server](extension-python.md)