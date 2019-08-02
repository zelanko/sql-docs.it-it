---
title: Risolvere i problemi di raccolta dati per Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c7566d9b25b15a334e48380daca6cb81e92f6a2b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715236"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Risolvere i problemi di raccolta dati per Machine Learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive i metodi di raccolta dei dati da usare quando si tenta di risolvere i problemi in modo autonomo o con l'assistenza del supporto tecnico Microsoft.

## <a name="sql-server-version-and-edition"></a>Versione ed edizione di SQL Server

SQL Server 2016 R Services è la prima versione di SQL Server per includere il supporto R integrato. SQL Server 2016 Service Pack 1 (SP1) include diversi miglioramenti importanti, tra cui la possibilità di eseguire script esterni. Se si usa SQL Server 2016, è necessario prendere in considerazione l'installazione di SP1 o versione successiva.

SQL Server 2017 e versioni successive hanno l'integrazione del linguaggio Python. Non è possibile ottenere l'integrazione delle funzionalità Python nelle versioni precedenti.

Per ulteriori informazioni su come ottenere l'edizione e le versioni, vedere questo articolo, in cui sono elencati i numeri di build per ogni [versione di SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

A seconda dell'edizione di SQL Server in uso, alcune funzionalità di Machine Learning potrebbero non essere disponibili o limitate. Negli articoli seguenti sono elencate le funzionalità di machine learning nelle edizioni Enterprise, Developer, standard ed Express.

* [Edizioni e funzionalità supportate di SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [Funzionalità di R e Python per edizioni di SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>Versioni di strumenti e linguaggi R

In generale, la versione di Microsoft R installata quando si seleziona la funzionalità R Services o la funzionalità Machine Learning Services è determinata dal numero di build del SQL Server. Se si aggiorna o si applica una patch SQL Server, è necessario aggiornare anche i relativi componenti R.

Per un elenco delle versioni e dei collegamenti ai download dei componenti R, vedere [installare i componenti di Machine Learning senza accesso a Internet](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access). Nei computer con accesso a Internet, la versione richiesta di R viene identificata e installata automaticamente.

È possibile aggiornare i componenti di R Server separatamente dal motore di database di SQL Server, in un processo noto come binding. Quindi, la versione di R usata quando si esegue il codice R in SQL Server potrebbe variare a seconda della versione installata di SQL Server e della migrazione del server alla versione più recente di R.

### <a name="determine-the-r-version"></a>Determinare la versione di R

Il modo più semplice per determinare la versione di R è ottenere le proprietà di runtime eseguendo un'istruzione come la seguente:

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
> Se R Services non funziona, provare a eseguire solo la parte dello script R da RGui.

Come ultima risorsa, è possibile aprire i file nel server per determinare la versione installata. A tale scopo, individuare il file rlauncher. config per ottenere il percorso del runtime di R e della directory di lavoro corrente. Si consiglia di creare e aprire una copia del file in modo da non modificare accidentalmente alcuna proprietà.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Per ottenere le versioni di R e RevoScaleR, aprire un prompt dei comandi di R o aprire il RGui associato all'istanza.

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

Sono disponibili diversi modi per ottenere la versione di Python. Il modo più semplice consiste nell'eseguire questa istruzione da Management Studio o da qualsiasi altro strumento di query SQL:

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

Se Machine Learning Services non è in esecuzione, è possibile determinare la versione di Python installata esaminando il file pythonlauncher. config. Si consiglia di creare e aprire una copia del file in modo da non modificare accidentalmente alcuna proprietà.

1. Solo per SQL Server 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. Ottenere il valore per **PYTHONHOME**.
3. Ottiene il valore della directory di lavoro corrente.

> [!NOTE]
> Se è stato installato Python e R in SQL Server 2017, la directory di lavoro e il pool di account di lavoro vengono condivisi per le lingue R e Python.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>Sono installate più istanze di R o Python?

Verificare se nel computer è installata più di una copia delle librerie R. Questa duplicazione può verificarsi se:

* Durante l'installazione si selezionano sia R Services (in-database) che R Server (standalone).
* Si installa Microsoft R Client oltre a SQL Server.
* Un set diverso di librerie R è stato installato con R Tools per Visual Studio, R Studio, Microsoft R Client o un altro IDE R.
* Il computer ospita più istanze di SQL Server e più di un'istanza USA Machine Learning.

Le stesse condizioni si applicano a Python.

Se si ritiene che siano installate più librerie o Runtime, assicurarsi di ottenere solo gli errori associati ai runtime di Python o R utilizzati dall'istanza di SQL Server.

## <a name="origin-of-errors"></a>Origine degli errori

Gli errori che si verificano quando si tenta di eseguire il codice R possono provenire da una qualsiasi delle origini seguenti:

* SQL Server motore di database, incluso il stored procedure sp_execute_external_script
* Launchpad attendibile SQL Server
* Altri componenti del Framework di estendibilità, inclusi i processi di avvio di R e Python e i processi satellite
* Provider, ad esempio Microsoft Open Database Connectivity (ODBC)
* Linguaggio R

Quando si lavora con il servizio per la prima volta, può essere difficile stabilire quali messaggi provengono dai servizi. Si consiglia di non solo acquisire il testo esatto del messaggio, ma il contesto in cui è stato visualizzato il messaggio. Si noti il software client che si sta usando per eseguire il codice di Machine Learning:

* Si sta usando Management Studio? Un'applicazione esterna?
* Si esegue il codice R in un client remoto o direttamente in un stored procedure?

## <a name="sql-server-log-files"></a>SQL Server file di log

Ottenere il log degli errori di SQL Server più recente. Il set completo di log degli errori è costituito dai file della seguente directory di log predefinita:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> Il nome esatto della cartella è diverso a seconda del nome dell'istanza.

## <a name="errors-returned-by-spexecuteexternalscript"></a>Errori restituiti da sp_execute_external_script

Ottenere il testo completo degli errori restituiti, se presenti, quando si esegue il comando sp_execute_external_script.

Per rimuovere i problemi di R o Python dalla considerazione, è possibile eseguire questo script, che avvia il runtime di R o Python e passa i dati avanti e indietro.

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

SQL Server genera log distinti per i runtime del linguaggio di script esterno. Questi errori non vengono generati dal linguaggio Python o R. Vengono generati dai componenti di estendibilità in SQL Server, inclusi i lanci specifici della lingua e i relativi processi satellite.

È possibile ottenere questi log dai percorsi predefiniti seguenti:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> Il nome esatto della cartella è diverso in base al nome dell'istanza. A seconda della configurazione, la cartella potrebbe trovarsi in un'unità diversa.

Ad esempio, i messaggi di log seguenti sono correlati al Framework di estendibilità:

* *LogonUser non riuscito per l'utente MSSQLSERVER01*
  
  Questo potrebbe indicare che gli account di lavoro che eseguono script esterni non possono accedere all'istanza.

* *InitializePhysicalUsersPool non riuscito*
  
  Questo messaggio potrebbe indicare che le impostazioni di sicurezza impediscono al programma di installazione di creare il pool di account di lavoro necessari per eseguire gli script esterni.

* *Inizializzazione gestione contesto di sicurezza non riuscita*

* *Inizializzazione di gestione sessioni satellite non riuscita*

## <a name="system-events"></a>Eventi di sistema

1. Aprire Windows Visualizzatore eventi, quindi cercare nel registro **eventi di sistema** i messaggi che includono la finestra di avvio della stringa.
2. Aprire il file ExtLaunchErrorlog e cercare la stringa *ErrorCode*. Esaminare il messaggio associato a ErrorCode.

I messaggi seguenti, ad esempio, sono errori di sistema comuni correlati all'SQL Server Framework di estendibilità:

* *Impossibile avviare il servizio Launchpad di SQL Server (MSSQLSERVER) a causa dell'errore seguente:<text>*

* *Il servizio non ha risposto tempestivamente alla richiesta di avvio o di controllo.*

* *È stato raggiunto un timeout (120000 millisecondi) durante l'attesa della connessione del servizio Launchpad di SQL Server (MSSQLSERVER).*

## <a name="dump-files"></a>File dump

Se si è a conoscenza del debug, è possibile usare i file di dump per analizzare un errore in Launchpad.

1. Individuare la cartella che contiene i log bootstrap del programma di installazione per SQL Server. Ad esempio, in SQL Server 2016, il percorso predefinito è C:\Programmi\Microsoft SQL Server\130\Setup Bootstrap\Log.
2. Aprire la sottocartella del log bootstrap specifica per l'estensibilità.
3. Se è necessario inviare una richiesta di supporto, aggiungere tutto il contenuto di questa cartella a un file compresso. Ad esempio, C:\Programmi\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
Il percorso esatto potrebbe variare nel sistema e potrebbe trovarsi in un'unità diversa dall'unità C. Assicurarsi di ottenere i log per l'istanza di in cui è installato Machine Learning.

## <a name="configuration-settings"></a>Impostazioni di configurazione

Questa sezione elenca i componenti o i provider aggiuntivi che possono costituire un'origine di errori durante l'esecuzione di script R o Python.

### <a name="what-network-protocols-are-available"></a>Quali protocolli di rete sono disponibili?

Machine Learning Services richiede i protocolli di rete seguenti per la comunicazione interna tra i componenti di estensibilità e per la comunicazione con client R o Python esterni.

* Named Pipes
* TCP/IP

Aprire Gestione configurazione SQL Server per determinare se un protocollo è installato e, se è installato, per determinare se è abilitato.

### <a name="security-configuration-and-permissions"></a>Configurazione e autorizzazioni di sicurezza

Per gli account di lavoro:

1. Nel pannello di controllo aprire **utenti e gruppi**e individuare il gruppo usato per eseguire i processi di script esterni. Per impostazione predefinita, il gruppo è **SQLRUserGroup**.
2. Verificare che il gruppo esista e che contenga almeno un account di lavoro.
3. In SQL Server Management Studio selezionare l'istanza in cui verranno eseguiti i processi di R o Python, selezionare **sicurezza**e quindi determinare se è presente un accesso per SQLRUserGroup.
4. Verificare le autorizzazioni per il gruppo di utenti.

Per gli account utente individuali:

1. Determinare se l'istanza supporta solo l'autenticazione in modalità mista, solo gli account di accesso SQL o l'autenticazione di Windows. Questa impostazione ha effetto sui requisiti del codice R o Python.
2. Per ogni utente che deve eseguire codice R, determinare il livello di autorizzazioni richiesto per ogni database in cui gli oggetti verranno scritti da R, sarà possibile accedere ai dati o verranno creati oggetti.
3. Per abilitare l'esecuzione di script, creare ruoli o aggiungere utenti ai ruoli seguenti, se necessario:

   - Tutto tranne *db_owner*: Richiedi Esegui qualsiasi SCRIPT esterno.
   - *db_datawriter*: Per scrivere i risultati da R o Python.
   - *db_ddladmin*: Per creare nuovi oggetti.
   - *db_datareader*: Per leggere i dati usati dal codice R o Python.
4. Si noti che gli account di avvio predefiniti sono stati modificati quando è stato installato SQL Server 2016.
5. Se un utente deve installare nuovi pacchetti R o usare pacchetti R installati da altri utenti, potrebbe essere necessario abilitare la gestione dei pacchetti nell'istanza e quindi assegnare autorizzazioni aggiuntive. Per altre informazioni, vedere [abilitare o disabilitare la gestione dei pacchetti R](r/r-package-how-to-enable-or-disable.md).

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>Quali cartelle sono soggette a blocco da software antivirus?

Il software antivirus può bloccare le cartelle, impedendo la configurazione delle funzionalità di machine learning e l'esecuzione corretta degli script. Determinare se le cartelle nella struttura ad albero SQL Server sono soggette a ricerca virus.

Tuttavia, quando si installano più servizi o funzionalità in un'istanza di, può essere difficile enumerare tutte le possibili cartelle utilizzate dall'istanza. Ad esempio, quando vengono aggiunte nuove funzionalità, è necessario identificare ed escludere le nuove cartelle.

Inoltre, alcune funzionalità creano nuove cartelle in modo dinamico in fase di esecuzione. Ad esempio, le tabelle di OLTP in memoria, le stored procedure e le funzioni creano le nuove directory in fase di esecuzione. Questi nomi di cartella contengono spesso GUID e non possono essere stimati. Il SQL Server Launchpad attendibile crea nuove directory di lavoro per i processi di script R e Python.

Poiché potrebbe non essere possibile escludere tutte le cartelle necessarie per il processo di SQL Server e le relative funzionalità, è consigliabile escludere l'intera struttura di directory dell'istanza di SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>Il firewall è aperto per SQL Server? L'istanza supporta le connessioni remote?

1. Per determinare se SQL Server supporta le connessioni remote, vedere [configurare le connessioni al server remoto](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Determinare se è stata creata una regola del firewall per SQL Server. Per motivi di sicurezza, in un'installazione predefinita, potrebbe non essere possibile per il client R o Python remoto connettersi all'istanza. Per ulteriori informazioni, vedere la pagina relativa [alla risoluzione dei problemi di connessione a SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="see-also"></a>Vedere anche

[Risolvere i problemi di Machine Learning in SQL Server](machine-learning-troubleshooting-faq.md)
