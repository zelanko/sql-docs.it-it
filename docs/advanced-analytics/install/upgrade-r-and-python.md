---
title: Aggiornare i componenti R e Python
description: Aggiornare R e Python in SQL Server Machine Learning Services o R Services per SQL Server usando sqlbindr. exe per eseguire l'associazione a Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 948ce20bf32aaa2051c4a805a3ca2f131a7c0c8f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715209"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Aggiornare i componenti di Machine Learning (R e Python) in istanze di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

L'integrazione di R e Python in SQL Server include pacchetti open source e proprietari Microsoft. Con la manutenzione SQL Server standard, i pacchetti vengono aggiornati in base al ciclo di rilascio SQL Server, con correzioni di bug per i pacchetti esistenti alla versione corrente, ma senza aggiornamenti della versione principale. 

Tuttavia, molti data scientist sono abituati a lavorare con i pacchetti più recenti Man mano che diventano disponibili. Per entrambe SQL Server Machine Learning Services (in-database) e R Services per SQL Server (in-database), è possibile ottenere le [versioni più recenti di R e Python](#version-map) *associando* **Microsoft Machine Learning server**. 

## <a name="what-is-binding"></a>Che cos'è il binding?

Binding è un processo di installazione che scambia il contenuto delle cartelle R_SERVICES e PYTHON_SERVICES con i file eseguibili, le librerie e gli strumenti più recenti da [Microsoft Machine Learning server](https://docs.microsoft.com/machine-learning-server/index).

Insieme ai componenti aggiornati viene fornita una commutazione nei modelli di manutenzione. Invece di [SQL Server ciclo](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017)di vita del prodotto, con [SQL Server aggiornamenti cumulativi](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), gli aggiornamenti del servizio sono ora conformi alla [sequenza temporale del supporto per Microsoft R Server & Machine Learning server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) nel ciclo di vita [moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Ad eccezione delle versioni del componente e degli aggiornamenti dei servizi, l'associazione non modifica le nozioni di base dell'installazione: L'integrazione di R e Python fa ancora parte di un'istanza del motore di database, le licenze restano invariate (nessun costo aggiuntivo associato all'associazione) e i criteri di supporto di SQL Server continuano a essere mantenuti per il motore di database. Nella parte restante di questo articolo viene illustrato il meccanismo di associazione e il relativo funzionamento per ogni versione di SQL Server.

> [!NOTE]
> Il binding si applica solo alle istanze (in-database) associate alle istanze SQL Server. L'associazione non è pertinente per un'installazione (autonoma).

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**Considerazioni sull'associazione SQL Server 2017**

Per SQL Server Machine Learning Services, è opportuno considerare l'associazione solo quando Microsoft Machine Learning Server inizia a offrire pacchetti aggiuntivi o versioni più recenti rispetto a quanto già disponibile.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Considerazioni sull'associazione SQL Server 2016**

Per i clienti SQL Server 2016 R Services, l'associazione fornisce pacchetti R aggiornati, nuovi pacchetti non inclusi nell'installazione originale ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) e [modelli con training](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)preliminare, che possono essere aggiornati a ogni nuova versione principale e secondaria di [Microsoft Machine Learning server](https://docs.microsoft.com/machine-learning-server/index). Il binding non fornisce supporto per Python, che è una funzionalità di SQL Server 2017.
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>Mappa della versione

La tabella seguente è una mappa delle versioni, che mostra le versioni dei pacchetti nei veicoli di rilascio, in modo che sia possibile verificare i potenziali percorsi di aggiornamento quando si esegue l'associazione a Microsoft Machine Learning Server (precedentemente noto come R Server, prima dell'aggiunta del supporto di Python. in MLS 9.2.1). 

Si noti che l'associazione non garantisce la versione più recente di R o Anaconda. Quando si esegue l'associazione a Microsoft Machine Learning Server (MLS), si ottiene la versione di R o Python installata tramite il programma di installazione, che potrebbe non essere la versione più recente disponibile sul Web.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versione iniziale | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9,3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (riparazione) su R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[modelli sottoposti a training](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versione iniziale | MLS 9,3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (riparazione) su R | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9,2 |  9,3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9,2  | 9,3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4,2 su Python 3,5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2  | 9,3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2  | 9,3| | | |
[modelli sottoposti a training](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9,2 | 9,3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>Funzionamento dell'aggiornamento componenti 

Le librerie e gli eseguibili r e Python vengono aggiornati quando si associa un'installazione esistente di R e Python a Machine Learning Server. L'associazione viene eseguita dal [programma di installazione di Microsoft Machine Learning server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) quando si esegue il programma di installazione in un'istanza del motore di database SQL Server esistente con integrazione di R o Python. Il programma di installazione rileva le funzionalità esistenti e richiede di riassociarle a Machine Learning Server. 

Durante l'associazione, il contenuto `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` di `\PYTHON_SERVICES` e viene sovrascritto con i file eseguibili e le `C:\Program Files\Microsoft\ML Server\R_SERVER` librerie `\PYTHON_SERVER`più recenti di e.

Allo stesso tempo, anche il modello di manutenzione viene ribaltato da SQL Server meccanismi di aggiornamento, al ciclo di rilascio principale e secondario più frequente di Microsoft Machine Learning Server. Il cambio di criteri di supporto è un'opzione interessante per i team di data science che richiedono moduli R e Python di nuova generazione per le proprie soluzioni. 

+ Senza binding, i pacchetti R e Python vengono corretti per le correzioni di bug quando si installa un SQL Server Service Pack o un aggiornamento cumulativo (CU). 
+ Con l'associazione, le versioni più recenti dei pacchetti possono essere applicate all'istanza, indipendentemente dalla pianificazione del rilascio di CU, in base ai [criteri del ciclo](https://support.microsoft.com/help/30881/modern-lifecycle-policy) di vita moderni e alle versioni di Microsoft Machine Learning server. Il criterio di supporto del ciclo di vita moderno offre aggiornamenti più frequenti per una durata più breve, un anno. Dopo l'associazione, si continuerà a usare il programma di installazione di MLS per gli aggiornamenti futuri di R e Python Man mano che diventano disponibili nei siti di download Microsoft.

Il binding si applica solo alle funzionalità di R e Python. In particolare, i pacchetti open source per le funzionalità R e Python (Microsoft R Open, Anaconda) e i pacchetti proprietari RevoScaleR, revoscalepy e così via. Il binding non modifica il modello di supporto per l'istanza del motore di database e non modifica la versione di SQL Server.

Il binding è reversibile. È possibile ripristinare SQL Server la manutenzione mediante [l'annullamento dell'associazione dell'istanza](#bkmk_Unbind) di e reparazione dell'istanza del motore di database SQL Server.

Sommato, i passaggi per l'associazione sono i seguenti:

+ Iniziare con un'installazione configurata esistente di R Services per SQL Server o SQL Server Machine Learning Services.
+ Determinare quale versione di Microsoft Machine Learning Server dispone dei componenti aggiornati che si desidera utilizzare.
+ Scaricare ed eseguire il programma di installazione per tale versione. Il programma di installazione rileva l'istanza esistente, aggiunge un'opzione di associazione e restituisce un elenco di istanze compatibili.
+ Scegliere l'istanza che si desidera associare, quindi completare il programma di installazione per eseguire l'associazione.

In termini di esperienza utente, la tecnologia e la modalità di utilizzo sono invariate. L'unica differenza è rappresentata dalla presenza di pacchetti con versioni più recenti e possibilmente da pacchetti aggiuntivi non disponibili originariamente tramite SQL Server.

## <a name="bkmk_BindWizard"></a>Associa a MLS usando il programma di installazione

Il programma di installazione di Microsoft Machine Learning rileva le funzionalità e la versione di SQL Server esistenti e richiama un'utilità denominata sqlbindr. exe per modificare l'associazione. Internamente, sqlbindr viene concatenato alla configurazione e viene usato indirettamente. Successivamente, è possibile chiamare sqlbindr direttamente dalla riga di comando per esercitare opzioni specifiche.

1. In SSMS eseguire `SELECT @@version` per verificare che il server soddisfi i requisiti minimi di compilazione. 

   Per SQL Server 2016 R Services, il valore minimo è [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) e [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Controllare la versione dei pacchetti R di base e RevoScaleR per verificare che le versioni esistenti siano inferiori rispetto a quelle con cui si prevede di sostituirle. 

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

1. Chiudere SSMS e tutti gli altri strumenti con una connessione aperta a SQL Server. Il binding sovrascrive i file di programma. Se SQL Server dispone di sessioni aperte, l'associazione avrà esito negativo con codice di errore di binding 6.

1. Scaricare Microsoft Machine Learning Server nel computer in cui è presente l'istanza che si desidera aggiornare. È consigliabile usare la [versione più recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Decomprimere la cartella e avviare ServerSetup. exe, che si trova in MLSWIN93.

   ![Installazione guidata di Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. In **configurare l'installazione**, confermare i componenti da aggiornare ed esaminare l'elenco delle istanze compatibili. 

   Questo passaggio è molto importante.

   A sinistra scegliere tutte le funzionalità che si desidera gestire o aggiornare. Non è possibile aggiornare alcune funzionalità e non altre. Una casella di controllo vuota rimuove la funzionalità, presupponendo che sia attualmente installata. Nello screenshot, data un'istanza di SQL Server 2016 R Services (MSSQL13), R e la versione R dei modelli con training preliminare sono selezionati. Questa configurazione è valida perché SQL Server 2016 supporta R ma non Python.

   Se si stanno aggiornando componenti in SQL Server 2016 R Services, non selezionare la funzionalità Python. Non è possibile aggiungere Python a SQL Server 2016 R Services.

   Sulla destra selezionare la casella di controllo accanto al nome dell'istanza. Se non è elencata alcuna istanza, si ha una combinazione incompatibile. Se non si seleziona un'istanza, viene creata una nuova installazione autonoma di Machine Learning Server e le librerie SQL Server sono invariate. Se non è possibile selezionare un'istanza, è possibile che non si trovi in [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Configurare il passaggio di installazione](media/mls-931-installer-mssql13.png)

1. Nella pagina **contratto di licenza** **selezionare Accetto** le condizioni per l'accettazione delle condizioni di licenza per Machine Learning server. 

1. Nelle pagine successive fornire il consenso alle condizioni di licenza aggiuntive per tutti i componenti open source selezionati, ad esempio Microsoft R Open o la distribuzione di Python Anaconda.

1. Nella pagina **quasi qui** prendere nota della cartella di installazione. La cartella predefinita è \Program C:\programmi\microsoft\ml server.

    Se si desidera modificare la cartella di installazione, fare clic su **Avanzate** per tornare alla prima pagina della procedura guidata. Tuttavia, è necessario ripetere tutte le selezioni precedenti.

Durante il processo di installazione, verranno sostituite tutte le librerie R o Python usate da SQL Server e Launchpad verrà aggiornato per usare i componenti più recenti. Di conseguenza, se l'istanza usava in precedenza le librerie nella cartella R_SERVICES predefinita, dopo l'aggiornamento queste librerie vengono rimosse e le proprietà del servizio Launchpad vengono modificate in modo da usare le librerie nella nuova posizione.

L'associazione influiscono sul contenuto di queste cartelle: C:\Programmi\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library viene sostituito con il contenuto di C:\Program C:\programmi\microsoft\ml Server\R_SERVER. La seconda cartella e il relativo contenuto vengono creati dal programma di installazione di Microsoft Machine Learning Server. 

Se l'aggiornamento non riesce, controllare i [codici di errore](#sqlbindr-error-codes) sqlbindr per ulteriori informazioni.

## <a name="confirm-binding"></a>Conferma associazione

Controllare di nuovo la versione di R e RevoScaleR per verificare di disporre di versioni più recenti. Usare la console di R distribuita con i pacchetti R nell'istanza del motore di database per ottenere le informazioni sul pacchetto:

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

Per SQL Server 2016 R Services associati a Machine Learning Server 9,3, il pacchetto R di base deve essere 3.4.3, RevoScaleR deve essere 9,3 ed è necessario anche MicrosoftML 9,3. 

Se sono stati aggiunti modelli con training preliminare, i modelli sono incorporati nella libreria MicrosoftML e possono essere chiamati tramite funzioni MicrosoftML. Per ulteriori informazioni, vedere la pagina relativa agli [esempi R per MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Binding offline (nessun accesso a Internet)

Per i sistemi senza connettività Internet, è possibile scaricare il programma di installazione e i file CAB in un computer connesso a Internet e quindi trasferire i file al server isolato. 

Il programma di installazione (ServerSetup. exe) include i pacchetti Microsoft (RevoScaleR, MicrosoftML, olapr, sqlRUtils). I file con estensione cab forniscono altri componenti di base. Il file CAB "SRO", ad esempio, fornisce R Open, la distribuzione Microsoft di R Open Source.

Nelle istruzioni seguenti viene illustrato come collocare i file per un'installazione offline.

1. Scaricare il programma di installazione di MLS. Viene scaricato come singolo file compresso. Si consiglia la [versione più recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), ma è anche possibile installare [versioni precedenti](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Scaricare i file con estensione cab. I collegamenti seguenti sono per la versione 9,3. Se sono necessarie versioni precedenti, i collegamenti aggiuntivi sono reperibili nella [R Server 9,1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Tenere presente che Python/anaconda può essere aggiunto solo a un'istanza di Machine Learning Services SQL Server. Sono disponibili modelli con training preliminare per R e Python. il file con estensione cab fornisce modelli nei linguaggi utilizzati.

    | Funzionalità | Scarica |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelli con training preliminare | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Trasferire i file con estensione zip e CAB al server di destinazione.

1. Nel server digitare `%temp%` il comando Run per ottenere la posizione fisica della directory Temp. Il percorso fisico varia in base al computer, ma è `C:\Users\<your-user-name>\AppData\Local\Temp`in genere.

1. Inserire i file con estensione cab nella cartella% Temp%.

1. Decomprimere il programma di installazione.

1. Eseguire ServerSetup. exe e seguire le istruzioni visualizzate per completare l'installazione.

## <a name="bkmk_BindCmd"></a>Operazioni da riga di comando

Dopo l'esecuzione di Microsoft Machine Learning Server, un'utilità della riga di comando denominata sqlbindr. exe diventa disponibile che è possibile utilizzare per ulteriori operazioni di binding. Ad esempio, se si decide di annullare un'associazione, è possibile eseguire nuovamente l'installazione o utilizzare l'utilità della riga di comando. Inoltre, è possibile utilizzare questo strumento per verificare la disponibilità e la compatibilità dell'istanza.

> [!TIP]
> Sqlbindr non è stato trovato? Probabilmente non è stato eseguito il programma di installazione. Sqlbindr è disponibile solo dopo l'esecuzione del programma di installazione di Machine Learning Server.

1. Aprire un prompt dei comandi come amministratore e passare alla cartella che contiene sqlbindr.exe. Il percorso predefinito è C:\Program Files\Microsoft\MLServer\Setup

2. Digitare il comando seguente per visualizzare un elenco delle istanze disponibili: `SqlBindR.exe /list`
  
   Annotare il nome completo dell'istanza indicato. Il nome dell'istanza, ad esempio, potrebbe essere MSSQL14. MSSQLSERVER per un'istanza predefinita o un valore simile a SERVERNAME. Istanzadenominatautente.

3. Eseguire il comando sqlbindr **. exe** con l'argomento */Bind* e specificare il nome dell'istanza da aggiornare, usando il nome dell'istanza restituito nel passaggio precedente.

   Per aggiornare l'istanza predefinita, ad esempio, digitare:`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Al termine dell'aggiornamento, riavviare il servizio Launchpad associato a qualsiasi istanza che è stata modificata.

## <a name="bkmk_Unbind"></a>Ripristinare o annullare il binding di un'istanza

È possibile ripristinare un'istanza associata a un'installazione iniziale dei componenti R e Python, stabiliti dal programma di installazione di SQL Server. Sono disponibili tre parti per ripristinare la manutenzione SQL Server.

+ [Passaggio 1: Annulla associazione da Microsoft Machine Learning Server](#step-1-unbind)
+ [Passaggio 2: Ripristinare lo stato originale dell'istanza](#step-2-restore)
+ [Passaggio 3: Reinstallare tutti i pacchetti aggiunti all'installazione](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Passaggio 1: Disassociare

Sono disponibili due opzioni per eseguire il rollback dell'associazione: eseguire nuovamente l'installazione o utilizzare l'utilità della riga di comando sqlbindr.

#### <a name="bkmk_wizunbind"></a>Annulla binding con installazione

1. Individuare il programma di installazione per Machine Learning Server. Se il programma di installazione è stato rimosso, potrebbe essere necessario scaricarlo di nuovo o copiarlo da un altro computer.
2. Assicurarsi di eseguire il programma di installazione nel computer in cui è presente l'istanza che si desidera annullare.
2. Il programma di installazione identifica le istanze locali candidate per l'annullamento dell'associazione.
3. Deselezionare la casella di controllo accanto all'istanza di che si desidera ripristinare la configurazione originale.
4. Accettare il contratto di licenza. È necessario indicare l'accettazione delle condizioni di licenza anche durante l'installazione di.
5. Scegliere **Fine**. Il processo richiede alcuni minuti.

#### <a name="bkmk_cmdunbind"></a>Annulla binding tramite la riga di comando

1. Aprire un prompt dei comandi e passare alla cartella contenente **sqlbindr.exe**, come descritto nella sezione precedente.

2. Eseguire il comando **SqlBindR.exe** con l'argomento */unbind* e specificare l'istanza.

   Ad esempio, il comando seguente ripristina l'istanza predefinita:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Passaggio 2: Ripristinare l'istanza di SQL Server

Eseguire SQL Server il programma di installazione per ripristinare l'istanza del motore di database con le funzionalità di R e Python. Gli aggiornamenti esistenti vengono conservati, ma se non sono stati SQL Server aggiornamenti di manutenzione per i pacchetti R e Python, questo passaggio applica tali patch.

In alternativa, si tratta di un maggior numero di operazioni, ma è anche possibile disinstallare e reinstallare completamente l'istanza del motore di database e quindi applicare tutti gli aggiornamenti del servizio.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Passaggio 3: Aggiungere eventuali pacchetti di terze parti

È possibile che siano stati aggiunti altri pacchetti open source o di terze parti alla raccolta di pacchetti. Poiché l'inversione dell'associazione cambia il percorso della libreria di pacchetti predefinita, è necessario reinstallare i pacchetti nella libreria usata da R e Python. Per altre informazioni, vedere [pacchetti predefiniti](../package-management/default-packages.md), [installare nuovi pacchetti R](../r/install-additional-r-packages-on-sql-server.md)e [installare nuovi pacchetti Python](../python/install-additional-python-packages-on-sql-server.md).

## <a name="sqlbindrexe-command-syntax"></a>Sintassi del comando sqlbindr. exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parametri

|Name|Descrizione|
|------|------|
|*list*| Visualizza un elenco di tutti gli ID delle istanze di database SQL nel computer corrente|
|*bind*| Aggiorna l'istanza di database SQL specificata alla versione più recente di R Server e assicura che all'istanza vengano applicati automaticamente gli aggiornamenti successivi di R Server|
|*unbind*|Disinstalla la versione più recente di R Server dall'istanza di database SQL specificata e impedisce l'applicazione degli aggiornamenti successivi di R Server|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>Errori di associazione

Il programma di installazione MLS e sqlbindr restituiscono entrambi i codici di errore e i messaggi seguenti.

|Codice di errore  | `Message`           | Dettagli               |
|------------|-------------------|-----------------------|
|Errore di binding 0 | OK (esito positivo) | Associazione passata senza errori. |
|Errore di binding 1 | Argomenti non validi | Errore di sintassi. |
|Errore di binding 2 | Azione non valida | Errore di sintassi. |
|Errore di binding 3 | Istanza non valida | Un'istanza esiste, ma non è valida per l'associazione. |
|Errore di binding 4 | Non associabile | |
|Errore di binding 5 | Già associato | È stato eseguito il comando *bind* , ma l'istanza specificata è già associata. |
|Errore di binding 6 | Binding non riuscito | Si è verificato un errore durante l'annullamento dell'associazione dell'istanza. Questo errore può verificarsi se si esegue il programma di installazione di MLS senza selezionare alcuna funzionalità. Per l'associazione è necessario selezionare un'istanza di MSSQL e R e Python, supponendo che l'istanza sia SQL Server 2017. Questo errore si verifica anche se sqlbindr non è in grado di scrivere nella cartella programmi. Aprire sessioni o handle per SQL Server provocherà l'errore. Se viene ricevuto questo errore, riavviare il computer e ripetere i passaggi di binding prima di avviare le nuove sessioni.|
|Errore di binding 7 | Non associato | L'istanza del motore di database ha R Services o SQL Server Machine Learning Services. L'istanza non è associata a Microsoft Machine Learning Server. |
|Errore di binding 8 | Annullamento dell'associazione non riuscito | Si è verificato un errore durante l'annullamento dell'associazione dell'istanza. |
|Errore di binding 9 | No instances found (Non è stata trovata alcuna istanza) | Non sono state trovate istanze del motore di database nel computer. |

## <a name="known-issues"></a>Problemi noti

In questa sezione vengono elencati i problemi noti specifici dell'utilizzo dell'utilità sqlbindr. exe o gli aggiornamenti di Machine Learning Server che potrebbero influire sulle istanze di SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Ripristino dei pacchetti installati in precedenza

Se è stato eseguito l'aggiornamento a Microsoft R Server 9.0.1, la versione di sqlbindr. exe per tale versione non è riuscita a ripristinare completamente i pacchetti originali o i componenti R, per richiedere che l'utente esegua SQL Server ripristino sull'istanza, applicare tutte le versioni del servizio e quindi riavviare istanza di.

La versione successiva di sqlbindr ripristina automaticamente le funzionalità di R originali, eliminando la necessità di reinstallare i componenti R o di riapplicare la patch al server. Tuttavia, è necessario installare eventuali aggiornamenti dei pacchetti R che potrebbero essere stati aggiunti dopo l'installazione iniziale.

Se sono stati usati i ruoli di gestione dei pacchetti per installare e condividere il pacchetto, questa attività è molto più semplice: è possibile usare i comandi R per sincronizzare i pacchetti installati con i file system usando i record nel database e viceversa. Per ulteriori informazioni, vedere [gestione dei pacchetti R per SQL Server](../r/install-additional-r-packages-on-sql-server.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemi con più aggiornamenti da SQL Server

Se in precedenza è stata aggiornata un'istanza di SQL Server 2016 R Services a 9.0.1, quando si esegue il nuovo programma di installazione per Microsoft R Server 9.1.0, viene visualizzato un elenco di tutte le istanze valide e, per impostazione predefinita, vengono selezionate le istanze con binding in precedenza. Se si continua, le istanze associate in precedenza non sono associate. Di conseguenza, l'installazione precedente di 9.0.1 viene rimossa, inclusi tutti i pacchetti correlati, ma non viene installata la nuova versione di Microsoft R Server (9.1.0).

Come soluzione alternativa, è possibile modificare l'installazione di R Server esistente come segue:
1. Nel pannello di controllo aprire **Installazione applicazioni**.
2. Individuare Microsoft R Server e fare clic su **modifica/modifica**.
3. All'avvio del programma di installazione, selezionare le istanze che si desidera associare a 9.1.0.

Microsoft Machine Learning Server 9.2.1 e 9,3 non presentano questo problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Binding o annullamento dell'associazione che lascia più cartelle temporanee

In alcuni casi le operazioni di binding e annullamento dell'associazione non ripuliscono le cartelle temporanee.
Se si trovano cartelle con un nome simile a questo, è possibile rimuoverlo al termine dell'installazione: R_SERVICES_<guid>

> [!NOTE]
> Assicurarsi di attendere il completamento dell'installazione. La rimozione delle librerie R associate a una versione può richiedere molto tempo e quindi aggiungere le nuove librerie R. Al termine dell'operazione, le cartelle temporanee vengono rimosse.

## <a name="see-also"></a>Vedere anche

+ [Installare Machine Learning Server per Windows (Internet connesso)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Installare Machine Learning Server per Windows (offline)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemi noti in Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Annunci di funzionalità della versione precedente di R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Funzionalità deprecate, sospese o modificate](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
