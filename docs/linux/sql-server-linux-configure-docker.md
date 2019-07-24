---
title: Opzioni di configurazione per SQL Server in Docker
description: Esplora le diverse modalità di utilizzo e interazione con SQL Server le immagini del contenitore di anteprima 2017 e 2019 in docker. Ciò include la conservazione dei dati, la copia di file e la risoluzione dei problemi.
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: d24bb3566195c71a3b62d16fab867ab5085404b7
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388375"
---
# <a name="configure-sql-server-container-images-on-docker"></a>Configurare SQL Server immagini del contenitore in Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come configurare e usare l' [immagine del contenitore MSSQL-Server-Linux](https://hub.docker.com/_/microsoft-mssql-server) con Docker. Questa immagine è costituita da SQL Server in esecuzione su Linux basato su Ubuntu 16.04. Può essere usata con il motore Docker 1.8 o versione successiva su Linux o in Docker per Mac/Windows.

> [!NOTE]
> Questo articolo è incentrato soprattutto sull'uso dell'immagine MSSQL-Server-Linux. L'immagine di Windows non viene analizzata, ma è possibile ottenere altre informazioni sulla [pagina relativa all'hub Docker di MSSQL-Server-Windows](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/).

## <a name="pull-and-run-the-container-image"></a>Effettuare il pull ed eseguire l'immagine del contenitore

Per eseguire il pull e l'esecuzione delle immagini del contenitore Docker per SQL Server 2017 e SQL Server 2019 Preview, seguire i prerequisiti e i passaggi illustrati nella Guida introduttiva seguente:

- [Eseguire l'immagine del contenitore SQL Server 2017 con Docker](quickstart-install-connect-docker.md?view=sql-server-2017)
- [Eseguire l'immagine del contenitore SQL Server 2019 Preview con Docker](quickstart-install-connect-docker.md?view=sql-server-ver15)

Questo articolo di configurazione fornisce altri scenari di utilizzo nelle sezioni seguenti.

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a>Eseguire immagini del contenitore basate su RHEL

Tutta la documentazione su SQL Server immagini contenitore Linux puntano a contenitori basati su Ubuntu. A partire da SQL Server 2019 Preview, è possibile usare i contenitori basati su Red Hat Enterprise Linux (RHEL). Modificare il repository del contenitore da **MCR.Microsoft.com/MSSQL/Server:2019-CTP3.1-Ubuntu** a **MCR.Microsoft.com/MSSQL/RHEL/Server:2019-CTP3.1** in tutti i comandi di Docker.

Ad esempio, il comando seguente estrae l'ultimo contenitore di anteprima SQL Server 2019 che usa RHEL:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a>Esegui immagini del contenitore di produzione

La Guida introduttiva nella sezione precedente esegue la versione Developer Edition gratuita di SQL Server dall'hub docker. La maggior parte delle informazioni si applica anche se si vuole eseguire immagini del contenitore di produzione, ad esempio le edizioni Enterprise, standard o Web. Tuttavia, esistono alcune differenze descritte di seguito.

- È possibile utilizzare SQL Server in un ambiente di produzione solo se si dispone di una licenza valida. [Qui](https://go.microsoft.com/fwlink/?linkid=857693)è possibile ottenere una licenza di produzione SQL Server Express gratuita. Le licenze SQL Server Standard ed Enterprise Edition sono disponibili tramite [Microsoft Volume Licensing](https://www.microsoft.com/licensing/default.aspx).


- È possibile configurare l'immagine del contenitore per sviluppatori anche per eseguire le edizioni di produzione. Per eseguire le edizioni di produzione, attenersi alla procedura seguente:

Esaminare i requisiti e le procedure di esecuzione nella [Guida introduttiva](quickstart-install-connect-docker.md). È necessario specificare l'edizione di produzione con la variabile di ambiente **MSSQL_PID** . Nell'esempio seguente viene illustrato come eseguire la versione più recente dell'immagine del contenitore SQL Server 2017 per Enterprise Edition:

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
> Passando il valore **Y** alla variabile di ambiente **ACCEPT_EULA** e un valore di edizione a **MSSQL_PID**, si esprime la presenza di una licenza valida e esistente per l'edizione e la versione di SQL Server che si intende usare. Si accetta anche che l'uso di SQL Server software in esecuzione in un'immagine del contenitore Docker sarà disciplinato dalle condizioni della licenza di SQL Server.

> [!NOTE]
> Per un elenco completo dei valori possibili per **MSSQL_PID**, vedere [configurare le impostazioni di SQL Server con le variabili di ambiente in Linux](sql-server-linux-configure-environment-variables.md).

::: moniker-end

## <a name="connect-and-query"></a>Connessione ed esecuzione di query

È possibile connettersi ed eseguire query SQL Server in un contenitore dall'esterno del contenitore o dall'interno del contenitore. Nelle sezioni seguenti vengono illustrati entrambi gli scenari. 

### <a name="tools-outside-the-container"></a>Strumenti esterni al contenitore

È possibile connettersi all'istanza di SQL Server nel computer Docker da qualsiasi strumento Linux, Windows o macOS esterno che supporta le connessioni SQL. Alcuni strumenti comuni includono:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) per Windows](sql-server-linux-manage-ssms.md)

Nell'esempio seguente viene usato **SQLCMD** per connettersi a SQL Server in esecuzione in un contenitore docker. L'indirizzo IP nella stringa di connessione è l'indirizzo IP del computer host in cui è in esecuzione il contenitore.

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

Se è stato eseguito il mapping di una porta host che non è l'impostazione predefinita **1433**, aggiungere la porta alla stringa di connessione. Se, ad esempio, è `-p 1400:1433` stato specificato `docker run` nel comando, connettersi specificando in modo esplicito la porta 1400.

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>Strumenti all'interno del contenitore

A partire da SQL Server 2017 Preview, gli [strumenti da riga di comando SQL Server](sql-server-linux-setup-tools.md) sono inclusi nell'immagine del contenitore. Se ci si connette all'immagine con un prompt dei comandi interattivo, è possibile eseguire gli strumenti localmente.

1. Usare il comando `docker exec -it` per avviare una shell Bash interattiva all'interno del contenitore in esecuzione. Nell'esempio `e69e056c702d` seguente viene riportato l'ID del contenitore.

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > Non è sempre necessario specificare l'intero ID del contenitore. È necessario specificare un numero sufficiente di caratteri per identificarlo in modo univoco. Quindi, in questo esempio, potrebbe essere sufficiente utilizzare `e6` o `e69` anziché l'ID completo.

2. Una volta all'interno del contenitore, eseguire la connessione in locale con sqlcmd. Si noti che sqlcmd non si trova nel percorso per impostazione predefinita, pertanto è necessario specificare il percorso completo.

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. Al termine di sqlcmd, digitare `exit`.

4. Al termine del prompt dei comandi interattivo, digitare `exit`. Dopo la chiusura della shell Bash interattiva, il contenitore continua l'esecuzione.

## <a name="run-multiple-sql-server-containers"></a>Eseguire più contenitori di SQL Server

Docker fornisce un modo per eseguire più contenitori di SQL Server nello stesso computer host. Si tratta dell'approccio per gli scenari che richiedono più istanze di SQL Server nello stesso host. Ogni contenitore deve esporsi su una porta diversa.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Nell'esempio seguente vengono creati due contenitori SQL Server 2017 e ne viene eseguito il mapping alle porte **1401** e **1402** nel computer host.

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

Nell'esempio seguente vengono creati due contenitori SQL Server 2019 Preview e ne viene eseguito il mapping alle porte **1401** e **1402** nel computer host.

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

Sono ora disponibili due istanze di SQL Server in esecuzione in contenitori distinti. I client possono connettersi a ogni istanza di SQL Server usando l'indirizzo IP dell'host Docker e il numero di porta per il contenitore.

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a>Creare un contenitore personalizzato

È possibile creare un [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) personalizzato per creare un contenitore SQL Server personalizzato. Per ulteriori informazioni, vedere [una demo che combina SQL Server e un'applicazione Node](https://github.com/twright-msft/mssql-node-docker-demo-app). Se si crea un Dockerfile personalizzato, tenere presente il processo in primo piano, perché questo processo controlla la durata del contenitore. Se viene chiuso, il contenitore viene arrestato. Se ad esempio si vuole eseguire uno script e avviare SQL Server, assicurarsi che il processo di SQL Server sia il comando più a destra. Tutti gli altri comandi vengono eseguiti in background. Questa operazione è illustrata nel comando seguente all'interno di una Dockerfile:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

Se sono stati invertiti i comandi nell'esempio precedente, il contenitore viene arrestato al termine dello script do-my-sql-commands.sh.

## <a id="persist"></a>Mantieni i tuoi dati

Le modifiche apportate alla configurazione del SQL Server e i file di database vengono salvati in modo permanente nel `docker stop` contenitore `docker start`anche se il contenitore viene riavviato con e. Tuttavia, se si rimuove il contenitore con `docker rm`, tutto il contenitore viene eliminato, inclusi SQL Server e i database. Nella sezione seguente viene illustrato come utilizzare i **volumi di dati** per salvare in modo permanente i file di database anche se i contenitori associati vengono eliminati.

> [!IMPORTANT]
> Per SQL Server, è fondamentale comprendere la persistenza dei dati in docker. Oltre alla discussione in questa sezione, vedere la documentazione di Docker su [come gestire i dati nei contenitori Docker](https://docs.docker.com/engine/tutorials/dockervolumes/).

### <a name="mount-a-host-directory-as-data-volume"></a>Montare una directory host come volume di dati

La prima opzione consiste nel montare una directory nell'host come volume di dati nel contenitore. A tale scopo, utilizzare il `docker run` comando con il `-v <host directory>:/var/opt/mssql` flag. In questo modo è possibile ripristinare i dati tra le esecuzioni dei contenitori.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

Questa tecnica consente anche di condividere e visualizzare i file nell'host all'esterno di Docker.

> [!IMPORTANT]
> Il mapping del volume host per Docker su Mac con l'immagine SQL Server in Linux non è attualmente supportato. Usare invece i contenitori del volume di dati. Questa restrizione è specifica per `/var/opt/mssql` la directory. La lettura da una directory montata funziona correttamente. Ad esempio, è possibile montare una directory host usando-v in Mac e ripristinare un backup da un file con estensione bak che risiede nell'host.

### <a name="use-data-volume-containers"></a>Usare i contenitori di volumi di dati

La seconda opzione consiste nell'usare un contenitore di volumi di dati. È possibile creare un contenitore di volumi di dati specificando un nome di volume anziché una directory host `-v` con il parametro. Nell'esempio seguente viene creato un volume di dati condiviso denominato sqlvolume.

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

> [!NOTE]
> Questa tecnica per la creazione implicita di un volume di dati nel comando Run non funziona con le versioni precedenti di Docker. In tal caso, usare i passaggi espliciti descritti nella documentazione di Docker, [creando e montando un contenitore del volume di dati](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container).

Anche se si arresta e rimuove il contenitore, il volume di dati viene reso permanente. È possibile visualizzarlo con il `docker volume ls` comando.

```bash
docker volume ls
```

Se successivamente si crea un altro contenitore con lo stesso nome del volume, il nuovo contenitore utilizzerà gli stessi dati SQL Server contenuti nel volume.

Per rimuovere un contenitore di volumi di dati, `docker volume rm` usare il comando.

> [!WARNING]
> Se si elimina il contenitore del volume di dati, tutti i dati SQL Server nel contenitore verranno eliminati *definitivamente* .

### <a name="backup-and-restore"></a>Backup e ripristino

Oltre a queste tecniche di contenitori, è anche possibile usare le tecniche standard di backup e ripristino di SQL Server. È possibile utilizzare i file di backup per proteggere i dati o per spostare i dati in un'altra istanza di SQL Server. Per altre informazioni, vedere [backup e ripristino SQL Server database in Linux](sql-server-linux-backup-and-restore-database.md).

> [!WARNING]
> Se si creano backup, assicurarsi di creare o copiare i file di backup all'esterno del contenitore. In caso contrario, se il contenitore viene rimosso, vengono eliminati anche i file di backup.

## <a name="execute-commands-in-a-container"></a>Eseguire comandi in un contenitore

Se si dispone di un contenitore in esecuzione, è possibile eseguire i comandi all'interno del contenitore da un terminale host.

Per ottenere l'ID del contenitore eseguire:

```bash
docker ps
```

Per avviare un terminale bash nell'esecuzione del contenitore:

```bash
docker exec -it <Container ID> /bin/bash
```

A questo punto è possibile eseguire i comandi come se fossero in esecuzione nel terminale all'interno del contenitore. Al termine, digitare `exit`. Questa operazione viene chiusa nella sessione interattiva dei comandi, ma l'esecuzione del contenitore continua.

## <a name="copy-files-from-a-container"></a>Copia i file da un contenitore

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
## <a id="tz"></a>Configurare il fuso orario

Per eseguire SQL Server in un contenitore Linux con un fuso orario specifico, configurare la variabile di ambiente **TZ** . Per trovare il valore del fuso orario corretto, eseguire il comando **tzselect** da un prompt di bash per Linux:

```bash
tzselect
```

Dopo aver selezionato il fuso orario, **tzselect** Visualizza un output simile al seguente:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

È possibile usare queste informazioni per impostare la stessa variabile di ambiente nel contenitore Linux. Nell'esempio seguente viene illustrato come eseguire SQL Server in un contenitore nel `Americas/Los_Angeles` fuso orario:

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
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

## <a id="tags"></a>Eseguire un'immagine del contenitore di SQL Server specifica

Esistono scenari in cui è possibile che non si desideri usare la versione più recente di SQL Server immagine del contenitore. Per eseguire un'immagine del contenitore di SQL Server specifica, attenersi alla procedura seguente:

1. Identificare il **tag** Docker per la versione che si vuole usare. Per visualizzare i tag disponibili, vedere [la pagina MSSQL-Server-Linux Docker Hub](https://hub.docker.com/_/microsoft-mssql-server).

2. Estrarre l'immagine del contenitore di SQL Server con il tag. Ad esempio, per eseguire il pull dell'immagine RC1 `<image_tag>` , sostituire nel comando seguente `rc1`con.

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. Per eseguire un nuovo contenitore con tale immagine, specificare il nome del tag nel `docker run` comando. Nel comando seguente sostituire `<image_tag>` con la versione che si vuole eseguire.

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

Questi passaggi possono essere usati anche per eseguire il downgrade di un contenitore esistente. Ad esempio, potrebbe essere necessario eseguire il rollback o il downgrade di un contenitore in esecuzione per la risoluzione dei problemi o il test. Per eseguire il downgrade di un contenitore in esecuzione, è necessario utilizzare una tecnica di persistenza per la cartella dati. Seguire la stessa procedura descritta nella [sezione aggiornamento](#upgrade), ma specificare il nome del tag della versione precedente quando si esegue il nuovo contenitore.

## <a id="version"></a>Controllare la versione del contenitore

Se si vuole ottenere informazioni sulla versione di SQL Server in un contenitore Docker in esecuzione, eseguire il comando seguente per visualizzarlo. Sostituire `<Container ID or name>` con l'ID o il nome del contenitore di destinazione. Sostituire `<YourStrong!Passw0rd>` con la password SQL Server per l'account di accesso sa.

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

È anche possibile identificare la versione SQL Server e il numero di build per un'immagine del contenitore Docker di destinazione. Il comando seguente Visualizza la versione SQL Server e le informazioni di compilazione per l'immagine **Microsoft/MSSQL-Server-Linux: 2017-Latest** . A tale scopo, esegue un nuovo contenitore con una variabile di ambiente **PAL_PROGRAM_INFO = 1**. Il contenitore risultante si chiude immediatamente e il comando `docker rm` lo rimuove.

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

## <a id="upgrade"></a>Aggiornare SQL Server nei contenitori

Per aggiornare l'immagine del contenitore con Docker, identificare prima di tutto il tag per la versione per l'aggiornamento. Estrarre questa versione dal registro di sistema con `docker pull` il comando:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

Questo Aggiorna l'immagine di SQL Server per tutti i nuovi contenitori creati, ma non aggiorna SQL Server in alcun contenitore in esecuzione. A tale scopo, è necessario creare un nuovo contenitore con l'immagine del contenitore SQL Server più recente ed eseguire la migrazione dei dati al nuovo contenitore.

1. Assicurarsi di usare una delle tecniche di persistenza dei [dati](#persist) per il contenitore di SQL Server esistente. In questo modo è possibile avviare un nuovo contenitore con gli stessi dati.

1. Arrestare il contenitore SQL Server con il `docker stop` comando.

1. Creare una nuova SQL Server contenitore con `docker run` e specificare una directory host mappata o un contenitore di volumi di dati. Assicurarsi di usare il tag specifico per l'aggiornamento del SQL Server. Il nuovo contenitore ora usa una nuova versione di SQL Server con i dati di SQL Server esistenti.

   > [!IMPORTANT]
   > L'aggiornamento è supportato solo tra RC1, RC2 e GA al momento.

1. Verificare i database e i dati nel nuovo contenitore.

1. Facoltativamente, rimuovere il contenitore precedente con `docker rm`.

## <a id="troubleshooting"></a> Risoluzione dei problemi

Le sezioni seguenti forniscono suggerimenti per la risoluzione dei problemi per l'esecuzione di SQL Server nei contenitori.

### <a name="docker-command-errors"></a>Errori del comando Docker

Se vengono visualizzati errori per tutti `docker` i comandi, assicurarsi che il servizio Docker sia in esecuzione e provare a eseguire con autorizzazioni elevate.

Ad esempio, in Linux è possibile che si ottenga l'errore seguente `docker` quando si eseguono i comandi:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

Se si riceve questo errore in Linux, provare a eseguire gli stessi comandi preceduti da `sudo`. Se il tentativo non riesce, verificare che il servizio Docker sia in esecuzione e, se necessario, avviarlo.

```bash
sudo systemctl status docker
sudo systemctl start docker
```

In Windows verificare di aver avviato PowerShell o il prompt dei comandi come amministratore.

### <a name="sql-server-container-startup-errors"></a>Errori di avvio del contenitore SQL Server

Se non è possibile eseguire il contenitore SQL Server, provare i test seguenti:

- Se viene ricevuto un errore, ad **esempio ' non è stato possibile creare l'endpoint CONTAINER_NAME nel Bridge di rete. Errore durante l'avvio del proxy: ascolto TCP 0.0.0.0:1433 binding: Indirizzo già in uso.** , si sta tentando di eseguire il mapping della porta del contenitore 1433 a una porta già in uso. Questo problema può verificarsi se si esegue SQL Server localmente nel computer host. Può verificarsi anche se si avviano due contenitori SQL Server e si tenta di eseguirne il mapping entrambi alla stessa porta host. In tal caso, usare il `-p` parametro per eseguire il mapping della porta del contenitore 1433 a una porta host diversa. Ad esempio: 

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

::: moniker-end

- Se viene ricevuto un errore, ad **esempio "autorizzazione negata durante il tentativo di connessione al socket del daemon Docker in UNIX:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: Dial Unix/var/run/docker.sock: Connect: autorizzazione** negata durante il tentativo di avviare un contenitore, quindi aggiungere l'utente al gruppo Docker in Ubuntu. Quindi disconnettersi e accedere di nuovo perché questa modifica influirà sulle nuove sessioni. 

   ```bash
    usermod -aG docker $USER
    ```
- Controllare se sono presenti messaggi di errore dal contenitore.

    ```bash
    docker logs e69e056c702d
    ```

- Assicurarsi di soddisfare i requisiti minimi di memoria e disco specificati nella sezione [prerequisiti](quickstart-install-connect-docker.md#requirements) dell'articolo della Guida introduttiva.

- Se si usa un software di gestione dei contenitori, assicurarsi che supporti i processi contenitore in esecuzione come radice. Il processo sqlservr nel contenitore viene eseguito come radice.

- Esaminare i [registri errori e di installazione SQL Server](#errorlogs).

### <a name="enable-dump-captures"></a>Abilita acquisizioni dump

Se il processo di SQL Server non riesce all'interno del contenitore, è necessario creare un nuovo contenitore con **SYS_PTRACE** abilitato. In questo modo viene aggiunta la funzionalità Linux per tracciare un processo, che è necessario per la creazione di un file dump in un'eccezione. Il file dump può essere utilizzato dal supporto tecnico per risolvere il problema. Il comando Docker Run seguente abilita questa funzionalità.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>Errori di connessione SQL Server

Se non è possibile connettersi all'istanza di SQL Server in esecuzione nel contenitore, provare i test seguenti:

- Verificare che il contenitore di SQL Server sia in esecuzione esaminando la colonna **stato** dell' `docker ps -a` output. In caso contrario, `docker start <Container ID>` utilizzare per avviarlo.

- Se è stato eseguito il mapping a una porta host non predefinita (non 1433), assicurarsi di specificare la porta nella stringa di connessione. È possibile visualizzare il mapping delle porte nella colonna **porte** dell' `docker ps -a` output. Il comando seguente, ad esempio, connette sqlcmd a un contenitore in ascolto sulla porta 1401:

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- Se è stato `docker run` usato con un volume di dati o un contenitore del volume di dati con mapping esistente, `MSSQL_SA_PASSWORD`SQL Server ignora il valore di. Al contrario, la password dell'utente SA preconfigurata viene utilizzata dai dati SQL Server nel contenitore del volume di dati o del volume di dati. Verificare di usare la password SA associata ai dati a cui si sta eseguendo la connessione.

- Esaminare i [registri errori e di installazione SQL Server](#errorlogs).

### <a name="sql-server-availability-groups"></a>Gruppi di disponibilità SQL Server

Se si usa Docker con SQL Server gruppi di disponibilità, esistono due requisiti aggiuntivi.

- Eseguire il mapping della porta utilizzata per la comunicazione di replica (valore predefinito 5022). Ad esempio, specificare `-p 5022:5022` come parte `docker run` del comando.

- Impostare in modo esplicito il nome host del `-h YOURHOSTNAME` contenitore con il `docker run` parametro del comando. Questo nome host viene usato quando si configura il gruppo di disponibilità. Se non viene specificato con `-h`, il valore predefinito è l'ID del contenitore.

### <a id="errorlogs"></a>SQL Server di installazione e log degli errori

È possibile esaminare i log degli errori e di installazione di SQL Server in **/var/opt/MSSQL/log**. Se il contenitore non è in esecuzione, avviare innanzitutto il contenitore. Usare quindi un prompt dei comandi interattivo per esaminare i log.

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
> Se è stata montata una directory host in **/var/opt/MSSQL** al momento della creazione del contenitore, è possibile esaminare la sottodirectory **log** sul percorso mappato nell'host.

## <a name="next-steps"></a>Passaggi successivi

Per iniziare a usare le immagini del contenitore di SQL Server 2017 in Docker, passare alla [Guida introduttiva](quickstart-install-connect-docker.md).

Vedere anche il [repository GitHub MSSQL-Docker](https://github.com/Microsoft/mssql-docker) per risorse, commenti e suggerimenti e problemi noti.

[Esplora la disponibilità elevata per i contenitori di SQL Server](sql-server-linux-container-ha-overview.md)
