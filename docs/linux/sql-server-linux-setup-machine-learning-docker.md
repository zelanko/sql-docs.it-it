---
title: Installare in Docker
titleSuffix: SQL Server Machine Learning Services
description: Informazioni su come installare SQL Server Machine Learning Services (Python e R) in Docker.
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 03/23/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5a53419aba5515a9a60817ec0cc2a9de5a648d2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "80228342"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>Installare SQL Server Machine Learning Services (Python e R) in Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come installare SQL Server Machine Learning Services in Docker. È possibile usare Machine Learning Services per eseguire gli script Python e R nel database. Non vengono forniti contenitori predefiniti con Machine Learning Services. È possibile crearne uno dai contenitori di SQL Server usando [un modello di esempio disponibile in GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="prerequisites"></a>Prerequisiti

- Interfaccia della riga di comando di Git.

- Motore Docker 1.8 o versione successiva in qualsiasi distribuzione di Linux supportata oppure Docker per Mac/Windows. Per altre informazioni, vedere [Get Docker](https://docs.docker.com/get-docker/) (Ottenere Docker).

- Vedere anche i [requisiti di sistema per SQL Server in Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonare il repository mssql-docker

Il comando seguente consente di clonare il repository git `mssql-docker` in una directory locale.

1. Aprire un terminale Bash in Linux o Mac oppure un terminale del sottosistema Windows per Linux in Windows.

2. Creare una directory in cui mantenere una copia locale del repository mssql-docker.

3. Eseguire il comando git clone per clonare il repository mssql-docker:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>Creare un'immagine del contenitore di SQL Server su Linux

Completare i passaggi seguenti per creare l'immagine docker:

1. Passare alla directory mssql-mlservices:

2. Nella stessa directory eseguire il comando seguente:

    ```bash
    docker builds -t mssql-server-mlservices
    ```

3. Eseguire il comando:

    ```bash
    docker runs -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e SA_PASSWORD=<your_sa_password> -v OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```

    Modificare `<your_sa_password>` in `SA_PASSWORD=<your_sa_password>` e modificare il percorso di `-v`. 

4. Confermare eseguendo questo comando:

    ```bash
    docker ps -a
    ```

   > [!NOTE]
   > Per creare l'immagine Docker è necessario installare pacchetti di dimensioni pari a diversi GB. Il completamento dell'esecuzione dello script può richiedere tempo, a seconda della larghezza di banda di rete.

## <a name="run-the-sql-server-linux-container-image"></a>Eseguire l'immagine del contenitore di SQL Server su Linux

1. Impostare le variabili di ambiente prima di eseguire il contenitore. Impostare la variabile di ambiente PATH_TO_MSSQL su una directory host:

   ```bash
   export MSSQL_PID='Developer'
   export ACCEPT_EULA='Y'
   export ACCEPT_EULA_ML='Y'
   export PATH_TO_MSSQL='/home/mssql/'
   ```

2. Eseguire lo script run.sh:

   ```bash
   ./run.sh
   ```

   Questo comando crea un contenitore di SQL Server con Machine Learning Services usando la Developer Edition (impostazione predefinita). La porta **1433** di SQL Server è esposta nell'host come porta **1401**.

   > [!NOTE]
   > Il processo di esecuzione delle edizioni di SQL Server di produzione nei contenitori è leggermente diverso. Per altre informazioni, vedere [Configurare immagini dei contenitori SQL Server in Docker](sql-server-linux-configure-docker.md). Se si usano gli stessi nomi di contenitore e le stesse porte, il resto di questa procedura dettagliata funziona comunque con i contenitori di produzione.

3. Per visualizzare i contenitori di Docker, usare il comando `docker ps`:

   ```bash
   sudo docker ps -a
   ```

4. Se nella colonna **STATUS** è impostato lo stato **Up**, SQL Server è in esecuzione nel contenitore e in ascolto sulla porta specificata nella colonna **PORTS**. Se la colonna **STATUS** del contenitore di SQL Server è impostata su **Exited**, vedere la [sezione relativa alla risoluzione dei problemi della guida alla configurazione](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a
   ```

    Output:

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="enable-machine-learning-services"></a>Abilitare Machine Learning Services

Per abilitare Machine Learning Services, connettersi all'istanza di SQL Server ed eseguire l'istruzione T-SQL seguente:

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>Passaggi successivi

Gli sviluppatori Python possono apprendere come usare Python con SQL Server seguendo queste esercitazioni:

+ [Esercitazione su Python: Stimare il noleggio di sci con la regressione lineare in Machine Learning Services per SQL Server](../advanced-analytics/tutorials/python-ski-rental-linear-regression.md)
+ [Esercitazione: Categorizzazione dei clienti tramite clustering K-Means con Machine Learning Services per SQL Server](../advanced-analytics/tutorials/python-clustering-model.md)

Gli sviluppatori R possono iniziare alcuni semplici esempi e con le nozioni di base sul funzionamento di R con SQL Server. Per il passaggio successivo, vedere i collegamenti seguenti:

+ [Esercitazione: Eseguire R in T-SQL](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Esercitazione: Analisi nel database per sviluppatori R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)
