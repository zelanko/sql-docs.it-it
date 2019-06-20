---
title: Configurare le impostazioni di SQL Server con le variabili di ambiente | Microsoft Docs
description: Questo articolo descrive come usare le variabili di ambiente per configurare impostazioni specifiche di SQL Server 2017 in Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 299a7db7304a0f6a1090d7d60dbbe4a7e451179d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719415"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Configurare le impostazioni di SQL Server con le variabili di ambiente in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

È possibile utilizzare diverse variabili di ambiente diverso per configurare SQL Server 2017 su Linux. Queste variabili vengono usate in due scenari:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

È possibile utilizzare diverse variabili di ambiente diverso per configurare SQL Server 2019 anteprima in Linux. Queste variabili vengono usate in due scenari:

::: moniker-end

- Per configurare la configurazione iniziale con il `mssql-conf setup` comando.
- Per configurare una nuova [contenitore di SQL Server in Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Se è necessario configurare SQL Server dopo questi scenari di installazione, vedere [configurare SQL Server in Linux con lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variabili di ambiente

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| Variabile di ambiente | Descrizione |
|-----|-----|
| **ACCEPT_EULA** | Accettare il contratto di licenza di SQL Server quando è impostato su qualsiasi valore (ad esempio, "Y"). |
| **MSSQL_SA_PASSWORD** | Configurare la password dell'utente dell'amministratore di sistema. |
| **MSSQL_PID** | Impostare la chiave di edizione o del prodotto SQL Server. I valori possibili includono: </br></br>**Copia di valutazione**</br>**Sviluppatore**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Un codice product key**</br></br>Se si specifica un codice product key, deve essere nel formato # # #-# # #-# # #-# # #-# # #, dove '#' è un numero o una lettera.|
| **MSSQL_LCID** | Imposta l'ID di lingua da usare per SQL Server. Ad esempio 1036 è il francese. |
| **MSSQL_COLLATION** | Imposta le regole di confronto predefinite per SQL Server. Questa impostazione sostituisce il mapping predefinito degli id di lingua (LCID) per le regole di confronto. |
| **MSSQL_MEMORY_LIMIT_MB** | Imposta la quantità massima di memoria (in MB) che è possibile usare SQL Server. Per impostazione predefinita è l'80% della memoria fisica totale. |
| **MSSQL_TCP_PORT** | Configurare la porta TCP in ascolto il Server SQL (valore predefinito 1433). |
| **MSSQL_IP_ADDRESS** | Impostare l'indirizzo IP. Attualmente, l'indirizzo IP deve essere IPv4 stile (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Impostare il percorso di directory di backup predefinito. |
| **MSSQL_DATA_DIR** | Passare alla directory in cui vengono creati i nuovi file di dati di SQL Server database (mdf). |
| **MSSQL_LOG_DIR** | Passare alla directory in cui vengono creati i nuovi file di log (ldf) del database di SQL Server. |
| **MSSQL_DUMP_DIR** | Passare alla directory in cui SQL Server verrà depositare i dump di memoria e altri file sulla risoluzione dei problemi per impostazione predefinita. |
| **MSSQL_ENABLE_HADR** | Abilitare il gruppo di disponibilità. Ad esempio, '1' è abilitata, e '0' è disabilitato |
| **MSSQL_AGENT_ENABLED** | Abilitare SQL Server Agent. Ad esempio, è abilitato 'true' e 'false' è disabilitata. Per impostazione predefinita, l'agente è disabilitato.  |
| **MSSQL_MASTER_DATA_FILE** | Imposta il percorso del file di dati database master. Deve essere denominato **master. mdf** fino al prima dell'esecuzione di SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Imposta il percorso del file di log database master. Deve essere denominato **Mastlog** fino al prima dell'esecuzione di SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Imposta il percorso dei file di log degli errori. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| Variabile di ambiente | Descrizione |
|-----|-----|
| **ACCEPT_EULA** | Accettare il contratto di licenza di SQL Server quando è impostato su qualsiasi valore (ad esempio, "Y"). |
| **MSSQL_SA_PASSWORD** | Configurare la password dell'utente dell'amministratore di sistema. |
| **MSSQL_PID** | Impostare la chiave di edizione o del prodotto SQL Server. I valori possibili includono: </br></br>**Copia di valutazione**</br>**Sviluppatore**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Un codice product key**</br></br>Se si specifica un codice product key, deve essere nel formato # # #-# # #-# # #-# # #-# # #, dove '#' è un numero o una lettera.|
| **MSSQL_LCID** | Imposta l'ID di lingua da usare per SQL Server. Ad esempio 1036 è il francese. |
| **MSSQL_COLLATION** | Imposta le regole di confronto predefinite per SQL Server. Questa impostazione sostituisce il mapping predefinito degli id di lingua (LCID) per le regole di confronto. |
| **MSSQL_MEMORY_LIMIT_MB** | Imposta la quantità massima di memoria (in MB) che è possibile usare SQL Server. Per impostazione predefinita è l'80% della memoria fisica totale. |
| **MSSQL_TCP_PORT** | Configurare la porta TCP in ascolto il Server SQL (valore predefinito 1433). |
| **MSSQL_IP_ADDRESS** | Impostare l'indirizzo IP. Attualmente, l'indirizzo IP deve essere IPv4 stile (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Impostare il percorso di directory di backup predefinito. |
| **MSSQL_DATA_DIR** | Passare alla directory in cui vengono creati i nuovi file di dati di SQL Server database (mdf). |
| **MSSQL_LOG_DIR** | Passare alla directory in cui vengono creati i nuovi file di log (ldf) del database di SQL Server. |
| **MSSQL_DUMP_DIR** | Passare alla directory in cui SQL Server verrà depositare i dump di memoria e altri file sulla risoluzione dei problemi per impostazione predefinita. |
| **MSSQL_ENABLE_HADR** | Abilitare il gruppo di disponibilità. Ad esempio, '1' è abilitata, e '0' è disabilitato |
| **MSSQL_AGENT_ENABLED** | Abilitare SQL Server Agent. Ad esempio, è abilitato 'true' e 'false' è disabilitata. Per impostazione predefinita, l'agente è disabilitato.  |
| **MSSQL_MASTER_DATA_FILE** | Imposta il percorso del file di dati database master. Deve essere denominato **master. mdf** fino al prima dell'esecuzione di SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Imposta il percorso del file di log database master. Deve essere denominato **Mastlog** fino al prima dell'esecuzione di SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Imposta il percorso dei file di log degli errori. |

::: moniker-end

## <a name="use-with-initial-setup"></a>Usare con la configurazione iniziale

Questo esempio viene eseguito `mssql-conf setup` con configurato le variabili di ambiente. Vengono specificate le variabili di ambiente seguenti:

- **ACCEPT_EULA** accetta il contratto di licenza utente finale.
- **MSSSQL_PID** specifica con licenza gratuita per gli sviluppatori edizione di SQL Server per l'uso non di produzione.
- **MSSQL_SA_PASSWORD** imposta una password complessa.
- **MSSQL_TCP_PORT** imposta la porta TCP che SQL Server è in ascolto al 1234.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Uso con Docker

Questo comando di docker di esempio Usa le variabili di ambiente seguenti per creare un nuovo contenitore di SQL Server:

- **ACCEPT_EULA** accetta il contratto di licenza utente finale.
- **MSSSQL_PID** specifica con licenza gratuita per gli sviluppatori edizione di SQL Server per l'uso non di produzione.
- **MSSQL_SA_PASSWORD** imposta una password complessa.
- **MSSQL_TCP_PORT** imposta la porta TCP che SQL Server è in ascolto al 1234. Ciò significa che invece di mapping la porta 1433 (valore predefinito) a una porta dell'host, la porta TCP personalizzata deve essere mappata con il `-p 1234:1234` comando in questo esempio.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Se si esegue Docker su Linux/macOS, usare la sintassi seguente con le virgolette singole:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

Se si esegue Docker in Windows, usare la sintassi seguente con le virgolette doppie:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> Il processo di esecuzione delle edizioni di produzione nei contenitori è leggermente diverso. Per altre informazioni, vedere [Run production container images](sql-server-linux-configure-docker.md#production) (Eseguire immagini del contenitore di produzione).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Se si esegue Docker su Linux/macOS, usare la sintassi seguente con le virgolette singole:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

Se si esegue Docker in Windows, usare la sintassi seguente con le virgolette doppie:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

Per altre impostazioni di SQL Server non elencate qui, vedere [configurare SQL Server in Linux con lo strumento mssql-conf](sql-server-linux-configure-mssql-conf.md).

Per altre informazioni su come installare ed eseguire SQL Server in Linux, vedere [installare SQL Server in Linux](sql-server-linux-setup.md).
