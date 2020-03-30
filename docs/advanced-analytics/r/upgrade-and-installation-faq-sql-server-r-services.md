---
title: Domande frequenti sull'aggiornamento e sull'installazione
description: Risposte ad alcune domande comuni sull'installazione delle funzionalità di Machine Learning in SQL Server.
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6357f98627842ab790b494cf1b4a1f9b2110ec9c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727351"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Domande frequenti sull'installazione e sull'aggiornamento di SQL Server Machine Learning o R Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo argomento fornisce le risposte ad alcune domande comuni sull'installazione delle funzionalità di Machine Learning in SQL Server. Sono anche riportate domande frequenti sugli aggiornamenti.

+ Alcuni problemi si verificano solo con gli aggiornamenti dalle versioni preliminari. È pertanto consigliabile identificare la versione e l'edizione prima di leggere queste note. Per ottenere informazioni sulla versione, eseguire `@@VERSION` in una query da SQL Server Management Studio.
+ Eseguire l'aggiornamento alla versione di servizio o alla versione finale più recente il prima possibile per risolvere eventuali problemi corretti nelle versioni recenti.

**Si applica a:** R Services per SQL Server 2016, Machine Learning Services per SQL Server (In-Database)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisiti e restrizioni per le versioni precedenti di SQL Server 2016 

A seconda della build di SQL Server che si sta installando, è possibile che si applichino alcune delle limitazioni seguenti:

- Nelle prime versioni di R Services per SQL Server 2016 è richiesta la notazione 8dot3 nell'unità che contiene la directory di lavoro. Se è stata installata una versione non definitiva, l'aggiornamento a SQL Server 2016 Service Pack 1 dovrebbe risolvere il problema. Questo requisito non si applica alle versioni successive a SP1.

- Non è possibile installare [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] in un cluster di failover in SQL Server 2016. Tuttavia, SQL Server 2019 fornisce supporto per il failover. Per altre informazioni, vedere [Novità](../what-s-new-in-sql-server-machine-learning-services.md).

- In una macchina virtuale di Azure potrebbero essere necessari interventi di configurazione aggiuntivi. Ad esempio, potrebbe essere necessario creare un'eccezione del firewall per supportare l'accesso remoto.

- Non è supportata l'installazione side-by-side con un'altra versione di R o con altre versioni di Revolution Analytics.

- Disabilitare la ricerca dei virus prima di iniziare l'installazione. Al termine dell'installazione, si consiglia di sospendere la ricerca dei virus nelle cartelle usate da [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]. Preferibilmente, sospendere la ricerca per l'intero albero di [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].

 - Installazione di Microsoft R Server in un'istanza di SQL Server installata in Windows Core. Nella versione RTM di SQL Server 2016 è stato riscontrato un problema durante l'aggiunta di Microsoft R Server a un'istanza nell'edizione di Windows Server Core. Questo problema è stato risolto. Se si riscontra questo problema, è possibile applicare la correzione descritta nell'articolo [KB3164398](https://support.microsoft.com/kb/3164398) per aggiungere la funzionalità R all'istanza esistente in Windows Server Core. Per altre informazioni, vedere [Impossibile installare Microsoft R Server (autonomo) in un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Installazione offline dei componenti di Machine Learning per una versione localizzata di SQL Server 2016

Nelle versioni precedenti di SQL Server 2016 non era possibile installare i file CAB specifici delle impostazioni locali durante l'installazione offline senza una connessione Internet. Questo problema è stato risolto nelle versioni successive, ma se il programma di installazione restituisce un messaggio che informa che non è possibile installare la lingua corretta, è possibile modificare il nome del file per consentire il proseguimento dell'installazione.

+ Modificare manualmente il file del programma di installazione per assicurarsi che sia installata la lingua corretta. Ad esempio, per installare la versione giapponese di SQL Server, modificare il nome del file da SRS_8.0.3.0_**1033**.cab a SRS_8.0.3.0_**1041**.cab.
+ L'identificatore di lingua usato per i componenti di Machine Learning deve corrispondere alla lingua di installazione di SQL Server oppure non è possibile completare l'installazione.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versioni preliminari: criteri di supporto, aggiornamento e problemi noti

Non sono più supportate nuove installazioni di una versione non definitiva di [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Se si usa una versione non definitiva, eseguire l'aggiornamento il prima possibile.

In questa sezione vengono fornite istruzioni dettagliate per scenari di aggiornamento specifici.

### <a name="how-to-upgrade-sql-server"></a>Come aggiornare SQL Server

Per aggiornare la versione di SQL Server, è possibile eseguire nuovamente l'installazione guidata.

+ [Eseguire l'aggiornamento di SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Aggiornare SQL Server usando l'Installazione guidata](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

È possibile aggiornare solo i componenti di Machine Learning usando un processo denominato binding: 
+ [Usare SqlBindR per aggiornare i componenti di Machine Learning](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fine del supporto per gli aggiornamenti sul posto dalle versioni non definitive

Gli aggiornamenti da versioni non definitive di SQL Server 2016 non sono più supportati. Sono inclusi SQL Server 2016 CTP3, CTP3.1, CTP3.2, RC0 o RC1.

Le versioni seguenti sono state installate con le versioni non definitive di SQL Server 2016.

| Versione | Compilare         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

In caso di dubbi sulla versione in uso, eseguire `@@VERSION` in una query da SQL Server Management Studio.

In generale, il processo di aggiornamento è il seguente:

1. Eseguire il backup di script e dati.
2. Disinstallare la versione non definitiva.
3. Installare una versione finale.

La disinstallazione di una versione non definitiva dei componenti di Machine Learning di SQL Server può essere complessa e potrebbe richiedere l'esecuzione di uno script speciale. Contattare il supporto tecnico.

###  <a name="uninstall-prior-to-upgrading-from-an-older-version-of-microsoft-r-server"></a><a name="bkmk_Uninstall"></a> Eseguire la disinstallazione prima dell'aggiornamento da una versione precedente di Microsoft R Server

Se è installata una versione non definitiva di Microsoft R Server, è necessario disinstallarla prima dell'aggiornamento a una versione più recente.

1.  Nel **Pannello di controllo**fare clic su **Installazione applicazioni**e selezionare `Microsoft SQL Server 2016 <version number>`.

2.  Nella finestra di dialogo con le opzioni per **aggiungere**, **ripristinare**o **rimuovere** i componenti selezionare **Rimuovi**.
  
3.  Nella pagina **Seleziona funzionalità** , in **Funzionalità condivise**, selezionare **R Server (Standalone)** . Fare clic su **Avanti**e quindi su **Fine** per disinstallare solo i componenti selezionati.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>Errori dell'installazione side-by-side di R Services e R Server (Standalone) 

Nelle versioni precedenti di SQL Server 2016, l'installazione di R Server (standalone) e R Services (In-Database) allo stesso tempo causava talvolta un errore di installazione con un messaggio di "accesso negato". Questo problema è stato risolto nel Service Pack 1 per SQL Server 2016.

Se si riscontra questo errore ed è necessario aggiornare queste funzionalità, eseguire un'installazione integrata di SQL Server 2016 con SP1. Esistono due modi per risolvere il problema, che richiedono entrambi la disinstallazione e la reinstallazione.

1. Disinstallare R Services (In-Database) e verificare che gli account utente per SQLRUserGroup vengano rimossi.

2. Riavviare il server e quindi reinstallare R Server (Standalone).

3. Eseguire il programma di installazione di SQL Server ancora una volta e questa volta selezionare **Aggiungi funzionalità a un'istanza esistente di SQL Server**.

4. Scegliere l'istanza e quindi selezionare l'opzione **R Services (In-Database)** da aggiungere.

Se questa procedura non riesce a risolvere il problema, provare la soluzione alternativa seguente:

1. Disinstallare R Services (In-Database) e R Server (Standalone) nello stesso momento.

2. Rimuovere gli account utente locali (SQLRUserGroup).

3. Riavviare il server.

4. Eseguire il programma di installazione di SQL Server e aggiungere solo la funzionalità R Services (In-Database). Non selezionare **R Server (Standalone)** .

In genere, è consigliabile non installare sia R Services (In-Database) che R Server (Standalone) nello stesso computer. Tuttavia, supponendo che il server disponga di capacità sufficiente, R Server Standalone potrebbe essere utile come strumento di sviluppo. Un altro possibile scenario è la necessità di usare le funzionalità di operazionalizzazione di R Server, ma anche l'accesso ai dati di SQL Server senza spostamento dei dati.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Le versioni di R Client e R Server non sono compatibili

Se si installa Microsoft R Client e lo si usa per eseguire R in un contesto di calcolo di SQL Server remoto, potrebbe essere presente un errore simile al seguente:

*You are running version 9.0.0 of Microsoft R Client on your computer, which is incompatible with the Microsoft R Server version 8.0.3. Download and install a compatible version.* (Sul computer è in esecuzione la versione 9.0.0 di Microsoft R, che non è compatibile con Microsoft R Server versione 8.0.3. Scaricare e installare una versione compatibile.)

In SQL Server 2016, era necessario che la versione di R eseguita in R Services per SQL Server fosse esattamente la stessa delle librerie in Microsoft R Client. Questo requisito è stato rimosso nelle versioni successive. È tuttavia consigliabile ottenere sempre le versioni più recenti dei componenti di Machine Learning e installare tutti i Service Pack. 

Se è disponibile una versione precedente di Microsoft R Server, per garantire la compatibilità con Microsoft R Client 9.0.0, installare gli aggiornamenti descritti in questo [articolo del supporto tecnico](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>L'installazione non riesce con l'errore "Only one Revolution Enterprise product can be installed at a time." (È possibile installare un solo prodotto Revolution Enterprise alla volta.)

Questo errore può verificarsi se si dispone di un'installazione precedente dei prodotti Revolution Analytics o di una versione non definitiva di SQL Server R Services. Prima di poter installare una versione più recente di Microsoft R Server, è necessario disinstallare le versioni precedenti. L'installazione side-by-side con altre versioni degli strumenti Revolution Enterprise non è supportata.

Tuttavia, le installazioni side-by-side sono supportate quando si usa R Server (Standalone) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] o SQL Server 2016.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Pulizia del Registro di sistema per disinstallare i componenti precedenti

Se si riscontrano problemi durante la rimozione di una versione precedente, può essere necessario modificare il Registro di sistema per rimuovere le chiavi correlate.

> [!IMPORTANT]
> Questo problema riguarda solo i casi in cui è installata una versione non definitiva di Microsoft R Server o una versione CTP di SQL Server 2016 R Services.
  
1. Aprire il Registro di sistema di Windows e individuare questa chiave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.
2. Eliminare una qualsiasi delle voci seguenti, se presente e se la chiave contiene solo il valore `sEstimatedSize2`:
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (per 8.0.2)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (per 8.0.1)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (per 8.0.0)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (per 7.5.0)

## <a name="see-also"></a>Vedere anche

 [Machine Learning Services per SQL Server (In-Database)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (Standalone)](../r/r-server-standalone.md)
