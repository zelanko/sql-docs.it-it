---
title: Configurare le impostazioni di SQL Server con le variabili di ambiente
description: Questo articolo descrive come usare le variabili di ambiente per configurare impostazioni specifiche di SQL Server 2017 in Linux.
author: VanMSFT
ms.author: vanto
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 51589a2183043c5c8ea8d1f9bf5d4af6fcc1eea3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419244"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Configurare le impostazioni di SQL Server con le variabili di ambiente in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

È possibile usare diverse variabili di ambiente per configurare SQL Server 2017 in Linux. Queste variabili vengono usate in due scenari:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

È possibile usare diverse variabili di ambiente per configurare SQL Server anteprima 2019 in Linux. Queste variabili vengono usate in due scenari:

::: moniker-end

- Per configurare la configurazione iniziale con `mssql-conf setup` il comando.
- Per configurare un nuovo [contenitore SQL Server in Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Se è necessario configurare SQL Server dopo questi scenari di installazione, vedere [configurare SQL Server in Linux con lo strumento MSSQL-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variabili di ambiente

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| Variabile di ambiente | Descrizione |
|-----|-----|
| **ACCEPT_EULA** | Impostare la variabile **ACCEPT_EULA** su qualsiasi valore per confermare l'accettazione delle [condizioni di licenza ](https://go.microsoft.com/fwlink/?LinkId=746388). Impostazione obbligatoria per l'immagine di SQL Server. |
| **MSSQL_SA_PASSWORD** | Configurare la password dell'utente SA. |
| **MSSQL_PID** | Impostare la SQL Server edizione o il codice Product Key. I valori possibili includono: </br></br>**Copia di valutazione**</br>**Sviluppatore**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Codice Product Key**</br></br>Se si specifica un codice Product Key, deve essere nel formato # # # # #-# # # # #-# # # # #-# # # # # # # # # # #, dove ' #' è un numero o una lettera.|
| **MSSQL_LCID** | Imposta l'ID lingua da utilizzare per SQL Server. Ad esempio, 1036 è francese. |
| **MSSQL_COLLATION** | Imposta le regole di confronto predefinite per SQL Server. In questo modo viene eseguito l'override del mapping predefinito dell'ID lingua (LCID) alle regole di confronto. |
| **MSSQL_MEMORY_LIMIT_MB** | Imposta la quantità massima di memoria (in MB) che SQL Server possibile utilizzare. Per impostazione predefinita, è il 80% della memoria fisica totale. |
| **MSSQL_TCP_PORT** | Configurare la porta TCP su cui è in ascolto il SQL Server (valore predefinito 1433). |
| **MSSQL_IP_ADDRESS** | Impostare l'indirizzo IP. Attualmente, l'indirizzo IP deve essere di tipo IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Impostare il percorso predefinito della directory di backup. |
| **MSSQL_DATA_DIR** | Modificare la directory in cui vengono creati i nuovi file di dati del database di SQL Server (con estensione MDF). |
| **MSSQL_LOG_DIR** | Modificare la directory in cui vengono creati i nuovi file di log del database di SQL Server (con estensione ldf). |
| **MSSQL_DUMP_DIR** | Modificare la directory in cui SQL Server depositeranno i dump della memoria e altri file per la risoluzione dei problemi per impostazione predefinita. |
| **MSSQL_ENABLE_HADR** | Abilitare il gruppo di disponibilità. Ad esempio,' 1' è abilitato è 0' è disabilitato |
| **MSSQL_AGENT_ENABLED** | Abilitare SQL Server Agent. Ad esempio,' true ' è abilitato è false ' è disabilitato. Per impostazione predefinita, Agent è disabilitato.  |
| **MSSQL_MASTER_DATA_FILE** | Imposta il percorso del file di dati del database master. Deve essere denominato **master. MDF** fino alla prima esecuzione del SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Imposta il percorso del file di log del database master. Deve essere denominato **Mastlog. ldf** fino alla prima esecuzione del SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Imposta il percorso dei file di log degli errori. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| Variabile di ambiente | Descrizione |
|-----|-----|
| **ACCEPT_EULA** | Impostare la variabile **ACCEPT_EULA** su qualsiasi valore per confermare l'accettazione delle [condizioni di licenza ](https://go.microsoft.com/fwlink/?LinkId=746388). Impostazione obbligatoria per l'immagine di SQL Server. |
| **MSSQL_SA_PASSWORD** | Configurare la password dell'utente SA. |
| **MSSQL_PID** | Impostare la SQL Server edizione o il codice Product Key. I valori possibili includono: </br></br>**Copia di valutazione**</br>**Sviluppatore**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Codice Product Key**</br></br>Se si specifica un codice Product Key, deve essere nel formato # # # # #-# # # # #-# # # # #-# # # # # # # # # # #, dove ' #' è un numero o una lettera.|
| **MSSQL_LCID** | Imposta l'ID lingua da utilizzare per SQL Server. Ad esempio, 1036 è francese. |
| **MSSQL_COLLATION** | Imposta le regole di confronto predefinite per SQL Server. In questo modo viene eseguito l'override del mapping predefinito dell'ID lingua (LCID) alle regole di confronto. |
| **MSSQL_MEMORY_LIMIT_MB** | Imposta la quantità massima di memoria (in MB) che SQL Server possibile utilizzare. Per impostazione predefinita, è il 80% della memoria fisica totale. |
| **MSSQL_TCP_PORT** | Configurare la porta TCP su cui è in ascolto il SQL Server (valore predefinito 1433). |
| **MSSQL_IP_ADDRESS** | Impostare l'indirizzo IP. Attualmente, l'indirizzo IP deve essere di tipo IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Impostare il percorso predefinito della directory di backup. |
| **MSSQL_DATA_DIR** | Modificare la directory in cui vengono creati i nuovi file di dati del database di SQL Server (con estensione MDF). |
| **MSSQL_LOG_DIR** | Modificare la directory in cui vengono creati i nuovi file di log del database di SQL Server (con estensione ldf). |
| **MSSQL_DUMP_DIR** | Modificare la directory in cui SQL Server depositeranno i dump della memoria e altri file per la risoluzione dei problemi per impostazione predefinita. |
| **MSSQL_ENABLE_HADR** | Abilitare il gruppo di disponibilità. Ad esempio,' 1' è abilitato è 0' è disabilitato |
| **MSSQL_AGENT_ENABLED** | Abilitare SQL Server Agent. Ad esempio,' true ' è abilitato è false ' è disabilitato. Per impostazione predefinita, Agent è disabilitato.  |
| **MSSQL_MASTER_DATA_FILE** | Imposta il percorso del file di dati del database master. Deve essere denominato **master. MDF** fino alla prima esecuzione del SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Imposta il percorso del file di log del database master. Deve essere denominato **Mastlog. ldf** fino alla prima esecuzione del SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Imposta il percorso dei file di log degli errori. |

::: moniker-end

## <a name="use-with-initial-setup"></a>Usare con l'installazione iniziale

Questo esempio viene `mssql-conf setup` eseguito con le variabili di ambiente configurate. Vengono specificate le variabili di ambiente seguenti:

- **ACCEPT_EULA** accetta il contratto di licenza con l'utente finale.
- **MSSSQL_PID** specifica l'edizione di SQL Server per sviluppatori con licenza gratuita per l'utilizzo non in produzione.
- **MSSQL_SA_PASSWORD** imposta una password complessa.
- **MSSQL_TCP_PORT** imposta la porta TCP su cui SQL Server resta in attesa su 1234.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Usare con Docker

Questo comando Docker di esempio usa le variabili di ambiente seguenti per creare un nuovo contenitore SQL Server:

- **ACCEPT_EULA** accetta il contratto di licenza con l'utente finale.
- **MSSSQL_PID** specifica l'edizione di SQL Server per sviluppatori con licenza gratuita per l'utilizzo non in produzione.
- **MSSQL_SA_PASSWORD** imposta una password complessa.
- **MSSQL_TCP_PORT** imposta la porta TCP su cui SQL Server resta in attesa su 1234. Ciò significa che anziché eseguire il mapping della porta 1433 (impostazione predefinita) a una porta host, è necessario eseguire il mapping della `-p 1234:1234` porta TCP personalizzata con il comando riportato in questo esempio.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Se si esegue Docker in Linux/macOS, usare la sintassi seguente con virgolette singole:

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

Se si esegue Docker in Linux/macOS, usare la sintassi seguente con virgolette singole:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

Se si esegue Docker in Windows, usare la sintassi seguente con le virgolette doppie:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

Per altre impostazioni SQL Server non elencate, vedere [configurare SQL Server in Linux con lo strumento MSSQL-conf](sql-server-linux-configure-mssql-conf.md).

Per ulteriori informazioni su come installare ed eseguire SQL Server in Linux, vedere [install SQL Server in Linux](sql-server-linux-setup.md).
