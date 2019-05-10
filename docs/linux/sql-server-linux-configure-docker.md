---
title: Opzioni di configurazione per SQL Server in Docker | Microsoft Docs
description: Esplorare i diversi modi di utilizzo e l'interazione con SQL Server 2017 e 2019 preview le immagini contenitore in Docker. Sono inclusi i dati persistenti, la copia dei file e la risoluzione dei problemi.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.custom: sql-linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 7261d8b5b72b835c726a268477c44e4d0663f131
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2019
ms.locfileid: "65376840"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configurare immagini del contenitore SQL Server in Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come configurare e usare la [immagine del contenitore mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server) con Docker. Questa immagine è costituita da SQL Server in esecuzione su Linux basato su Ubuntu 16.04. Può essere usata con il motore Docker 1.8 o versione successiva su Linux o in Docker per Mac/Windows.

> [!NOTE]
> Questo articolo illustra in modo specifico usando l'immagine mssql-server-linux. L'immagine di Windows non è coperto, ma è possibile ottenere ulteriori informazioni sul [pagina Hub Docker mssql-server-windows](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a name="pull-and-run-the-container-image"></a>Effettuare il pull ed eseguire l'immagine del contenitore

Per eseguire il pull ed eseguire le immagini del contenitore per l'anteprima di SQL Server 2017 e SQL Server 2019 Docker, seguire i prerequisiti e i passaggi nella Guida introduttiva seguente:

- [Eseguire l'immagine del contenitore SQL Server 2017 con Docker](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Eseguire l'immagine del contenitore SQL Server 2019 anteprima con Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

Questo articolo configurazione fornisce scenari di utilizzo aggiuntivi nelle sezioni seguenti.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> Eseguire le immagini contenitore basate su RHEL

Tutta la documentazione sulle immagini di contenitore Linux di SQL Server del punto per contenitori basati su Ubuntu. A partire da SQL Server 2019 anteprima, è possibile usare contenitori basati su Red Hat Enterprise Linux (RHEL). Nel repository del contenitore da modificare **mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu** al **mcr.microsoft.com/mssql/rhel/server:2019-CTP2.4** in tutti i comandi di docker.

Ad esempio, il comando seguente esegue il pull il contenitore di anteprima più recente di SQL Server 2019 che utilizza RHEL:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP2.4
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP2.4
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> Eseguire le immagini del contenitore di produzione

La Guida introduttiva nella sezione precedente viene eseguita l'edizione Developer gratuita di SQL Server dall'Hub Docker. La maggior parte delle informazioni si applica comunque Se si desidera eseguire immagini del contenitore, ad esempio le edizioni Enterprise, Standard o Web di produzione. Tuttavia, esistono alcune differenze descritte di seguito.

- È possibile utilizzare SQL Server in un ambiente di produzione solo se si ha una licenza valida. È possibile ottenere una licenza di produzione SQL Server Express gratuita [qui](https://go.microsoft.com/fwlink/?linkid=857693). Licenze di SQL Server edizioni Standard ed Enterprise sono disponibili tramite [Microsoft Volume Licensing](https://www.microsoft.com/licensing/default.aspx).


- L'immagine del contenitore per gli sviluppatori può essere configurato per l'esecuzione anche le edizioni di produzione. Usare la procedura seguente per eseguire edizioni di produzione:

Esaminare i requisiti ed eseguire le procedure nel [Guida introduttiva](quickstart-install-connect-docker.md). È necessario specificare l'edizione di produzione con il **MSSQL_PID** variabile di ambiente. Nell'esempio seguente viene illustrato come eseguire l'immagine del contenitore SQL Server 2017 più recente per la versione Enterprise Edition:

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d store/microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "store/microsoft/mssql-server-linux:2017-latest"
 ```

> [!IMPORTANT]
> Passando il valore **Y** alla variabile di ambiente **ACCEPT_EULA** e un valore edition **MSSQL_PID**, Esprimi che si abbia una licenza valida ed esistente per l'edizione e la versione di SQL Server che si intende usare. L'utente accetta inoltre che l'utilizzo del software di SQL Server in esecuzione in un'immagine del contenitore Docker sarà disciplinato dalle condizioni di licenza di SQL Server.

> [!NOTE]
> Per un elenco completo dei valori possibili per **MSSQL_PID**, vedere [le impostazioni di configurazione SQL Server con le variabili di ambiente in Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Connettersi ed eseguire query

È possibile connettersi ed eseguire query di SQL Server in un contenitore dall'esterno del contenitore o dall'interno di contenitori. Le sezioni seguenti illustrano entrambi gli scenari. 

### <a name="tools-outside-the-container"></a>Strumenti all'esterno del contenitore

È possibile connettersi all'istanza di SQL Server nel computer che esegue Docker da uno strumento esterno Linux, Windows o macOS che supporta le connessioni SQL. Alcuni strumenti comuni includono:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) per Windows](sql-server-linux-manage-ssms.md)

L'esempio seguente usa **sqlcmd** per connettersi a SQL Server in esecuzione in un contenitore Docker. L'indirizzo IP nella stringa di connessione è l'indirizzo IP del computer host che esegue il contenitore.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Se una porta dell'host che non rappresenta il valore predefinito è stata mappata **1433**, aggiungere tale porta alla stringa di connessione. Ad esempio, se è stato specificato `-p 1400:1433` nella `docker run` comando e quindi connettersi in modo esplicito da specificare la porta 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Strumenti all'interno del contenitore

A partire da SQL Server 2017 preview, il [gli strumenti da riga di comando di SQL Server](sql-server-linux-setup-tools.md) sono inclusi nell'immagine del contenitore. Se si collega all'immagine con un prompt dei comandi interattiva, è possibile eseguire gli strumenti in locale.

1. Usare il comando `docker exec -it` per avviare una shell Bash interattiva all'interno del contenitore in esecuzione. Nell'esempio seguente `e69e056c702d` è l'ID del contenitore.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Non è sempre necessario specificare l'id intero contenitore. È sufficiente specificare un numero di caratteri sufficiente per identificarlo in modo univoco. Pertanto in questo esempio, potrebbe essere sufficiente per utilizzare `e6` o `e69` anziché l'id completo.

2. Una volta all'interno del contenitore, eseguire la connessione in locale con sqlcmd. Si noti che sqlcmd non è il percorso per impostazione predefinita, pertanto è necessario specificare il percorso completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Al termine con sqlcmd, digitare `exit`.

4. Al termine il prompt dei comandi interattivi, digitare `exit`. Dopo la chiusura della shell Bash interattiva, il contenitore continua l'esecuzione.

## <a name="run-multiple-sql-server-containers"></a>Esecuzione di più contenitori di SQL Server

Docker offre un modo per eseguire più contenitori di SQL Server nello stesso computer host. Questo è l'approccio per scenari che richiedono più istanze di SQL Server nello stesso host. Ogni contenitore deve esporre se stesso su una porta diversa.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Nell'esempio seguente crea due contenitori di SQL Server 2017 e ne esegue il mapping alle porte **1401** e **1402** nel computer host.

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

Nell'esempio seguente crea due contenitori di anteprima di SQL Server 2019 e ne esegue il mapping alle porte **1401** e **1402** nel computer host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

::: moniker-end

Sono ora presenti due istanze di SQL Server in esecuzione in contenitori separati. I client possono connettersi a ogni istanza di SQL Server usando l'indirizzo IP dell'host Docker e il numero di porta per il contenitore.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a> Creare un contenitore personalizzato

È possibile creare il proprio [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) per creare un contenitore personalizzato di SQL Server. Per altre informazioni, vedere [una demo che combina SQL Server e un'applicazione Node](https://github.com/twright-msft/mssql-node-docker-demo-app). Se si crea il Dockerfile, tenere il processo di primo piano, poiché questo processo consente di controllare il ciclo di vita del contenitore. Se presente, il contenitore verrà arrestato. Ad esempio, se si desidera eseguire uno script e avviare SQL Server, assicurarsi che il processo di SQL Server è il comando più a destra. Tutti gli altri comandi vengono eseguiti in background. Questo comportamento è illustrato nel comando seguente all'interno di un file Docker:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Se è invertito i comandi nell'esempio precedente, il contenitore sarà arresto al termine dello script-my-sql-commands.sh.

## <a id="persist"></a> Salvataggio permanente dei dati

Le modifiche alla configurazione di SQL Server e i file di database vengono rese persistenti nel contenitore anche se si riavvia il contenitore con `docker stop` e `docker start`. Tuttavia, se si rimuove il contenitore con `docker rm`, tutti gli elementi nel contenitore viene eliminato, tra cui SQL Server e dei database. La sezione seguente illustra come usare **volumi di dati** per rendere persistenti i file di database anche se i contenitori associati vengono eliminati.

> [!IMPORTANT]
> Per SQL Server, è importante comprendere la persistenza dei dati in Docker. Oltre a discussioni in questa sezione, vedere la documentazione di Docker nel [come gestire i dati in contenitori Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montare una directory host come volume di dati

La prima opzione consiste nel montare una directory nell'host di un volume di dati nel contenitore. A tale scopo, usare il `docker run` comando con il `-v <host directory>:/var/opt/mssql` flag. In questo modo i dati da ripristinare tra le esecuzioni di contenitore.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

::: moniker-end

Questa tecnica consente anche di condividere e visualizzare i file nell'host all'esterno di Docker.

> [!IMPORTANT]
> Mapping del volume host per Docker nel Mac con SQL Server a un'immagine Linux non è supportato in questo momento. Usare i contenitori dei volumi di dati. Questa restrizione è specifica per il `/var/opt/mssql` directory. Durante la lettura da un directory montata di funziona correttamente. Ad esempio, è possibile montare una directory di host utilizzando - v in computer Mac e ripristinare un backup da un file con estensione bak che risiede nell'host.

### <a name="use-data-volume-containers"></a>Usare i contenitori dei volumi di dati

La seconda opzione consiste nell'utilizzare un contenitore di volumi di dati. È possibile creare un contenitore di volumi di dati specificando un nome di volume invece di una directory di host con il `-v` parametro. L'esempio seguente crea un volume di dati condiviso denominato **sqlvolume**.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```
::: moniker-end

> [!NOTE]
> Questa tecnica per la creazione in modo implicito un volume di dati nel comando run non funziona con le versioni precedenti di Docker. In tal caso, usare la procedura esplicita descritta nella documentazione di Docker, [creazione e montaggio di un contenitore del volume dati](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Anche se si arresta e rimuovere questo contenitore, viene mantenuto il volume dei dati. È possibile visualizzarla con il `docker volume ls` comando.

```bash
docker volume ls
```

Se si crea quindi un altro contenitore con lo stesso nome di volume, il nuovo contenitore Usa gli stessi dati di SQL Server contenuti nel volume.

Per rimuovere un contenitore di volumi di dati, usare il `docker volume rm` comando.

> [!WARNING]
> Se si elimina il contenitore del volume dei dati, i dati di SQL Server nel contenitore vengono *definitivamente* eliminato.

### <a name="backup-and-restore"></a>Backup e ripristino

Oltre a queste tecniche di contenitore, è anche possibile usare backup di SQL Server standard e ripristinare le tecniche. È possibile usare i file di backup per proteggere i dati o per spostare i dati in un'altra istanza di SQL Server. Per altre informazioni, vedere [Backup e ripristino di database di SQL Server in Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Se si creano i backup, assicurarsi di creare o copiare i file di backup all'esterno del contenitore. Se viene rimosso il contenitore, in caso contrario, vengono eliminati anche i file di backup.

## <a name="execute-commands-in-a-container"></a>Eseguire i comandi in un contenitore

Se si dispone di un contenitore in esecuzione, è possibile eseguire comandi all'interno del contenitore da un host terminal.

Per ottenere l'ID del contenitore eseguire:

```bash
docker ps
```

Per avviare un terminale nel contenitore esegue bash:

```bash
docker exec -ti <Container ID> /bin/bash
```

A questo punto è possibile eseguire comandi come se sono in esecuzione nel terminale all'interno del contenitore. Al termine, digitare `exit`. Questo viene chiuso durante la sessione di comando interattiva, ma continua l'esecuzione del contenitore.

## <a name="copy-files-from-a-container"></a>Copiare i file da un contenitore

Per copiare un file all'esterno del contenitore, usare il comando seguente:

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

## <a name="copy-files-into-a-container"></a>Copiare i file in un contenitore

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

Per eseguire SQL Server in un contenitore Linux con un fuso orario specifico, configurare il **TZ** variabile di ambiente. Per trovare il valore di fuso orario corretto, eseguire la **tzselect** comando da un prompt di bash di Linux:

```bash
tzselect
```

Dopo aver selezionato il fuso orario **tzselect** Visualizza un output simile al seguente:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

È possibile usare queste informazioni per impostare la stessa variabile di ambiente nel contenitore Linux. Nell'esempio seguente viene illustrato come eseguire SQL Server in un contenitore di `Americas/Los_Angeles` fuso orario:

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
   -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```
::: moniker-end

## <a id="tags"></a> Eseguire un'immagine del contenitore SQL Server specifica

Esistono scenari in cui è possibile evitare di usare l'immagine del contenitore SQL Server più recente. Per eseguire un'immagine del contenitore SQL Server specifica, procedere come segue:

1. Identificare il Docker **tag** per la versione da usare. Per visualizzare i tag disponibili, vedere [pagina dell'hub Docker mssql-server-linux](https://hub.docker.com/_/microsoft-mssql-server).

2. Estrarre l'immagine del contenitore SQL Server con il tag. Ad esempio, per eseguire il pull dell'immagine RC1, sostituire `<image_tag>` nel comando seguente con `rc1`.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Per eseguire un nuovo contenitore con tale immagine, specificare il nome di tag nel `docker run` comando. Nel comando seguente, sostituire `<image_tag>` con la versione da eseguire.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Questi passaggi sono anche utilizzabile per effettuare il downgrade di un contenitore esistente. Ad esempio, si potrebbe desidera eseguire il rollback o il downgrade di un contenitore in esecuzione per la risoluzione dei problemi o il test. Per effettuare il downgrade di un contenitore in esecuzione, è necessario usare una tecnica di persistenza per la cartella di dati. Seguire la stessa procedura descritta nel [aggiornamento sezione](#upgrade), ma specificare il nome del tag della versione precedente, quando si esegue il nuovo contenitore.

## <a id="version"></a> Controllare la versione del contenitore

Se si desidera conoscere la versione di SQL Server in un contenitore docker in esecuzione, eseguire il comando seguente per visualizzarlo. Sostituire `<Container ID or name>` con il nome o ID di contenitore di destinazione. Sostituire `<YourStrong!Passw0rd>` con la password di SQL Server per l'account di accesso SA.

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

È anche possibile identificare la versione di SQL Server e numero di build per un'immagine contenitore docker di destinazione. Il comando seguente consente di visualizzare le informazioni di compilazione e versione di SQL Server per il **microsoft/mssql-server-linux:2017-più recente** immagine. A tale scopo, esegue un nuovo contenitore con una variabile di ambiente **PAL_PROGRAM_INFO = 1**. Il contenitore risultante viene immediatamente chiuso e il `docker rm` comando lo rimuove.

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

Il comando precedente Visualizza informazioni sulla versione simile all'output seguente:

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

## <a id="upgrade"></a> Aggiornamento di SQL Server in contenitori

Per aggiornare l'immagine del contenitore con Docker, prima di tutto identificare i tag per la versione dell'aggiornamento. Eseguire il pull dal Registro di sistema con questa versione il `docker pull` comando:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Aggiorna l'immagine di SQL Server per eventuali nuovi contenitori creati, ma non viene aggiornato SQL Server in tutti i contenitori in esecuzione. A tale scopo, è necessario creare un nuovo contenitore con l'immagine del contenitore SQL Server più recente e la migrazione dei dati a tale nuovo contenitore.

1. Assicurarsi che si usa uno dei [tecniche di persistenza dei dati](#persist) per il contenitore di SQL Server esistente. In questo modo è possibile avviare un nuovo contenitore con gli stessi dati.

1. Arrestare il contenitore di SQL Server con il `docker stop` comando.

1. Creare un nuovo contenitore di SQL Server con `docker run` e specificare una directory mappata host o un contenitore di volumi di dati. Assicurarsi di usare il tag specifico per l'aggiornamento di SQL Server. Il nuovo contenitore Usa ora una nuova versione di SQL Server con i dati di SQL Server esistenti.

   > [!IMPORTANT]
   > In questa fase di aggiornamento è supportato solo tra RC1 e RC2 a livello generale.

1. Verificare i database e i dati nel nuovo contenitore.

1. Facoltativamente, rimuovere il vecchio contenitore con `docker rm`.

## <a id="troubleshooting"></a> Risoluzione dei problemi

Le sezioni seguenti forniscono suggerimenti sulla risoluzione dei problemi per l'esecuzione di SQL Server in contenitori.

### <a name="docker-command-errors"></a>Errori di comando di docker

Se si verificano errori per qualsiasi `docker` comandi, assicurarsi che il servizio docker è in esecuzione e provare a eseguire con autorizzazioni elevate.

Ad esempio, in Linux, si potrebbe essere visualizzato l'errore seguente durante l'esecuzione `docker` comandi:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Se si verifica questo errore in Linux, provare a eseguire gli stessi comandi preceduti `sudo`. Se il problema persiste, verificare il servizio docker è in esecuzione e avviarlo, se necessario.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

In Windows, verificare che si avvia PowerShell o prompt dei comandi come amministratore.

### <a name="sql-server-container-startup-errors"></a>Errori di avvio contenitore SQL Server

Se il contenitore di SQL Server non viene eseguito correttamente, provare a eseguire i test seguenti:

- Se si verifica un errore, ad esempio **' non è stato possibile creare endpoint CONTAINER_NAME nel bridge di rete. Errore durante l'avvio proxy: bind 0.0.0.0:1433 di ascolto tcp: indirizzo già in uso.'** , quindi si sta provando a eseguire il mapping a una porta che è già in uso la porta del contenitore 1433. Questa situazione può verificarsi se si esegue SQL Server in locale nel computer host. Può inoltre verificarsi se si avvia due contenitori di SQL Server e provare a eseguire il mapping di entrambi per la stessa porta host. In questo caso, usare il `-p` parametro per eseguire il mapping a una porta dell'host diversa la porta del contenitore 1433. Ad esempio: 

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu`.
```

::: moniker-end

- Verificare se sono presenti eventuali messaggi di errore dal contenitore.

    ```bash
    docker logs e69e056c702d
    ```

- Assicurarsi che siano soddisfatti i requisiti minimi di memoria e disco specificati nella [prerequisiti](quickstart-install-connect-docker.md#requirements) sezione dell'articolo della Guida introduttiva.

- Se si usa qualsiasi software di gestione di contenitori, assicurarsi che supporta i processi contenitore in esecuzione come utente root. Il processo sqlservr nel contenitore viene eseguito come utente root.

- Rivedere le [log degli errori e il programma di installazione di SQL Server](#errorlogs).

### <a name="enable-dump-captures"></a>Abilitare le acquisizioni di dump

Se il processo di SQL Server non riesce all'interno del contenitore, è necessario creare un nuovo contenitore con **SYS_PTRACE** abilitata. Questo aggiunge la funzionalità di Linux per tracciare un processo che è necessario per la creazione di un file di dump di un'eccezione. Il file di dump può essere usato dal supporto per consentire di risolvere il problema. Il seguente comando docker run abilita questa funzionalità.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>Errori di connessione di SQL Server

Se non è possibile connettersi all'istanza di SQL Server in esecuzione nel contenitore, provare a eseguire i test seguenti:

- Assicurarsi che il contenitore SQL Server sia in esecuzione esaminando il **lo stato** colonna del `docker ps -a` output. In caso contrario, usare `docker start <Container ID>` per avviarla.

- Se è mappata a una porta dell'host non predefinita (non 1433), assicurarsi che si specifica la porta nella stringa di connessione. È possibile visualizzare il mapping delle porte nel **porte** colonna del `docker ps -a` output. Il comando seguente, ad esempio, si connette sqlcmd in un contenitore in ascolto sulla porta 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Se è stata usata `docker run` con un volume di dati con mapping esistente o un contenitore di volumi di dati, SQL Server ignora il valore di `MSSQL_SA_PASSWORD`. Al contrario, la password dell'utente dell'amministratore di sistema configurata in precedenza viene utilizzata dai dati nel volume di dati o il contenitore di volumi di dati SQL Server. Verificare che si sta utilizzando la password dell'amministratore di sistema associata ai dati che a cui si stia collegando.

- Rivedere le [log degli errori e il programma di installazione di SQL Server](#errorlogs).

### <a name="sql-server-availability-groups"></a>Gruppi di disponibilità SQL Server

Se si usa Docker con gruppi di disponibilità di SQL Server, esistono due requisiti aggiuntivi.

- Eseguire il mapping di porta che viene usata per la comunicazione di replica (impostazione predefinita 5022). Ad esempio, specificare `-p 5022:5022` come parte di `docker run` comando.

- Impostare in modo esplicito il nome host del contenitore con il `-h YOURHOSTNAME` parametro del `docker run` comando. Questo nome host viene usato quando si configura il gruppo di disponibilità. Se non si specifica con `-h`, l'impostazione predefinita è l'ID del contenitore.

### <a id="errorlogs"></a> Log degli errori e il programma di installazione di SQL Server

È possibile esaminare il programma di installazione di SQL Server e log degli errori **/var/opt/mssql/log**. Se il contenitore non è in esecuzione, avviare innanzitutto il contenitore. Usare quindi un prompt dei comandi interattiva per controllare i log.

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

Dalla sessione bash all'interno del contenitore, eseguire i comandi seguenti:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> Se è stata montata una directory di host in cui **/var/opt/mssql** durante la creazione del contenitore, è invece possibile cercare nel **log** sottodirectory nel percorso mappato nell'host.

## <a name="next-steps"></a>Passaggi successivi

Introduzione a immagini del contenitore SQL Server 2017 in Docker, consultare il [Guida introduttiva](quickstart-install-connect-docker.md).

Vedere anche il [repository GitHub mssql-docker](https://github.com/Microsoft/mssql-docker) per le risorse, feedback e problemi noti.

[Esplorare la disponibilità elevata per i contenitori di SQL Server](sql-server-linux-container-ha-overview.md)
