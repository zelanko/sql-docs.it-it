---
title: Sincronizzazione del pacchetto R dal file system - servizi di SQL Server Machine Learning
description: Aggiornare le librerie di R in SQL Server con le versioni più recenti installate nel file system.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 57677e8d7573411be2e77baa7ffd8564ec9cbeb4
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511358"
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronizzazione tramite il pacchetto R per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La versione di RevoScaleR incluso in SQL Server 2017 include la possibilità di sincronizzare le raccolte di pacchetti R tra il file system e l'istanza e database in cui vengono utilizzati i pacchetti.

Questa funzionalità è stata fornita per renderne più semplice eseguire il backup le raccolte di pacchetti R associate ai database di SQL Server. Usando questa funzionalità, un amministratore può ripristinare non solo il database, ma tutti i pacchetti R che sono stati usati dai data Scientist di utilizzo del database.

Questo articolo descrive la funzionalità di sincronizzazione di pacchetto e come usare il [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) funzione per eseguire le attività seguenti:

+ Sincronizzare un elenco di pacchetti per un intero database di SQL Server

+ Sincronizzare i pacchetti usati da un singolo utente o da un gruppo di utenti

+ Se un utente passa a un Server SQL differente, è possibile eseguire un backup del database di lavoro dell'utente e ripristinarlo nel nuovo server e verranno installati i pacchetti per l'utente nei file system nel nuovo server, come richiesto da R.

Ad esempio, è possibile utilizzare la sincronizzazione di pacchetti in questi scenari:

+ L'amministratore di database è ripristinato un'istanza di SQL Server in un nuovo computer e richiede agli utenti di connettersi dai committenti R ed eseguire `rxSyncPackages` per aggiornare e ripristinare i propri pacchetti.

+ Si ritiene che un pacchetto R nel file system è danneggiato, pertanto si esegue `rxSyncPackages` in SQL Server.

## <a name="requirements"></a>Requisiti

Prima di poter usare la sincronizzazione di pacchetto, è necessario disporre la versione appropriata di Machine Learning Server o Microsoft R. Questa funzionalità viene fornita in Microsoft R versione 9.1.0 o versione successiva. 

È necessario abilitare anche il [funzionalità di gestione pacchetti](r-package-how-to-enable-or-disable.md) nel server.

### <a name="determine-whether-your-server-supports-package-management"></a>Determinare se il server supporta la gestione dei pacchetti

Questa funzionalità è disponibile in SQL Server 2017 CTP 2 o versione successiva.

È possibile aggiungere questa funzionalità a un'istanza di SQL Server 2016 per l'aggiornamento dell'istanza per usare la versione più recente di Microsoft R. Per altre informazioni, vedere [SqlBindR.exe Usa per eseguire l'aggiornamento di SQL Server R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="enable-the-package-management-feature"></a>Abilitare la funzionalità di gestione pacchetti

Per utilizzare la sincronizzazione del pacchetto richiede che la nuova funzionalità di gestione pacchetti sia abilitata nell'istanza di SQL Server e nei singoli database. Per altre informazioni, vedere [abilitare o disabilitare la gestione dei pacchetti per SQL Server](r-package-how-to-enable-or-disable.md).

1. L'amministratore del server abilita la funzionalità per l'istanza di SQL Server.
2. Per ogni database, l'amministratore concede singoli utenti la possibilità di installare o condividere pacchetti di R, usando ruoli predefiniti del database.

Quando questa operazione, è possibile usare funzioni RevoScaleR, ad esempio [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) per installare i pacchetti in un database.  Informazioni sugli utenti e i pacchetti che possono utilizzare viene archiviate nell'istanza di SQL Server. 

Ogni volta che si aggiunge un nuovo pacchetto utilizzando le funzioni di gestione pacchetti, entrambi i record in SQL Server e il file system vengono aggiornati. Queste informazioni sono utilizzabile per ripristinare le informazioni del pacchetto per l'intero database.

### <a name="permissions"></a>Permissions

+ La persona che esegue la funzione di sincronizzazione del pacchetto deve essere un'entità per l'istanza di SQL Server e database che contiene i pacchetti di sicurezza.

+ Il chiamante della funzione deve essere un membro di uno di questi ruoli di gestione del pacchetto: **rpkgs-shared** oppure **rpkgs-private**.

+ Per sincronizzare i pacchetti contrassegnati come **condivisa**, la persona che sta eseguendo la funzione deve essere un membro di **rpkgs-shared** ruolo e i pacchetti che devono essere spostati sia stato installato per un oggetto condiviso libreria di ambito.

+ Per sincronizzare i pacchetti contrassegnati come **privato**, sia il proprietario del pacchetto o l'amministratore deve eseguire la funzione e i pacchetti devono essere privati.

+ Per sincronizzare i pacchetti per conto di altri utenti, il proprietario deve BA un membro del **db_owner** ruolo predefinito del database.

## <a name="how-package-synchronization-works"></a>Funzionamento della sincronizzazione del pacchetto

Per usare sincronizzazione del pacchetto, chiamare [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), che è una nuova funzione negli [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). 

Per ogni chiamata a `rxSyncPackages`, è necessario specificare un'istanza di SQL Server e database. Quindi, elencare i pacchetti per la sincronizzazione oppure specificare l'ambito del pacchetto.

1. Creare il contesto di calcolo di SQL Server usando il `RxInSqlServer` (funzione). Se non si specifica un contesto di calcolo, viene usato il contesto di calcolo corrente.

2. Specificare il nome di un database nell'istanza nel contesto di calcolo specificato. I pacchetti vengono sincronizzati per ogni database.

3. Specificare i pacchetti per la sincronizzazione tramite l'argomento di ambito.

    Se si usa **privato** ambito, solo i pacchetti al proprietario specificato vengono sincronizzati. Se si specifica **condivisa** ambito, tutti i pacchetti non privata nel database sono sincronizzati. 
    
    Se si esegue la funzione senza specificare uno **privati** oppure **condiviso** ambito, vengono sincronizzati tutti i pacchetti.

4. Se il comando ha esito positivo, vengono aggiunti i pacchetti esistenti nel file system al database, con l'ambito specificato e il proprietario.

    Se il file system è danneggiato, i pacchetti vengono ripristinati in base all'elenco gestita nel database.

    Se la funzionalità di gestione pacchetti non è disponibile nel database di destinazione, viene generato un errore: "La funzionalità di gestione pacchetti non è abilitata in SQL Server o è troppo vecchia versione"

### <a name="example-1-synchronize-all-package-by-database"></a>Esempio 1. Sincronizzare tutti i pacchetti dal database

Questo esempio ottiene i nuovi pacchetti dal file system locale e installa i pacchetti nel database [TestDB]. Poiché nessun proprietario è specifico, l'elenco include tutti i pacchetti che sono stati installati per gli ambiti privati e condivisi.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>Esempio 2. Limitare i pacchetti sincronizzati dall'ambito di

Negli esempi seguenti sincronizzare solo i pacchetti nell'ambito specificato.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>Esempio 3. Limitare i pacchetti sincronizzati dal proprietario

Nell'esempio seguente viene illustrato come sincronizzare solo i pacchetti che sono stati installati per un utente specifico. In questo esempio, l'utente viene identificato dal nome dell'account di accesso SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>Risorse correlate

[Gestione dei pacchetti R per SQL Server](install-additional-r-packages-on-sql-server.md)
