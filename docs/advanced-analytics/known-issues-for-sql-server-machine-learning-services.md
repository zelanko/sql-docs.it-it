---
title: Problemi noti per Python e R
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8cf0441397c8c3a6d743b08692a6d2bac289a03f
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176196"
---
# <a name="known-issues-in-sql-server-machine-learning-services"></a>Problemi noti in SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive i problemi noti o le limitazioni con i componenti di Machine Learning forniti come opzione in [SQL Server Machine Learning Services](what-is-sql-server-machine-learning.md) e [SQL Server 2016 R Services](r/sql-server-r-services.md).

## <a name="setup-and-configuration-issues"></a>Problemi di installazione e configurazione

Per una descrizione dei processi e delle domande comuni correlate all'installazione e alla configurazione iniziali, vedere [domande frequenti sull'installazione](r/upgrade-and-installation-faq-sql-server-r-services.md)e sull'aggiornamento. Contiene informazioni sugli aggiornamenti, l'installazione side-by-side e l'installazione di nuovi componenti R o Python.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. Risultati incoerenti nei calcoli MKL a causa della variabile di ambiente mancante

**Si applica a:** R_SERVER binari 9,0, 9,1, 9,2 o 9,3.

R_SERVER usa Intel Math Kernel Library (MKL). Per i calcoli che coinvolgono MKL, è possibile che si verifichino risultati incoerenti se nel sistema manca una variabile di ambiente. 

Impostare la variabile `'MKL_CBWR'=AUTO` di ambiente per garantire la riproducibilità numerica condizionale in r_server. Per ulteriori informazioni, vedere [Introduzione alla riproducibilità numerica condizionale (CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr).

**Soluzione alternativa**

1. Nel pannello di controllo fare clic su sistema **e sicurezza** > **sistema** > **Impostazioni** > di sistema avanzate**variabili di ambiente**.

2. Creare un nuovo utente o una variabile di sistema. 

  + Impostare il nome della variabile su' MKL_CBWR '.
  + Imposta "valore variabile" su "AUTO".

3. Riavviare R_SERVER. In SQL Server è possibile riavviare Launchpad di SQL Server servizio.

> [!NOTE]
> Se si esegue l'anteprima SQL Server 2019 in Linux, modificare o creare *. bash_profile* nella home directory dell'utente, aggiungendo la riga `export MKL_CBWR="AUTO"`. Eseguire questo file digitando `source .bash_profile` al prompt dei comandi di Bash. Riavviare r_server digitando `Sys.getenv()` al prompt dei comandi di R.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. Errore di Runtime script R (SQL Server 2017 regressione CU5-CU7)

Per SQL Server 2017, negli aggiornamenti cumulativi da 5 a 7, esiste una regressione nel file **rlauncher. config** , dove il percorso del file di directory temporanea include uno spazio. Questa regressione viene corretta in CU8.

L'errore che verrà visualizzato quando si esegue lo script R include i messaggi seguenti:

> *Non è possibile comunicare con il runtime per lo script ' R '. Verificare i requisiti del runtime di ' R '.*
>
> Messaggi STDERR dallo script esterno: 
>
> *Errore irreversibile: non è possibile creare ' R_TempDir '*

**Soluzione alternativa**

Applicare CU8 quando diventerà disponibile. In alternativa, è possibile ricreare **rlauncher. config** eseguendo **registerrext** con Uninstall/install in un prompt dei comandi con privilegi elevati. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

Nell'esempio seguente vengono illustrati i comandi con l'istanza predefinita "MSSQL14. MSSQLSERVER "installato in" C:\Programmi\Microsoft SQL Server\":

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. Non è possibile installare SQL Server funzionalità di Machine Learning in un controller di dominio

Se si tenta di installare SQL Server 2016 R Services o SQL Server Machine Learning Services in un controller di dominio, il programma di installazione non riesce, con gli errori seguenti:

> *Si è verificato un errore durante il processo di installazione della funzionalità*
> 
> *Impossibile trovare il gruppo con identità*
> 
> *Codice errore componente: 0x80131509*

L'errore si verifica perché, in un controller di dominio, il servizio non è in grado di creare i 20 account locali necessari per eseguire Machine Learning. In generale, non è consigliabile installare SQL Server in un controller di dominio. Per ulteriori informazioni, vedere il [Bollettino del supporto 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Installare la versione del servizio più recente per garantire la compatibilità con Microsoft R Client

Se si installa la versione più recente di Microsoft R Client e la si usa per eseguire R su SQL Server in un contesto di calcolo remoto, è possibile che si ottenga un errore simile al seguente:

> *Si esegue la versione 9. x. x di Microsoft R Client nel computer, che non è compatibile con Microsoft R Server versione 8. x.x. Download and install a compatible version.* (Sul computer è in esecuzione la versione 9.0.0 di Microsoft R, che non è compatibile con Microsoft R Server versione 8.0.3. Scaricare e installare una versione compatibile.)

SQL Server 2016 richiede che le librerie R nel client corrispondano esattamente alle librerie R nel server. La restrizione è stata rimossa per le versioni successive alla R Server 9.0.1. Tuttavia, se si verifica questo errore, verificare la versione delle librerie R usate dal client e dal server e, se necessario, aggiornare il client in modo che corrisponda alla versione del server.

La versione di R installata con R Services per SQL Server viene aggiornata ogni volta che viene installata una versione di SQL Server Service. Per assicurarsi di avere sempre le versioni più aggiornate dei componenti R, assicurarsi di installare tutti i Service Pack.

Per garantire la compatibilità con Microsoft R Client 9.0.0, installare gli aggiornamenti descritti in questo [articolo del supporto tecnico](https://support.microsoft.com/kb/3210262).

Per evitare problemi con i pacchetti R, è anche possibile aggiornare la versione delle librerie R installate nel server, modificando il contratto di servizio in modo da usare i criteri di supporto del ciclo di vita moderni, come descritto nella [sezione successiva](#bkmk_sqlbindr). Quando si esegue questa operazione, la versione di R installata con SQL Server viene aggiornata in base alla stessa pianificazione usata per gli aggiornamenti di Machine Learning Server (in precedenza Microsoft R Server).

**Si applica a:** SQL Server 2016 R Services, con R Server versione 9.0.0 o precedente

### <a name="5-r-components-missing-from-cu3-setup"></a>5. Componenti R mancanti dall'installazione di CU3

È stato effettuato il provisioning di un numero limitato di macchine virtuali di Azure senza i file di installazione di R che devono essere inclusi con SQL Server. Il problema si applica alle macchine virtuali di cui è stato effettuato il provisioning nel periodo compreso tra 2018-01-05 e 2018-01-23. Questo problema può anche influire sulle installazioni locali se è stato applicato l'aggiornamento di CU3 per SQL Server 2017 durante il periodo da 2018-01-05 a 2018-01-23.

È stata fornita una versione del servizio che include la versione corretta dei file di installazione di R.

+ [Pacchetto di aggiornamento cumulativo 3 per SQL Server 2017 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

Per installare i componenti e ripristinare SQL Server 2017 CU3, è necessario disinstallare CU3 e reinstallare la versione aggiornata:

1. Scaricare il file di installazione di CU3 aggiornato, che include i programmi di installazione di R.
2. Disinstallare CU3. Nel pannello di controllo cercare **Disinstalla un aggiornamento**e quindi selezionare "hotfix 3015 for SQL Server 2017 (KB4052987) (64-bit)". Procedere con i passaggi di disinstallazione.
3. Reinstallare l'aggiornamento di CU3 facendo doppio clic sull'aggiornamento per KB4052987 appena scaricato: `SQLServer2017-KB4052987-x64.exe`. Seguire le istruzioni di installazione.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. Non è possibile installare i componenti Python nelle installazioni offline di SQL Server 2017 CTP 2,0 o versione successiva

Se si installa una versione provvisoria di SQL Server 2017 in un computer senza accesso a Internet, il programma di installazione potrebbe non riuscire a visualizzare la pagina che richiede il percorso dei componenti Python scaricati. In tale istanza è possibile installare la funzionalità Machine Learning Services, ma non i componenti Python.

Questo problema è stato risolto nella versione di rilascio. Questa limitazione non si applica inoltre ai componenti R.

**Si applica a:** SQL Server 2017 con Python

### <a name="bkmk_sqlbindr"></a>Avviso di versione non compatibile quando ci si connette a una versione precedente di R Services per SQL Server da un client usando[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Quando si esegue il codice R in un contesto di calcolo SQL Server 2016, è possibile che venga visualizzato l'errore seguente:

> *Si sta eseguendo la versione 9.0.0 di Microsoft R Client nel computer, che non è compatibile con la versione di Microsoft R Server 8.0.3. Download and install a compatible version.* (Sul computer è in esecuzione la versione 9.0.0 di Microsoft R, che non è compatibile con Microsoft R Server versione 8.0.3. Scaricare e installare una versione compatibile.)

Questo messaggio viene visualizzato se una delle due istruzioni seguenti è vera,

+ È stato installato R Server (standalone) in un computer client utilizzando l'installazione guidata di [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
+ È stato installato Microsoft R Server usando il [programma di installazione di Windows separato](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Per assicurarsi che il server e il client usino la stessa versione, potrebbe essere necessario usare l' _associazione_, supportata per Microsoft R Server 9,0 e versioni successive, per aggiornare i componenti R nelle istanze di SQL Server 2016. Per determinare se è disponibile il supporto per gli aggiornamenti per la versione di R Services, vedere [eseguire l'aggiornamento di un'istanza di r Services con Sqlbindr. exe](install/upgrade-r-and-python.md).

**Si applica a:** SQL Server 2016 R Services, con R Server versione 9.0.0 o precedente

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. Durante l'installazione di alcune versioni del servizio SQL Server 2016 è possibile che le versioni più recenti dei componenti R non vengano installate

Quando si installa un aggiornamento cumulativo o si installa un Service Pack per SQL Server 2016 in un computer non connesso a Internet, l'installazione guidata potrebbe non riuscire a visualizzare la richiesta che consente di aggiornare i componenti R usando i file CAB scaricati. Questo errore si verifica in genere quando vengono installati più componenti insieme al motore di database.

Come soluzione alternativa, è possibile installare la versione del servizio usando la riga di comando e specificando l' `MRCACHEDIRECTORY` argomento, come illustrato in questo esempio, che installa gli aggiornamenti di CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Per ottenere i programmi di installazione più recenti, vedere [installare componenti di Machine Learning senza accesso a Internet](install/sql-ml-component-install-without-internet-access.md).

**Si applica a:** SQL Server 2016 R Services, con R Server versione 9.0.0 o precedente

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. Non è possibile avviare i servizi Launchpad se la versione è diversa dalla versione R

Se si installa R Services per SQL Server separatamente dal motore di database e le versioni di build sono diverse, potrebbe essere visualizzato il seguente errore nel registro eventi di sistema:

> *Impossibile avviare il servizio Launchpad di SQL Server a causa del seguente errore: Il servizio non ha risposto tempestivamente alla richiesta di avvio o di controllo.*

Ad esempio, questo errore può verificarsi se si installa il motore di database usando la versione di rilascio, si applica una patch per aggiornare il motore di database e quindi si aggiunge la funzionalità R Services usando la versione di rilascio.

Per evitare questo problema, usare un'utilità, ad esempio gestione file, per confrontare le versioni di Launchpad. exe con la versione dei file binari SQL, ad esempio sqldk. dll. Tutti i componenti devono avere lo stesso numero di versione. Se si aggiorna un componente, assicurarsi di applicare lo stesso aggiornamento a tutti gli altri componenti installati.

Cercare Launchpad nella `Binn` cartella per l'istanza. Ad esempio, in un'installazione predefinita di SQL Server 2016, il percorso potrebbe essere `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. I contesti di calcolo remoto sono bloccati da un firewall in SQL Server istanze in esecuzione in macchine virtuali di Azure

Se è stato installato [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] in una macchina virtuale di Azure, potrebbe non essere possibile usare i contesti di calcolo che richiedono l'uso dell'area di lavoro della macchina virtuale. Il motivo è che, per impostazione predefinita, il firewall in macchine virtuali di Azure include una regola che blocca l'accesso alla rete per gli account utente R locali.

Come soluzione alternativa, nella macchina virtuale di Azure aprire **Windows Firewall con sicurezza avanzata**, selezionare **regole in uscita**e disabilitare la regola seguente: **Bloccare l'accesso alla rete per gli account utente locali di R in SQL Server istanza MSSQLSERVER**. È anche possibile lasciare la regola abilitata, ma modificare la proprietà di sicurezza per **consentire se protetto**.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. Autenticazione implicita in SQLEXPRESS

Quando si eseguono processi R da una workstation di Data Science remota usando l'autenticazione integrata di Windows, SQL Server usa *l'autenticazione implicita* per generare le chiamate ODBC locali che potrebbero essere richieste dallo script. Questa funzionalità, tuttavia, non funziona nella build RTM di SQL Server Express Edition.

Per risolvere il problema, è consigliabile eseguire l'aggiornamento a una versione più recente del servizio.

Se l'aggiornamento non è fattibile, come soluzione alternativa, usare un account di accesso SQL per eseguire processi R remoti che potrebbero richiedere chiamate ODBC incorporate.

**Si applica a:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. Limiti di prestazioni quando le librerie utilizzate da SQL Server vengono chiamate da altri strumenti

È possibile chiamare le librerie di Machine Learning installate per SQL Server da un'applicazione esterna, ad esempio RGui. Questo potrebbe essere il modo più pratico per eseguire determinate attività, ad esempio l'installazione di nuovi pacchetti o l'esecuzione di test ad hoc su esempi di codice molto brevi. Tuttavia, al di fuori di SQL Server, le prestazioni potrebbero essere limitate. 

Ad esempio, anche se si usa l'edizione Enterprise di SQL Server, R viene eseguito in modalità a thread singolo quando si esegue il codice R usando strumenti esterni. Per ottenere i vantaggi delle prestazioni in SQL Server, avviare una connessione SQL Server e usare [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) per chiamare il runtime di script esterno.

In generale, evitare di chiamare le librerie di Machine Learning usate dal SQL Server da strumenti esterni. Se è necessario eseguire il debug del codice R o Python, in genere è più semplice da eseguire all'esterno di SQL Server. Per ottenere le stesse librerie in SQL Server, è possibile installare Microsoft R Client, [SQL Server 2017 Machine Learning Server (autonomo)](install/sql-machine-learning-standalone-windows-install.md)o [SQL Server 2016 R Server (standalone)](install/sql-r-standalone-windows-install.md).

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools non supporta le autorizzazioni richieste da script esterni

Quando si usa Visual Studio o SQL Server Data Tools per pubblicare un progetto di database, se un'entità dispone di autorizzazioni specifiche per l'esecuzione di script esterni, è possibile che venga visualizzato un errore simile al seguente:

> *Modello TSQL: Errore rilevato durante la reverse engineering del database. L'autorizzazione non è stata riconosciuta e non è stata importata.*

Attualmente il modello DACPAC non supporta le autorizzazioni usate da R Services o Machine Learning Services, ad esempio concedere qualsiasi SCRIPT esterno o eseguire qualsiasi SCRIPT esterno. Questo problema verrà risolto in una versione futura.

Come soluzione alternativa, eseguire le istruzioni di concessione aggiuntive in uno script post-distribuzione.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. L'esecuzione di script esterni è limitata a causa dei valori predefiniti di governance delle risorse

In Enterprise Edition è possibile usare pool di risorse per gestire processi di script esterni. In alcune build di rilascio, la quantità massima di memoria che può essere allocata ai processi R è pari al 20%. Di conseguenza, se il server ha 32 GB di RAM, i file eseguibili R (RTerm. exe e BxlServer. exe) potrebbero usare un massimo di 6,4 GB in un'unica richiesta.

Se si verificano limitazioni delle risorse, controllare l'impostazione predefinita corrente. Se il 20% non è sufficiente, vedere la documentazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per su come modificare questo valore.

**Si applica a:** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>Problemi di esecuzione di script R

Questa sezione contiene problemi noti specifici dell'esecuzione di R in SQL Server, oltre ad alcuni problemi correlati alle librerie e agli strumenti R pubblicati da Microsoft, tra cui RevoScaleR.

Per ulteriori problemi noti che potrebbero influire sulle soluzioni R, vedere il sito [Machine Learning server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) .

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. Avviso di accesso negato durante l'esecuzione di script R in SQL Server in un percorso non predefinito

Se l'istanza di SQL Server è stata installata in un percorso non predefinito, ad esempio all'esterno della `Program Files` cartella, viene generato l'avviso ACCESS_DENIED quando si tenta di eseguire script per l'installazione di un pacchetto. Esempio:

> *In `normalizePath(path.expand(path), winslash, mustWork)` : percorso [2] = "~ ExternalLibraries/R/8/1": Accesso negato*

Il motivo è che una funzione R tenta di leggere il percorso e ha esito negativo se il gruppo di utenti predefinito **SQLRUserGroup**non dispone dell'accesso in lettura. L'avviso generato non blocca l'esecuzione dello script R corrente, ma è possibile che l'avviso si ripeta ripetutamente ogni volta che l'utente esegue qualsiasi altro script R.

Se SQL Server è stato installato nel percorso predefinito, questo errore non si verifica poiché tutti gli utenti di Windows dispongono delle autorizzazioni di lettura `Program Files` per la cartella.

Questo problema è stato risolto in una versione imminente del servizio. Come soluzione alternativa, fornire il gruppo **SQLRUserGroup**con accesso in lettura per tutte le cartelle padre di `ExternalLibraries`.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. Errore di serializzazione tra le versioni precedenti e nuove di RevoScaleR

Quando si passa un modello utilizzando un formato serializzato a un'istanza di SQL Server remota, è possibile che venga ricevuto l'errore: 

> *Errore in memDecompress (dati, tipo = decompressione) errore interno-3 in memDecompress (2).*

Questo errore viene generato se il modello è stato salvato utilizzando una versione recente della funzione di serializzazione, [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), ma l'istanza SQL Server in cui si deserializza il modello ha una versione precedente delle API RevoScaleR, da SQL Server 2017 CU2 o versioni precedenti.

Come soluzione alternativa, è possibile aggiornare l'istanza di SQL Server 2017 a CU3 o versione successiva.

L'errore non viene visualizzato se la versione dell'API è la stessa o se si sta migrando un modello salvato con una funzione di serializzazione precedente a un server che utilizza una versione più recente dell'API di serializzazione.

In altre parole, utilizzare la stessa versione di RevoScaleR per le operazioni di serializzazione e deserializzazione.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-_learningrate_-parameter-in-tree-and-forest-models"></a>3. Il Punteggio in tempo reale non gestisce correttamente il parametro _learningRate_ nei modelli di albero e foresta

Se si crea un modello usando un metodo di albero delle decisioni o di una foresta delle decisioni e si specifica la velocità di apprendimento, è `sp_rxpredict` possibile che vengano `PREDICT` visualizzati risultati incoerenti quando si `rxPredict`USA o la funzione SQL, rispetto all'uso di.

La ragione è un errore nell'API che elabora i modelli serializzati ed è limitato al `learningRate` parametro, ad esempio in [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)o

Questo problema viene risolto in una versione imminente del servizio.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. Limitazioni relative all'affinità processori per i processi R

Nella build di rilascio iniziale di SQL Server 2016, è possibile impostare l'affinità del processore solo per le CPU nel primo gruppo k. Se, ad esempio, il server è un computer con 2 socket con due gruppi k, per i processi R verranno usati solo i processori del primo gruppo k. La stessa limitazione si applica quando si configura la governance delle risorse per i processi di script R.

Questo problema è stato risolto in SQL Server 2016 Service Pack 1. Si consiglia di eseguire l'aggiornamento alla versione più recente del servizio.

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

Come soluzione alternativa, è possibile riscrivere la query SQL per usare CAST o CONVERT e presentare i dati a R usando il tipo di dati corretto. In generale, le prestazioni sono migliori quando si lavora con i dati usando SQL invece di modificare i dati nel codice R.

**Si applica a:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. Limiti per le dimensioni dei modelli serializzati

Quando si salva un modello in una tabella SQL Server, è necessario serializzare il modello e salvarlo in un formato binario. In teoria, le dimensioni massime di un modello che può essere archiviato con questo metodo sono pari a 2 GB, ovvero la dimensione massima delle colonne varbinary in SQL Server.

Se è necessario usare modelli più grandi, sono disponibili le soluzioni alternative seguenti:

+ Eseguire i passaggi per ridurre le dimensioni del modello. Alcuni pacchetti R Open Source includono una grande quantità di informazioni nell'oggetto modello e la maggior parte di queste informazioni può essere rimossa per la distribuzione. 
+ Usare la selezione delle funzioni per rimuovere le colonne non necessarie.
+ Se si usa un algoritmo open source, prendere in considerazione un'implementazione simile usando l'algoritmo corrispondente in MicrosoftML o RevoScaleR. Questi pacchetti sono stati ottimizzati per gli scenari di distribuzione.
+ Dopo che il modello è stato razionalizzato e le dimensioni sono state ridotte usando i passaggi precedenti, vedere se la funzione [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) in base R può essere usata per ridurre le dimensioni del modello prima di passarla a SQL Server. Questa opzione è consigliata quando il modello è prossimo al limite di 2 GB.
+ Per i modelli più grandi, è possibile utilizzare la funzionalità [FileTable](../relational-databases/blob/filetables-sql-server.md) SQL Server per archiviare i modelli, anziché utilizzare una colonna varbinary.

    Per utilizzare le tabelle FileTable, è necessario aggiungere un'eccezione del firewall, perché i dati archiviati nelle tabelle FileTable vengono gestiti dal driver filesystem FILESTREAM in SQL Server e le regole del firewall predefinite bloccano l'accesso ai file di rete. Per ulteriori informazioni, vedere [Enable Prerequisites for FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md).

    Dopo aver abilitato FileTable, per scrivere il modello, si ottiene un percorso da SQL tramite l'API FileTable e quindi si scrive il modello nel percorso dal codice. Quando è necessario leggere il modello, ottenere il percorso da SQL e quindi chiamare il modello usando il percorso dallo script. Per altre informazioni, vedere [accedere alle tabelle FileTable con API di input/output dei file](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7. Evitare di cancellare le aree di lavoro quando si esegue codice [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R in un contesto di calcolo

Se si usa un comando r per cancellare l'area di lavoro di oggetti durante l'esecuzione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] codice r in un contesto di calcolo o se si deseleziona l'area di lavoro come parte di uno script R chiamato usando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), è possibile che venga ricevuto questo errore: *area di lavoro Impossibile trovare l'oggetto revoScriptConnection*

`revoScriptConnection` è un oggetto dell'area di lavoro R che contiene informazioni su una sessione R chiamata da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se, tuttavia, il codice R include un comando per cancellare i dati dell'area di lavoro, ad esempio `rm(list=ls()))`, anche tutte le informazioni relative alla sessione e altri oggetti presenti nell'area di lavoro R vengono cancellati.

Come soluzione alternativa, evitare la cancellazione indiscriminata di variabili e altri oggetti durante l'esecuzione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]R in. Sebbene la cancellazione dell'area di lavoro sia comune quando si usa la console di R, può avere conseguenze impreviste.

* Per eliminare variabili specifiche, usare la funzione `remove` R: ad esempio,`remove('name1', 'name2', ...)`
* Se devono essere eliminate più variabili, salvare i nomi delle variabili temporanee in un elenco ed eseguire periodicamente operazioni di Garbage Collection.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. Limitazioni sui dati che possono essere forniti come input per uno script R

Non è possibile usare in uno script R i tipi seguenti di risultati delle query:

- Dati da una query [!INCLUDE[tsql](../includes/tsql-md.md)] che fa riferimento alle colonne AlwaysEncrypted.
  
- Dati da una query [!INCLUDE[tsql](../includes/tsql-md.md)] che fa riferimento alle colonne mascherate.
  
     Se è necessario usare dati mascherati in uno script R, una possibile soluzione consiste nel creare una copia dei dati in una tabella temporanea e usare invece tali dati.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. L'uso di stringhe come fattori può causare un calo delle prestazioni

L'uso di variabili di tipo stringa come fattori può aumentare significativamente la quantità di memoria usata per le operazioni R. Si tratta di un problema noto di R in generale e sono disponibili molti articoli sull'argomento. Vedere, ad esempio, [i fattori non sono cittadini di prima classe in r, di John Mount, in r-bloggers)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) o [stringsAsFactors: Biografia non autorizzata, di Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Anche se il problema non è specifico di SQL Server, può influire significativamente sulle prestazioni del codice R eseguito in SQl server. Le stringhe vengono in genere archiviate come varchar o nvarchar e se una colonna di dati di tipo stringa ha molti valori univoci, il processo di conversione interna di questi valori in numeri interi e di nuovo in stringhe da R può causare errori di allocazione della memoria.

Se non è assolutamente necessario un tipo di dati stringa per altre operazioni, il mapping dei valori stringa a un tipo di dati numerico (Integer) come parte della preparazione dei dati può risultare vantaggioso dal punto di vista delle prestazioni e della scalabilità.

Per informazioni su questo problema e su altri suggerimenti, vedere [performance for R Services-ottimizzazione dei dati](r/r-and-data-optimization-r-services.md).

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. Gli argomenti *varsToKeep* e *varsToDrop* non sono supportati per le origini dati SQL Server

Quando si usa la funzione rxDataStep per scrivere i risultati in una tabella, l'uso di *varsToKeep* e *varsToDrop* è un modo pratico per specificare le colonne da includere o escludere come parte dell'operazione. Questi argomenti tuttavia non sono supportati per le origini dati SQL Server.

### <a name="11-limited-support-for-sql-data-types-in-sp_execute_external_script"></a>11. Supporto limitato per i tipi di dati SQL\_in\_SP\_Execute External script

Non tutti i tipi di dati supportati in SQL possono essere usati in R. Come soluzione alternativa, è consigliabile eseguire il cast del tipo di dati non supportato a un tipo di dati supportato prima di\_passare\_i\_dati a SP Execute External script.

Per altre informazioni, vedere [librerie R e tipi di dati](r/r-libraries-and-data-types.md).

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Possibile danneggiamento della stringa con stringhe Unicode nelle colonne varchar

Il passaggio di dati Unicode in colonne [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] varchar da a R/Python può causare un danneggiamento della stringa. Ciò è dovuto alla codifica per queste stringhe Unicode nelle [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] regole di confronto potrebbe non corrispondere alla codifica UTF-8 predefinita usata in R/Python. 

Per inviare dati di tipo stringa non ASCII da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a R/Python, usare la codifica UTF-8 (disponibile [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]in) o usare il tipo nvarchar per lo stesso.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-sp_execute_external_script"></a>13. È possibile restituire solo un `raw` valore di tipo`sp_execute_external_script`

Quando un tipo di dati binario (il tipo di dati **RAW** r) viene restituito da R, il valore deve essere inviato nel frame di dati di output.

Con tipi di dati diversi da **RAW**, è possibile restituire i valori dei parametri insieme ai risultati della stored procedure aggiungendo la parola chiave output. Per ulteriori informazioni, vedere [parametri](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Se si desidera utilizzare più set di output che includono valori di tipo **RAW**, una possibile soluzione alternativa consiste nell'eseguire più chiamate del stored procedure o per inviare di nuovo i set di risultati [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a utilizzando ODBC.

### <a name="14-loss-of-precision"></a>14. Perdita di precisione

Poiché [!INCLUDE[tsql](../includes/tsql-md.md)] e R supportano diversi tipi di dati, i tipi di dati numerici possono subire una perdita di precisione durante la conversione.

Per altre informazioni sulla conversione implicita del tipo di dati, vedere [librerie R e tipi di dati](r/r-libraries-and-data-types.md).

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. Errore di ambito variabile quando si usa il parametro transformFunc

Per trasformare i dati durante la modellazione, è possibile passare un argomento *transformFunc* in una funzione, `rxLinmod` ad `rxLogit`esempio o. Tuttavia, le chiamate di funzione nidificata possono causare errori di ambito nel contesto di calcolo SQL Server, anche se le chiamate funzionano correttamente nel contesto di calcolo locale.

> *Il set di dati di esempio per l'analisi non contiene variabili*

Si supponga, ad esempio, di avere definito due funzioni `f` , `g`e nell'ambiente globale locale, e `g` che chiami `f`. Nelle chiamate remote o distribuite che `g`implicano, la `g` chiamata a potrebbe avere esito negativo `f` con questo errore, perché non è possibile `f` trovarla, `g` anche se sono stati passati e alla chiamata remota.

Se si verifica questo problema, è possibile risolverlo incorporando la definizione di `f` all'interno della definizione di `g`, in qualsiasi punto prima che `g` chiamerebbe normalmente `f`.

Esempio:

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

Quando si leggono colonne **varchar** da un database, lo spazio vuoto viene tagliato. Per evitare questo problema, racchiudere le stringhe tra caratteri che non siano spazi vuoti.

Quando si utilizzano funzioni `rxDataStep` come per creare tabelle di database con colonne **varchar** , la larghezza della colonna viene stimata in base a un campione di dati. Se la larghezza può variare, potrebbe essere necessario riempire tutte le stringhe a una lunghezza comune.

L'uso di una trasformazione per modificare il tipo di dati di una variabile non è supportato quando si usano chiamate ripetute a `rxImport` o a `rxTextToXdf` per importare e aggiungere righe, combinando più file di input in un singolo file XDF.

### <a name="17-limited-support-for-rxexec"></a>17. Supporto limitato per rxExec

In SQL Server 2016 la `rxExec` funzione fornita dal pacchetto RevoScaleR può essere usata solo in modalità a thread singolo.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. Aumentare la dimensione massima dei parametri per supportare rxGetVarInfo

Se si usano set di dati con un numero molto elevato di variabili (ad esempio, oltre 40.000), `max-ppsize` impostare il flag quando si avvia R per usare funzioni `rxGetVarInfo`quali. Il flag `max-ppsize` specifica le dimensioni massime dello stack di protezione dell'indicatore di misura.

Se si usa la console di R (ad esempio, RGui. exe o RTerm. exe), è possibile impostare il valore di _Max-ppsize_ su 500000 digitando:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. Problemi con la funzione rxDTree

La funzione `rxDTree` attualmente non supporta le trasformazioni nella formula. In particolare, l'uso della sintassi `F()` per la creazione di fattori in tempo reale non è supportata. Tuttavia, i dati numerici vengono automaticamente suddivisi in contenitori.

I fattori ordinati vengono trattati proprio come i fattori in tutte le funzioni di analisi RevoScaleR eccetto `rxDTree`.

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20. Data. table come OutputDataSet in R

`data.table` L'`OutputDataSet` uso di come in R non è supportato in SQL Server 2017 aggiornamento cumulativo 13 (CU13) e versioni precedenti. Potrebbe essere visualizzato il messaggio seguente:

```
Msg 39004, Level 16, State 20, Line 2
A 'R' script error occurred during execution of 
'sp_execute_external_script' with HRESULT 0x80004004.
Msg 39019, Level 16, State 2, Line 2
An external script error occurred: 
Error in alloc.col(newx) : 
  Internal error: length of names (0) is not length of dt (11)
Calls: data.frame ... as.data.frame -> as.data.frame.data.table -> copy -> alloc.col

Error in execution.  Check the output for more information.
Error in eval(expr, envir, enclos) : 
  Error in execution.  Check the output for more information.
Calls: source -> withVisible -> eval -> eval -> .Call
Execution halted
```

`data.table``OutputDataSet` come in R è supportato in SQL Server 2017 aggiornamento cumulativo 14 (CU14) e versioni successive.

## <a name="python-script-execution-issues"></a>Problemi di esecuzione degli script Python

Questa sezione contiene problemi noti specifici per l'esecuzione di Python in SQL Server, nonché per i problemi relativi ai pacchetti Python pubblicati da Microsoft, inclusi [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. La chiamata al modello con Training non riesce se il percorso del modello è troppo lungo

Se sono stati installati i modelli con training preliminare in una versione iniziale di SQL Server 2017, il percorso completo del file di modello sottoposto a training potrebbe essere troppo lungo per la lettura di Python. Questa limitazione è stata risolta in una versione successiva del servizio.

Esistono diverse possibili soluzioni alternative: 

+ Quando si installano i modelli sottoposti a training, scegliere un percorso personalizzato.
+ Se possibile, installare l'istanza di SQL Server in un percorso di installazione personalizzato con un percorso più breve, ad esempio C:\SQL\MSSQL14. MSSQLSERVER.
+ Utilizzare l'utilità di Windows [fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) per creare un collegamento reale che esegue il mapping del file del modello a un percorso più breve.
+ Eseguire l'aggiornamento alla versione più recente del servizio.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. Errore durante il salvataggio del modello serializzato in SQL Server

Quando si passa un modello a un'istanza di SQL Server remota e si tenta di leggere il modello binario usando `rx_unserialize` la funzione in [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), è possibile che venga ricevuto l'errore: 

> *NameError: il nome ' rx_unserialize_model ' non è definito*

Questo errore viene generato se il modello è stato salvato utilizzando una versione recente della funzione di serializzazione, ma l'istanza SQL Server in cui si deserializza il modello non riconosce l'API di serializzazione.

Per risolvere il problema, aggiornare l'istanza di SQL Server 2017 a CU3 o versione successiva.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. L'impossibilità di inizializzare una variabile varbinary genera un errore in BxlServer

Se si esegue il codice Python in SQL Server `sp_execute_external_script`usando e il codice ha variabili di output di tipo varbinary (max), varchar (max) o tipi simili, la variabile deve essere inizializzata o impostata come parte dello script. In caso contrario, il componente scambio di dati, BxlServer, genera un errore e smette di funzionare.

Questa limitazione verrà risolta in una versione imminente del servizio. Come soluzione alternativa, assicurarsi che la variabile sia inizializzata nello script Python. È possibile utilizzare qualsiasi valore valido, come negli esempi seguenti:

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

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. Avviso di telemetria al completamento dell'esecuzione del codice Python

A partire da SQL Server 2017 CU2, il messaggio seguente potrebbe essere visualizzato anche se il codice Python viene eseguito in modo corretto:

> *Messaggi stderr dallo script esterno:* 
>  *~ PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state viene usato prima della dichiarazione globale*

Questo problema è stato risolto in SQL Server 2017 aggiornamento cumulativo 3 (CU3). 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5. Tipi di dati numerici, decimali e Money non supportati

A partire da SQL Server 2017 aggiornamento cumulativo 12 (CU12), i tipi di dati numeric, Decimal e Money in con i set di risultati non sono supportati `sp_execute_external_script`quando si usa Python con. Potrebbero essere visualizzati i messaggi seguenti:

> *Codice 39004, stato SQL: S1000] si è verificato un errore di script ' Python ' durante l'esecuzione di of'sp_execute_external_script ' con HRESULT 0x80004004.*

> *Codice 39019, stato SQL: S1000] si è verificato un errore di script esterno:*
> 
> *Errore SqlSatelliteCall: Tipo non supportato nello schema di output. Tipi supportati: bit, smallint, int, DateTime, smallmoney, Real e float. char, varchar sono parzialmente supportati.*

Questo problema è stato risolto in SQL Server 2017 aggiornamento cumulativo 14 (CU14).

### <a name="6-bad-interpreter-error-when-installing-python-packages-with-pip-on-linux"></a>6. Errore dell'interprete errato durante l'installazione di pacchetti Python con pip in Linux 

In SQL Server 2019, se si tenta di usare **PIP**. Esempio:

```bash
/opt/mssql/mlservices/runtime/python/bin/pip -h
```

Si otterrà quindi questo errore:

> *bash:/opt/MSSQL/mlservices/Runtime/Python/bin/PIP:/opt/Microsoft/mlserver/9.4.7/bin/Python/Python: interprete non valido: Nessun file o directory di questo tipo*

**Soluzione alternativa**

Installare **PIP** dall' [autorità del pacchetto python (PyPA)](https://www.pypa.io):

```bash
wget 'https://bootstrap.pypa.io/get-pip.py' 
/opt/mssql/mlservices/bin/python/python ./get-pip.py 
```

**Consiglio**

Vedere [Install Python Packages with sqlmlutils](package-management/install-additional-python-packages-on-sql-server.md).

**Si applica a:** SQL Server 2019 in Linux

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open

Questa sezione elenca i problemi specifici degli strumenti di connettività, sviluppo e prestazioni di R forniti da Revolution Analytics. Questi strumenti sono disponibili nelle versioni provvisorie precedenti di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

In generale, è consigliabile disinstallare le versioni precedenti e installare la versione più recente di SQL Server o Microsoft R Server.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. Revolution R Enterprise non è supportato

L'installazione side-by-side di Revolution R Enterprise [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] con qualsiasi versione di non è supportata.

Se si dispone di una licenza esistente per Revolution R Enterprise, è necessario inserirla in un computer separato sia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dall'istanza di sia da qualsiasi workstation che si desidera utilizzare per la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] connessione all'istanza di.

Alcune versioni non definitive [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] di includono un ambiente di sviluppo R per Windows che è stato creato da Revolution Analytics. Questo strumento non è più disponibile e non è supportato.

Per la compatibilità [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]con, è consigliabile installare invece Microsoft R client. [R Tools per Visual Studio](https://www.visualstudio.com/vs/rtvs/) e [Visual Studio Code](https://code.visualstudio.com/) supportano anche le soluzioni Microsoft R.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. Problemi di compatibilità con il driver ODBC di SQLite e RevoScaleR

La revisione 0,92 del driver ODBC SQLite è incompatibile con RevoScaleR. Le revisioni 0.88-0.91 e 0,93 e versioni successive sono note come compatibili.

## <a name="next-steps"></a>Passaggi successivi

[Risoluzione dei problemi di Machine Learning in SQL Server](machine-learning-troubleshooting-faq.md)
