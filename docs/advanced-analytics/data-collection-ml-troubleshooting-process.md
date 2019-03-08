---
title: 'Risolvere i problemi di raccolta dati per machine learning: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a4fdd31cddaba1c46cc14ae6dbdeeb6ad92449da
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579131"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Risolvere i problemi di raccolta dati per machine learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive i metodi di raccolta dati che si deve usare durante il tentativo per risolvere i problemi in autonomia o con l'aiuto del cliente di Microsoft supportare.

**Si applica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (R e Python)

## <a name="sql-server-version-and-edition"></a>Edizione e versione di SQL Server

SQL Server 2016 R Services è la prima versione di SQL Server da includere il supporto integrato di R. SQL Server 2016 Service Pack 1 (SP1) include alcuni miglioramenti fondamentali, tra cui la possibilità di eseguire gli script esterni. Se sei un cliente di SQL Server 2016, è consigliabile installare SP1 o versione successiva.

SQL Server 2017 aggiunta dell'integrazione del linguaggio Python. Non è possibile ottenere l'integrazione delle funzionalità Python nelle versioni precedenti.

Per assistenza per il recupero di edizione e le versioni, vedere questo articolo, che elenca i numeri di build per ognuna delle [versioni di SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

A seconda dell'edizione di SQL Server in uso, alcune funzionalità di apprendimento automatico potrebbe essere disponibile o limitata. Nell'elenco seguente di articoli della funzionalità di machine learning nelle edizioni Enterprise, Developer, Standard ed Express.

* [Edizioni e funzionalità supportate di SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [R e Python funzionalità supportate dalle edizioni di SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>Versioni di linguaggio e degli strumenti R

In generale, la versione di Microsoft R che viene installato quando si seleziona la funzionalità R Services o la funzionalità di servizi di Machine Learning è determinata dal numero di build di SQL Server. Se si esegue l'aggiornamento o applicare patch di SQL Server, è anche necessario aggiornare o applicare patch i componenti R.

Per un elenco di rilasci e collegamenti ai download di componenti di R, vedere [installa i componenti di apprendimento automatico senza accesso a internet](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access). Nei computer con accesso a internet, la versione richiesta di R è identificata e installata automaticamente.

È possibile aggiornare i componenti di R Server separatamente dal motore di database di SQL Server, in un processo noto come associazione. Pertanto, la versione di R che usano quando si esegue codice R in SQL Server potrebbe variare a seconda la versione installata di SQL Server e indica se è stata eseguita la migrazione di server alla versione più recente di R.

### <a name="determine-the-r-version"></a>Determinare la versione di R

Il modo più semplice per determinare la versione di R è possibile ottenere le proprietà di runtime che esegue un'istruzione simile al seguente:

```sql
exec sp_execute_external_script
       @language = N'R'
       , @script = N'
# Transform R version properties to data.frame
OutputDataSet <- data.frame(
  property_name = c("R.version", "Revo.version"),
  property_value = c(R.Version()$version.string, Revo.version$version.string),
  stringsAsFactors = FALSE)
# Retrieve properties like R.home, libPath & default packages
OutputDataSet <- rbind(OutputDataSet, data.frame(
  property_name = c("R.home", "libPaths", "defaultPackages"),
  property_value = c(R.home(), .libPaths(), paste(getOption("defaultPackages"), collapse=", ")),
  stringsAsFactors = FALSE)
)
'
WITH RESULT SETS ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));

```

> [!TIP]
> Se R Services non funziona, provare a eseguire solo la parte di script R da RGui.

Come ultima risorsa, è possibile aprire i file nel server per determinare la versione installata. A tale scopo, individuare il file rlauncher config per ottenere la posizione del runtime di R e la directory di lavoro corrente. È consigliabile crearne e aprire una copia del file in modo da non modificare accidentalmente alcuna proprietà.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Per ottenere la versione di R e le versioni di RevoScaleR, aprire un prompt dei comandi di R o aprire RGui associati all'istanza.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

La console di R Visualizza le informazioni sulla versione all'avvio. Ad esempio, la versione seguente rappresenta la configurazione predefinita per SQL Server 2017:

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Versioni di Python

Esistono diversi modi per ottenere la versione di Python. Il modo più semplice consiste nell'eseguire questa istruzione da Management Studio o qualsiasi altro strumento di query SQL:

```sql
-- Get Python runtime properties:
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import sys
import pkg_resources
OutputDataSet = pandas.DataFrame(
                    {"property_name": ["Python.home", "Python.version", "Revo.version", "libpaths"],
                    "property_value": [sys.executable[:-10], sys.version, pkg_resources.get_distribution("revoscalepy").version, str(sys.path)]}
)
'
with WITH RESULT SETS (SQL keywords) ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));
```

Se non è in esecuzione servizi di Machine Learning, è possibile determinare la versione di Python installata esaminando il file pythonlauncher.config. È consigliabile crearne e aprire una copia del file in modo da non modificare accidentalmente alcuna proprietà.

1. Solo per SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. Ottiene il valore per **PYTHONHOME**.
3. Ottenere il valore della directory di lavoro corrente.

> [!NOTE]
> Se è stato installato Python e R in SQL Server 2017, la directory di lavoro e il pool di account di lavoro vengono condivise per i linguaggi R e Python.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>Sono più istanze di R o Python installato?

Verificare se più di una copia delle librerie di R è installata nel computer. Questa duplicazione può verificarsi se:

* Durante l'installazione si selezionano sia R Services (In-Database) di R Server (Standalone).
* Si installa Microsoft R Client oltre a SQL Server.
* È stato installato un diverso set di librerie di R con R Tools per Visual Studio, R Studio, Microsoft R Client o un altro IDE R.
* Il computer ospita più istanze di SQL Server e più di un'istanza Usa machine learning.

Le stesse condizioni si applicano a Python.

Se si ritiene che siano installati più librerie o i runtime, assicurarsi di ottenere solo gli errori associati i runtime di Python o R che vengono utilizzati dall'istanza di SQL Server.

## <a name="origin-of-errors"></a>Origine degli errori

Gli errori che vengono visualizzati quando si tenta di eseguire codice R possono provenire da una qualsiasi delle seguenti origini:

* Motore di database di SQL Server, incluse stored procedure sp_execute_external_script
* Launchpad attendibile di SQL Server
* Altri componenti del framework di estensibilità, tra cui R e Python nelle schermate di avvio e i processi satellite
* Provider, ad esempio Microsoft Open Database Connectivity (ODBC)
* Linguaggio R

Quando si lavora con il servizio per la prima volta, può essere difficile stabilire quali messaggi provengono da quali servizi. Si consiglia di acquisire il testo del messaggio esatta non solo, ma il contesto in cui è stato illustrato il messaggio. Si noti il software client che si usa per eseguire il codice di machine learning:

* Si sta usando Management Studio? Un'applicazione esterna?
* Si esegue codice R in un client remoto o direttamente in una stored procedure?

## <a name="sql-server-log-files"></a>File di log di SQL Server

Ottenere il più recente di SQL Server di log degli errori. Il set completo di log degli errori include i file della directory log predefinita seguente:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> Il nome esatto della cartella è diverso in base al nome di istanza.

## <a name="errors-returned-by-spexecuteexternalscript"></a>Errori restituiti da sp_execute_external_script

Ottiene il testo completo di errori che vengono restituiti, se presente, quando si esegue il comando di sp_execute_external_script.

Per rimuovere i problemi di R o Python dalla considerazione, è possibile eseguire questo script, che avvia il runtime di R o Python e passa i dati e viceversa.

**Per R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Per Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>Errori generati dal framework di estendibilità

SQL Server genera i log separati per i runtime di linguaggio di script esterni. Questi errori non vengono generati dal linguaggio Python o R. Non appena vengono generati dai componenti di estendibilità in SQL Server, incluse nelle schermate di avvio specifiche della lingua e i processi satellite.

È possibile ottenere i log dai percorsi predefiniti seguenti:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> Il nome esatto della cartella varia in base al nome dell'istanza. A seconda della configurazione, la cartella potrebbe essere in un'unità diversa.

Ad esempio, i messaggi di log seguenti riguardano il framework di estendibilità:

* *LogonUser non riuscito per l'utente MSSQLSERVER01*
  
  Ciò potrebbe indicare che gli account di lavoro che eseguono gli script esterni non possono accedere all'istanza.

* *InitializePhysicalUsersPool non è riuscita*
  
  Questo messaggio può significare che le impostazioni di protezione impediscano il programma di installazione dalla creazione del pool di account di lavoro che sono necessari per eseguire gli script esterni.

* *Inizializzazione di gestione di contesto di sicurezza non è riuscita*

* *Inizializzazione di gestione di sessioni satellite non è riuscita*

## <a name="system-events"></a>Eventi di sistema

1. Aprire il Visualizzatore eventi di Windows e cercare il **eventi di sistema** log dei messaggi che includono la stringa *Launchpad*.
2. Aprire il file ExtLaunchErrorlog e cercare la stringa *ErrorCode*. Esaminare il messaggio che ha associato con il codice di errore.

Ad esempio, i messaggi seguenti sono comuni errori di sistema che riguardano il framework di estendibilità di SQL Server:

* *Il servizio SQL Server Launchpad (MSSQLSERVER) non è stato possibile avviare a causa dell'errore seguente:  <text>*

* *Il servizio non ha risposto alla richiesta di avvio o di controllo in modo tempestivo.*

* *Timeout raggiunto (120000 millisecondi) durante l'attesa per il servizio SQL Server Launchpad (MSSQLSERVER) per la connessione.*

## <a name="dump-files"></a>File di dump

Se si è esperti di debug, è possibile utilizzare i file di dump per analizzare un errore nella finestra di avvio.

1. Individuare la cartella che contiene i log di bootstrap di installazione per SQL Server. Ad esempio, in SQL Server 2016, il percorso predefinito è C:\Program Files\Microsoft SQL Server\130\Setup bootstrap\log\.
2. Aprire la sottocartella di bootstrap log specifici all'estendibilità.
3. Se è necessario inviare una richiesta di supporto, aggiungere l'intero contenuto della cartella in un file compresso. Ad esempio, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
La posizione esatta potrebbe essere diverso nel sistema e potrebbe essere in un'unità diversa dall'unità C. Assicurarsi di ottenere i log per l'istanza in cui è installato l'apprendimento automatico.

## <a name="configuration-settings"></a>Impostazioni di configurazione

Questa sezione sono elencati i componenti aggiuntivi o i provider che possono essere fonte di errori quando si eseguono script R o Python.

### <a name="what-network-protocols-are-available"></a>Quali protocolli di rete sono disponibili?

Servizi di Machine Learning richiede i seguenti protocolli di rete per la comunicazione interna tra i componenti di estendibilità e per la comunicazione con client esterni di R o Python.

* Named Pipes
* TCP/IP

Aprire Gestione configurazione di SQL Server per determinare se è installato un protocollo e, se è installato, per determinare se è abilitato.

### <a name="security-configuration-and-permissions"></a>Configurazione di sicurezza e autorizzazioni

Per gli account di lavoro:

1. Nel Pannello di controllo, aprire **utenti e gruppi**e individuare il gruppo usato per eseguire processi di script esterni. Per impostazione predefinita, il gruppo è **SQLRUserGroup**.
2. Verificare che il gruppo esista e che contenga account almeno un ruolo di lavoro.
3. In SQL Server Management Studio, selezionare l'istanza in cui verranno eseguiti i processi R o Python, selezionare **sicurezza**e quindi determinare se è presente un account di accesso per SQLRUserGroup.
4. Esaminare le autorizzazioni per il gruppo di utenti.

Per gli account utente individuali:

1. Determinare se l'istanza supporta l'autenticazione modalità mista, solo gli accessi SQL o solo l'autenticazione di Windows. Questa impostazione interessa i R o Python code requisiti.
2. Per ogni utente che ha bisogno di eseguire codice R, determinare il livello di autorizzazioni per ogni database in cui gli oggetti verranno scritti da R, sarà possibile accedere ai dati o oggetti vengono creati richiesto.
3. Per abilitare l'esecuzione dello script, creare i ruoli o aggiungere utenti ai ruoli seguenti, in base alle esigenze:

   - Tutti tranne *db_owner*: Richiedi EXECUTE ANY EXTERNAL SCRIPT.
   - *db_datawriter*: Per scrivere i risultati da R o Python.
   - *db_ddladmin*: Per creare nuovi oggetti.
   - *db_datareader*: Per leggere i dati che viene usati dal codice R o Python.
4. Prendere nota di eventuali account di avvio predefinito è stato modificato durante l'installazione di SQL Server 2016.
5. Se un utente deve installare nuovi pacchetti R o usare i pacchetti R che sono stati installati da altri utenti, è necessario abilitare la gestione dei pacchetti nell'istanza e quindi assegnare le autorizzazioni aggiuntive. Per altre informazioni, vedere [abilitare o disabilitare la gestione dei pacchetti R](r/r-package-how-to-enable-or-disable.md).

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>Le cartelle sono soggetti a blocco dal software antivirus?

Il software antivirus può bloccare cartelle, impedendo di apportare entrambi il programma di installazione di machine learning le funzionalità e l'esecuzione di script ha esito positivo. Determinare se le cartelle nell'albero del Server SQL sono soggette a ricerca di virus.

Tuttavia, quando più servizi o funzionalità vengono installate in un'istanza, può essere difficile enumerare tutte le cartelle possibili che vengono usate dall'istanza. Ad esempio, quando vengono aggiunte nuove funzionalità, le nuove cartelle devono essere identificate ed esclusi.

Inoltre, alcune funzionalità di creare dinamicamente nuove cartelle in fase di esecuzione. Ad esempio, le tabelle di OLTP in memoria, le stored procedure e funzioni di creare nuove directory in fase di esecuzione. Questi nomi di cartella spesso contengono GUID e non possono essere previsto. Il servizio SQL Server Trusted Launchpad Crea nuova directory di lavoro per R e Python di generare script dei processi.

Poiché potrebbe non essere possibile escludere tutte le cartelle che sono necessari per il processo di SQL Server e delle relative funzionalità, è consigliabile escludere l'intero albero di directory istanza di SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>Viene aperto il firewall per SQL Server? L'istanza supporta le connessioni remote?

1. Per determinare se SQL Server supporta le connessioni remote, vedere [configurare le connessioni al server remoto](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Determinare se una regola del firewall è stata creata per SQL Server. Per motivi di sicurezza in un'installazione predefinita, potrebbe non essere possibile per i client remoti di R o Python per connettersi all'istanza. Per altre informazioni, vedere [risoluzione dei problemi di connessione a SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="see-also"></a>Vedere anche

[Risolvere i problemi di apprendimento automatico in SQL Server](machine-learning-troubleshooting-faq.md)
