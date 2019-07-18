---
title: Eseguire SQL Server Machine Learning Services in un contenitore | Microsoft Docs
description: Questa esercitazione illustra come usare SQL Server Machine Learning Services in un contenitore Linux in esecuzione in docker.
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f3d3774adf4bee07269b25c3359b031ca24eb99e
ms.sourcegitcommit: ef7834ed0f38c1712f45737018a0bfe892e894ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2019
ms.locfileid: "68300428"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>Eseguire SQL Server Machine Learning Services in un contenitore

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questa esercitazione illustra come creare un contenitore Docker con SQL Server Machine Learning Services ed eseguire script di Machine Learning da Transact-SQL.

> [!div class="checklist"]
> * Clonare il repository MSSQL-docker.
> * Creare SQL Server immagine del contenitore Linux con Machine Learning Services.
> * Eseguire SQL Server immagine del contenitore Linux con Machine Learning Services.
> * Eseguire script R o Python usando istruzioni Transact-SQL.
> * Arrestare e rimuovere il contenitore SQL Server Linux. 

## <a name="prerequisites"></a>Prerequisiti

* Interfaccia della riga di comando di git.
* Motore Docker 1.8 o versione successiva in qualsiasi distribuzione di Linux supportata oppure Docker per Mac/Windows. Per altre informazioni, vedere [Installare Docker](https://docs.docker.com/engine/installation/).
* Almeno 2 GB di spazio su disco.
* Almeno 2 GB di RAM.
* [Requisiti di sistema per SQL Server su Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonare il repository MSSQL-Docker

1. Aprire un terminale bash in un terminale Linux/Mac o WSL in Windows.

1. Creare una directory locale per conservare una copia del repository MSSQL-Docker in locale.
1. Eseguire il comando git clone per clonare il repository MSSQL-docker.

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>Creare SQL Server immagine del contenitore Linux con Machine Learning Services

1. Passare alla directory MSSQL-mlservices.

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. Eseguire lo script build.sh.

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > Per la creazione dell'immagine Docker è necessario installare pacchetti di dimensioni diverse di GB. Il completamento dello script può richiedere fino a 20 minuti a seconda della larghezza di banda di rete.

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>Eseguire SQL Server immagine del contenitore Linux con Machine Learning Services

1. Impostare le variabili di ambiente prima di eseguire il contenitore. Impostare la variabile di ambiente PATH_TO_MSSQL su una directory host.

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. Eseguire lo script run.sh.

   ```bash
   ./run.sh
   ```

   Questo comando crea un contenitore di SQL Server con Machine Learning Services con Developer Edition (impostazione predefinita). SQL Server porta **1433** è esposta nell'host come porta **1401**.

   > [!NOTE]
   > Il processo per l'esecuzione di edizioni SQL Server di produzione nei contenitori è leggermente diverso. Per altre informazioni, vedere [configurare SQL Server immagini del contenitore in Docker](sql-server-linux-configure-docker.md). Se si usano gli stessi nomi di contenitore e le stesse porte, il resto di questa procedura dettagliata funziona comunque con i contenitori di produzione.

1. Per visualizzare i contenitori di Docker, usare il comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

1. Se nella colonna **STATUS** è impostato lo stato**Up**, SQL Server è in esecuzione nel contenitore e in ascolto sulla porta specificata nella colonna **PORTS**. Se la colonna **STATUS** del contenitore di SQL Server è impostata su **Exited**, vedere la [sezione relativa alla risoluzione dei problemi della guida alla configurazione](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a
   ```

    Output: 
    
    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="change-the-sa-password"></a>Cambiare la password dell'amministratore di sistema

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="execute-r--python-scripts-from-transact-sql"></a>Eseguire script R/Python da Transact-SQL

1. Connettersi a SQL Server nel contenitore e abilitare l'opzione di configurazione script esterno eseguendo l'istruzione T-SQL seguente.

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. Verificare Machine Learning Services funziona eseguendo il semplice sp_execute_external_script R/Python seguente.

    ```sql
    execute sp_execute_external_script 
    @language = N'R',
    @script = N'
    print("Hello World!")
    print(R.version)
    print(Revo.version)
    OutputDataSet <- InputDataSet', 
    @input_data_1 = N'select 1'
    with result sets((i int));
    go
    ```

    ```sql
    execute sp_execute_external_script 
    @language = N'Python',
    @script = N'
    import sys
    print(sys.version)
    print("Hello World!")
    OutputDataSet = InputDataSet',
    @input_data_1 = N'select 1'
    with result sets((i int));
    go 
    ```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come eseguire le operazioni seguenti:

> [!div class="checklist"]
> * Clonare il repository MSSQL-docker.
> * Creare SQL Server immagine del contenitore Linux con Machine Learning Services.
> * Eseguire SQL Server immagine del contenitore Linux con Machine Learning Services.
> * Eseguire script R o Python usando istruzioni Transact-SQL.
> * Arrestare e rimuovere il contenitore SQL Server Linux.

Esaminare quindi altri scenari di configurazione e risoluzione dei problemi di Docker:

> [!div class="nextstepaction"]
>[Guida alla configurazione per SQL Server in Docker](sql-server-linux-configure-docker.md)
