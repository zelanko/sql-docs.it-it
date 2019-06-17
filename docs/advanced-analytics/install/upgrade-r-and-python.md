---
title: Aggiornare i componenti R e Python - servizi di SQL Server Machine Learning
description: Eseguire l'aggiornamento di R e Python in servizi di SQL Server 2016 o SQL Server 2017 Machine Learning Services usare sqlbindr.exe da associare a Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 93384c8152109b01720ae7e861731638316d4966
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141430"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Aggiornamento di machine learning (R e Python) componenti nelle istanze di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integrazione di R e Python in SQL Server include pacchetti open source e proprietaria Microsoft. Sotto la manutenzione standard di SQL Server, i pacchetti vengono aggiornati in base al ciclo di rilascio di SQL Server, con correzioni di bug per i pacchetti esistenti alla versione corrente, ma non gli aggiornamenti di versione principale. 

Tuttavia, molti data Scientist sono abituati a lavorare con i pacchetti più recenti appena diventano disponibili. Per SQL Server 2017 Machine Learning Services (In-Database) e SQL Server 2016 R Services (In-Database), è possibile ottenere [le versioni più recenti di R e Python](#version-map) dal *associazione* a **Microsoft Machine Learning Server**. 

## <a name="what-is-binding"></a>Definizione di associazione?

L'associazione è un processo di installazione che scambia il contenuto delle cartelle /Site e PYTHON_SERVICES R_SERVICES con gli eseguibili più recenti, librerie e gli strumenti dalla [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index).

Insieme a componenti aggiornati viene fornito un commutatore in modelli di manutenzione. Anziché il [ciclo di vita del prodotto SQL Server](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017), con [gli aggiornamenti cumulativi di SQL Server](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), gli aggiornamenti del servizio è ora conforme al [sequenza temporale del supporto per Microsoft R Server co & mputer Server di apprendimento](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) nella [ciclo di vita moderni](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Ad eccezione delle versioni dei componenti e gli aggiornamenti dei servizi, binding non modifica le nozioni di base dell'installazione: Integrazione di R e Python è ancora parte di un'istanza di motore di database, gestione delle licenze non è stata modificata (nessun costo aggiuntivo associato all'associazione) e i criteri di supporto di SQL Server mantiene il motore di database. La parte restante di questo articolo illustra il meccanismo di associazione e sul relativo funzionamento per ogni versione di SQL Server.

> [!NOTE]
> Binding si applica alle istanze (In-Database) solo che sono associate a istanze di SQL Server. Associazione non è rilevante per l'installazione (autonomo).

**Considerazioni sull'associazione di SQL Server 2017**

Per i servizi di SQL Server 2017 Machine Learning, si potrebbe prendere in considerazione associazione solo quando si inizia a Microsoft Machine Learning Server offrire altri pacchetti o le versioni più recenti su ciò che si dispongono già.

**Considerazioni sull'associazione di SQL Server 2016**

Per i clienti di SQL Server 2016 R Services, associazione fornisce i pacchetti aggiornati R, nuovi pacchetti non fa parte dell'installazione originale ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)), e [pretrained modelli](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models), ognuno dei quali può essere ulteriormente aggiornato a ogni nuova versione principale e secondaria di [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index). Associazione non fornisce supporto per Python, che è una funzionalità di SQL Server 2017. 

<a name="version-map"></a>

## <a name="version-map"></a>Mapping della versione

Nella tabella seguente è un mapping della versione, che mostra le versioni dei pacchetti in versione veicoli in modo che è possibile verificare potenziali percorsi di aggiornamento quando si associa a Microsoft Machine Learning Server (precedentemente noto come R Server, prima dell'aggiunta del supporto di Python a partire nel servizio per inserzioni multiple 9.2.1). 

Si noti che l'associazione non garantisce la versione più recente di R o Anaconda. Quando si associa a Microsoft Machine Learning Server (servizio per inserzioni multiple), si ottiene la versione di R o Python installata tramite l'installazione, che potrebbe non essere la versione più recente disponibile sul web.

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versione iniziale | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) tramite R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[modelli con training preliminare](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1,0 |  1,0 |  1,0 |  1,0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1,0 |  1,0 |  1,0 |  1,0 |


[**SQL Server 2017 Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versione iniziale | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) tramite R | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1,0 |  1,0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1,0 |  1,0 | | | |
Anaconda 4.2 over Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[modelli con training preliminare](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>Funzionamento dell'aggiornamento di componenti 

File eseguibili e librerie di R e Python vengono aggiornati quando si associa un'installazione esistente di R e Python di Machine Learning Server. Associazione viene eseguita per il [programma di installazione di Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) quando si esegue il programma di installazione in un'esistente del database del motore istanza di SQL Server 2016 o 2017, con integrazione di R o Python. Il programma di installazione rileva le funzionalità esistenti e viene richiesto di associare di nuovo a Machine Learning Server. 

Durante l'associazione, il contenuto di C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES e \PYTHON_SERVICES viene sovrascritto con i file eseguibili e librerie di c:\programmi\microsoft\ml Server\R_SERVER e \PYTHON_SERVER più recente.

Allo stesso tempo, il modello di manutenzione viene capovolto anche dai meccanismi di aggiornamento di SQL Server, al ciclo di rilascio principale e secondario più frequente di Microsoft Machine Learning Server. Cambio di criteri di supporto è un'opzione interessante per i team di analisi scientifica dei dati che richiedono la generazione più recente di R e i moduli di Python per le proprie soluzioni. 

+ Senza l'associazione, pacchetti R e Python sono applicate patch per le correzioni di bug quando si installa un SQL Server service pack o aggiornamento cumulativo (CU). 
+ Con l'associazione, le versioni più recenti del pacchetto è applicabile per l'istanza, indipendentemente dalla pianificazione della versione aggiornamento Cumulativo, sotto il [criteri del ciclo di vita moderni](https://support.microsoft.com/help/30881/modern-lifecycle-policy) e versioni successive di Microsoft Machine Learning Server. I criteri di supporto del ciclo di vita moderno offre aggiornamenti più frequenti su una durata più breve, un anno. Post-associazione, si continuerà a usare il programma di installazione di servizio per inserzioni multiple per gli aggiornamenti futuri di R e Python appena diventano disponibili nei siti di download Microsoft.

Binding si applica alle funzionalità R e Python. Vale a dire, i pacchetti open source per le funzionalità di R e Python (Microsoft R Open, Anaconda) e i proprietari dei pacchetti RevoScaleR e revoscalepy così via. Associazione non modifica il modello di supporto per l'istanza del motore di database e non cambia la versione di SQL Server.

L'associazione è reversibile. È possibile ripristinare la gestione di SQL Server tramite [disassociare l'istanza](#bkmk_Unbind) e ripristino in corso l'istanza di motore di database di SQL Server.

Passaggi per l'associazione sommato, sono i seguenti:

+ Iniziare con un'installazione esistente, configurata di SQL Server 2016 R Services (o Machine Learning Services di SQL Server 2017).
+ Determinare quale versione di Microsoft Machine Learning Server include i componenti aggiornati da usare.
+ Scaricare ed eseguire il programma di installazione per la versione. Il programma di installazione rileva l'istanza esistente, aggiunge un'opzione di associazione e restituisce un elenco di istanze compatibile.
+ Scegliere l'istanza che si desidera eseguire l'associazione e quindi completare la configurazione per eseguire l'associazione.

In termini di esperienza utente, la tecnologia e come funziona in rimane invariato. L'unica differenza è la presenza di più recente-con controllo delle versioni dei pacchetti e possibilmente altri pacchetti non è inizialmente disponibili tramite SQL Server (ad esempio MicrosoftML per i clienti di SQL Server 2016 R Services).

## <a name="bkmk_BindWizard"></a>Eseguire l'associazione al servizio per inserzioni multiple tramite il programma di installazione

Il programma di installazione di Microsoft Machine Learning rileva le funzionalità esistenti e la versione di SQL Server e richiama un'utilità denominata SqlBindR.exe per modificare l'associazione. Internamente, SqlBindR viene concatenato al programma di installazione e usato indirettamente. In un secondo momento, è possibile chiamare SqlBindR direttamente dalla riga di comando per verificare il comportamento opzioni specifiche.

1. In SSMS eseguire `SELECT @@version` per verificare il server soddisfi i requisiti minimi di compilazione. 

   Per SQL Server 2016 R Services, il valore minimo è [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) e [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Controllare la versione di base di R e pacchetti RevoScaleR per verificare che siano inferiori rispetto a ciò che si prevede di sostituirle con le versioni esistenti. Per SQL Server 2016 R Services, pacchetto di Base di R è 3.2.2 e RevoScaleR è 8.0.3.

    ```sql
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. Chiudere SSMS e qualsiasi altro strumento con una connessione aperta a SQL Server. Associazione sovrascrive i file di programma. Se SQL Server dispone di sessioni aperte, associazione avrà esito negativo con codice di errore di binding 6.

1. Scaricare Microsoft Machine Learning Server nel computer che dispone dell'istanza da aggiornare. È consigliabile la [versione più recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Decomprimere la cartella e avviare ServerSetup.exe, che si trova sotto MLSWIN93.

   ![Installazione guidata di Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. Sul **configurare l'installazione**confermare i componenti da aggiornare e rivedere l'elenco delle istanze compatibile. 

   Questo passaggio è molto importante.

   A sinistra, scegliere tutte le funzionalità che si desidera mantenere o eseguire l'aggiornamento. Non è possibile aggiornare alcune funzionalità e non altri. Una casella di controllo vuoto rimuove tale caratteristica, presupponendo che sia attualmente installato. Nello screenshot, dati un'istanza di SQL Server 2016 R Services (MSSQL13), vengono selezionati R e la versione di R dei modelli con training preliminare. Questa configurazione è valida perché SQL Server 2016 supporta R, ma non di Python.

   Se si esegue l'aggiornamento di componenti in SQL Server 2016 R Services, non selezionare la funzionalità di Python. È possibile aggiungere Python per SQL Server 2016 R Services.

   A destra, selezionare la casella di controllo accanto al nome dell'istanza. Se nessuna istanza è elencata, è necessario una combinazione compatibile. Se non si seleziona un'istanza, viene creata una nuova installazione autonoma di Machine Learning Server e le librerie di SQL Server sono identiche. Se non è possibile selezionare un'istanza, potrebbe non essere in [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Configurare il passaggio di installazione](media/mls-931-installer-mssql13.png)

1. Nel **contratto di licenza** pagina, selezionare **accetto le condizioni** per accettare le condizioni di licenza per Machine Learning Server. 

1. Nelle pagine successive, fornire il consenso alle condizioni di licenza aggiuntive per i componenti open source che è selezionato, ad esempio Microsoft R Open o la distribuzione Anaconda Python.

1. Nel **ci siamo quasi** pagina, prendere nota della cartella di installazione. La cartella predefinita è \Program Files\Microsoft\ML Server.

    Se si desidera modificare la cartella di installazione, fare clic su **avanzate** per tornare alla prima pagina della procedura guidata. Tuttavia, è necessario ripetere tutte le selezioni precedenti.

Durante il processo di installazione, vengono sostituite tutte le librerie di R o Python usate da SQL Server e finestra di avvio viene aggiornato per usare i componenti più recenti. Di conseguenza, se l'istanza usata in precedenza le librerie nella cartella R_SERVICES predefinita, dopo l'aggiornamento queste librerie vengono rimossi e le proprietà per il servizio Launchpad vengono modificate per usare le librerie nella nuova posizione.

Associazione influisce sul contenuto di queste cartelle: C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library viene sostituito con il contenuto di c:\programmi\microsoft\ml Server\R_SERVER. La seconda cartella e il relativo contenuto viene creati dal programma di installazione di Microsoft Machine Learning Server. 

Se l'aggiornamento non riesce, controllare [codici di errore SqlBindR](#sqlbindr-error-codes) per altre informazioni.

## <a name="confirm-binding"></a>Verificare l'associazione

Controlla di nuovo la versione di R e RevoScaleR per confermare di che avere le versioni più recenti. Usare la console di R distribuita con i pacchetti di R nell'istanza del motore di database per ottenere informazioni sul pacchetto:

```sql
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Per SQL Server 2016 R Services associato a Machine Learning Server 9.3, il pacchetto di Base di R deve essere 3.4.3 ed è necessario avere anche MicrosoftML 9.3 RevoScaleR devono essere 9.3. 

Se si aggiungono i modelli con training preliminare, i modelli vengono incorporati nella libreria di MicrosoftML ed è possibile chiamarli tramite funzioni di MicrosoftML. Per altre informazioni, vedere [esempi di R per MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Associazione non in linea (Nessun accesso a internet)

Per i sistemi senza connettività internet, è possibile scaricare i file di programma di installazione e con estensione cab in un computer connesso a internet e quindi trasferire i file al server di tipo isolato. 

Il programma di installazione (ServerSetup.exe) include i pacchetti Microsoft (RevoScaleR, MicrosoftML, olapR, sqlRUtils). I file con estensione cab forniscono altri componenti di base. Ad esempio, il cab "SRO" fornisce R Open, distribuzione di Microsoft di r open source.

Le istruzioni seguenti illustrano come inserire i file per un'installazione offline.

1. Scaricare il programma di installazione di servizio per inserzioni multiple. Scarica come un singolo file compresso. È consigliabile la [versione più recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), ma è anche possibile installare [le versioni precedenti](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Scaricare i file con estensione cab. I collegamenti seguenti sono per la versione 9.3. Se sono necessarie le versioni precedenti, i collegamenti aggiuntivi sono reperibile nel [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). È importante ricordare che/Anaconda Python possono essere aggiunti solo a un'istanza di SQL Server 2017 Machine Learning Services. Esistono modelli con training preliminare per R e Python; file CAB sono disponibili modelli nelle lingue in uso.

    | Funzionalità | Scarica |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelli con training preliminare | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Trasferire i file con estensione zip e CAB al server di destinazione.

1. Nel server, digitare `%temp%` nel comando Esegui per ottenere il percorso fisico della directory temporanea. Varia in base al percorso fisico dal computer, ma è in genere `C:\Users\<your-user-name>\AppData\Local\Temp`.

1. Inserire i file con estensione cab nella cartella % temp %.

1. Decomprimere il programma di installazione.

1. Eseguire ServerSetup.exe e seguire le istruzioni visualizzate per completare l'installazione.

## <a name="bkmk_BindCmd"></a>Operazioni dalla riga di comando

Dopo aver eseguito Microsoft Machine Learning Server, un'utilità della riga di comando denominata SqlBindR.exe diventa disponibile che è possibile usare altre operazioni di associazione. Ad esempio, se si decide di annullare un'associazione, si potrebbe eseguire nuovamente l'installazione o utilizzare l'utilità della riga di comando. Inoltre, è possibile utilizzare questo strumento per verificare, ad esempio, compatibilità e la disponibilità.

> [!TIP]
> Non è possibile trovare SqlBindR? Probabilmente non è stato eseguito il programma di installazione. SqlBindR è disponibile solo dopo aver eseguito il programma di installazione di Machine Learning Server.

1. Aprire un prompt dei comandi come amministratore e passare alla cartella che contiene sqlbindr.exe. Il percorso predefinito è c:\Programmi\Microsoft Files\Microsoft\MLServer\Setup

2. Digitare il comando seguente per visualizzare un elenco delle istanze disponibili: `SqlBindR.exe /list`
  
   Annotare il nome completo dell'istanza indicato. Il nome dell'istanza, ad esempio, potrebbe essere MSSQL14. MSSQLSERVER per un'istanza predefinita o un elemento, ad esempio SERVERNAME. ISTANZADENOMINATAUTENTE.

3. Eseguire la **SqlBindR.exe** con il */Bind* argomento e specificare il nome dell'istanza da aggiornare, usando il nome dell'istanza che è stato restituito nel passaggio precedente.

   Ad esempio, per aggiornare l'istanza predefinita, digitare:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Al termine dell'aggiornamento, riavviare il servizio Launchpad associato a tutte le istanze che sono stata modificata.

## <a name="bkmk_Unbind"></a>Ripristinare o annullare l'associazione di un'istanza

È possibile ripristinare un'istanza associata a un'installazione iniziale dei componenti R e Python, stabilite dal programma di installazione di SQL Server. Esistono tre parti di eseguendo il ripristino di SQL Server per la manutenzione.

+ [Passaggio 1: Annullare l'associazione a Microsoft Machine Learning Server](#step-1-unbind)
+ [Passaggio 2: Ripristinare l'istanza per lo stato originale](#step-2-restore)
+ [Passaggio 3: Reinstallare tutti i pacchetti che aggiungono all'installazione](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Passaggio 1: annullamento del binding

Si dispone di due opzioni per eseguire il rollback dell'associazione: ripetere nuovamente l'installazione oppure usare l'utilità della riga di comando SqlBindR.

#### <a name="bkmk_wizunbind"></a> Annullare l'associazione utilizzando il programma di installazione

1. Individuare il programma di installazione per Machine Learning Server. Se è stato rimosso il programma di installazione, è necessario scaricarlo nuovamente oppure copiarlo da un altro computer.
2. Assicurarsi di eseguire il programma di installazione nel computer che dispone dell'istanza che si desidera annullare l'associazione.
2. Il programma di installazione identifica le istanze locali che sono candidati per l'annullamento dell'associazione.
3. Deselezionare la casella di controllo accanto all'istanza che si desidera ripristinare la configurazione originale.
4. Accettare il contratto di licenza. È necessario indicare l'accettazione delle condizioni di licenza anche durante l'installazione.
5. Scegliere **Fine**. Il processo richiede un po' di tempo.

#### <a name="bkmk_cmdunbind"></a> Annullamento del binding utilizzando la riga di comando

1. Aprire un prompt dei comandi e passare alla cartella contenente **sqlbindr.exe**, come descritto nella sezione precedente.

2. Eseguire il comando **SqlBindR.exe** con l'argomento */unbind* e specificare l'istanza.

   Ad esempio, il comando seguente ripristina l'istanza predefinita:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Passaggio 2: Ripristinare l'istanza di SQL Server

Eseguire il programma di installazione di SQL Server per ripristinare l'istanza del motore di database con le funzionalità di R e Python. Gli aggiornamenti esistenti vengono mantenuti, ma se hai perso qualsiasi manutenzione degli aggiornamenti per i pacchetti R e Python per SQL Server, questo passaggio si applica le patch.

In alternativa, si tratta di altro lavoro, ma è possibile inoltre completamente disinstallare e reinstallare l'istanza del motore di database e quindi applicare tutti gli aggiornamenti del servizio.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Passaggio 3: Aggiungere tutti i pacchetti di terze parti

Si potrebbero essere aggiunti altri pacchetti open source o di terze parti per la libreria di pacchetti. Poiché l'annullamento dell'associazione passa il percorso della libreria di pacchetto predefinito, è necessario reinstallare i pacchetti nella libreria che ora usano R e Python. Per altre informazioni, vedere [predefinito dei pacchetti](../package-management/default-packages.md), [installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md), e [installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md).

## <a name="sqlbindrexe-command-syntax"></a>Sintassi del comando SqlBindR.exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parametri

|Nome|Descrizione|
|------|------|
|*list*| Visualizza un elenco di tutti gli ID delle istanze di database SQL nel computer corrente|
|*bind*| Aggiorna l'istanza di database SQL specificata alla versione più recente di R Server e assicura che all'istanza vengano applicati automaticamente gli aggiornamenti successivi di R Server|
|*unbind*|Disinstalla la versione più recente di R Server dall'istanza di database SQL specificata e impedisce l'applicazione degli aggiornamenti successivi di R Server|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>Errori di associazione

Programma di installazione di servizio per inserzioni multiple e SqlBindR restituiscono entrambi i seguenti codici di errore e i messaggi.

|Codice di errore  | `Message`           | Dettagli               |
|------------|-------------------|-----------------------|
|Eseguire l'associazione di errore 0 | OK (esito positivo) | Associazione passato senza errori. |
|Eseguire l'associazione di errore 1 | Argomenti non validi | Errore di sintassi. |
|Eseguire l'associazione di errore 2 | Azione non valida | Errore di sintassi. |
|Eseguire l'associazione di errore 3 | Istanza non valida | Un'istanza esiste, ma non è valida per l'associazione. |
|Eseguire l'associazione di errore 4 | Non associabile | |
|Eseguire l'associazione di errore 5 | Già associato | È stato eseguito il comando *bind* , ma l'istanza specificata è già associata. |
|Eseguire l'associazione di errore 6 | Binding non è riuscita | Si è verificato un errore durante l'annullamento dell'associazione l'istanza. Questo errore può verificarsi se si esegue il programma di installazione di servizio per inserzioni multiple senza selezionare alcuna funzionalità. L'associazione richiede che si seleziona un'istanza MSSQL sia R e Python, presupponendo che l'istanza è SQL Server 2017. Questo errore si verifica anche se SqlBindR non è possibile scrivere nella cartella Program Files. Sessioni aperte o gli handle di SQL Server causerà questo errore si verifica. Se si verifica questo errore, riavviare il computer e ripetere la procedura di associazione prima di avviare nuove sessioni.|
|Eseguire l'associazione di errore 7 | Non è associato | L'istanza del motore di database con R Services o SQL Server Machine Learning Services. L'istanza non è associato a Microsoft Machine Learning Server. |
|Eseguire l'associazione di errore 8 | Annullamento del binding non è riuscita | Si è verificato un errore durante l'annullamento dell'associazione l'istanza. |
|Eseguire l'associazione di errore 9 | No instances found (Non è stata trovata alcuna istanza) | Nessuna istanza del motore di database sono stata trovata nel computer. |

## <a name="known-issues"></a>Problemi noti

Questa sezione elenca i problemi noti specifici da usare dell'utilità SqlBindR.exe o agli aggiornamenti di Machine Learning Server che potrebbero influire sulle istanze di SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Il ripristino dei pacchetti installati in precedenza

Se è stato aggiornato a Microsoft R Server 9.0.1, la versione di SqlBindR.exe per tale versione non è stato possibile ripristinare i pacchetti originali o i componenti R completamente, che richiedono che l'utente eseguire il ripristino di SQL Server nell'istanza, si applicano a tutte le versioni del servizio e quindi riavviare l'istanza.

Versione più recente di SqlBindR viene automaticamente ripristinare le funzionalità di R originale, eliminando la necessità di reinstallazione dei componenti R o patch nuovamente il server. Tuttavia, è necessario installare tutti gli aggiornamenti dei pacchetti R che potrebbero essere state aggiunte dopo l'installazione iniziale.

Se si usa i ruoli di gestione pacchetti per installare e condividere pacchetti, questa attività è molto più semplice: è possibile usare i comandi R per sincronizzare i pacchetti installati nel file System utilizzando i record nel database e viceversa. Per altre informazioni, vedere [gestione dei pacchetti R per SQL Server](../r/install-additional-r-packages-on-sql-server.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemi con più aggiornamenti da SQL Server

Se è stato precedentemente aggiornato un'istanza di SQL Server 2016 R Services alla versione 9.0.1, quando si esegue il nuovo programma di installazione per Microsoft R Server 9.1.0, viene visualizzato un elenco di tutte le istanze valide e quindi Seleziona istanze precedentemente associate per impostazione predefinita. Se si continua, le istanze precedentemente associate sono non associate. Di conseguenza, le versioni precedenti 9.0.1 viene rimossa l'installazione, inclusi quelli correlati a pacchetti, ma non è installata la nuova versione di Microsoft R Server (9.1.0).

In alternativa, è possibile modificare l'installazione di R Server esistente come indicato di seguito:
1. Nel Pannello di controllo, aprire **Aggiungi / Rimuovi programmi**.
2. Microsoft R Server fare clic su **modificare**.
3. Quando viene avviato il programma di installazione, selezionare le istanze in cui che si desidera associare a 9.1.0.

Microsoft Machine Learning Server 9.2.1 e 9.3 non è il problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>L'associazione o disassociazione lascia più cartelle temporanee

Talvolta l'associazione e le operazioni di annullamento dell'associazione non riesce pulire le cartelle temporanee.
Se si ritiene di cartelle con un nome simile al seguente, è possibile rimuoverlo al termine dell'installazione: R_SERVICES_<guid>

> [!NOTE]
> Assicurarsi di attendere fino al completamento installazione. Può richiedere molto tempo per rimuovere le librerie di R associate a una versione e quindi aggiungere le nuove librerie di R. Al termine dell'operazione, vengono rimosse le cartelle temporanee.

## <a name="see-also"></a>Vedere anche

+ [Installazione di Machine Learning Server per Windows (connesso a Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Installazione di Machine Learning Server per Windows (offline)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemi noti di Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Annunci di funzionalità dalla versione precedente di R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Funzionalità deprecate, funzionalità o modificate](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
