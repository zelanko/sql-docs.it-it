---
title: Configurare l'utilizzo e raccolta di dati di diagnostica per SQL Server in Linux
description: Viene descritto come dai clienti di SQL Server e i dati di diagnostica vengono raccolti e configurato in Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 36c5194df015b26e5c9925575a9e524ef17ce602
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057227"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-on-linux"></a>Configurare l'utilizzo e raccolta di dati di diagnostica per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Per impostazione predefinita, Microsoft SQL Server raccoglie informazioni su come i clienti usano l'applicazione. In particolare, SQL Server raccoglie informazioni sull'esperienza di installazione, l'utilizzo e le prestazioni. Queste informazioni consentono a Microsoft di migliorare il prodotto per meglio soddisfare le esigenze dei clienti. Ad esempio, Microsoft raccoglie informazioni sui tipi di codici di errore riscontrati dai clienti in modo da poter correggere i bug correlati, migliorare la documentazione su come usare SQL Server e determinare se occorre aggiungere funzionalità al prodotto per offrire un'esperienza migliore ai clienti.

Questo documento vengono fornite informazioni dettagliate su quali tipi di informazioni vengono raccolte e sulla configurazione di Microsoft SQL Server in Linux per l'invio che raccolte informazioni a Microsoft. SQL Server 2017 include un'informativa sulla privacy che spiega quali informazioni Microsoft e non vengano raccolti dagli utenti. Per altre informazioni, vedere la [informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkID=868444).

In particolare, Microsoft non invia alcuna informazione dei tipi seguenti tramite questo meccanismo:

- Qualsiasi valore all'interno delle tabelle utente
- Credenziali di accesso o altre informazioni di autenticazione
- Informazioni personali

SQL Server 2017 raccoglie e invia sempre informazioni sull'esperienza di installazione dal processo di installazione, in modo che sia possibile individuare e correggere eventuali problemi di installazione riscontrati dai clienti. SQL Server 2017 può essere configurato per non inviare informazioni (in una singola istanza per ogni server) a Microsoft attraverso **mssql-conf**. MSSQL-conf è uno script di configurazione installato con SQL Server 2017 per Red Hat Enterprise Linux, SUSE Linux Enterprise Server e Ubuntu.

> [!NOTE]
> È possibile disabilitare l'invio di informazioni a Microsoft solo nelle versioni a pagamento di SQL Server.

## <a name="disable-usage-and-diagnostic-data-collection"></a>Disabilitare la raccolta di dati di diagnostica e utilizzo

Questa opzione consente di modificare se SQL Server invia informazioni sull'utilizzo e raccolta di dati di diagnostica a Microsoft o non. Per impostazione predefinita, questo valore è impostato su true. Per modificare il valore, eseguire i comandi seguenti:

> [!IMPORTANT]
> È possibile non disattivare la raccolta dati di diagnostica e utilizzo gratuitamente edizioni di SQL Server, Express e Developer.

### <a name="on-red-hat-suse-and-ubuntu"></a>In Ubuntu, SUSE e Red Hat

1. Eseguire lo script mssql-conf come radice con il **impostata** comando per **telemetry.customerfeedback**. Nell'esempio seguente consente di disattivare la raccolta dei dati di diagnostica e utilizzo, specificando **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>In Docker
Per disabilitare l'utilizzo e raccolta di dati diagnostici in docker, è necessario disporre di Docker [persistenti i dati](sql-server-linux-configure-docker.md). 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Aggiungere un `mssql.conf` file con le righe `[telemetry]` e `customerfeedback = false` nella directory host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. Eseguire l'immagine del contenitore

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Aggiungere un `mssql.conf` file con le righe `[telemetry]` e `customerfeedback = false` nella directory host:

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. Eseguire l'immagine del contenitore

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>Controllo locale per SQL Server in Linux utilizzo e raccolta di dati di diagnostica

Microsoft SQL Server 2017 include funzionalità abilitate per Internet che possono raccogliere e inviare a Microsoft dati relativi al computer o dispositivo ("informazioni standard sul computer"). Il componente di controllo locale della raccolta dati di diagnostica e utilizzo di SQL Server è possibile scrivere i dati raccolti dal servizio in una cartella specificata, che rappresenta i dati (log) che verranno inviati a Microsoft. Lo scopo del controllo locale è quello di consentire ai clienti di visualizzare tutti i dati che Microsoft raccoglie con questa funzionalità, per motivi di conformità alle normative o rispetto della privacy.

In SQL Server in Linux, controllo locale è configurabile a livello di istanza per il motore di Database di SQL Server. Altri componenti di SQL Server e strumenti di SQL Server non è la funzionalità di controllo locale per la raccolta di dati di diagnostica e utilizzo.

### <a name="enable-local-audit"></a>Abilitare il controllo locale

Questa opzione Abilita controllo locale e consente di impostare la directory in cui vengono creati i log di controllo locale.

1. Creare una directory di destinazione per i nuovi log di controllo locale. L'esempio seguente crea una nuova **/tmp/controllo** directory:

   ```bash
   sudo mkdir /tmp/audit
   ```

2. Modificare il proprietario e il gruppo della directory in cui il **mssql** utente:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. Eseguire lo script mssql-conf come radice con il **impostata** comando per **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. Riavviare il servizio SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>In Docker
Per abilitare il controllo locale in docker, è necessario disporre di Docker [persistenti i dati](sql-server-linux-configure-docker.md). 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. La directory di destinazione per i nuovi log di controllo locale sarà nel contenitore. Creare una directory di destinazione per i nuovi log di controllo locale nella directory host nel computer. L'esempio seguente crea una nuova **/controllo** directory:

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. Aggiungere un `mssql.conf` file con le righe `[telemetry]` e `userrequestedlocalauditdirectory = <host directory>/audit` nella directory host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. Eseguire l'immagine del contenitore

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. La directory di destinazione per i nuovi log di controllo locale sarà nel contenitore. Creare una directory di destinazione per i nuovi log di controllo locale nella directory host nel computer. L'esempio seguente crea una nuova **/controllo** directory:

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. Aggiungere un `mssql.conf` file con le righe `[telemetry]` e `userrequestedlocalauditdirectory = <host directory>/audit` nella directory host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. Eseguire l'immagine del contenitore

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
   ```

::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su SQL Server in Linux, vedere la [Panoramica di SQL Server in Linux](sql-server-linux-overview.md).
