---
title: Distribuire in modalità offline
titleSuffix: SQL Server big data clusters
description: Informazioni su come eseguire una distribuzione non in linea di un cluster di big data di SQL Server.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 49c96300792adfefa32152ec73911ba32fac47ee
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994012"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>Eseguire una distribuzione non in linea di un cluster di big data di SQL Server

Questo articolo descrive come eseguire una distribuzione non in linea di un cluster di big data di SQL Server 2019 (anteprima). I cluster di big data necessari affinché l'accesso a un repository di Docker da cui pull delle immagini del contenitore. Un'installazione offline è uno in cui le immagini necessarie vengono inserite in un repository di Docker privato. Tale repository privato viene quindi utilizzato come origine dell'immagine di una nuova distribuzione.

## <a name="prerequisites"></a>Prerequisiti

- Motore Docker 1.8 o versione successiva in qualsiasi distribuzione di Linux supportata oppure Docker per Mac/Windows. Per altre informazioni, vedere [Installare Docker](https://docs.docker.com/engine/installation/).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>Caricare immagini in un repository privato

I passaggi seguenti descrivono come il cluster di big data il pull delle immagini del contenitore dal repository Microsoft e quindi eseguirne il push nel repository privato.

> [!TIP]
> I passaggi seguenti illustrano il processo. Tuttavia, per semplificare l'attività, è possibile usare la [script automatico](#automated) invece di eseguire manualmente questi comandi.

1. In primo luogo, accedere al Registro di sistema Microsoft Docker con il **accesso a docker** comando. Usare il nome utente e password che Microsoft fornito come parte del programma di adozione anticipata.

   ```PowerShell
   docker login private-repo.microsoft.com -u  <SOURCE_DOCKER_USERNAME> -p <SOURCE_DOCKER_PASSWORD>
   ```

   > [!TIP]
   > Questi comandi usano PowerShell ad esempio, ma è possibile eseguirli da cmd, bash o da qualunque shell dei comandi eseguibili docker. In Linux, aggiungere `sudo` per ogni comando.

1. Eseguire il pull di cluster di big data le immagini del contenitore, ripetere il comando seguente. Sostituire `<SOURCE_IMAGE_NAME>` con ogni [nome immagine](#images). Sostituire `<SOURCE_DOCKER_TAG>` con il tag per i big data cluster versione, ad esempio **ctp3.0**.  

   ```PowerShell
   docker pull private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. Accedere alla destinazione privato registro Docker.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. Contrassegnare le immagini locali con il comando seguente per ogni immagine:

   ```PowerShell
   docker tag private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. Effettuare il push di immagini locale al repository Docker privato:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> Immagini dei contenitori del cluster dei big Data

Le seguenti immagini del contenitore del cluster dei big data sono necessarie per un'installazione offline:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-java**
 - **mssql-mlservices-pythonserver**
 - **mssql-mlservices-rserver**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-portal**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**

## <a id="automated"></a> Script automatizzato

È possibile usare uno script automatizzato python che verrà automaticamente pull di tutte le immagini del contenitore necessarie ed eseguirne il push in un repository privato.

> [!NOTE]
> Python è un prerequisito per l'uso dello script. Per altre informazioni su come installare Python, vedere la [documentazione di Python](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Tramite bash o PowerShell, scaricare lo script con **curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. Quindi eseguire lo script con uno dei seguenti comandi:

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Seguire le istruzioni per l'immissione nel repository di Microsoft e le informazioni del repository privato. Al termine dell'esecuzione dello script, tutte le necessarie immagini devono trovarsi nel tuo repository privato.

## <a name="install-tools-offline"></a>Installare gli strumenti non in linea

Le distribuzioni cluster di big data richiedono vari strumenti, tra cui **Python**, **mssqlctl**, e **kubectl**. Usare la procedura seguente per installare questi strumenti in un server offline.

### <a id="python"></a> Installare python in modalità offline

1. In un computer con accesso a internet, scaricare uno dei seguenti file compressi contenente Python:

   | Sistema operativo | Scarica |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copiare il file compresso nel computer di destinazione ed estrarre i file in una cartella di propria scelta.

1. Per Windows in esecuzione, solo `installLocalPythonPackages.bat` da tale cartella e passare il percorso completo nella stessa cartella come parametro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="mssqlctl"></a> Installare mssqlctl offline

1. In un computer con accesso a internet e [Python](https://wiki.python.org/moin/BeginnersGuide/Download), eseguire il comando seguente per scaricare tutti disattivare il **mssqlctl** pacchetti nella cartella corrente.

   ```PowerShell
   pip download -r https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

1. Scaricare il **Requirements. txt** file.

   ```PowerShell
   curl -o requirements.txt "https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt"
   ```

1. Copiare i pacchetti scaricati e le **Requirements. txt** file nel computer di destinazione.

1. Eseguire il comando seguente nel computer di destinazione, specificando la cartella che è stato copiato i file precedenti in.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> Installare kubectl offline

Per installare **kubectl** a un computer offline, usare la procedura seguente.

1. Uso **curl** per scaricare **kubectl** in una cartella di propria scelta. Per altre informazioni, vedere [installare kubectl binario usando curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).

1. Copiare la cartella nel computer di destinazione.

## <a name="deploy-from-private-repository"></a>Distribuire da repository privato

Per distribuire dal repository privato, usare la procedura descritta nel [Guida alla distribuzione](deployment-guidance.md), ma usare un file di configurazione di distribuzione personalizzato che specifica le informazioni del repository Docker private. Quanto segue **mssqlctl** comandi illustrano come modificare le impostazioni di Docker in un file di configurazione di distribuzione personalizzato denominato **custom.json**:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.repository=<your-docker-repository>"
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.registry=<your-docker-registry>"
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.imageTag=<your-docker-image-tag>"
```

La distribuzione richiede il nome utente di docker e la password, oppure è possibile specificarli nel **DOCKER_USERNAME** e **DOCKER_PASSWORD** le variabili di ambiente.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle distribuzioni di cluster di big data, vedere [come distribuire i dati di grandi dimensioni di SQL Server di cluster in Kubernetes](deployment-guidance.md).
