---
title: Distribuzione offline
titleSuffix: SQL Server big data clusters
description: Informazioni su come eseguire una distribuzione offline di un cluster SQL Server Big Data.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd8b3128fc11037a5ade494813611d473c995f8f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419373"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Eseguire una distribuzione offline di un cluster SQL Server Big Data

Questo articolo descrive come eseguire una distribuzione offline di un cluster SQL Server 2019 Big Data (anteprima). I cluster di Big data devono avere accesso a un repository Docker da cui estrarre le immagini del contenitore. Un'installazione offline è una posizione in cui le immagini obbligatorie vengono inserite in un repository Docker privato. Il repository privato viene quindi utilizzato come origine dell'immagine per una nuova distribuzione.

## <a name="prerequisites"></a>Prerequisiti

- Motore Docker 1.8 o versione successiva in qualsiasi distribuzione di Linux supportata oppure Docker per Mac/Windows. Per altre informazioni, vedere [Installare Docker](https://docs.docker.com/engine/installation/).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Caricare immagini in un repository privato

I passaggi seguenti descrivono come eseguire il pull delle immagini del contenitore del cluster Big Data dal repository Microsoft e quindi eseguirne il push nel repository privato.

> [!TIP]
> I passaggi seguenti illustrano il processo. Tuttavia, per semplificare l'attività, è possibile usare lo [script automatizzato](#automated) anziché eseguire manualmente questi comandi.

1. Estrarre le immagini del contenitore del cluster Big Data ripetendo il comando seguente. Sostituire `<SOURCE_IMAGE_NAME>` con ogni [nome di immagine](#images). Sostituire `<SOURCE_DOCKER_TAG>` con il tag per la versione del cluster Big data, ad esempio **2019-CTP 3.2-Ubuntu**.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Accedere al registro Docker privato di destinazione.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Contrassegnare le immagini locali con il comando seguente per ogni immagine:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Eseguire il push delle immagini locali nel repository Docker privato:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a>Immagini del contenitore cluster di Big Data

Per un'installazione offline sono necessarie le seguenti Big Data immagini del contenitore cluster:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**
 - **mssql-mleap-serving-runtime**
 - **MSSQL-supporto per la sicurezza**

## <a id="automated"></a>Script automatizzato

È possibile usare uno script Python automatizzato che effettuerà automaticamente il pull di tutte le immagini del contenitore necessarie e ne effettuerà il push in un repository privato.

> [!NOTE]
> Python è un prerequisito per l'uso dello script. Per altre informazioni su come installare Python, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Da bash o PowerShell scaricare lo script con **curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. Eseguire quindi lo script con uno dei comandi seguenti:

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Seguire le istruzioni per immettere il repository Microsoft e le informazioni sul repository privato. Al termine dello script, tutte le immagini obbligatorie dovrebbero trovarsi nel repository privato.

## <a name="install-tools-offline"></a>Installare gli strumenti offline

Le distribuzioni di cluster di Big data richiedono diversi strumenti, tra cui **Python**, **azdata**e **kubectl**. Usare la procedura seguente per installare questi strumenti in un server offline.

### <a id="python"></a>Installare Python offline

1. In un computer con accesso a Internet, scaricare uno dei file compressi seguenti contenenti Python:

   | Sistema operativo | Scarica |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copiare il file compresso nel computer di destinazione ed estrarlo in una cartella di propria scelta.

1. Solo per Windows, eseguire `installLocalPythonPackages.bat` da tale cartella e passare il percorso completo della stessa cartella come parametro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a>Installare azdata offline

1. In un computer con accesso a Internet e [Python](https://wiki.python.org/moin/BeginnersGuide/Download)eseguire il comando seguente per scaricare tutti i pacchetti **azdata** nella cartella corrente.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. Copiare i pacchetti scaricati e il file **requirements. txt** nel computer di destinazione.

1. Eseguire il comando seguente nel computer di destinazione, specificando la cartella in cui sono stati copiati i file precedenti.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a>Installare kubectl offline

Per installare **kubectl** in un computer offline, seguire questa procedura.

1. Usare **curl** per scaricare **kubectl** in una cartella di propria scelta. Per altre informazioni, vedere [Install kubectl Binary using curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).

1. Copiare la cartella nel computer di destinazione.

## <a name="deploy-from-private-repository"></a>Distribuisci da repository privato

Per eseguire la distribuzione dal repository privato, attenersi alla procedura descritta nella [Guida alla distribuzione](deployment-guidance.md), ma usare un file di configurazione della distribuzione personalizzato che specifichi le informazioni del repository Docker privato. I comandi **azdata** seguenti illustrano come modificare le impostazioni di Docker in un file di configurazione della distribuzione personalizzato denominato **Control. JSON**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

La distribuzione richiede il nome utente e la password Docker oppure è possibile specificarli nelle variabili di ambiente **DOCKER_USERNAME** e **DOCKER_PASSWORD** .

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulle distribuzioni Big Data cluster, vedere [How to deploy SQL Server Big Data Clusters on Kubernetes](deployment-guidance.md).
