---
title: Eseguire la distribuzione offline
titleSuffix: SQL Server big data clusters
description: Informazioni su come eseguire una distribuzione offline di un cluster Big Data di SQL Server.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd8b3128fc11037a5ade494813611d473c995f8f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419373"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Eseguire una distribuzione offline di un cluster Big Data di SQL Server

Questo articolo descrive come eseguire una distribuzione offline di un cluster Big Data di SQL Server 2019 (anteprima). I cluster Big Data devono avere accesso a un repository Docker da cui eseguire il pull delle immagini dei contenitori. In un'installazione offline le immagini richieste vengono inserite in un repository Docker privato. Il repository privato viene quindi usato come origine delle immagini per una nuova distribuzione.

## <a name="prerequisites"></a>Prerequisites

- Motore Docker 1.8 o versione successiva in qualsiasi distribuzione di Linux supportata oppure Docker per Mac/Windows. Per altre informazioni, vedere [Installare Docker](https://docs.docker.com/engine/installation/).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Caricare le immagini in un repository privato

I passaggi seguenti descrivono come eseguire il pull delle immagini dei contenitori dei cluster Big Data dal repository Microsoft e quindi eseguirne il push nel repository privato.

> [!TIP]
> I passaggi seguenti descrivono il processo. Per semplificare l'attività, tuttavia, è possibile usare lo [script automatico](#automated) invece di eseguire manualmente questi comandi.

1. Eseguire il pull delle immagini dei contenitori dei cluster Big Data ripetendo il comando seguente. Sostituire `<SOURCE_IMAGE_NAME>` con ogni [nome di immagine](#images). Sostituire `<SOURCE_DOCKER_TAG>` con il tag per la versione del cluster Big Data, ad esempio **2019-CTP3.2-ubuntu**.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Accedere al registro Docker privato di destinazione.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Aggiungere un tag alle immagini locali con il comando seguente per ogni immagine:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Eseguire il push delle immagini locali nel repository Docker privato:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> Immagini dei contenitori dei cluster Big Data

Per un'installazione offline, sono necessarie le immagini dei contenitori dei cluster Big Data seguenti:

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
 - **mssql-security-support**

## <a id="automated"></a> Script automatico

È possibile usare uno script Python automatico che effettua automaticamente il pull di tutte le immagini dei contenitori necessarie e il push in un repository privato.

> [!NOTE]
> Python è un prerequisito per l'uso dello script. Per altre informazioni su come installare Python, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Dalla shell Bash o da PowerShell scaricare lo script con **curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. Eseguire quindi lo script con uno dei comandi seguenti:

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Seguire le istruzioni per immettere le informazioni sul repository Microsoft e sul repository privato. Al completamento dello script, tutte le immagini richieste dovrebbero trovarsi nel repository privato.

## <a name="install-tools-offline"></a>Installare gli strumenti offline

Le distribuzioni di cluster Big Data richiedono diversi strumenti, tra cui **Python**, **azdata** e **kubectl**. Usare le procedure seguenti per installare questi strumenti in un server offline.

### <a id="python"></a> Installare Python offline

1. In un computer con accesso a Internet, scaricare uno dei file compressi seguenti contenenti Python:

   | Sistema operativo | Scarica |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copiare il file compresso nel computer di destinazione ed estrarlo nella cartella desiderata.

1. Solo per Windows, eseguire `installLocalPythonPackages.bat` dalla cartella di installazione e passare il percorso completo della cartella come parametro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a> Installare azdata offline

1. In un computer con accesso a Internet e con [Python](https://wiki.python.org/moin/BeginnersGuide/Download) eseguire il comando seguente per scaricare tutti i pacchetti di **azdata** nella cartella corrente.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. Copiare i pacchetti scaricati e il file **requirements.txt** nel computer di destinazione.

1. Eseguire il comando seguente nel computer di destinazione, specificando la cartella in cui sono stati copiati i file in precedenza.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> Installare kubectl offline

Per installare **kubectl** in un computer offline, seguire questa procedura.

1. Usare **curl** per scaricare **kubectl** nella cartella desiderata. Per altre informazioni, vedere [Installare i file binari di kubectl usando curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).

1. Copiare la cartella nel computer di destinazione.

## <a name="deploy-from-private-repository"></a>Eseguire la distribuzione dal repository privato

Per eseguire la distribuzione dal repository privato, seguire la procedura descritta nella [guida alla distribuzione](deployment-guidance.md), ma usare un file di configurazione della distribuzione personalizzato che specifichi le informazioni sul repository Docker privato. I comandi **azdata** seguenti illustrano come modificare le impostazioni di Docker in un file di configurazione della distribuzione personalizzato denominato **control.json**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

La distribuzione richiede il nome utente e la password Docker oppure è possibile specificarli nelle variabili di ambiente **DOCKER_USERNAME** e **DOCKER_PASSWORD**.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle distribuzioni di cluster Big Data, vedere [Come distribuire cluster Big Data di SQL Server in Kubernetes](deployment-guidance.md).
