---
title: Problemi noti per l'integrazione di Python - servizi di SQL Server Machine Learning e linguaggio R
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/13/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6dc02c56bda3cdf904e0c53115d4fbbfcfafe9fc
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645526"
---
# <a name="known-issues-in-machine-learning-services"></a>Problemi noti di Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive i problemi noti o le limitazioni con componenti di apprendimento automatico che vengono fornite come opzione nel [SQL Server 2016 R Services](install/sql-r-services-windows-install.md) e [SQL Server 2017 Machine Learning Services con R e Python](install/sql-machine-learning-services-windows-install.md).

## <a name="setup-and-configuration-issues"></a>Problemi di installazione e configurazione

Per una descrizione dei processi e domande comuni correlate alla configurazione iniziale e la configurazione, vedere [domande frequenti su installazione e aggiornamento](r/upgrade-and-installation-faq-sql-server-r-services.md). Contiene informazioni sugli aggiornamenti, installazione side-by-side e l'installazione dei nuovi componenti di R o Python.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. Risultati incoerenti nei calcoli di MKL perché mancano variabile di ambiente

**Si applica a:** File binari R_SERVER 9.0, 9.1, 9.2 o 9.3.

R_SERVER Usa Intel Math Kernel Library (MKL). Per i calcoli che coinvolgono MKL, risultati incoerenti possono verificarsi se il sistema manca una variabile di ambiente. 

Impostare la variabile di ambiente `'MKL_CBWR'=AUTO` per garantire la riproducibilità numerica condizionale in R_SERVER. Per altre informazioni, vedere [Introduzione a condizionale numerici riproducibilità (CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr).

**Soluzione alternativa**

1. Nel Pannello di controllo, fare clic su **sistema e sicurezza** > **System** > **impostazioni di sistema avanzate**  >   **Le variabili di ambiente**.

2. Creare una nuova variabile di sistema o dell'utente. 

  + Nome della variabile set a 'MKL_CBWR'.
  + Impostare il valore' variabile' su 'AUTO'.

3. Riavviare R_SERVER. In SQL Server, è possibile riavviare il servizio Launchpad di SQL Server.

> [!NOTE]
> Se si esegue il 2019 anteprima di SQL Server in Linux, modificare o creare *file con estensione bash_profile* nella home directory utente, aggiungendo la riga `export MKL_CBWR="AUTO"`. Eseguire questo file digitando `source .bash_profile` un prompt dei comandi bash. Riavviare R_SERVER digitando `Sys.getenv()` al prompt dei comandi R.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. Errore di runtime dello Script R (SQL Server 2017 CU5-CU7 regressione)

Per SQL Server 2017, in aggiornamenti cumulativi da 5 a 7, è disponibile una regressione nel **rlauncher** file in cui il percorso del file directory temporanea include uno spazio. Questa regressione è stato corretto in CU8.

L'errore che verrà visualizzato quando si esegue lo script R include i messaggi seguenti:

> *Impossibile comunicare con il runtime per lo script 'R'. Verificare i requisiti del runtime di 'R'.*
>
> Messaggi STDERR dallo script esterno: 
>
> *Errore irreversibile: non è possibile creare 'R_TempDir'*

**Soluzione alternativa**

Applicare CU8 quando diventa disponibile. In alternativa, è possibile ricreare **rlauncher** eseguendo **registerrext** con disinstallare/installare in un prompt dei comandi con privilegi elevati. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

L'esempio seguente mostra i comandi con l'istanza predefinita "MSSQL14. Installato MSSQLSERVER"in" c:\Programmi\Microsoft SQL Server\":

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. Non è possibile installare le funzionalità di SQL Server machine learning in un controller di dominio

Se si tenta di installare SQL Server 2016 R Services o Machine Learning Services di SQL Server 2017 in un controller di dominio, il programma di installazione ha esito negativo, con questi errori:

> *Si è verificato un errore durante l'installazione della funzionalità*
> 
> *Impossibile trovare gruppo con identità*
> 
> *Codice di errore componente: 0x80131509*

L'errore si verifica perché, in un controller di dominio, il servizio non è possibile creare gli account locali 20 necessari per eseguire l'apprendimento automatico. In generale, non è consigliabile installare SQL Server in un controller di dominio. Per altre informazioni, vedere [bollettino supporto 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Installare la versione più recente del servizio per garantire la compatibilità con Microsoft R Client

Se si installa la versione più recente di Microsoft R Client e usarlo per eseguire R in SQL Server in un contesto di calcolo remoto, è possibile ottenere un errore simile al seguente:

> *Si sta usando il computer che non è compatibile con Microsoft R Server versione 8.x.x 9.x.x versione di Microsoft R Client. Download and install a compatible version.* (Sul computer è in esecuzione la versione 9.0.0 di Microsoft R, che non è compatibile con Microsoft R Server versione 8.0.3. Scaricare e installare una versione compatibile.)

SQL Server 2016 richiede che le librerie di R nel client corrispondano esattamente le librerie di R nel server. La limitazione è stata rimossa per le versioni successive a R Server 9.0.1. Tuttavia, se si verifica questo errore, verificare la versione delle librerie di R che viene usata dai client e del server e, se necessario, aggiorna il client in modo da corrispondere la versione del server.

La versione di R installata con SQL Server R Services viene aggiornata ogni volta che viene installata una versione del servizio SQL Server. Per assicurarsi di avere sempre le versioni più aggiornate dei componenti R, assicurarsi di installare tutti i service pack.

Per garantire la compatibilità con Microsoft R Client 9.0.0, installare gli aggiornamenti descritti in questo [articolo del supporto tecnico](https://support.microsoft.com/kb/3210262).

Per evitare problemi con i pacchetti di R, è inoltre possibile aggiornare la versione delle librerie di R che vengono installati nel server, modificando il contratto di servizio per usare i criteri di supporto del ciclo di vita moderni, come descritto in [nella sezione successiva](#bkmk_sqlbindr). Quando si esegue questa operazione, la versione di R installata con SQL Server viene aggiornata in base alla stessa pianificazione usato per gli aggiornamenti di machine Learning Server (in precedenza Microsoft R Server).

**Si applica a:** SQL Server 2016 R Services, con R Server versione 9.0.0 o versioni precedenti

### <a name="5-r-components-missing-from-cu3-setup"></a>5. Componenti R mancante dal programma di installazione CU3

Sono stati eseguito il provisioning di un numero limitato di macchine virtuali di Azure senza i file di installazione di R che devono essere inclusi in SQL Server. Il problema si applica alle macchine virtuali sottoposte a provisioning nel periodo 2018-01-05-2018-01-23. Questo problema potrebbe influire sulle installazioni locali, se è applicato l'aggiornamento CU3 per SQL Server 2017 durante il periodo di da 2018 01 05 2018-01-23.

Una versione del servizio è stata fornita che include la versione corretta dei file di installazione di R.

+ [Il pacchetto di aggiornamento cumulativo 3 per SQL Server 2017 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

Per installare i componenti e ripristinare SQL Server 2017 CU3, è necessario disinstallare CU3 e reinstallare la versione aggiornata:

1. Scaricare il file di installazione CU3 aggiornato, che include i programmi di installazione di R.
2. Disinstallare CU3. Nel Pannello di controllo, cercare **disinstallare un aggiornamento**e quindi selezionare "Hotfix 3015 per SQL Server 2017 (KB4052987) (64 bit)". Procedere con la procedura di disinstallazione.
3. Reinstallare l'aggiornamento CU3, facendo doppio clic sull'aggiornamento per KB4052987 appena scaricato: `SQLServer2017-KB4052987-x64.exe`. Seguire le istruzioni di installazione.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. Non è possibile installare i componenti Python in installazioni non in linea di SQL Server 2017 CTP 2.0 o versione successiva

Se si installa una versione non definitiva di SQL Server 2017 in un computer senza accesso a internet, il programma di installazione potrebbe non riuscire a visualizzare la pagina che richiede il percorso dei componenti di Python scaricati. In tal caso, è possibile installare la funzionalità di servizi di Machine Learning, ma non i componenti Python.

Questo problema viene risolto nella versione di rilascio. Inoltre, questa limitazione non si applica ai componenti di R.

**Si applica a:** SQL Server 2017 con Python

### <a name="bkmk_sqlbindr"></a> Avviso di versione non compatibile quando ci si connette a una versione precedente di SQL Server R Services da un client usando [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Quando si esegue codice R nel contesto di calcolo di un server SQL Server 2016, è possibile visualizzare l'errore seguente:

> *Si esegue la versione 9.0.0 di Microsoft R Client nel computer, non è compatibile con Microsoft R Server versione 8.0.3. Download and install a compatible version.* (Sul computer è in esecuzione la versione 9.0.0 di Microsoft R, che non è compatibile con Microsoft R Server versione 8.0.3. Scaricare e installare una versione compatibile.)

Questo messaggio viene visualizzato se una delle due istruzioni seguenti è vera,

+ Si è installato R Server (Standalone) in un computer client mediante Installazione guidata di [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
+ È stato installato Microsoft R Server usando il [separare programma di installazione di Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Per garantire che il server e client usino la stessa versione potrebbe essere necessario usare _associazione_, supportato per Microsoft R Server 9.0 e versioni successive aggiornare i componenti di R in istanze di SQL Server 2016. Per determinare se il supporto per gli aggiornamenti è disponibile per la versione di R Services, vedere [aggiorna un'istanza di R Services tramite SqlBindR.exe](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

**Si applica a:** SQL Server 2016 R Services, con R Server versione 9.0.0 o versioni precedenti

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. Durante l'installazione di alcune versioni del servizio SQL Server 2016 è possibile che le versioni più recenti dei componenti R non vengano installate

Quando si installa un aggiornamento cumulativo o installare un service pack per SQL Server 2016 in un computer che non è connesso a internet, l'installazione guidata non venga visualizzato il prompt che consente di aggiornare i componenti di R usando i file CAB scaricati. In genere questo errore si verifica quando sono stati installati più componenti insieme al motore di database.

In alternativa, è possibile installare la versione del servizio tramite la riga di comando e specificando la `MRCACHEDIRECTORY` argomento, come illustrato in questo esempio, che installa gli aggiornamenti CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Per ottenere i programmi di installazione più recente, vedere [installa i componenti di apprendimento automatico senza accesso a internet](install/sql-ml-component-install-without-internet-access.md).

**Si applica a:** SQL Server 2016 R Services, con R Server versione 9.0.0 o versioni precedenti

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. Il servizio LaunchPad non viene avviato se la versione è diversa dalla versione di R

Se si installa SQL Server R Services separatamente dal motore di database e le versioni di compilazione sono diverse, si potrebbe essere visualizzato l'errore seguente nel registro eventi di sistema:

> *Il servizio Launchpad di SQL Server non è stato possibile avviare a causa dell'errore seguente: Il servizio non ha risposto alla richiesta di avvio o di controllo in modo tempestivo.*

Ad esempio, questo errore potrebbe verificarsi se si installa il motore di database usando la versione di rilascio, applicare una patch per aggiornare il motore di database e quindi aggiungere la funzionalità R Services tramite la versione di rilascio.

Per evitare questo problema, usare un'utilità, ad esempio Gestione File per confrontare le versioni di Launchpad.exe con la versione dei file binari SQL, ad esempio sqldk.dll. Tutti i componenti devono avere lo stesso numero di versione. Se si aggiorna un componente, assicurarsi di applicare lo stesso aggiornamento a tutti gli altri componenti installati.

Cercare nel Launchpad di `Binn` cartella per l'istanza. Ad esempio, in un'installazione predefinita di SQL Server 2016, il percorso potrebbe essere `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. Contesti di calcolo remoti siano bloccati da un firewall nelle istanze di SQL Server in esecuzione su macchine virtuali di Azure

Se è stato installato [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] in una macchina virtuale Windows Azure, potrebbe non essere in grado di usare i contesti di calcolo che richiedono l'uso dell'area di lavoro della macchina virtuale. Il motivo è che, per impostazione predefinita, il firewall nelle macchine virtuali di Azure include una regola che blocca accesso alla rete per gli account utente R locali.

In alternativa, nella VM di Azure, aprire **Windows Firewall con sicurezza avanzata**, selezionare **regole connessioni in uscita**e disabilitare la regola seguente: **Bloccare l'accesso alla rete per gli account utente locale di R in SQL Server instance MSSQLSERVER**. È anche possibile lasciare la regola attivata, ma modificare la proprietà di sicurezza in **Consenti connessioni sicure**.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. Autenticazione implicita in SQLEXPRESS

Quando si eseguono processi R da una workstation di analisi scientifica dei dati remota tramite l'autenticazione di Windows integrata, SQL Server viene utilizzato *l'autenticazione implicita* per generare eventuali chiamate ODBC locali che potrebbero essere richiesti dallo script. Questa funzionalità, tuttavia, non funziona nella build RTM di SQL Server Express Edition.

Per risolvere il problema, è consigliabile eseguire l'aggiornamento a una versione più recente del servizio.

Se l'aggiornamento non è fattibile, risolvere il problema, usare un account di accesso SQL per eseguire processi R remoti che potrebbero richiedere chiamate ODBC incorporate.

**Si applica a:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. Limiti delle prestazioni quando vengono chiamate librerie usate da SQL Server da altri strumenti

È possibile chiamare le librerie di machine learning che vengono installate per SQL Server da un'applicazione esterna, ad esempio RGui. In questo modo potrebbe essere il modo più semplice per eseguire determinate attività, ad esempio nuovi pacchetti di installazione o esecuzione di test ad hoc su molto brevi esempi di codice. Tuttavia, all'esterno di SQL Server, potrebbe risultare limitato. 

Ad esempio, anche se si utilizza SQL Server Enterprise Edition, R viene eseguito in modalità a thread singolo quando si esegue il codice R usando strumenti esterni. Per ottenere i vantaggi delle prestazioni in SQL Server, avviare una connessione di SQL Server e utilizzare [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per chiamare il runtime dello script esterno.

In generale, evitare di chiamare le librerie di machine learning che vengono usate da SQL Server da strumenti esterni. Se è necessario debug R o Python code, è in genere più semplice eseguire questa operazione di fuori di SQL Server. Per ottenere le stesse librerie che sono in SQL Server, è possibile installare Microsoft R Client [Machine Learning Server (Standalone) di SQL Server 2017](install/sql-machine-learning-standalone-windows-install.md), o [SQL Server 2016 R Server (Standalone)](install/sql-r-standalone-windows-install.md).

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools non supporta le autorizzazioni necessarie per gli script esterni

Quando si usa Visual Studio o SQL Server Data Tools per pubblicare un progetto di database, se qualsiasi entità dispone di autorizzazioni specifiche per l'esecuzione di script esterni, è possibile ottenere un errore simile alla seguente:

> *Modello di TSQL: Errore rilevato durante la decodificazione del database. L'autorizzazione non è stata riconosciuta e non è stato importato.*

Il modello DACPAC non supporta attualmente le autorizzazioni usate da R Services o i servizi di Machine Learning, ad esempio GRANT ANY EXTERNAL SCRIPT o EXECUTE ANY EXTERNAL SCRIPT. Questo problema verrà risolto in una versione futura.

In alternativa, eseguire la concessione di ulteriore istruzioni in uno script di post-distribuzione.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. L'esecuzione di script esterni è limitata a causa di valori predefiniti di governance delle risorse

In Enterprise Edition è possibile usare pool di risorse per gestire processi di script esterni. In alcune build di versione iniziali, la memoria massima che è stato possibile allocare ai processi R è il 20%. Pertanto, se il server ha 32 GB di RAM, gli eseguibili di R (RTerm.exe e BxlServer.exe) è stato possibile usare un massimo di 6,4 GB in un'unica richiesta.

Se si verificano i limiti delle risorse, controllare il valore predefinito. Se il 20% non è sufficiente, vedere la documentazione per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] su come modificare questo valore.

**Si applica a:** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>Problemi di esecuzione degli script R

In questa sezione contiene i problemi noti che sono specifici per l'esecuzione di R in SQL Server, nonché alcuni problemi relativi alle librerie di R e strumenti pubblicati da Microsoft, tra cui RevoScaleR.

Per altri problemi noti che potrebbero influire sulle soluzioni R, vedere la [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) sito.

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. Accesso negato avviso durante l'esecuzione di script R in SQL Server in un percorso non predefinito

Se l'istanza di SQL Server è stato installato in un percorso non predefinito, ad esempio all'esterno di `Program Files` cartella, l'avviso ACCESS_DENIED viene generato quando si prova a eseguire gli script che installa un pacchetto. Ad esempio:

> *In `normalizePath(path.expand(path), winslash, mustWork)` : percorso [2] = "~ExternalLibraries/R/8/1": Accesso negato*

Il motivo è che tenta di leggere il percorso di una funzione R e ha esito negativo se il gruppo users predefinito **SQLRUserGroup**, non dispone dell'accesso in lettura. L'avviso che viene generato non blocca l'esecuzione dello script R corrente, ma potrebbe ricorrere più volte il messaggio di avviso ogni volta che l'utente esegue qualsiasi altro script R.

Se è stato installato SQL Server nel percorso predefinito, questo errore si verifica, perché le autorizzazioni di lettura in tutti gli utenti di Windows il `Program Files` cartella.

Questo problema ia risolto in una versione futura del servizio. In alternativa, specificare il gruppo **SQLRUserGroup**, con accesso in lettura per tutte le cartelle padre di `ExternalLibraries`.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. Errore di serializzazione tra le versioni precedenti e nuove di RevoScaleR

Quando si passa un modello usando un formato serializzato a un'istanza remota di SQL Server, si potrebbe essere visualizzato l'errore: 

> *Errore nel memDecompress (dati, tipo = decomprimere) Errore interno -3 nel memDecompress(2).*

Questo errore viene generato se è stato salvato il modello utilizzando una versione aggiornata della funzione di serializzazione [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), ma l'istanza di SQL Server in cui si deserializzare il modello a dispone di una versione precedente delle APIs RevoScaleR, da SQL Server 2017 CU2 o versione precedente.

In alternativa, è possibile aggiornare l'istanza di SQL Server 2017 CU3 o successiva.

L'errore non viene visualizzata se la versione dell'API è lo stesso, o se si sta spostando un modello salvato con una funzione di serializzazione precedente a un server che usa una versione più recente dell'API di serializzazione.

In altre parole, usare la stessa versione di RevoScaleR per le operazioni di serializzazione e deserializzazione.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>3. Assegnazione dei punteggi in tempo reale non gestisce correttamente i _learningRate_ parametro nei modelli di struttura ad albero e della foresta

Se si crea un modello usando un albero delle decisioni o un metodo di foresta delle decisioni e specifica la velocità di apprendimento, si possono ottenere risultati incoerenti quando si usa `sp_rxpredict` o il codice SQL `PREDICT` (funzione), invece del `rxPredict`.

E la causa un errore nell'API che modella i processi serializzati, viene limitata al `learningRate` parametri: ad esempio, in [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees), o

Questo problema viene risolto in una versione futura del servizio.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. Limitazioni relative all'affinità processori per i processi R

Nella compilazione di rilascio iniziale di SQL Server 2016, è possibile impostare l'affinità processori solo per le CPU del primo gruppo k. Ad esempio, se il server è un computer a 2 socket con due gruppi k, per i processi R sono usati solo processori appartenenti il primo gruppo k. La stessa limitazione si applica quando si configura la governance delle risorse per processi di script R.

Questo problema è stato risolto in SQL Server 2016 Service Pack 1. È consigliabile eseguire l'aggiornamento alla versione più recente del servizio.

**Si applica a:** Versione RTM di SQL Server 2016 R Services

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5. Non è possibile apportare modifiche ai tipi di colonna durante la lettura di dati in un contesto di calcolo di SQL Server

Se il contesto di calcolo è impostato sull'istanza di SQL Server, non è possibile usare l'argomento _colClasses_ (o altri argomenti simili) per modificare il tipo di dati delle colonne presenti nel codice R.

L'istruzione seguente, ad esempio, causerebbe un errore se la colonna CRSDepTimeStr non fosse già un numero intero:

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

In alternativa, è possibile riscrivere la query SQL per usare CAST o CONVERT e presentare i dati in R usando il tipo di dati corretto. In generale, le prestazioni sono migliori quando si utilizzano i dati usando SQL anziché modificando i dati nel codice R.

**Si applica a:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. Limiti sulle dimensioni dei modelli serializzati

Quando si salva un modello in una tabella di SQL Server, è necessario serializzare il modello e salvarlo in un formato binario. In teoria le dimensioni massime di un modello che è possibile archiviare con questo metodo sono 2 GB, ovvero la dimensione massima delle colonne varbinary in SQL Server.

Se è necessario usare i modelli di dimensioni maggiori, sono disponibili soluzioni alternative seguenti:

+ Eseguire operazioni per ridurre le dimensioni del modello. Alcuni pacchetti R open source includono una grande quantità di informazioni nell'oggetto modello e molte di queste informazioni può essere rimossi per la distribuzione. 
+ Utilizzare selezione delle caratteristiche per rimuovere le colonne non necessarie.
+ Se si usa un algoritmo open source, prendere in considerazione un'implementazione simile usando l'algoritmo corrispondente in MicrosoftML o RevoScaleR. Questi pacchetti sono stati ottimizzati per scenari di distribuzione.
+ Dopo che il modello è stato razionalizzato e le dimensioni ridotte seguendo i passaggi precedenti, verificare se il [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) funzione r di base può essere utilizzata per ridurre le dimensioni del modello prima di passarlo a SQL Server. Questa opzione è consigliata quando il modello è prossimo al limite di 2 GB.
+ Per i modelli di dimensioni maggiori, è possibile usare SQL Server [FileTable](../relational-databases/blob/filetables-sql-server.md) funzionalità per archiviare i modelli, anziché utilizzare una colonna varbinary.

    Per usare le tabelle Filetable, è necessario aggiungere un'eccezione del firewall, perché i dati archiviati in tabelle Filetable sono gestiti dal driver del file System di Filestream in SQL Server e le regole del firewall predefinite bloccare l'accesso ai file di rete. Per altre informazioni, vedere [abilitare i prerequisiti per la tabella FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md).

    Dopo avere abilitato la tabella FileTable, per scrivere il modello, si ottiene un percorso da SQL usando l'API tabelle FileTable e quindi scrittura il modello in tale posizione dal codice. Quando è necessario leggere il modello, ottenere il percorso da SQL e quindi chiamare il modello usando il percorso dello script di. Per altre informazioni, vedere [accedere alle tabelle Filetable con API File di Input / Output](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7. Non deselezionare le aree di lavoro quando si esegue codice R in un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contesto di calcolo

Se si usa un comando di R per cancellare l'area di lavoro degli oggetti durante l'esecuzione di codice R in un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contesto di calcolo o se si deseleziona l'area di lavoro come parte di uno script R chiamato tramite [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), si verifichi questo errore : *revoScriptConnection oggetto dell'area di lavoro non trovata*

`revoScriptConnection` è un oggetto dell'area di lavoro R che contiene informazioni su una sessione R chiamata da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se, tuttavia, il codice R include un comando per cancellare i dati dell'area di lavoro, ad esempio `rm(list=ls()))`, anche tutte le informazioni relative alla sessione e altri oggetti presenti nell'area di lavoro R vengono cancellati.

In alternativa, evitare indiscriminato variabili e altri oggetti mentre in esecuzione R in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Anche se l'area di lavoro di cancellazione è comune quando si lavora nella console di R, può avere conseguenze impreviste.

* Per eliminare variabili specifiche, usare l'oggetto R `remove` funzione: ad esempio, `remove('name1', 'name2', ...)`
* Se devono essere eliminate più variabili, salvare i nomi delle variabili temporanee in un elenco ed eseguire periodicamente operazioni di Garbage Collection.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. Limitazioni sui dati che possono essere forniti come input per uno script R

Non è possibile usare in uno script R i tipi seguenti di risultati delle query:

- Dati da una query [!INCLUDE[tsql](../includes/tsql-md.md)] che fa riferimento alle colonne AlwaysEncrypted.
  
- Dati da una query [!INCLUDE[tsql](../includes/tsql-md.md)] che fa riferimento alle colonne mascherate.
  
     Se è necessario usare dati mascherati in uno script R, una possibile soluzione consiste nel creare una copia dei dati in una tabella temporanea e usare invece tali dati.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. Uso di stringhe come fattori che possono determinare un peggioramento delle prestazioni

Utilizzo di variabili di tipo string come fattori possono aumentare notevolmente la quantità di memoria utilizzata per le operazioni R. Si tratta in genere un problema noto con R e sono disponibili molti articoli sull'argomento. Ad esempio, vedere [fattori non sono elementi di primaria importanza in R, di John montaggio, in R blogger)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) o [stringsAsFactors: Una biografia non autorizzata, da Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Anche se il problema non è specifico di SQL Server, può influire notevolmente sulle prestazioni del codice R eseguito in SQl Server. Le stringhe vengono in genere archiviate come varchar o nvarchar e se una colonna di dati stringa contenga molti valori univoci, il processo di conversione internamente questi valori integer e nuovamente in stringhe da R può anche causare errori di allocazione di memoria.

Se non è assolutamente necessario un tipo di dati stringa per le altre operazioni, mapping dei valori di stringa a un valore numerico (integer) tipo di dati come parte della preparazione dei dati può essere vantaggioso dal punto di vista delle prestazioni e scalabilità.

Per una discussione di questo problema e per altri suggerimenti, vedere [prestazioni per R Services - ottimizzazione dei dati](r/r-and-data-optimization-r-services.md).

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. Gli argomenti *varsToKeep* e *varsToDrop* non sono supportati per le origini dati di SQL Server

Quando si utilizza la funzione rxDataStep per scrivere i risultati in una tabella, usando il *varsToKeep* e *varsToDrop* è un modo pratico per specificare le colonne da includere o escludere durante l'operazione. Tuttavia, questi argomenti non sono supportati per le origini dati di SQL Server.

### <a name="11-limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>11. Supporto limitato per i tipi di dati SQL in sp\_execute\_esterni\_script

Non tutti i tipi di dati che sono supportati in SQL possono essere usati in R. In alternativa, prendere in considerazione il cast di tipo di dati non supportata su un tipo di dati supportati prima di passare i dati da sp\_execute\_esterni\_script.

Per altre informazioni, vedere [tipi di dati e le librerie R](r/r-libraries-and-data-types.md).

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Possibile danneggiamento della stringa usando le stringhe unicode in colonne varchar

Il passaggio di dati unicode nelle colonne varchar da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] può causare il danneggiamento della stringa da R o Python. Ciò è dovuto alla codifica per questi stringa unicode in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] le regole di confronto potrebbe non corrispondere a con la codifica predefinita UTF-8 usati in R o Python. 

Inviare eventuali dati di tipo stringa non ASCII [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da R o Python, usare la codifica UTF-8 (disponibile in [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) o usare nvarchar tipo per lo stesso.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>13. Un solo valore di tipo `raw` può essere restituito da `sp_execute_external_script`

Quando un tipo di dati binari (R **raw** tipo di dati) viene restituito da R, il valore deve essere inviato nel frame di dati di output.

Con dati di tipi diversi da **raw**, è possibile restituire i valori dei parametri e i risultati della stored procedure aggiungendo la parola chiave OUTPUT. Per altre informazioni, vedere [parametri](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Se si desidera utilizzare più set di output che includono valori di tipo **raw**, una possibile soluzione alternativa è eseguire più chiamate della stored procedure o per inviare il risultato imposta nuovamente lo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite ODBC.

### <a name="14-loss-of-precision"></a>14. Perdita di precisione

Poiché [!INCLUDE[tsql](../includes/tsql-md.md)] e R supportano diversi tipi di dati, tipi di dati numerici possono subire una perdita di precisione durante la conversione.

Per altre informazioni sulla conversione implicita del tipo di dati, vedere [tipi di dati e le librerie R](r/r-libraries-and-data-types.md).

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. Variabile di errore dell'ambito quando si usa il parametro transformFunc

Per trasformare i dati mentre si modellano, è possibile passare un *transformFunc* argomento di una funzione, ad esempio `rxLinmod` o `rxLogit`. Tuttavia, le chiamate di funzione annidata possono causare errori di ambito nel contesto di calcolo di SQL Server, anche se le chiamate funzionano correttamente nel contesto di calcolo locale.

> *Il set di dati di esempio per l'analisi non dispone di variabili*

Ad esempio, si supponga che due funzioni, è stata definita `f` e `g`, nell'ambiente globale locale, e `g` chiamate `f`. Nelle chiamate che coinvolgono remote o distribuite `g`, la chiamata a `g` potrebbe non riuscire con l'errore, perché `f` non viene trovato, anche se sono stati passati `f` e `g` alla chiamata remota.

Se si verifica questo problema, è possibile risolverlo incorporando la definizione di `f` all'interno della definizione di `g`, in qualsiasi punto prima che `g` chiamerebbe normalmente `f`.

Ad esempio:

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

Per evitare l'errore, riscrivere la definizione come indicato di seguito:

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16. Importazione e modifica dei dati con RevoScaleR

Quando **varchar** colonne vengono letti da un database, lo spazio vuoto viene rimosso. Per evitare questo problema, racchiudere le stringhe tra caratteri che non siano spazi vuoti.

Quando le funzioni come `rxDataStep` vengono usati per creare tabelle di database che hanno **varchar** colonne, la larghezza della colonna viene stimata in base a un campione di dati. Se la larghezza può variare, potrebbe essere necessario riempire tutte le stringhe a una lunghezza comune.

L'uso di una trasformazione per modificare il tipo di dati di una variabile non è supportato quando si usano chiamate ripetute a `rxImport` o a `rxTextToXdf` per importare e aggiungere righe, combinando più file di input in un singolo file XDF.

### <a name="17-limited-support-for-rxexec"></a>17. Supporto limitato per rxExec

In SQL Server 2016, il `rxExec` funzione che viene fornito per RevoScaleR pacchetto può essere usato solo in modalità a thread singolo.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. Aumentare la dimensione massima dei parametri per supportare rxGetVarInfo

Se si utilizzano set di dati con un numero estremamente elevato di variabili (ad esempio, oltre 40.000), impostare il `max-ppsize` flag all'avvio R per usare le funzioni, ad esempio `rxGetVarInfo`. Il flag `max-ppsize` specifica le dimensioni massime dello stack di protezione dell'indicatore di misura.

Se si usa la console di R (ad esempio, RGui.exe o RTerm.exe), è possibile impostare il valore di _max-ppsize_ su 500000 digitando:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. Problemi con la funzione rxDTree

La funzione `rxDTree` attualmente non supporta le trasformazioni nella formula. In particolare, l'uso della sintassi `F()` per la creazione di fattori in tempo reale non è supportata. Tuttavia, i dati numerici vengano automaticamente inserita in contenitori.

I fattori ordinati vengono trattati proprio come i fattori in tutte le funzioni di analisi RevoScaleR eccetto `rxDTree`.

## <a name="python-script-execution-issues"></a>Problemi di esecuzione degli script di Python

In questa sezione contiene i problemi noti che sono specifici per l'esecuzione di Python in SQL Server, nonché i problemi relativi ai pacchetti Python pubblicati da Microsoft, tra cui [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. Chiamata al modello con training preliminare ha esito negativo se al modello di percorso è troppo lungo

Se i modelli con training preliminare è stato installato in una versione preliminare di SQL Server 2017, il percorso completo del file di modello con training potrebbe essere troppo lungo per Python da leggere. Questa limitazione è stato risolto in una versione più recente del servizio.

Esistono diversi potenziali soluzioni alternative: 

+ Quando si installa i modelli con training preliminare, scegliere un percorso personalizzato.
+ Se possibile, installare l'istanza di SQL Server in un percorso di installazione personalizzata con un percorso più breve, ad esempio C:\SQL\MSSQL14. MSSQLSERVER.
+ Usare l'utilità di Windows [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) per creare un collegamento che esegue il mapping a un percorso più breve il file del modello.
+ Aggiornamento alla versione del servizio più recente.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. Errore durante il salvataggio serializzata del modello a SQL Server

Quando si passa un modello a un'istanza remota di SQL Server e tentare di leggere il modello binario usando il `rx_unserialize` funzionare [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), si potrebbe essere visualizzato l'errore: 

> *NameError: rx_unserialize_model' name' non è definito*

Questo errore viene generato se è stato salvato il modello utilizzando una versione aggiornata della funzione di serializzazione, ma l'istanza di SQL Server in cui si esegue la deserializzazione il modello non riconosce l'API di serializzazione.

Per risolvere il problema, aggiornare l'istanza di SQL Server 2017 CU3 o successiva.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. Errore di inizializzazione di una variabile varbinary provoca un errore di BxlServer

Se si esegue codice Python in SQL Server usando `sp_execute_external_script`e il codice ha un output le variabili di tipo varbinary (max), varchar (max) o tipi simili, la variabile deve essere inizializzata o impostata come parte dello script. In caso contrario, il componente di scambio di dati, BxlServer, genera un errore e smette di funzionare.

Questa limitazione verrà risolto in una versione futura del servizio. Come risolvere il problema, assicurarsi che la variabile viene inizializzata nello script Python. Qualsiasi valore valido può essere utilizzato, come negli esempi seguenti:

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N'b = 0x0'
  , @params = N'@b varbinary(max) OUTPUT'
  , @b = @b OUTPUT;
go
```

```sql
declare @b varchar(30);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N' b = ""  '
  , @params = N'@b varchar(30) OUTPUT'
  , @b = @b OUTPUT;
go
```

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. Avviso di dati di telemetria dopo l'esecuzione di codice Python

A partire da SQL Server 2017 CU2, potrebbe essere visualizzato il seguente messaggio anche se il codice Python in caso contrario, viene eseguito correttamente:

> *Messaggi STDERR dallo script esterno:*
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state è utilizzato prima della dichiarazione globale*


Questo problema è stato risolto in SQL Server 2017 Cumulative Update 3 (CU3). 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open

Questa sezione elenca i problemi specifici di connettività di R, lo sviluppo e strumenti per le prestazioni forniti da Revolution Analitica. Questi strumenti erano inclusi nelle versioni definitive precedenti di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

In generale, è consigliabile disinstallare queste versioni precedenti e installare la versione più recente di SQL Server o Microsoft R Server.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. Revolution R Enterprise non è supportato

Installare Revolution R Enterprise by side con le versioni di [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] non è supportato.

Se si dispone di una licenza esistente per Revolution R Enterprise, è necessario inserirla in un computer separato da entrambi i [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] istanza e qualsiasi workstation che si desidera usare per connettersi al [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] istanza.

Alcune versioni non definitive di [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluso un ambiente di sviluppo R per Windows che è stato creato da Revolution Analitica. Questo strumento non viene più fornito e non è supportato.

Per garantire la compatibilità con [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], si consiglia di installare Microsoft R Client. [R Tools per Visual Studio](https://www.visualstudio.com/vs/rtvs/) e [Visual Studio Code](https://code.visualstudio.com/) supporta anche le soluzioni di Microsoft R.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. Problemi di compatibilità con il driver ODBC di SQLite e RevoScaleR

Revisione 0.92 del driver ODBC di SQLite è incompatibile con RevoScaleR. Le revisioni 0.88-0.91 e 0.93 e le versioni successive per essere compatibili.

## <a name="see-also"></a>Vedere anche

[Novità di SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Risoluzione dei problemi di apprendimento automatico in SQL Server](machine-learning-troubleshooting-faq.md)
