---
title: Abilitare o disabilitare la gestione dei pacchetti R remoti
description: Abilitare la gestione dei pacchetti R remota in SQL Server 2016 R Services o SQL Server Machine Learning Services (in-database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 260109e978c8997622f24c41341e11f1e2efa7cc
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715636"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>Abilitare o disabilitare la gestione dei pacchetti remota per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive come abilitare la gestione remota dei pacchetti R da una workstation client o da un Machine Learning Server diverso. Una volta abilitata la funzionalità di gestione dei pacchetti in SQL Server, è possibile usare i comandi RevoScaleR in un client per installare i pacchetti in SQL Server.

> [!NOTE]
> Attualmente è supportata la gestione delle librerie R. il supporto per Python è nella roadmap.

Per impostazione predefinita, la funzionalità di gestione dei pacchetti esterna per SQL Server è disabilitata. È necessario eseguire uno script separato per abilitare la funzionalità come descritto nella sezione successiva.

## <a name="overview-of-process-and-tools"></a>Panoramica del processo e degli strumenti

Per abilitare o disabilitare la gestione dei pacchetti in SQL Server, utilizzare l'utilità da riga di comando **RegisterRExt. exe**, inclusa nel pacchetto **RevoScaleR** .

L'abilitazione [di questa funzionalità](#bkmk_enable) è un processo in due passaggi, che richiede un amministratore di database: si Abilita la gestione dei pacchetti nell'istanza di SQL Server (una volta per ogni istanza di SQL Server) e quindi si Abilita la gestione dei pacchetti nel database SQL (una volta per ogni database SQL Server ).

La [disabilitazione](#bkmk_disable) della funzionalità di gestione dei pacchetti richiede anche passaggi multipel: rimuovere le autorizzazioni e i pacchetti a livello di database (una volta per ogni database), quindi rimuovere i ruoli dal server (una volta per ogni istanza).

## <a name="bkmk_enable"></a>Abilita gestione pacchetti

1. In SQL Server aprire un prompt dei comandi con privilegi elevati e passare alla cartella che contiene l'utilità RegisterRExt. exe. Il percorso predefinito è `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Eseguire il comando seguente, fornendo gli argomenti appropriati per l'ambiente:

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Questo comando crea oggetti a livello di istanza nel computer SQL Server necessari per la gestione dei pacchetti. Riavvia anche la finestra di avvio per l'istanza.

    Se non si specifica un'istanza, viene utilizzata l'istanza predefinita. Se non si specifica un utente, viene utilizzato il contesto di sicurezza corrente. Ad esempio, il comando seguente consente la gestione dei pacchetti nell'istanza di nel percorso di RegisterRExt. exe, usando le credenziali dell'utente che ha aperto il prompt dei comandi:

    `REgisterRExt.exe /install pkgmgmt`

3. Per aggiungere la gestione dei pacchetti a un database specifico, eseguire il comando seguente da un prompt dei comandi con privilegi elevati:

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Questo comando crea alcuni elementi del database, inclusi i seguenti ruoli del database usati per controllare le autorizzazioni utente: `rpkgs-users`, `rpkgs-private`e `rpkgs-shared`.

    Ad esempio, il comando seguente abilita la gestione dei pacchetti nel database, nell'istanza in cui viene eseguito RegisterRExt. Se non si specifica un utente, viene utilizzato il contesto di sicurezza corrente.

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. Ripetere il comando per ogni database in cui devono essere installati i pacchetti.

5. Per verificare che i nuovi ruoli siano stati creati correttamente, in SQL Server Management Studio fare clic sul database, espandere **sicurezza**ed espandere **ruoli del database**.

    È anche possibile eseguire una query su sys. database_principals, ad esempio la seguente:

    ```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,   
        pr.authentication_type_desc, pe.state_desc,   
        pe.permission_name, s.name + '.' + o.name AS ObjectName  
    FROM sys.database_principals AS pr  
    JOIN sys.database_permissions AS pe  
        ON pe.grantee_principal_id = pr.principal_id  
    JOIN sys.objects AS o  
        ON pe.major_id = o.object_id  
    JOIN sys.schemas AS s  
        ON o.schema_id = s.schema_id;
    ```

Dopo aver abilitato questa funzionalità, è possibile usare la funzione RevoScaleR per installare o disinstallare i pacchetti da un client R remoto.

## <a name="bkmk_disable"></a>Disabilitare la gestione dei pacchetti

1. Da un prompt dei comandi con privilegi elevati, eseguire di nuovo l'utilità RegisterRExt e disabilitare la gestione dei pacchetti a livello di database:

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Questo comando rimuove gli oggetti di database correlati alla gestione dei pacchetti dal database specificato. Rimuove anche tutti i pacchetti installati dal percorso di file system protetto nel computer SQL Server.

2. Ripetere questo comando in ogni database in cui è stata usata la gestione dei pacchetti.

3.  Opzionale Dopo aver cancellato tutti i database dei pacchetti utilizzando il passaggio precedente, eseguire il comando seguente da un prompt dei comandi con privilegi elevati:

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Tramite questo comando viene rimossa la funzionalità di gestione pacchetti dall'istanza di. Potrebbe essere necessario riavviare manualmente il servizio Launchpad ancora una volta per visualizzare le modifiche.

## <a name="next-steps"></a>Passaggi successivi

+ [Usare RevoScaleR per installare nuovi pacchetti R](use-revoscaler-to-manage-r-packages.md)
+ [Suggerimenti per l'installazione di pacchetti R](packages-installed-in-user-libraries.md)
+ [Pacchetti predefiniti](../package-management/default-packages.md)
