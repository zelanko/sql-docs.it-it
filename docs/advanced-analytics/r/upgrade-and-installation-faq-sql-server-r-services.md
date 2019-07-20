---
title: Domande frequenti sull'aggiornamento e sull'installazione
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
ms.openlocfilehash: 71a6149f1d89a4a1df114f376c250c203a8721cf
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344914"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Domande frequenti sull'installazione e sull'aggiornamento per SQL Server Machine Learning o R Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo argomento fornisce le risposte ad alcune domande comuni sull'installazione delle funzionalità di Machine Learning in SQL Server. Vengono inoltre illustrate le domande frequenti sugli aggiornamenti.

+ Alcuni problemi si verificano solo con gli aggiornamenti delle versioni preliminari. È pertanto consigliabile identificare la versione e l'edizione prima di leggere le note. Per ottenere informazioni sulla versione, `@@VERSION` eseguire in una query da SQL Server Management Studio.
+ Eseguire l'aggiornamento alla versione più recente o al rilascio del servizio il prima possibile per risolvere eventuali problemi risolti nelle versioni recenti.

**Si applica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (in-database)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Requisiti e restrizioni per le versioni precedenti di SQL Server 2016 

A seconda della compilazione di SQL Server che si sta installando, è possibile che si applichino alcune delle limitazioni seguenti:

- Nelle prime versioni di SQL Server 2016 R Services è richiesta la notazione 8dot3 nell'unità che contiene la directory di lavoro. Se è stata installata una versione non definitiva, l'aggiornamento a SQL Server 2016 Service Pack 1 dovrebbe risolvere il problema. Questo requisito non si applica alle versioni successive a SP1.

- Attualmente non è possibile installare [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] in un cluster di failover. Tuttavia, SQL Server anteprima 2019 fornisce supporto per il failover se si desidera valutare questa funzionalità in un ambiente di testing. Per ulteriori informazioni [, vedere Novità](../what-s-new-in-sql-server-machine-learning-services.md).

- In una macchina virtuale di Azure potrebbe essere necessaria una configurazione aggiuntiva. Ad esempio, potrebbe essere necessario creare un'eccezione del firewall per supportare l'accesso remoto.

- Non è supportata l'installazione side-by-side con un'altra versione di R o con altre versioni di Revolution Analytics.

- Disabilitare l'analisi dei virus prima di iniziare l'installazione. Al termine dell'installazione, si consiglia di sospendere l'analisi antivirus sulle cartelle utilizzate [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]da. Preferibilmente, sospendere l'analisi sull'intero [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] albero.

 - Installazione di Microsoft R Server in un'istanza di SQL Server installata in Windows Core. Nella versione RTM di SQL Server 2016, si è verificato un problema noto durante l'aggiunta di Microsoft R Server a un'istanza di in Windows Server Core Edition. Questo problema è stato risolto. Se si verifica questo problema, è possibile applicare la correzione descritta in [KB3164398](https://support.microsoft.com/kb/3164398) per aggiungere la funzionalità R all'istanza esistente in Windows Server Core. Per altre informazioni, vedere [Impossibile installare Microsoft R Server (autonomo) in un sistema operativo Windows Server Core](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Installazione offline dei componenti di machine learning per una versione localizzata di SQL Server 2016

Nelle versioni precedenti di SQL Server 2016 non è stato possibile installare i file CAB specifici delle impostazioni locali durante l'installazione offline senza una connessione Internet. Questo problema è stato risolto nelle versioni successive, ma se il programma di installazione restituisce un messaggio che informa che non è possibile installare la lingua corretta, è possibile modificare il nome file per consentire il proseguimento del programma di installazione.

+ Modificare manualmente il file del programma di installazione per assicurarsi che sia installata la lingua corretta. Ad esempio, per installare la versione giapponese di SQL Server, è necessario modificare il nome del file da SRS_ 8.0.3.0 _**1033**. cab a srs_ 8.0.3.0 _**1041**. cab.
+ L'identificatore di lingua usato per i componenti di Machine Learning deve corrispondere alla lingua di installazione SQL Server oppure non è possibile completare l'installazione.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Versioni preliminari: criteri di supporto, aggiornamento e problemi noti

Le nuove installazioni di qualsiasi versione non definitiva di [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] non sono più supportate. Se si usa una versione provvisoria, eseguire l'aggiornamento appena possibile.

In questa sezione vengono fornite istruzioni dettagliate per scenari di aggiornamento specifici.

### <a name="how-to-upgrade-sql-server"></a>Come aggiornare SQL Server

Per aggiornare la versione di SQL Server, è possibile eseguire nuovamente l'installazione guidata.

+ [Eseguire l'aggiornamento di SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Aggiornare SQL Server utilizzando l'installazione guidata](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

È possibile aggiornare solo i componenti di Machine Learning usando un processo denominato binding: 
+ [Usare sqlbindr per aggiornare i componenti di Machine Learning](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fine del supporto per gli aggiornamenti sul posto dalle versioni provvisorie

Gli aggiornamenti da versioni non definitive di SQL Server 2016 non sono più supportati. Sono inclusi SQL Server 2016 CTP3, CTP 3.1, CTP 3.2, RC0 o RC1.

Le versioni seguenti sono state installate con le versioni provvisorie di SQL Server 2016.

| Version | Compilazione         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

In caso di dubbi sulla versione in uso, eseguire `@@VERSION` una query da SQL Server Management Studio.

In generale, il processo di aggiornamento è il seguente:

1. Eseguire il backup di script e dati.
2. Disinstallare la versione non definitiva.
3. Installare una versione di rilascio.

La disinstallazione di una versione non definitiva di SQL Server componenti di machine learning può essere complessa e potrebbe richiedere l'esecuzione di uno script speciale. Contattare il supporto tecnico.

###  <a name="bkmk_Uninstall"></a>Disinstalla prima dell'aggiornamento da una versione precedente di Microsoft R Server

Se è installata una versione non definitiva di Microsoft R Server, è necessario disinstallarla prima dell'aggiornamento a una versione più recente.

1.  Nel **Pannello di controllo**fare clic su **Installazione applicazioni**e selezionare `Microsoft SQL Server 2016 <version number>`.

2.  Nella finestra di dialogo con le opzioni per **aggiungere**, **ripristinare**o **rimuovere** i componenti selezionare **Rimuovi**.
  
3.  Nella pagina **Seleziona funzionalità** , in **Funzionalità condivise**, selezionare **R Server (Standalone)** . Fare clic su **Avanti**e quindi su **Fine** per disinstallare solo i componenti selezionati.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>Errori side-by-side di R Services e R Server (autonomo) 

Nelle versioni precedenti di SQL Server 2016, l'installazione di R Server (standalone) e R Services (in-database) allo stesso tempo causava talvolta un errore di installazione con un messaggio "accesso negato". Questo problema è stato risolto nel Service Pack 1 per SQL Server 2016.

Se si è verificato questo errore ed è necessario aggiornare queste funzionalità, eseguire un'installazione integrata di SQL Server 2016 con SP1. Esistono due modi per risolvere il problema, entrambi i quali richiedono la disinstallazione e la reinstallazione.

1. Disinstallare R Services (in-database) e verificare che gli account utente per SQLRUserGroup siano rimossi.

2. Riavviare il server, quindi reinstallare R Server (standalone).

3. Eseguire SQL Server installazione ancora una volta e questa volta selezionare **Aggiungi funzionalità a SQL Server esistente**.

4. Scegliere l'istanza e quindi selezionare l'opzione **R Services (in-database)** da aggiungere.

Se questa procedura non riesce a risolvere il problema, provare la soluzione alternativa seguente:

1. Disinstallare R Services (in-database) e R Server (standalone) nello stesso momento.

2. Rimuovere gli account utente locali (SQLRUserGroup).

3. Riavviare il server.

4. Eseguire SQL Server installazione e aggiungere la funzionalità R Services (in-database). Non selezionare **R Server (standalone)** .

In genere, è consigliabile non installare sia R Services (in-database) che R Server (standalone) nello stesso computer. Tuttavia, supponendo che il server disponga di capacità sufficiente, potrebbe essere utile R Server autonomo come strumento di sviluppo. Un altro possibile scenario è che è necessario usare le funzionalità di operatività di R Server, ma anche l'accesso ai dati SQL Server senza spostamento dei dati.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Le versioni di R Client e R Server non sono compatibili

Se si installa Microsoft R Client e lo si usa per eseguire R in un contesto di calcolo SQL Server remoto, potrebbe essere presente un errore simile al seguente:

*Si sta eseguendo la versione 9.0.0 di Microsoft R client nel computer, che non è compatibile con la versione di Microsoft R Server 8.0.3. Download and install a compatible version.* (Sul computer è in esecuzione la versione 9.0.0 di Microsoft R, che non è compatibile con Microsoft R Server versione 8.0.3. Scaricare e installare una versione compatibile.)

In SQL Server 2016, era necessario che la versione di R eseguita in R Services per SQL Server corrisponda esattamente alle librerie in Microsoft R Client. Questo requisito è stato rimosso nelle versioni successive. È tuttavia consigliabile ottenere sempre le versioni più recenti dei componenti di machine learning e installare tutti i Service Pack. 

Se si dispone di una versione precedente di Microsoft R Server ed è necessario garantire la compatibilità con Microsoft R Client 9.0.0, installare gli aggiornamenti descritti in questo [articolo del supporto tecnico](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>L'installazione non riesce con l'errore "Only one Revolution Enterprise product can be installed at a time." (È possibile installare un solo prodotto Revolution Enterprise alla volta.)

Questo errore può verificarsi se si dispone di un'installazione precedente dei prodotti Revolution Analytics o di una versione non definitiva di SQL Server R Services. Prima di poter installare una versione più recente di Microsoft R Server, è necessario disinstallare le versioni precedenti. L'installazione side-by-side con altre versioni degli strumenti Revolution Enterprise non è supportata.

Tuttavia, le installazioni side-by-side sono supportate quando si usa R Server (Standalone) con [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] o SQL Server 2016.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Pulizia del registro di sistema per disinstallare i componenti precedenti

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

 [SQL Server Machine Learning Services (in-database)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (autonomo)](../r/r-server-standalone.md)
