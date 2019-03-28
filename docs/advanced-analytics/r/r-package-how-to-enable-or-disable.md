---
title: Abilitare o disabilitare la gestione dei pacchetti R remoto - servizi di SQL Server Machine Learning
description: Abilitare gestione remota dei pacchetti R in SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ee52fd9b7a116156f794303b828a83e9b06de6ab
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509818"
---
# <a name="enable-or-disable-remote-package-management-for-sql-server"></a>Abilitare o disabilitare la gestione dei pacchetti remote per SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Questo articolo descrive come abilitare gestione remota dei pacchetti R da una workstation client o una versione diversa di Machine Learning Server. Dopo avere abilitata la funzionalità di gestione pacchetti in SQL Server, è possibile utilizzare i comandi di RevoScaleR in un client per installare i pacchetti in SQL Server.

> [!NOTE]
> Gestione delle librerie di R è attualmente supportata; supporto per Python è implementata in futuro.

Per impostazione predefinita, la funzionalità di gestione pacchetti esterni per SQL Server è disabilitata. È necessario eseguire uno script separato per abilitare la funzionalità, come descritto nella sezione successiva.

## <a name="overview-of-process-and-tools"></a>Panoramica del processo e gli strumenti

Per abilitare o disabilitare la gestione dei pacchetti in SQL Server, utilizzare l'utilità della riga di comando **RegisterRExt.exe**, che viene incluso con il **RevoScaleR** pacchetto.

[Abilitazione](#bkmk_enable) questa funzionalità è un processo in due passaggi, che richiede un amministratore del database: si Abilita gestione dei pacchetti nell'istanza di SQL Server (una sola volta per ogni istanza di SQL Server) e quindi abilitare la gestione dei pacchetti nel database di SQL (una sola volta per ogni SQL Server database).

[La disabilitazione](#bkmk_disable) la funzionalità di gestione di pacchetti richiede passaggi multipel: rimuovere i pacchetti a livello di database e le autorizzazioni (una sola volta per ogni database) e quindi rimuovere i ruoli del server (una sola volta per ogni istanza).

## <a name="bkmk_enable"></a> Abilitare la gestione dei pacchetti

1. In SQL Server, aprire un prompt dei comandi con privilegi elevati e passare alla cartella contenente l'utilità, RegisterRExt.exe. Il percorso predefinito è `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExe.exe`.

2. Eseguire il comando seguente, che fornisce gli argomenti appropriati per l'ambiente:

    `RegisterRExt.exe /install pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Questo comando crea gli oggetti a livello di istanza nel computer SQL Server che sono necessari per la gestione dei pacchetti. Riavvia anche la finestra di avvio per l'istanza.

    Se non si specifica un'istanza, viene utilizzata l'istanza predefinita. Se non si specifica un utente, viene utilizzato il contesto di sicurezza corrente. Ad esempio, il comando seguente consente la gestione di pacchetti nell'istanza nel percorso di RegisterRExt.exe, utilizzando le credenziali dell'utente che ha aperto il prompt dei comandi:

    `REgisterRExt.exe /install pkgmgmt`

3. Per aggiungere Gestione dei pacchetti a un database specifico, eseguire il comando seguente da un prompt dei comandi con privilegi elevati:

    `RegisterRExt.exe /install pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`
   
    Questo comando crea alcuni elementi del database, inclusi i seguenti ruoli del database vengono utilizzati per controllare le autorizzazioni utente: `rpkgs-users`, `rpkgs-private`, e `rpkgs-shared`.

    Ad esempio, il comando seguente consente la gestione di pacchetti nel database, nell'istanza in cui viene eseguito RegisterRExt. Se non si specifica un utente, viene utilizzato il contesto di sicurezza corrente.

    `RegisterRExt.exe /install pkgmgmt /database:TestDB`

4. Ripetere il comando per ogni database in cui i pacchetti devono essere installati.

5. Per verificare che i nuovi ruoli siano stati creati correttamente, SQL Server Management Studio, fare clic con il database, espandere **sicurezza**, espandere **ruoli predefiniti del Database**.

    È anche possibile eseguire una query su Sys. database_principals come il seguente:

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

Dopo aver abilitato questa funzionalità, è possibile usare funzioni RevoScaleR per installare o disinstallare i pacchetti da un client R remoto.

## <a name="bkmk_disable"></a> Disabilitare la gestione dei pacchetti

1. Da un prompt dei comandi con privilegi elevati, eseguire di nuovo l'utilità RegisterRExt e disabilitare la gestione dei pacchetti a livello di database:

    `RegisterRExt.exe /uninstall pkgmgmt /database:databasename [/instance:name] [/user:username] [/password:*|password]`

    Questo comando rimuove gli oggetti di database correlati a gestione dei pacchetti dal database specificato. Rimuove anche tutti i pacchetti che sono stati installati dal percorso di sistema del file protetto nel computer SQL Server.

2. Ripetere questo comando in ogni database in cui è stata usata gestione dei pacchetti.

3.  (Facoltativo) Dopo che tutti i database sono stati cancellati dei pacchetti usando il passaggio precedente, eseguire il comando seguente al prompt dei comandi con privilegi elevati:

    `RegisterRExt.exe /uninstall pkgmgmt [/instance:name] [/user:username] [/password:*|password]`

    Questo comando rimuove le funzionalità di gestione pacchetti dall'istanza. Si potrebbe essere necessario riavviare manualmente il servizio Launchpad ancora una volta per visualizzare le modifiche.

## <a name="next-steps"></a>Passaggi successivi

+ [Usare RevoScaleR per installare nuovi pacchetti R](use-revoscaler-to-manage-r-packages.md)
+ [Suggerimenti per l'installazione di pacchetti R](packages-installed-in-user-libraries.md)
+ [Pacchetti predefiniti](installing-and-managing-r-packages.md)
