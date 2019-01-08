---
title: Guida introduttiva alla distribuzione
titleSuffix: SQL Server 2019 big data clusters
description: Procedura dettagliata di una distribuzione di cluster di big data 2019 Server SQL (anteprima) in Azure Kubernetes Service (AKS).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: quickstart
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: f5ddd80eaf29db657c42eec5c84c8485e8b0d8b6
ms.sourcegitcommit: 85fd3e1751de97a16399575397ab72ebd977c8e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/17/2018
ms.locfileid: "53531156"
---
# <a name="quickstart-deploy-sql-server-big-data-cluster-on-azure-kubernetes-service-aks"></a>Guida introduttiva: Distribuire il cluster di big data di SQL Server in Azure Kubernetes Service (AKS)

In questa Guida introduttiva si distribuirà un cluster di big data di SQL Server 2019 (anteprima) nel servizio contenitore di AZURE in una configurazione predefinita adatta per gli ambienti di sviluppo/test.

> [!NOTE]
> Servizio contenitore di AZURE è semplicemente un'unica posizione per host Kubernetes. I cluster di big data possono essere distribuiti in Kubernetes indipendentemente dall'infrastruttura sottostante. Per altre informazioni, vedere [come distribuire i dati di grandi dimensioni di SQL Server di cluster in Kubernetes](deployment-guidance.md).

Oltre a un'istanza di SQL Master, il cluster include due istanze del pool di archiviazione, un'istanza del pool di dati e calcolo di un'istanza del pool. I dati viene mantenuti usando volumi permanenti Kubernetes che usano le classi di archiviazione predefinito AKS. Per personalizzare ulteriormente la configurazione, vedere le variabili di ambiente nel [Guida alla distribuzione](deployment-guidance.md).

Se si preferisce eseguire uno script per creare il cluster AKS e installare un cluster di big data nello stesso momento, vedere [distribuire un cluster di big data in Azure Kubernetes Service (AKS) di SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="prerequisites"></a>Prerequisiti

Questa Guida introduttiva richiede che sia già stato configurato un cluster AKS con una versione minima versione 1.10. Per altre informazioni, vedere la [distribuire nel servizio contenitore di AZURE](deploy-on-aks.md) Guida.

- [Strumenti di big data di SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Estensione di SQL Server 2019**
   - **Kubectl**
   - **mssqlctl**

## <a name="verify-aks-configuration"></a>Verificare la configurazione di servizio contenitore di AZURE

Dopo aver creato il cluster AKS distribuita, è possibile eseguire il seguente comando di kubectl per visualizzare la configurazione del cluster. Verificare che tale kubectl fa riferimento il contesto del cluster corretto.

```bash
kubectl config view
```

## <a name="define-environment-variables"></a>Definire le variabili di ambiente

Impostare le variabili di ambiente necessarie per la distribuzione di cluster di big data leggermente diverso a seconda se si usano client Windows o Linux/macOS.  Scegliere i passaggi seguenti a seconda del sistema operativo in uso.

Prima di continuare, tenere presenti le linee guida seguenti:

- Nel [finestra di comando](https://docs.microsoft.com/visualstudio/ide/reference/command-window), sono incluse le virgolette nelle variabili di ambiente. Se si usano le virgolette per eseguire il wrapping di una password, le virgolette sono inclusi nella password.
- In bash le virgolette non sono inclusi nella variabile. Gli esempi usino le virgolette doppie `"`.
- È possibile impostare le variabili di ambiente della password con qualsiasi nome desiderato, ma assicurarsi che questi sono sufficientemente complessi e non usare la `!`, `&`, o `'` caratteri.
- Il `sa` account sia un amministratore di sistema nell'istanza Master di SQL Server che viene creato durante l'installazione. Dopo aver creato il contenitore SQL Server, la variabile di ambiente `MSSQL_SA_PASSWORD` specificata diventa individuabile eseguendo `echo $MSSQL_SA_PASSWORD` nel contenitore. Per motivi di sicurezza, modificare il `sa` password in base alle procedure consigliate documentate [qui](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker?view=sql-server-2017#change-the-sa-password).

Inizializzare le variabili di ambiente seguenti.  Sono necessari per distribuire un cluster di big data:

### <a name="windows"></a>WINDOWS

Utilizzando una finestra di comando (non PowerShell), configurare le variabili di ambiente seguenti:

```cmd
SET ACCEPT_EULA=Y
SET CLUSTER_PLATFORM=aks

SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

SET DOCKER_REGISTRY=private-repo.microsoft.com
SET DOCKER_REPOSITORY=mssql-private-preview
SET DOCKER_USERNAME=<your username, credentials provided by Microsoft>
SET DOCKER_PASSWORD=<your password, credentials provided by Microsoft>
SET DOCKER_EMAIL=<your Docker email, use the username provided by Microsoft>
SET DOCKER_PRIVATE_REGISTRY="1"
```

### <a name="linuxmacos"></a>Linux/macOS

Inizializzare le variabili di ambiente seguenti:

```bash
export ACCEPT_EULA="Y"
export CLUSTER_PLATFORM="aks"

export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

export DOCKER_REGISTRY="private-repo.microsoft.com"
export DOCKER_REPOSITORY="mssql-private-preview"
export DOCKER_USERNAME="<your username, credentials provided by Microsoft>"
export DOCKER_PASSWORD="<your password, credentials provided by Microsoft>"
export DOCKER_EMAIL="<your Docker email, use the username provided by Microsoft>"
export DOCKER_PRIVATE_REGISTRY="1"
```

> [!NOTE]
> Durante l'anteprima pubblica limitata, le credenziali di Docker per scaricare le immagini del cluster di SQL Server i big data vengono fornite a ogni cliente da Microsoft. Per richiedere l'accesso, registrare [qui](https://aka.ms/eapsignup)e specificare l'interesse dimostrato per provare i cluster di big data di SQL Server.

## <a name="deploy-a-big-data-cluster"></a>Distribuire un cluster di big data

Per distribuire un cluster di big data 2019 CTP 2.2 di SQL Server nel cluster Kubernetes, eseguire il comando seguente:

```bash
mssqlctl create cluster <your-cluster-name>
```

> [!NOTE]
> Il nome del cluster deve essere solo alfanumerici caratteri minuscoli, senza spazi. Tutti gli artefatti di Kubernetes per il cluster di big data verranno creati in uno spazio dei nomi con lo stesso nome del cluster il nome specificato.

La finestra di comando o nella shell restituisce lo stato della distribuzione. È anche possibile controllare lo stato della distribuzione eseguendo questi comandi in una finestra di comando diverse:

```bash
kubectl get all -n <your-cluster-name>
kubectl get pods -n <your-cluster-name>
kubectl get svc -n <your-cluster-name>
```

È possibile visualizzare un stato e la configurazione per ogni pod più granulari eseguendo:
```bash
kubectl describe pod <pod name> -n <your-cluster-name>
```

> [!TIP]
> Per altre informazioni su come monitorare e risolvere i problemi di una distribuzione, vedere la [risoluzione dei problemi di distribuzione](deployment-guidance.md#troubleshoot) sezione dell'articolo di istruzioni di distribuzione.

## <a name="open-the-cluster-administration-portal"></a>Aprire il portale di amministrazione del Cluster

Il pod Controller è in esecuzione, è possibile utilizzare il portale di amministrazione Cluster per monitorare la distribuzione. È possibile accedere al portale con l'esterno indirizzo IP e porta numero per il `service-proxy-lb` (ad esempio: **https://\<ip-address\>: 30777/portale**). Le credenziali per accedere al portale di amministrazione sono i valori delle `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD` variabili di ambiente fornite sopra.

È possibile ottenere l'indirizzo IP del servizio servizio-proxy-lb eseguendo questo comando in una finestra bash o cmd:

```bash
kubectl get svc service-proxy-lb -n <your-cluster-name>
```

> [!NOTE]
> Si verrà visualizzato un avviso di sicurezza all'accesso alla pagina web poiché si sta usando i certificati SSL generati automaticamente. Nelle future versioni, Microsoft fornirà la possibilità di fornire i propri certificati firmati.

## <a name="connect-to-the-big-data-cluster"></a>Connettersi al cluster di big data

Dopo che lo script di distribuzione è stata completata, è possibile ottenere l'indirizzo IP dell'istanza master di SQL Server e i punti finali Spark o HDFS usando i passaggi descritti di seguito. Tutti gli endpoint del cluster vengono visualizzati nella sezione nel portale di amministrazione Cluster anche per semplificarne la consultazione all'endpoint del servizio.

Azure offre il servizio di bilanciamento del carico di Azure al servizio contenitore di AZURE. Eseguire il seguente comando in una finestra di comando o la finestra di bash:

```bash
kubectl get svc endpoint-master-pool -n <your-cluster-name>
kubectl get svc service-security-lb -n <your-cluster-name>
```

Cercare il **External-IP** valore assegnato ai servizi. Connettersi all'istanza master di SQL Server usando l'indirizzo IP per il `endpoint-master-pool` alla porta 31433 (es:  **\<ip-address\>, 31433**) e per l'endpoint del cluster SQL Server i big data usando l'indirizzo IP esterno per il `service-security-lb` servizio.   Che i big data cluster punto finale è che consente di interagire con HDFS e inviare processi Spark tramite Knox.

## <a name="next-steps"></a>Passaggi successivi

Ora che viene distribuito il cluster di big data di SQL Server, provare alcune delle nuove funzionalità:

> [!div class="nextstepaction"]
> [Come usare i notebook in fase di anteprima di SQL Server 2019](notebooks-guidance.md)
