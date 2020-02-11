---
title: Aggiornare i componenti R e Python
description: Aggiornare R e Python in Machine Learning Services per SQL Server o R Services per SQL Server usando sqlbindr.exe per il binding a Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: abc14f78a969abd4adbbb2dcf12b4ee316614d23
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69634546"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Aggiornare i componenti di Machine Learning (R e Python) nelle istanze di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

L'integrazione di R e Python in SQL Server include pacchetti open source e pacchetti proprietari di Microsoft. Con il modello di manutenzione standard di SQL Server, i pacchetti vengono aggiornati in base al ciclo di rilascio di SQL Server, con correzioni di bug per i pacchetti esistenti della versione corrente, ma senza aggiornamenti della versione principale. 

Molti data scientist, tuttavia, sono abituati a lavorare con i pacchetti più recenti man mano che questi risultano disponibili. Per entrambe le versioni, Machine Learning Services (In-Database) per SQL Server e R Services (In-Database) per SQL Server, è possibile ottenere [versioni più recenti di R e Python](#version-map) tramite il *binding* a **Microsoft Machine Learning Server**. 

## <a name="what-is-binding"></a>Che cosa si intende per binding?

In questo contesto, il binding è un processo di installazione che scambia il contenuto delle cartelle R_SERVICES e PYTHON_SERVICES con i file eseguibili, le librerie e gli strumenti più recenti di [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index).

Oltre ai componenti aggiornati, cambiano i modelli di manutenzione. In alternativa al [ciclo di vita del prodotto di SQL Server](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017), con [aggiornamenti cumulativi di SQL Server](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), gli aggiornamenti di manutenzione sono ora conformi alla [sequenza temporale di supporto per Microsoft R Server e Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) nel [ciclo di vita moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Fatta eccezione per le versioni dei componenti e degli aggiornamenti di manutenzione, il binding non modifica le caratteristiche fondamentali dell'installazione: L'integrazione di R e Python fa ancora parte di un'istanza del motore di database, la gestione delle licenze rimane invariata (nessun costo aggiuntivo per il binding) e per il motore di database sono ancora validi i criteri di supporto di SQL Server. La parte restante di questo articolo illustra il meccanismo di binding e ne spiega il funzionamento per ogni versione di SQL Server.

> [!NOTE]
> Questo meccanismo si applica solo alle istanze (In-Database) associate a istanze di SQL Server. Non è pertinente per un'installazione di tipo (Standalone).

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**Considerazioni sul binding per SQL Server 2017**

Nel caso di Machine Learning Services per SQL Server, è opportuno prendere in considerazione il binding solo quando Microsoft Machine Learning Server inizia a offrire pacchetti aggiuntivi o versioni più recenti rispetto a quanto già disponibile.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Considerazioni sul binding per SQL Server 2016**

Per i clienti di R Services per SQL Server 2016, il binding consente di usufruire di pacchetti R aggiornati, nuovi pacchetti non inclusi nell'installazione originale ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) e [modelli con training preliminare](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models), che possono essere aggiornati a ogni nuova versione principale e secondaria di [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index). Il binding non fornisce il supporto per Python, che è una funzionalità di SQL Server 2017.
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>Mappa delle versioni

La tabella seguente presenta una mappa con le versioni dei pacchetti nei rispettivi veicoli di rilascio per consentire di verificare i possibili percorsi di aggiornamento quando si esegue il binding a Microsoft Machine Learning Server (in precedenza noto come R Server, prima dell'aggiunta del supporto di Python a partire da MLS 9.2.1). 

Si noti che il binding non garantisce l'installazione della versione più recente di R o Anaconda. Quando si esegue il binding a Microsoft Machine Learning Server (MLS), si ottiene la versione di R o Python installata tramite il programma di installazione, che potrebbe non essere quella più recente disponibile sul Web.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**R Services per SQL Server 2016**](../install/sql-r-services-windows-install.md)

Componente |Versione iniziale | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) su R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.d. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[modelli con training preliminare](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.d. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.d. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.d. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**Machine Learning Services per SQL Server**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versione iniziale | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) su R | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4.2 su Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[modelli con training preliminare](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>Come funziona l'aggiornamento dei componenti 

Quando si esegue il binding di un'installazione esistente di R e Python a Machine Learning Server, le librerie e gli eseguibili di R e Python vengono aggiornati. Il binding viene eseguito dal [programma di installazione di Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) quando si esegue il programma di installazione in un'istanza esistente del motore di database SQL Server con l'integrazione di R o Python. Il programma di installazione rileva le funzionalità esistenti e richiede di eseguire nuovamente il binding a Machine Learning Server. 

Durante il binding, il contenuto di `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` e `\PYTHON_SERVICES` viene sovrascritto con i file eseguibili e le librerie più recenti di `C:\Program Files\Microsoft\ML Server\R_SERVER` e `\PYTHON_SERVER`.

Allo stesso tempo, anche il modello di manutenzione viene modificato e i meccanismi di aggiornamento di SQL Server vengono sostituiti dal ciclo di rilascio più frequente delle versioni principali e secondarie adottato per Microsoft Machine Learning Server. Questi nuovi criteri di supporto costituiscono un'opzione interessante per i team di data science che richiedono i moduli R e Python più recenti per le proprie soluzioni. 

+ Senza il binding, i pacchetti R e Python vengono aggiornati per le correzioni di bug quando si installa un Service Pack o un aggiornamento cumulativo (CU) di SQL Server. 
+ Con il binding, le versioni di pacchetto più recenti possono essere applicate all'istanza, indipendentemente dal programma di rilascio degli aggiornamenti cumulativi, in base ai [criteri del ciclo di vita moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy) e al rilascio delle versioni di Microsoft Machine Learning Server. I criteri di supporto del ciclo di vita moderno prevedono aggiornamenti più frequenti per un periodo più breve, nell'arco di un anno. Dopo il binding, si continua a usare il programma di installazione di MLS per gli aggiornamenti futuri di R e Python man mano che questi diventano disponibili nei siti di download Microsoft.

Il binding si applica solo alle funzionalità R e Python. In particolare, i pacchetti open source per le funzionalità R e Python (Microsoft R Open, Anaconda) e i pacchetti proprietari RevoScaleR, revoscalepy e così via. Il binding non modifica il modello di supporto per l'istanza del motore di database e non modifica la versione di SQL Server.

Il binding è reversibile. È possibile tornare al modello di manutenzione di SQL Server [annullando il binding dell'istanza](#bkmk_Unbind) e ripristinando l'istanza del motore di database SQL Server.

Di seguito è riportata una sintesi dei passaggi da eseguire per configurare il binding:

+ Iniziare con un'installazione configurata esistente di R Services per SQL Server o Machine Learning Services per SQL Server.
+ Determinare quale versione di Microsoft Machine Learning Server dispone dei componenti aggiornati da usare.
+ Scaricare ed eseguire il programma di installazione per tale versione. Il programma di installazione rileva l'istanza esistente, aggiunge un'opzione di binding e restituisce un elenco di istanze compatibili.
+ Scegliere l'istanza desiderata e quindi completare il programma di installazione per eseguire il binding.

A livello di esperienza utente, la tecnologia e la modalità d'uso rimangono invariate. L'unica differenza è data dalla presenza di pacchetti con versioni più recenti ed eventualmente di pacchetti aggiuntivi, originariamente non disponibili tramite SQL Server.

## <a name="bkmk_BindWizard"></a>Eseguire il binding a MLS tramite il programma di installazione

Il programma di installazione di Microsoft Machine Learning rileva le funzionalità e la versione di SQL Server esistenti e richiama l'utilità SqlBindR.exe per modificare il binding. A livello interno, l'utilità SqlBindR è concatenata al programma di installazione e viene usata indirettamente. In un secondo momento è comunque possibile chiamare SqlBindR direttamente dalla riga di comando per selezionare opzioni specifiche.

1. In SSMS eseguire `SELECT @@version` per verificare che il server soddisfi i requisiti minimi di build. 

   Nel caso di R Services per SQL Server 2016, il requisito minimo è [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) e [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Controllare le versioni esistenti dei pacchetti R di base e RevoScaleR per verificare che siano minori di quelle con cui si prevede di sostituirle. 

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

1. Chiudere SSMS e tutti gli altri strumenti che hanno una connessione aperta a SQL Server. Il binding sovrascrive i file di programma. Se SQL Server ha sessioni aperte, il binding avrà esito negativo con codice di errore 6.

1. Scaricare Microsoft Machine Learning Server nel computer in cui è presente l'istanza da aggiornare. È consigliabile scaricare la [versione più recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Decomprimere la cartella e avviare ServerSetup.exe, che si trova in MLSWIN93.

   ![Installazione guidata di Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. In **Configure the installation** (Configurare l'installazione) verificare i componenti da aggiornare ed esaminare l'elenco delle istanze compatibili. 

   Questo passaggio è molto importante.

   Nell'area a sinistra scegliere le funzionalità da mantenere o da aggiornare. Non è possibile limitare l'aggiornamento ad alcune funzionalità. Se si lascia vuota una casella di controllo, la funzionalità corrispondente viene rimossa, supponendo che attualmente sia installata. Nello screenshot, per un'istanza di R Services per SQL Server 2016 (MSSQL13), sono selezionati il componente R e la versione per R dei modelli con training preliminare. Questa configurazione è valida perché SQL Server 2016 supporta R ma non Python.

   Se si aggiornano i componenti in R Services per SQL Server 2016, non selezionare la funzionalità Python. Non è possibile aggiungere Python a R Services per SQL Server 2016.

   Nell'area a destra selezionare la casella di controllo accanto al nome dell'istanza. Se non è elencata alcuna istanza, significa che si ha una combinazione incompatibile. Se non si seleziona un'istanza, viene creata una nuova installazione autonoma di Machine Learning Server e le librerie SQL Server rimangono invariate. Se non è possibile selezionare un'istanza, è possibile che non sia soddisfatto il requisito minimo di [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Passaggio di configurazione dell'installazione](media/mls-931-installer-mssql13.png)

1. Nella pagina **License agreement** (Contratto di licenza) selezionare **I accept these terms** (Accetto le condizioni) per accettare le condizioni di licenza per Machine Learning Server. 

1. Nelle pagine successive fornire il proprio consenso alle condizioni di licenza aggiuntive per tutti i componenti open source selezionati, ad esempio Microsoft R Open o la distribuzione Anaconda di Python.

1. Nella pagina **Almost there** (Quasi fatto) prendere nota della cartella di installazione. La cartella predefinita è \Programmi\Microsoft\ML Server.

    Se si vuole modificare la cartella di installazione, fare clic su **Advanced** (Avanzate) per tornare alla prima pagina della procedura guidata. In tal caso è tuttavia necessario ripetere tutte le selezioni precedenti.

Durante il processo di installazione, le librerie R o Python usate da SQL Server vengono sostituite e Launchpad viene aggiornato per l'uso dei componenti più recenti. Di conseguenza, se in precedenza l'istanza usava le librerie nella cartella R_SERVICES predefinita, dopo l'aggiornamento queste librerie vengono rimosse e le proprietà del servizio Launchpad vengono modificate in modo da usare le librerie nel nuovo percorso.

Il binding ha effetto sul contenuto di queste cartelle: C:\Programmi\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library viene sostituita con il contenuto di C:\Programmi\Microsoft\ML Server\R_SERVER. La seconda cartella e il relativo contenuto vengono creati dal programma di installazione di Microsoft Machine Learning Server. 

Se l'aggiornamento non riesce, controllare i [codici di errore di SqlBindR](#sqlbindr-error-codes) per altre informazioni.

## <a name="confirm-binding"></a>Verificare il binding

Controllare di nuovo la versione di R e RevoScaleR per verificare di disporre delle versioni più recenti. Per ottenere le informazioni sui pacchetti, usare la console di R distribuita con i pacchetti di R nell'istanza del motore di database:

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

In caso di binding di R Services per SQL Server 2016 a Machine Learning Server 9.3, sono necessari il pacchetto R di base 3.4.3, RevoScaleR 9.3 e MicrosoftML 9.3. 

Gli eventuali modelli con training preliminare aggiunti sono incorporati nella libreria MicrosoftML e possono essere chiamati tramite le funzioni di MicrosoftML. Per altre informazioni, vedere [Esempi di R per MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Binding offline (senza accesso a Internet)

Per i sistemi senza connettività Internet, è possibile scaricare il programma di installazione e i file con estensione cab in un computer connesso a Internet e quindi trasferire i file nel server isolato. 

Il programma di installazione (ServerSetup.exe) include i pacchetti Microsoft (RevoScaleR, MicrosoftML, olapR, sqlRUtils). I file con estensione cab includono altri componenti di base. Il file CAB "SRO", ad esempio, fornisce R Open, la distribuzione Microsoft di R open source.

Le istruzioni seguenti illustrano come posizionare i file per un'installazione offline.

1. Scaricare il programma di installazione di MLS. Il programma viene scaricato come singolo file compresso. È consigliabile usare la [versione più recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), ma è possibile installare anche [versioni precedenti](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Scaricare i file con estensione cab. Di seguito sono indicati i collegamenti per la versione 9.3. Se sono necessarie versioni precedenti, è possibile trovare altri collegamenti in [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Tenere presente che Python/Anaconda può essere aggiunto solo a un'istanza di Machine Learning Services per SQL Server. Sono disponibili modelli con training preliminare per entrambi i linguaggi R e Python. Il file con estensione cab fornisce modelli nei linguaggi usati.

    | Funzionalità | Download |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelli con training preliminare | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Trasferire i file con estensione zip e cab nel server di destinazione.

1. Nel server digitare `%temp%` nel comando Esegui per ottenere il percorso fisico della directory temp. Il percorso varia a seconda del computer usato, ma è in genere `C:\Users\<your-user-name>\AppData\Local\Temp`.

1. Inserire i file con estensione cab nella cartella %temp%.

1. Decomprimere il programma di installazione.

1. Eseguire ServerSetup.exe e seguire le istruzioni visualizzate per completare l'installazione.

## <a name="bkmk_BindCmd"></a>Operazioni da riga di comando

Dopo l'esecuzione di Microsoft Machine Learning Server, diventa disponibile un'utilità della riga di comando denominata SqlBindR.exe che è possibile usare per altre operazioni di binding. Se, ad esempio, si decide di annullare un binding, è possibile eseguire nuovamente il programma di installazione oppure usare l'utilità della riga di comando. È inoltre possibile usare questo strumento per verificare la disponibilità e la compatibilità delle istanze.

> [!TIP]
> Se non si riesce a trovare SqlBindR, è probabile che non sia stato eseguito il programma di installazione. SqlBindR è disponibile solo dopo l'esecuzione del programma di installazione di Machine Learning Server.

1. Aprire un prompt dei comandi come amministratore e passare alla cartella che contiene sqlbindr.exe. Il percorso predefinito è C:\Programmi\Microsoft\MLServer\Setup

2. Digitare il comando seguente per visualizzare un elenco delle istanze disponibili: `SqlBindR.exe /list`
  
   Annotare il nome completo dell'istanza indicato. Ad esempio, il nome dell'istanza potrebbe essere MSSQL14.MSSQLSERVER per un'istanza predefinita o comunque un nome nel formato NOMESERVER.ISTANZADENOMINATA.

3. Eseguire il comando **SqlBindR.exe** con l'argomento */bind* e specificare il nome dell'istanza da aggiornare, usando il nome dell'istanza restituito nel passaggio precedente.

   Ad esempio, per aggiornare l'istanza predefinita, digitare: `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Al termine dell'aggiornamento, riavviare il servizio Launchpad associato a qualsiasi istanza modificata.

## <a name="bkmk_Unbind"></a>Annullare il binding di un'istanza

È possibile annullare un'istanza con binding e ripristinare un'installazione iniziale dei componenti R e Python, come configurata dal programma di installazione di SQL Server. Il processo di ripristino del modello di manutenzione di SQL Server prevede tre passaggi.

+ [Passaggio 1: Annullare il binding da Microsoft Machine Learning Server](#step-1-unbind)
+ [Passaggio 2: Ripristinare lo stato originale dell'istanza](#step-2-restore)
+ [Passaggio 3: Reinstallare i pacchetti aggiunti all'installazione](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Passaggio 1: Annullare il binding

Per eseguire il rollback del binding sono disponibili due opzioni: eseguire nuovamente il programma di installazione o usare l'utilità della riga di comando SqlBindR.

#### <a name="bkmk_wizunbind"></a> Annullare il binding con il programma di installazione

1. Individuare il programma di installazione per Machine Learning Server. Se il programma di installazione è stato rimosso, può essere necessario scaricarlo di nuovo o copiarlo da un altro computer.
2. Assicurarsi di eseguire il programma di installazione nel computer in cui è presente l'istanza di cui si vuole annullare il binding.
2. Il programma di installazione identifica le istanze locali candidate per l'annullamento del binding.
3. Deselezionare la casella di controllo accanto all'istanza di cui si vuole ripristinare la configurazione originale.
4. Accettare il contratto di licenza. È necessario indicare che si accettano le condizioni di licenza anche durante l'installazione.
5. Fare clic su **Fine**. L'esecuzione del processo richiede alcuni minuti.

#### <a name="bkmk_cmdunbind"></a> Annullare il binding tramite la riga di comando

1. Aprire un prompt dei comandi e passare alla cartella contenente **sqlbindr.exe**, come descritto nella sezione precedente.

2. Eseguire il comando **SqlBindR.exe** con l'argomento */unbind* e specificare l'istanza.

   Il comando seguente, ad esempio, ripristina l'istanza predefinita:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Passaggio 2: Ripristinare l'istanza di SQL Server

Eseguire il programma di installazione di SQL Server per ripristinare l'istanza del motore di database con le funzionalità R e Python. Gli aggiornamenti esistenti vengono mantenuti, ma se non sono stati eseguiti alcuni aggiornamenti di manutenzione di SQL Server per i pacchetti R e Python, questo passaggio applica tali patch.

In alternativa, anche se questo processo è più impegnativo, è possibile disinstallare e reinstallare completamente l'istanza del motore di database e quindi applicare tutti gli aggiornamenti di manutenzione.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Passaggio 3: Aggiungere eventuali pacchetti di terze parti

È possibile che siano stati aggiunti altri pacchetti open source o di terze parti alla libreria di pacchetti. Poiché l'annullamento del binding cambia il percorso della libreria di pacchetti predefinita, è necessario reinstallare i pacchetti nella libreria effettivamente usata da R e Python. Per altre informazioni, vedere [Informazioni sui pacchetti R](../package-management/r-package-information.md) e le relative istruzioni di [installazione](../package-management/install-additional-r-packages-on-sql-server.md) e [Informazioni sui pacchetti Python](../package-management/python-package-information.md) e le relative istruzioni di [installazione](../package-management/install-additional-python-packages-on-sql-server.md).

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

## <a name="binding-errors"></a>Errori di binding

Il programma di installazione di MLS e l'utilità SqlBindR restituiscono entrambi i codici di errore e i messaggi seguenti.

|Codice di errore  | Message           | Dettagli               |
|------------|-------------------|-----------------------|
|Errore di binding 0 | OK (success) (Operazione riuscita) | Binding completato senza errori. |
|Errore di binding 1 | Invalid arguments (Argomenti non validi) | Errore di sintassi. |
|Errore di binding 2 | Invalid action (Azione non valida) | Errore di sintassi. |
|Errore di binding 3 | Invalid instance (Istanza non valida) | È presente un'istanza, ma non è valida per il binding. |
|Errore di binding 4 | Not bindable (Istanza non associabile) | |
|Errore di binding 5 | Already bound (Istanza già associata) | È stato eseguito il comando *bind* , ma l'istanza specificata è già associata. |
|Errore di binding 6 | Bind failed (Binding non riuscito) | Si è verificato un errore durante l'annullamento del binding dell'istanza. Questo errore può verificarsi se si esegue il programma di installazione di MLS senza selezionare alcuna funzionalità. Per il binding è necessario selezionare un'istanza di MSSQL e i componenti R e Python, purché l'istanza sia SQL Server 2017. Questo errore si verifica anche nel caso in cui SqlBindR non riesca a scrivere nella cartella Programmi. Il problema può essere dovuto a sessioni o handle aperti a SQL Server. Se viene restituito questo errore, riavviare il computer e ripetere i passaggi per il binding prima di avviare nuove sessioni.|
|Errore di binding 7 | Not bound (Istanza non associata) | Nell'istanza del motore di database è presente R Services o Machine Learning Services per SQL Server. L'istanza non è associata a Microsoft Machine Learning Server. |
|Errore di binding 8 | Unbind failed (Annullamento del binding non riuscito) | Si è verificato un errore durante l'annullamento del binding dell'istanza. |
|Errore di binding 9 | No instances found (Non è stata trovata alcuna istanza) | Non sono state trovate istanze del motore di database nel computer. |

## <a name="known-issues"></a>Problemi noti

In questa sezione sono elencati i problemi noti relativi all'uso dell'utilità SqlBindR.exe o agli aggiornamenti di Machine Learning Server che possono avere effetto sulle istanze di SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Ripristino dei pacchetti installati in precedenza

Se è stato eseguito l'aggiornamento a Microsoft R Server 9.0.1, la versione di SqlBindR.exe per tale versione non riesce a ripristinare completamente i pacchetti o i componenti R originali. Di conseguenza, l'utente deve eseguire il ripristino di SQL Server sull'istanza, applicare tutte le versioni di manutenzione e quindi riavviare l'istanza.

La versione successiva di SqlBindR ripristina automaticamente le funzionalità di R originali, eliminando la necessità di reinstallare i componenti R o di riapplicare patch al server. È tuttavia necessario installare gli eventuali aggiornamenti dei pacchetti R aggiunti dopo l'installazione iniziale.

Se sono stati usati ruoli di gestione dei pacchetti per installare e condividere un pacchetto, questa attività è molto più semplice: è possibile usare i comandi R per sincronizzare i pacchetti installati con il file system usando i record nel database e viceversa. Per altre informazioni, vedere [Gestione dei pacchetti R per SQL Server](../r/install-additional-r-packages-on-sql-server.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemi relativi a più aggiornamenti di SQL Server

Se in precedenza è stata aggiornata un'istanza di R Services per SQL Server 2016 alla versione 9.0.1, quando si esegue il nuovo programma di installazione per Microsoft R Server 9.1.0, viene visualizzato un elenco di tutte le istanze valide e, per impostazione predefinita, vengono selezionate le istanze associate in precedenza. Se si continua, il binding delle istanze associate in precedenza viene annullato. Di conseguenza, l'installazione precedente della versione 9.0.1 viene rimossa, inclusi tutti i pacchetti correlati, ma la nuova versione di Microsoft R Server (9.1.0) non viene installata.

Come soluzione alternativa, è possibile modificare l'installazione esistente di R Server nel modo seguente:
1. Nel Pannello di controllo aprire **Programmi e funzionalità**.
2. Individuare Microsoft R Server e fare clic su **Cambia/Modifica**.
3. All'avvio del programma di installazione, selezionare le istanze per cui eseguire il binding alla versione 9.1.0.

Microsoft Machine Learning Server 9.2.1 e 9.3 non presentano questo problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Cartelle temporanee non rimosse automaticamente dopo il binding o l'annullamento del binding

In alcuni casi, le operazioni di binding e annullamento del binding non eseguono la pulizia delle cartelle temporanee.
Se si trovano cartelle con un nome simile a questo, è possibile rimuoverle al termine dell'installazione: R_SERVICES_<guid>

> [!NOTE]
> Attendere il completamento dell'installazione. Può essere necessario molto tempo per rimuovere le librerie R associate a una versione e quindi aggiungere le nuove librerie R. Al termine dell'operazione, le cartelle temporanee vengono rimosse.

## <a name="see-also"></a>Vedere anche

+ [Installare Machine Learning Server per Windows (con connessione Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Installare Machine Learning Server per Windows (offline)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemi noti di Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Annunci di funzionalità della versione precedente di R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Funzionalità deprecate, sospese o modificate](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
