---
title: Installazione e aggiornamento domande frequenti (FAQ) - servizi di SQL Server Machine Learning
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/15/2018
ms.topic: conceptual
ms.author: davidph
author: dphansen
manager: cgronlun
ms.openlocfilehash: 3a4a0c740268a8e2d6691e3c8a87634cc05f9ab1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642312"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Domande frequenti su installazione e aggiornamento per R Server o SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In questo argomento offre risposta ad alcune domande comuni sull'installazione di machine learning funzionalità in SQL Server. Contiene anche domande comuni sugli aggiornamenti.

+ Alcuni problemi si verificano solo con gli aggiornamenti da versioni non definitive. Pertanto, è consigliabile identificare la versione ed edizione innanzitutto prima di leggere queste note. Per ottenere informazioni sulla versione, eseguire `@@VERSION` in una query da SQL Server Management Studio.
+ Eseguire l'aggiornamento per la versione più recente o una versione del servizio appena possibile per risolvere eventuali problemi che sono stati risolti nelle versioni recenti.

**Si applica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (In-Database)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisiti e restrizioni per le versioni precedenti di SQL Server 2016 

A seconda della compilazione di SQL Server che si sta installando, potrebbe applicare alcune delle limitazioni seguenti:

- Nelle prime versioni di SQL Server 2016 R Services, la notazione 8.3 dovevano sull'unità contenente la directory di lavoro. Se è installata una versione non definitiva, l'aggiornamento a SQL Server 2016 Service Pack 1 dovrebbe risolvere il problema. Questo requisito non si applica alle versioni dopo il SP1.

- Attualmente, non è possibile installare [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] in un cluster di failover. Tuttavia, anteprima di SQL Server 2019 fornisce supporto per il failover se si vuole valutare questa capablity in un ambiente di test. Per altre informazioni, vedere [What ' s New](../what-s-new-in-sql-server-machine-learning-services.md).

- In una VM di Azure, potrebbe essere necessaria un'ulteriore configurazione. Ad esempio, si potrebbe essere necessario creare un'eccezione del firewall per supportare l'accesso remoto.

- Installazione side-by-side con un'altra versione di R o con versioni diverse da Revolution Analitica, non è supportata.

- Disabilitare l'antivirus prima di iniziare l'installazione. Al termine dell'installazione, si consiglia di sospendere la ricerca dei virus nelle cartelle utilizzate da [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]. Preferibilmente, sospendere l'analisi nell'intero [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] struttura ad albero.

 - Installare Microsoft R Server in un'istanza di SQL Server installata in Windows Core. Nella versione RTM di SQL Server 2016, si è verificato un problema noto durante l'aggiunta di Microsoft R Server in un'istanza nell'edizione di Windows Server Core. Questo problema è stato risolto. Se si verifica questo problema, è possibile applicare la correzione descritta nel [KB3164398](https://support.microsoft.com/kb/3164398) per aggiungere la funzionalità R all'istanza esistente in Windows Server Core. Per altre informazioni, vedere [Impossibile installare Microsoft R Server (autonomo) in un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Installazione offline di componenti di apprendimento automatico per una versione localizzata di SQL Server 2016

Prime versioni di SQL Server 2016 non è stato possibile installare i file con estensione cab specifiche delle impostazioni locali durante l'installazione offline senza una connessione internet. Questo problema è stato risolto nelle versioni successive, ma se il programma di installazione restituisce un messaggio che informa che non è possibile installare quella desiderata, è possibile modificare il nome del file per consentire il proseguimento dell'installazione.

+ Modificare manualmente il file di programma di installazione per assicurarsi che sia installata la lingua corretta. Ad esempio, per installare la versione giapponese di SQL Server, si potrebbe modificare il nome del file da SRS_8.0.3.0_**1033**CAB a SRS_8.0.3.0_**1041**CAB.
+ L'identificatore di lingua utilizzata per l'apprendimento di componenti deve essere quello utilizzato per la lingua di installazione di SQL Server oppure è possibile completare l'installazione.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versioni non definitive: supporta i criteri di aggiornamento e problemi noti

Le nuove installazioni di qualsiasi versione non definitiva di [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] non è più supportata. Se si usa una versione non definitiva, eseguire l'aggiornamento appena possibile.

In questa sezione contiene istruzioni dettagliate per scenari di aggiornamento specifici.

### <a name="how-to-upgrade-sql-server"></a>Come eseguire l'aggiornamento di SQL Server

È possibile aggiornare la versione di SQL Server eseguendo di nuovo l'installazione guidata.

+ [Eseguire l'aggiornamento di SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Aggiornamento di SQL Server usando l'installazione guidata](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

È possibile eseguire l'aggiornamento solo di machine learning componenti tramite un processo denominato associazione: 
+ [Usare SqlBindR per aggiornare i componenti di apprendimento automatico](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fine del supporto per gli aggiornamenti sul posto da versioni non definitive

Gli aggiornamenti da versioni non definitive di SQL Server 2016 non sono più supportati. Ciò include SQL Server 2016 CTP3, CTP3.1, CTP3.2, RC0 o RC1.

Le versioni seguenti sono state installate con versioni non definitive di SQL Server 2016.

| Version | Compilazione         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Se si hanno dubbi sulla versione in uso, eseguire `@@VERSION` in una query da SQL Server Management Studio.

In generale, il processo per l'aggiornamento è come segue:

1. Eseguire il backup dei dati e script.
2. Disinstallare la versione non definitiva.
3. Installare una versione di rilascio.

Disinstallazione di una versione non definitiva di SQL Server componenti di apprendimento automatico possono risultare complessi e potrebbe richiedere l'esecuzione di uno script speciale. Contattare il supporto tecnico.

###  <a name="bkmk_Uninstall"></a> Disinstallare prima l'aggiornamento da una versione precedente di Microsoft R Server

Se è installata una versione non definitiva di Microsoft R Server, è necessario disinstallarla prima dell'aggiornamento a una versione più recente.

1.  Nel **Pannello di controllo**fare clic su **Installazione applicazioni**e selezionare `Microsoft SQL Server 2016 <version number>`.

2.  Nella finestra di dialogo con le opzioni per **aggiungere**, **ripristinare**o **rimuovere** i componenti selezionare **Rimuovi**.
  
3.  Nella pagina **Seleziona funzionalità** , in **Funzionalità condivise**, selezionare **R Server (Standalone)**. Fare clic su **Avanti**e quindi su **Fine** per disinstallare solo i componenti selezionati.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services e gli errori side-by-side di R Server (Standalone) 

Nelle versioni precedenti di SQL Server 2016, l'installazione di R Server (Standalone) e R Services (In-Database) nello stesso momento talvolta installazione a causa di esito negativo con un messaggio "accesso negato". Questo problema è stato risolto nel Service Pack 1 per SQL Server 2016.

Se si ha rilevato l'errore ed è necessario eseguire l'aggiornamento di queste funzionalità, eseguire un'installazione integrata di SQL Server 2016 con SP1. Esistono due modi per risolvere il problema, che richiedono la disinstallazione e reinstallazione.

1. Disinstallare R Services (In-Database) e assicurarsi che gli account utente per SQLRUserGroup vengono rimossi.

2. Riavviare il server e quindi reinstallare R Server (Standalone).

3. Eseguire SQL Server di installazione una volta più e selezionare **aggiungere funzionalità a SQL Server esistente**.

4. Scegliere l'istanza e quindi selezionare il **R Services (In-Database)** opzione da aggiungere.

Se questa procedura non riesce a risolvere il problema, provare a eseguire la soluzione alternativa seguente:

1. Disinstallare R Server (Standalone) e R Services (In-Database) nello stesso momento.

2. Rimuovere gli account utente locale (SQLRUserGroup).

3. Riavviare il server.

4. Eseguire il programma di installazione di SQL Server e aggiungere solo la funzionalità R Services (In-Database). Non si seleziona **R Server (Standalone)**.

In generale, è consigliabile che non si installa R Services (In-Database) sia R Server (Standalone) nello stesso computer. Supponendo che il server dispone di sufficiente capacità, tuttavia, può risultare che r Server (Standalone) potrebbe essere utile come strumento di sviluppo. Un altro possibile scenario è che è necessario usare le funzionalità di operazionalizzazione di R Server, ma desidera anche accedere ai dati di SQL Server senza spostare i dati.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Le versioni di R Client e R Server non sono compatibili

Se si installa Microsoft R Client e usarlo per eseguire R in un contesto di calcolo di SQL Server remoto, è possibile ottenere un errore simile al seguente:

*Si sta usando il computer che non è compatibile con Microsoft R Server versione 8.0.3 versione 9.0.0 di Microsoft R client. Download and install a compatible version.* (Sul computer è in esecuzione la versione 9.0.0 di Microsoft R, che non è compatibile con Microsoft R Server versione 8.0.3. Scaricare e installare una versione compatibile.)

In SQL Server 2016, era necessario che la versione di R che era in esecuzione in SQL Server R Services coincidere esattamente le librerie disponibili in Microsoft R Client. Tale requisito è stato rimosso nelle versioni successive. Tuttavia, è consigliabile che sempre ottenere le versioni più recenti di apprendimento di componenti e installare tutti i service pack. 

Se si ha una versione precedente di Microsoft R Server ed è necessario garantire la compatibilità con Microsoft R Client 9.0.0, installare gli aggiornamenti descritti in questo [articolo del supporto tecnico](https://support.microsoft.com/kb/3210262).


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

 [SQL Server Machine Learning Services (In-Database)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (Standalone)](../r/r-server-standalone.md)
