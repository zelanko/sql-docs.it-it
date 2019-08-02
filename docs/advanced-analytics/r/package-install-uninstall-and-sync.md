---
title: Sincronizzazione dei pacchetti R dal file system
description: Aggiornare le librerie R in SQL Server con le versioni più recenti installate nel file system.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4e0b6133bcecc553934cd657785ea9ee765c6fd9
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715069"
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronizzazione dei pacchetti R per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La versione di RevoScaleR inclusa in SQL Server 2017 include la possibilità di sincronizzare le raccolte di pacchetti R tra i file system e l'istanza di e il database in cui vengono usati i pacchetti.

Questa funzionalità è stata fornita per semplificare il backup delle raccolte di pacchetti R associate a SQL Server database. Grazie a questa funzionalità, un amministratore può ripristinare non solo il database, ma tutti i pacchetti R usati dai data scientist che lavorano in tale database.

Questo articolo descrive la funzionalità di sincronizzazione dei pacchetti e come usare la funzione [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) per eseguire le attività seguenti:

+ Sincronizzare un elenco di pacchetti per un intero database di SQL Server

+ Sincronizzare i pacchetti utilizzati da un singolo utente o da un gruppo di utenti

+ Se un utente passa a un SQL Server diverso, è possibile eseguire un backup del database di lavoro dell'utente e ripristinarlo nel nuovo server e i pacchetti per l'utente verranno installati nel file system nel nuovo server, come richiesto da R.

È ad esempio possibile usare la sincronizzazione dei pacchetti in questi scenari:

+ L'amministratore di database ha ripristinato un'istanza di SQL Server in un nuovo computer e chiede agli utenti di connettersi dai client `rxSyncPackages` R ed eseguire per aggiornare e ripristinare i pacchetti.

+ Si ritiene che un pacchetto R nel file System sia danneggiato in modo da `rxSyncPackages` essere eseguito nel SQL Server.

## <a name="requirements"></a>Requisiti

Prima di poter usare la sincronizzazione dei pacchetti, è necessario disporre della versione appropriata di Microsoft R o Machine Learning Server. Questa funzionalità è disponibile in Microsoft R Version 9.1.0 o versioni successive. 

È inoltre necessario abilitare la [funzionalità di gestione pacchetti](r-package-how-to-enable-or-disable.md) sul server.

### <a name="determine-whether-your-server-supports-package-management"></a>Determinare se il server supporta la gestione dei pacchetti

Questa funzionalità è disponibile in SQL Server 2017 CTP 2 o versione successiva.

È possibile aggiungere questa funzionalità a un'istanza di SQL Server 2016 aggiornando l'istanza di per usare la versione più recente di Microsoft R. Per altre informazioni, vedere [usare Sqlbindr. exe per aggiornare R Services per SQL Server](../install/upgrade-r-and-python.md).

### <a name="enable-the-package-management-feature"></a>Abilitare la funzionalità di gestione dei pacchetti

Per utilizzare la sincronizzazione dei pacchetti, è necessario che la nuova funzionalità di gestione pacchetti sia abilitata nell'istanza di SQL Server e nei singoli database. Per ulteriori informazioni, vedere [abilitare o disabilitare la gestione dei pacchetti per SQL Server](r-package-how-to-enable-or-disable.md).

1. L'amministratore del server Abilita la funzionalità per l'istanza di SQL Server.
2. Per ogni database, l'amministratore concede ai singoli utenti la possibilità di installare o condividere pacchetti R usando i ruoli del database.

Al termine di questa operazione, è possibile utilizzare le funzioni RevoScaleR, ad esempio [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) per installare i pacchetti in un database.  Le informazioni sugli utenti e i pacchetti che è possibile utilizzare vengono archiviati nell'istanza di SQL Server. 

Ogni volta che si aggiunge un nuovo pacchetto utilizzando le funzioni di gestione dei pacchetti, vengono aggiornati sia i record in SQL Server che i file system. Queste informazioni possono essere utilizzate per ripristinare le informazioni sul pacchetto per l'intero database.

### <a name="permissions"></a>Permissions

+ La persona che esegue la funzione di sincronizzazione del pacchetto deve essere un'entità di sicurezza sull'istanza SQL Server e sul database che contiene i pacchetti.

+ Il chiamante della funzione deve essere un membro di uno di questi ruoli di gestione dei pacchetti: **rpkgs-Shared** o **rpkgs-private**.

+ Per sincronizzare i pacchetti contrassegnati come **condivisi**, la persona che esegue la funzione deve essere membro del ruolo **rpkgs-Shared** e i pacchetti da spostare devono essere stati installati in una libreria con ambito condiviso.

+ Per sincronizzare i pacchetti contrassegnati come **privati**, il proprietario del pacchetto o l'amministratore deve eseguire la funzione e i pacchetti devono essere privati.

+ Per sincronizzare i pacchetti per conto di altri utenti, il proprietario deve essere un membro del ruolo del database **db_owner** .

## <a name="how-package-synchronization-works"></a>Funzionamento della sincronizzazione del pacchetto

Per usare la sincronizzazione dei pacchetti, chiamare [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), che è una nuova funzione in [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). 

Per ogni chiamata a `rxSyncPackages`, è necessario specificare un'istanza di SQL Server e un database. Quindi, elencare i pacchetti da sincronizzare o specificare l'ambito del pacchetto.

1. Creare il contesto di calcolo SQL Server usando la `RxInSqlServer` funzione. Se non si specifica un contesto di calcolo, viene usato il contesto di calcolo corrente.

2. Consente di specificare il nome di un database nell'istanza nel contesto di calcolo specificato. I pacchetti sono sincronizzati per ogni database.

3. Specificare i pacchetti da sincronizzare utilizzando l'argomento scope.

    Se si usa l'ambito **privato** , vengono sincronizzati solo i pacchetti di proprietà del proprietario specificato. Se si specifica l'ambito **condiviso** , tutti i pacchetti non privati nel database vengono sincronizzati. 
    
    Se si esegue la funzione senza specificare un ambito **privato** o **condiviso** , tutti i pacchetti vengono sincronizzati.

4. Se il comando ha esito positivo, i pacchetti esistenti nel file system vengono aggiunti al database, con l'ambito e il proprietario specificati.

    Se la file system è danneggiata, i pacchetti vengono ripristinati in base all'elenco gestito nel database.

    Se la funzionalità di gestione dei pacchetti non è disponibile nel database di destinazione, viene generato un errore: "La funzionalità di gestione pacchetti non è abilitata per la SQL Server o la versione è obsoleta"

### <a name="example-1-synchronize-all-package-by-database"></a>Esempio 1. Sincronizza tutto il pacchetto per database

In questo esempio vengono recuperati tutti i nuovi pacchetti dal file system locale e vengono installati i pacchetti nel database [TestDB]. Poiché nessun proprietario è specifico, l'elenco include tutti i pacchetti che sono stati installati per ambiti privati e condivisi.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>Esempio 2. Limitare i pacchetti sincronizzati per ambito

Negli esempi seguenti vengono sincronizzati solo i pacchetti nell'ambito specificato.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>Esempio 3. Limitare i pacchetti sincronizzati per proprietario

Nell'esempio seguente viene illustrato come sincronizzare solo i pacchetti installati per un utente specifico. In questo esempio, l'utente è identificato dal nome dell'account di accesso SQL *User1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>Risorse correlate

[Gestione dei pacchetti R per SQL Server](install-additional-r-packages-on-sql-server.md)
