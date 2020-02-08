---
title: Opzioni di configurazione per SQL Server in Docker
description: Informazioni sulle diverse opzioni disponibili per usare le immagini del contenitore di SQL Server 2017 e SQL Server 2019 in Docker e interagire con esse. Sono incluse informazioni sulla persistenza dei dati, la copia di file e la risoluzione dei problemi.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/08/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: e97f535dedd2b6ee25abfc886d1f08272697c549
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76162632"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configurare immagini del contenitore di SQL Server in Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come configurare e usare l'[immagine del contenitore mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) con Docker. 

Per altri scenari di distribuzione, vedere:

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes - Cluster Big Data](../big-data-cluster/deploy-get-started.md)

Questa immagine è costituita da SQL Server in esecuzione su Linux basato su Ubuntu 16.04. Può essere usata con il motore Docker 1.8 o versione successiva su Linux o in Docker per Mac/Windows.

> [!NOTE]
> Questo articolo è incentrato nello specifico sull'uso dell'immagine mssql-server-linux. L'immagine di Windows non è qui trattata, ma è possibile ottenere informazioni su di essa nella [pagina mssql-server-windows di Docker Hub](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

> [!IMPORTANT]
> Prima di scegliere di eseguire un contenitore SQL Server per i casi d'uso di produzione, vedere i [criteri di supporto per i contenitori SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) per assicurarsi che l'esecuzione avvenga in una configurazione supportata.

Questo video di 6 minuti offre un'introduzione relativa all'esecuzione di SQL Server nei contenitori:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2019-in-Containers/player?WT.mc_id=dataexposed-c9-niner]


## <a name="pull-and-run-the-container-image"></a>Effettuare il pull ed eseguire l'immagine del contenitore

Per il pull e l'esecuzione delle immagini del contenitore Docker per SQL Server 2017 e SQL Server 2019, seguire i prerequisiti e i passaggi illustrati nella guida di avvio rapido seguente:

- [Eseguire l'immagine del contenitore di SQL Server 2017 con Docker](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Eseguire l'immagine del contenitore di SQL Server 2019 con Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

Questo articolo dedicato alla configurazione descrive altri scenari di utilizzo nelle sezioni seguenti.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> Eseguire immagini del contenitore basate su RHEL

La documentazione dedicata alle immagini del contenitore di SQL Server per Linux si riferisce a contenitori basati su Ubuntu. A partire da SQL Server 2019, è possibile usare contenitori basati su Red Hat Enterprise Linux (RHEL). Modificare il repository dei contenitori da **mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04** a **mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8** in tutti i comandi di Docker.

Il comando seguente, ad esempio, esegue il pull del contenitore di Cumulative Update 1 per SQL Server 2019 che usa RHEL 8:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> Eseguire immagini del contenitore di produzione

Le istruzioni di avvio rapido nella sezione precedente prevedono l'uso dell'edizione Developer gratuita di SQL Server da Docker Hub. La maggior parte delle informazioni è comunque applicabile per l'esecuzione di immagini del contenitore di produzione, ad esempio per le edizioni Enterprise, Standard o Web. Esistono tuttavia alcune differenze descritte di seguito.

- È possibile usare SQL Server in un ambiente di produzione solo se è disponibile una licenza valida. [Qui](https://go.microsoft.com/fwlink/?linkid=857693) è possibile ottenere una licenza di produzione per SQL Server Express gratuita. Le licenze delle edizioni SQL Server Standard ed Enterprise sono disponibili tramite [Microsoft Volume Licensing](https://www.microsoft.com/licensing/default.aspx).


- È possibile configurare l'immagine del contenitore Developer anche per eseguire le edizioni di produzione. Per eseguire le edizioni di produzione, seguire questa procedura:

Esaminare i requisiti e ed eseguire le procedure in questo [avvio rapido](quickstart-install-connect-docker.md). È necessario specificare l'edizione di produzione con la variabile di ambiente **MSSQL_PID**. L'esempio seguente mostra come eseguire la versione più recente dell'immagine del contenitore di SQL Server 2017 per l'edizione Enterprise:

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "mcr.microsoft.com/mssql/server:2017-latest"
```

> [!IMPORTANT]
> Passando il valore **Y** alla variabile di ambiente **ACCEPT_EULA** e un valore di edizione a **MSSQL_PID**, si conferma la disponibilità di una licenza valida ed esistente per l'edizione e la versione di SQL Server che si intende usare. Si accetta anche che l'uso del software SQL Server in un'immagine del contenitore Docker sarà disciplinato dalle condizioni della licenza di SQL Server.

> [!NOTE]
> Per un elenco completo dei valori possibili per **MSSQL_PID**, vedere [Configurare le impostazioni di SQL Server con le variabili di ambiente in Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Connessione ed esecuzione di query

È possibile connettersi a SQL Server ed eseguire query in un contenitore dall'esterno o dall'interno del contenitore. Nelle sezioni seguenti vengono illustrati entrambi gli scenari. 

### <a name="tools-outside-the-container"></a>Strumenti all'esterno del contenitore

È possibile connettersi all'istanza di SQL Server nel computer che esegue Docker da uno strumento esterno Linux, Windows o macOS che supporti le connessioni SQL. Alcuni strumenti comuni includono:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) per Windows](sql-server-linux-manage-ssms.md)

Nell'esempio seguente viene usato **sqlcmd** per connettersi a SQL Server in esecuzione in un contenitore Docker. L'indirizzo IP nella stringa di connessione è l'indirizzo IP del computer host in cui è in esecuzione il contenitore.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Se è stato eseguito il mapping di una porta host diversa dalla porta predefinita **1433**, aggiungere tale porta alla stringa di connessione. Ad esempio, se si specifica `-p 1400:1433` nel comando `docker run` connettersi specificando in modo esplicito la porta 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Strumenti all'interno del contenitore

A partire da SQL Server 2017, gli [strumenti da riga di comando di SQL Server](sql-server-linux-setup-tools.md) sono inclusi nell'immagine del contenitore. Se ci si connette all'immagine con un prompt dei comandi interattivo, è possibile eseguire gli strumenti localmente.

1. Usare il comando `docker exec -it` per avviare una shell Bash interattiva all'interno del contenitore in esecuzione. Nell'esempio seguente `e69e056c702d` è l'ID del contenitore.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Non è sempre necessario specificare l'intero ID del contenitore. È sufficiente specificare un numero sufficiente di caratteri per identificarlo in modo univoco. In questo esempio potrebbe essere quindi sufficiente usare `e6` o `e69` anziché l'ID completo.

2. Una volta all'interno del contenitore, eseguire la connessione in locale con sqlcmd. Si noti che sqlcmd non è incluso nel percorso per impostazione predefinita, quindi occorre specificare il percorso completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Dopo aver completato le operazioni con sqlcmd, digitare `exit`.

4. Al termine delle operazioni con il prompt dei comandi interattivo, digitare `exit`. Dopo la chiusura della shell Bash interattiva, il contenitore continua l'esecuzione.

## <a name="run-multiple-sql-server-containers"></a>Eseguire più contenitori di SQL Server

Docker prevede un modo per eseguire più contenitori di SQL Server nello stesso computer host. Usare questo approccio per gli scenari che richiedono più istanze di SQL Server nello stesso host. Ogni contenitore deve essere esposto su una porta diversa.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Nell'esempio seguente vengono creati due contenitori di SQL Server 2017 e ne viene eseguito il mapping alle porte **1401** e **1402** nel computer host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

L'esempio seguente crea due contenitori di SQL Server 2019 ed esegue il mapping di questi alle porte **1401** e **1402** nel computer host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

Sono ora disponibili due istanze di SQL Server in esecuzione in contenitori separati. I client possono connettersi a ogni istanza di SQL Server usando l'indirizzo IP dell'host Docker e il numero di porta per il contenitore.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a> Creare un contenitore personalizzato

È possibile creare un [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) personalizzato per creare un contenitore di SQL Server personalizzato. Per altre informazioni, vedere [una demo che combina SQL Server e un'applicazione Node](https://github.com/twright-msft/mssql-node-docker-demo-app). Se si crea un Dockerfile personalizzato, tenere conto del processo in primo piano, perché questo processo controlla la durata del contenitore. Se viene chiuso, il contenitore verrà arrestato. Ad esempio, se si vuole eseguire uno script e avviare SQL Server, assicurarsi che il processo di SQL Server sia il comando più a destra. Tutti gli altri comandi vengono eseguiti in background. Il comando seguente illustra questa operazione all'interno di un Dockerfile:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Se si invertissero i comandi nell'esempio precedente, il contenitore verrebbe arrestato al termine dello script do-my-sql-commands.sh.

## <a id="persist"></a> Rendere persistenti i dati

Le modifiche apportate alla configurazione del SQL Server e i file di database vengono salvati in modo permanente nel contenitore anche se il contenitore viene riavviato con `docker stop` e `docker start`. Tuttavia, se si rimuove il contenitore con `docker rm` viene eliminato tutto il contenuto al suo interno, inclusi SQL Server e i database. La sezione seguente illustra come usare i **volumi di dati** per rendere persistenti i file di database anche se vengono eliminati i contenitori associati.

> [!IMPORTANT]
> Per SQL Server è fondamentale comprendere la persistenza dei dati in Docker. Oltre alle informazioni in questa sezione, vedere la documentazione di Docker su [come gestire i dati nei contenitori Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montare una directory host come volume di dati

La prima opzione consiste nel montare una directory nell'host come volume di dati nel contenitore. A tale scopo, usare il comando `docker run` con il flag `-v <host directory>:/var/opt/mssql`. In questo modo è possibile ripristinare i dati tra le esecuzioni dei contenitori.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

Questa tecnica consente anche di condividere e visualizzare i file nell'host all'esterno di Docker.

> [!IMPORTANT]
> Il mapping del volume host per **Docker in Windows** non supporta attualmente il mapping della directory `/var/opt/mssql` completa. È tuttavia possibile eseguire il mapping di una sottodirectory, ad esempio `/var/opt/mssql/data` al computer host.

> [!IMPORTANT]
> Il mapping del volume host per **Docker su Mac** con l'immagine di SQL Server in Linux non è attualmente supportato. Usare invece i contenitori di volumi di dati. Questa restrizione è specifica per la directory `/var/opt/mssql`. La lettura da una directory montata funziona correttamente. Ad esempio, è possibile montare una directory host usando -v in Mac e ripristinare un backup da un file con estensione bak che risiede nell'host.

### <a name="use-data-volume-containers"></a>Usare i contenitori di volumi di dati

La seconda opzione consiste nell'usare un contenitore di volumi di dati. È possibile creare un contenitore di volumi di dati specificando un nome di volume anziché una directory host con il parametro `-v`. Nell'esempio seguente viene creato un volume di dati condiviso denominato **sqlvolume**.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

> [!NOTE]
> Questa tecnica per la creazione implicita di un volume di dati nel comando run non funziona con le versioni precedenti di Docker. In tal caso, usare i passaggi espliciti descritti nella documentazione di Docker, in [Creating and mounting a data volume container](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container) (Creazione e montaggio di un contenitore di volumi di dati).

Anche se si arresta e rimuove il contenitore, il volume di dati è persistente. È possibile visualizzarlo con il comando `docker volume ls`.

```bash
docker volume ls
```

Se successivamente si crea un altro contenitore con lo stesso nome di volume, il nuovo contenitore userà gli stessi dati di SQL Server contenuti nel volume.

Per rimuovere un contenitore di volumi di dati, usare il comando `docker volume rm`.

> [!WARNING]
> Se si elimina il contenitore del volume di dati, tutti i dati di SQL Server nel contenitore verranno eliminati *definitivamente*.

### <a name="backup-and-restore"></a>Backup e ripristino

Oltre a queste tecniche con i contenitori, è anche possibile usare le tecniche standard di backup e ripristino di SQL Server. È possibile usare i file di backup per proteggere i dati o per spostare i dati in un'altra istanza di SQL Server. Per altre informazioni, vedere [Backup e ripristino di database di SQL Server in Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Se si creano backup, assicurarsi di creare o copiare i file di backup all'esterno del contenitore. In caso contrario, se il contenitore viene rimosso, vengono eliminati anche i file di backup.

## <a name="execute-commands-in-a-container"></a>Eseguire comandi in un contenitore

Se è disponibile un contenitore in esecuzione, è possibile eseguire i comandi all'interno del contenitore da un terminale host.

Per ottenere l'ID del contenitore, eseguire:

```bash
docker ps
```

Per avviare un terminale bash nel contenitore, eseguire:

```bash
docker exec -it <Container ID> /bin/bash
```

A questo punto è possibile eseguire i comandi come se fossero in esecuzione nel terminale all'interno del contenitore. Al termine, digitare `exit`. Viene così chiusa la sessione di esecuzione interattiva dei comandi, ma l'esecuzione del contenitore continua.

## <a name="copy-files-from-a-container"></a>Copiare file da un contenitore

Per copiare un file dal contenitore, usare il comando seguente:

```bash
docker cp <Container ID>:<Container path> <host path>
```

**Esempio:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>Copiare file in un contenitore

Per copiare un file nel contenitore, usare il comando seguente:

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**Esempio:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a id="tz"></a> Configurare il fuso orario

Per eseguire SQL Server in un contenitore Linux con un fuso orario specifico, configurare la variabile di ambiente `TZ`. Per trovare il valore del fuso orario corretto, eseguire il comando `tzselect` da un prompt di bash per Linux:

```bash
tzselect
```

Dopo aver selezionato il fuso orario, `tzselect` visualizza un output simile al seguente:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

È possibile usare queste informazioni per impostare la stessa variabile di ambiente nel contenitore Linux. L'esempio seguente mostra come eseguire SQL Server in un contenitore nel fuso orario `Americas/Los_Angeles`:

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

## <a id="tags"></a> Eseguire un'immagine del contenitore di SQL Server specifica

Esistono scenari in cui è possibile che non si voglia usare la versione più recente dell'immagine del contenitore di SQL Server. Per eseguire un'immagine del contenitore di SQL Server specifica, seguire questa procedura:

1. Identificare il **tag** di Docker per la versione che si vuole usare. Per visualizzare i tag disponibili, vedere la [pagina mssql-server-linux dell'hub Docker](https://hub.docker.com/_/microsoft-mssql-server).

2. Eseguire il pull dell'immagine del contenitore di SQL Server con il tag. Ad esempio, per eseguire il pull dell'immagine RC1, sostituire `<image_tag>` nel comando seguente con `rc1`.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Per eseguire un nuovo contenitore con tale immagine, specificare il nome del tag nel comando `docker run`. Nel comando seguente sostituire `<image_tag>` con la versione che si vuole eseguire.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Questi passaggi possono essere usati anche per effettuare il downgrade di un contenitore esistente. Ad esempio, potrebbe essere necessario effettuare il rollback o il downgrade di un contenitore in esecuzione per la risoluzione dei problemi o per attività di test. Per effettuare il downgrade di un contenitore in esecuzione, è necessario usare una tecnica di persistenza per la cartella dati. Seguire la stessa procedura descritta nella [sezione dedicata all'aggiornamento](#upgrade), ma specificare il nome del tag della versione precedente quando si esegue il nuovo contenitore.

## <a id="version"></a> Controllare la versione del contenitore

Se si vuole scoprire la versione di SQL Server in un contenitore Docker in esecuzione, eseguire il comando seguente per visualizzarla. Sostituire `<Container ID or name>` con l'ID o il nome del contenitore di destinazione. Sostituire `<YourStrong!Passw0rd>` con la password di SQL Server per l'account di accesso sa.

```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'SELECT @@VERSION'
```

```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourStrong!Passw0rd>" `
   -Q 'SELECT @@VERSION'
```

È anche possibile identificare la versione di SQL Server e il numero di build per un'immagine del contenitore Docker di destinazione. Il comando seguente visualizza la versione di SQL Server e informazioni sulla build per l'immagine **mcr.microsoft.com/mssql/server:2017-latest**. A tale scopo, esegue un nuovo contenitore con una variabile di ambiente **PAL_PROGRAM_INFO = 1**. Il contenitore risultante viene chiuso immediatamente e il comando `docker rm` lo rimuove.

```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
   -ti mcr.microsoft.com/mssql/server:2017-latest && \
   sudo docker rm sqlver
```

```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
   -ti mcr.microsoft.com/mssql/server:2017-latest; `
   docker rm sqlver
```

I comandi precedenti visualizzano informazioni sulla versione simili all'output seguente:

```Text
sqlservr
  Version 14.0.3029.16
  Build ID ee3d3882f1c48a7a7e590a620153012eaedc2f37143d485df945a079b9d4eeea
  Build Type release
  Git Version 65d42c4
  Built at Sat Jun 16 01:20:11 GMT 2018

PAL
  Build ID 60cfcb134bbae96d311f6a4f56aeb5a685b3809de80bcb61ec587a8f58b555eb
  Build Type release
  Git Version 21a4c11
  Built at Sat Jun 16 01:18:53 GMT 2018

Packages
  system.sfp                    6.2.9200.1,21a4c1178,
  system.common.sfp             10.0.15063.540
  system.certificates.sfp       6.2.9200.1,21a4c1178,
  system.netfx.sfp              4.6.1590.0
  secforwarderxplat.sfp         14.0.3029.16
  sqlservr.sfp                  14.0.3029.16
  sqlagent.sfp                  14.0.3029.16
```

## <a id="upgrade"></a> Aggiornare SQL Server nei contenitori

Per aggiornare l'immagine del contenitore con Docker, identificare prima di tutto il tag per la versione per l'aggiornamento. Eseguire il pull di questa versione dal Registro di sistema con il comando `docker pull`:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

L'immagine di SQL Server viene così aggiornata per tutti i nuovi contenitori creati, ma SQL Server non viene aggiornato in alcun contenitore in esecuzione. A tale scopo, è necessario creare un nuovo contenitore con l'immagine del contenitore di SQL Server più recente ed eseguire la migrazione dei dati al nuovo contenitore.

1. Assicurarsi di usare una delle [tecniche di persistenza dei dati](#persist) per il contenitore di SQL Server esistente. In questo modo è possibile avviare un nuovo contenitore con gli stessi dati.

1. Arrestare il contenitore di SQL Server con il comando `docker stop`.

1. Creare un nuovo contenitore di SQL Server con `docker run` e specificare una directory host mappata o un contenitore di volumi di dati. Assicurarsi di usare il tag specifico per l'aggiornamento di SQL Server. Il nuovo contenitore usa ora una nuova versione di SQL Server con i dati di SQL Server esistenti.

   > [!IMPORTANT]
   > L'aggiornamento è supportato solo tra le versioni RC1, RC2 e GA al momento.

1. Verificare i database e i dati nel nuovo contenitore.

1. Facoltativamente, rimuovere il contenitore precedente con `docker rm`.

## <a id="buildnonrootcontainer"></a> Compilare ed eseguire contenitori di SQL Server 2017 non radice

Eseguire la procedura seguente per creare un contenitore di SQL Server 2017 che si avvia come utente `mssql` (non root).

> [!NOTE]
> I contenitori di SQL Server 2019 vengono avviati automaticamente come utenti non root. I passaggi seguenti, quindi, si applicano solo ai contenitori di SQL Server 2017, che si avviano come root per impostazione predefinita.

1. Scaricare il [dockerfile di esempio per il contenitore di SQL Server non radice](https://raw.githubusercontent.com/microsoft/mssql-docker/master/linux/preview/examples/mssql-server-linux-non-root/Dockerfile) e salvarlo come `dockerfile`.

2. Eseguire il comando seguente nel contesto della directory dockerfile per compilare il contenitore di SQL Server non radice:

```bash
cd <path to dockerfile>
docker build -t 2017-latest-non-root .
```

3. Avviare il contenitore.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword@" --cap-add SYS_PTRACE --name sql1 -p 1433:1433 -d 2017-latest-non-root
```

> [!NOTE]
> Il flag `--cap-add SYS_PTRACE` è necessario per i contenitori di SQL Server non radice per generare dump a scopo di risoluzione dei problemi.

4. Verificare che il contenitore sia in esecuzione come utente non radice:

docker exec nel contenitore.
```bash
docker exec -it sql1 bash
```

Eseguire `whoami` che restituirà l'utente in esecuzione nel contenitore.

```bash
whoami
```

## <a id="nonrootuser"></a> Eseguire il contenitore come un altro utente non radice nell'host

Per eseguire il contenitore di SQL Server come un altro utente non radice, aggiungere il flag -u al comando docker run. Il contenitore non radice prevede una restrizione, ovvero deve essere eseguito come parte del gruppo radice, a meno che non venga montato un volume in '/var/opt/mssql' a cui l'utente non radice può accedere. Il gruppo radice non concede alcuna autorizzazione radice aggiuntiva all'utente non radice.

**Eseguire come utente con UID 4000**

È possibile avviare SQL Server con un UID personalizzato. Ad esempio, il comando seguente avvia SQL Server con l'UID 4000:
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> Verificare che il contenitore di SQL Server disponga di un utente denominato, ad esempio 'mssql' o 'root'. In caso contrario non sarà possibile eseguire SQLCMD all'interno del contenitore. È possibile verificare se il contenitore di SQL Server è in esecuzione come utente denominato eseguendo `whoami` nel contenitore.

**Eseguire il contenitore non radice come utente radice**

Se necessario, è possibile eseguire il contenitore non radice come utente radice. In questo modo, tutte le autorizzazioni per i file vengono concesse automaticamente al contenitore poiché ha privilegi più elevati.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**Eseguire come utente nel computer host**

È possibile avviare SQL Server con un utente esistente nel computer host con il comando seguente:
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**Eseguire come utente e gruppo diversi**

È possibile avviare SQL Server con un utente e un gruppo personalizzati. In questo esempio, il volume montato ha le autorizzazioni configurate per l'utente o il gruppo nel computer host.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a id="storagepermissions"></a> Configurare le autorizzazioni di archiviazione permanenti per i contenitori non radice

Per consentire all'utente non radice di accedere ai file di database in volumi montati, assicurarsi che l'utente o il gruppo con cui viene eseguito il contenitore possa intervenire sull'archivio file permanente.  

È possibile ottenere la proprietà corrente dei file di database con questo comando.

```bash
ls -ll <database file dir>
```

Se SQL Server non ha accesso ai file di database persistenti, eseguire uno dei comandi seguenti.

**Concedere al gruppo radice l'accesso in lettura/scrittura ai file di database**

Concedere le autorizzazioni per il gruppo radice alle directory seguenti in modo che il contenitore di SQL Server non radice abbia accesso ai file di database.

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

**Impostare l'utente non radice come proprietario dei file.**

Può trattarsi dell'utente non radice predefinito o di qualsiasi altro utente non radice che si vuole specificare. In questo esempio si imposta UID 10001 come utente non radice.

```bash
chown -R 10001:0 <database file dir>
```

## <a id="changefilelocation"></a> Modificare il percorso predefinito del file

Aggiungere la variabile `MSSQL_DATA_DIR` per modificare la directory dei dati nel comando `docker run`, quindi montare un volume in quel percorso a cui ha accesso l'utente del contenitore.

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a id="troubleshooting"></a> Risoluzione dei problemi

Le sezioni seguenti includono suggerimenti per la risoluzione dei problemi per l'esecuzione di SQL Server in contenitori.

### <a name="docker-command-errors"></a>Errori per i comandi Docker

Se vengono visualizzati errori per i comandi `docker`, verificare che il servizio Docker sia in esecuzione e provare a eseguirlo con autorizzazioni elevate.

Ad esempio, in Linux potrebbe essere visualizzato l'errore seguente quando si eseguono i comandi `docker`:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Se si riceve questo errore in Linux, provare a eseguire gli stessi comandi preceduti da `sudo`. Se il tentativo non riesce, verificare che il servizio Docker sia in esecuzione e, se necessario, avviarlo.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

In Windows assicurarsi di avviare PowerShell o il prompt dei comandi come amministratore.

### <a name="sql-server-container-startup-errors"></a>Errori di avvio del contenitore di SQL Server

Se non è possibile eseguire il contenitore di SQL Server, provare i test seguenti:

- Se si riceve un errore del tipo **'Non è stato possibile creare l'endpoint NOME_CONTENITORE nel bridge di rete. Errore durante l'avvio del proxy: listen tcp 0.0.0.0:1433 bind: indirizzo già in uso.'** , si sta tentando di eseguire il mapping della porta del contenitore 1433 a una porta già in uso. Questo problema può verificarsi se si esegue SQL Server localmente nel computer host. Può verificarsi anche se si avviano due contenitori di SQL Server e si tenta di eseguirne il mapping per entrambi alla stessa porta host. In tal caso, usare il parametro `-p` per eseguire il mapping della porta del contenitore 1433 a una porta host diversa. Ad esempio: 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

::: moniker-end

- Se si riceve un errore del tipo **'Autorizzazione negata durante il tentativo di connessione al socket del daemon Docker in unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: autorizzazione negata'** durante il tentativo di avviare un contenitore, aggiungere l'utente al gruppo Docker in Ubuntu. Quindi disconnettersi e accedere di nuovo perché questa modifica influirà sulle nuove sessioni. 

   ```bash
    usermod -aG docker $USER
   ```
- Controllare se sono presenti messaggi di errore dal contenitore.

    ```bash
    docker logs e69e056c702d
    ```

- Assicurarsi di soddisfare i requisiti minimi di memoria e disco specificati nella sezione dei [prerequisiti](quickstart-install-connect-docker.md#requirements) dell'articolo di avvio rapido.

- Se si usa un software di gestione dei contenitori, assicurarsi che supporti l'esecuzione come root dei processi dei contenitori. Il processo sqlservr nel contenitore viene eseguito come root.

- Esaminare i [log di installazione e degli errori di SQL Server](#errorlogs).

### <a name="enable-dump-captures"></a>Abilitare le acquisizioni di dump

Se il processo di SQL Server non riesce all'interno del contenitore, è necessario creare un nuovo contenitore con **SYS_PTRACE** abilitato. In questo modo viene aggiunta la funzionalità Linux per tracciare un processo, necessaria per la creazione di un file dump per un'eccezione. Il file dump può essere usato dal supporto tecnico per risolvere il problema. Il comando docker run seguente abilita questa funzionalità.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>Errori di connessione a SQL Server

Se non è possibile connettersi all'istanza di SQL Server in esecuzione nel contenitore, provare i test seguenti:

- Verificare che il contenitore di SQL Server sia in esecuzione esaminando la colonna **STATUS** dell'output di `docker ps -a`. In caso contrario, usare `docker start <Container ID>` per avviarlo.

- Se è stato eseguito il mapping a una porta host non predefinita (non 1433), assicurarsi di specificare la porta nella stringa di connessione. È possibile visualizzare il mapping delle porte nella colonna **PORTS** dell'output di `docker ps -a`. Il comando seguente, ad esempio, connette sqlcmd a un contenitore in ascolto sulla porta 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Se è stato usato `docker run` con un volume di dati o un contenitore del volume di dati mappato esistente, SQL Server ignora il valore di `MSSQL_SA_PASSWORD`. Viene invece usata la password dell'utente sa preconfigurata dai dati di SQL Server nel volume di dati o nel contenitore del volume di dati. Verificare di usare la password sa associata ai dati da collegare.

- Esaminare i [log di installazione e degli errori di SQL Server](#errorlogs).

### <a name="sql-server-availability-groups"></a>Gruppi di disponibilità di SQL Server

Se si usa Docker con i gruppi di disponibilità di SQL Server, esistono due requisiti aggiuntivi.

- Eseguire il mapping della porta usata per le comunicazioni di replica (valore predefinito 5022). Ad esempio, specificare `-p 5022:5022` come parte del comando `docker run`.

- Impostare in modo esplicito il nome host del contenitore con il parametro `-h YOURHOSTNAME` del comando `docker run`. Questo nome host viene usato quando si configura il gruppo di disponibilità. Se non viene specificato con `-h`, il valore predefinito è l'ID del contenitore.

### <a id="errorlogs"></a> Log di installazione e degli errori di SQL Server

È possibile esaminare i log di installazione e degli errori di SQL Server in **/var/opt/mssql/log**. Se il contenitore non è in esecuzione, avviare prima di tutto il contenitore. Usare quindi un prompt dei comandi interattivo per esaminare i log.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Dalla sessione bash all'interno del contenitore eseguire i comandi seguenti:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Se è stata montata una directory host in **/var/opt/mssql** al momento della creazione del contenitore, è invece possibile esaminare la sottodirectory **log** nel percorso mappato nell'host.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni introduttive sull'uso delle immagini del contenitore di SQL Server 2017 in Docker, vedere questo [articolo di avvio rapido](quickstart-install-connect-docker.md).

Nel [repository GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) sono inoltre disponibili risorse, feedback e documentazione su problemi noti.

[Esplorare la disponibilità elevata per i contenitori di SQL Server](sql-server-linux-container-ha-overview.md)
