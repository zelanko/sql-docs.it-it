---
title: Distribuire applicazioni con azdata
titleSuffix: SQL Server big data clusters
description: Distribuire uno script Python o R come applicazione in SQL Server 2019 Big Data cluster (anteprima).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 06b76e7eb8eec8db1993ca558a1f57355457c4ad
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419489"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>Come distribuire un'app in un cluster SQL Server Big Data (anteprima)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come distribuire e gestire lo script R e Python come applicazione all'interno di un cluster SQL Server 2019 Big Data (anteprima).

## <a name="whats-new-and-improved"></a>Novità e miglioramenti

- Una singola utilità della riga di comando per la gestione di cluster e app.
- Semplifica la distribuzione delle app offrendo un controllo granulare tramite file di specifiche.
- Supporto per l'hosting di tipi di applicazione aggiuntivi-SSIS e MLeap (novità di CTP 2,3)
- [Estensione vs code](app-deployment-extension.md) per gestire la distribuzione delle applicazioni

Le applicazioni vengono distribuite e `azdata` gestite mediante l'utilità della riga di comando. Questo articolo fornisce esempi su come distribuire le app dalla riga di comando. Per informazioni su come usarlo in Visual Studio Code fare riferimento a [vs code estensione](app-deployment-extension.md).

Sono supportati i tipi di app seguenti:
- App R e Python (funzioni, modelli e app)
- Servizio MLeap
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Prerequisiti

- [SQL Server 2019 Big Data cluster](deployment-guidance.md)
- [utilità della riga di comando azdata](deploy-install-azdata.md)

## <a name="capabilities"></a>Funzionalità

In SQL Server 2019 (anteprima) è possibile creare, eliminare, descrivere, inizializzare, elencare l'esecuzione e aggiornare l'applicazione. La tabella seguente descrive i comandi di distribuzione dell'applicazione che è possibile usare con **azdata**.

|Comando |Descrizione |
|:---|:---|
|`azdata login` | Accedere a un cluster SQL Server Big Data |
|`azdata app create` | Creare un'applicazione. |
|`azdata app delete` | Eliminare l'applicazione. |
|`azdata app describe` | Descrivere l'applicazione. |
|`azdata app init` | Avvia la nuova ossatura dell'applicazione. |
|`azdata app list` | Elencare le applicazioni. |
|`azdata app run` | Eseguire l'applicazione. |
|`azdata app update`| Aggiornare l'applicazione. |

È possibile ottenere informazioni sul `--help` parametro, come nell'esempio seguente:

```bash
azdata app create --help
```

Le sezioni seguenti descrivono questi comandi in modo più dettagliato.

## <a name="sign-in"></a>Accesso

Prima di distribuire o interagire con le applicazioni, accedere prima al cluster SQL Server Big data con il `azdata login` comando. Specificare l'indirizzo IP esterno del `controller-svc-external` servizio (ad `https://ip-address:30080`esempio,) insieme al nome utente e alla password del cluster.

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

Se si usa AKS, è necessario eseguire il comando seguente per ottenere l'indirizzo IP del `mgmtproxy-svc-external` servizio eseguendo questo comando in una finestra bash o cmd:


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm o Minikube

Se si usa Kubeadm o Minikube, eseguire il comando seguente per ottenere l'indirizzo IP per accedere al cluster

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Creare un'app

Per creare un'applicazione, usare `azdata` con il `app create` comando. Questi file risiedono localmente nel computer da cui si sta creando l'app.

Usare la sintassi seguente per creare una nuova app in Big Data cluster:

```bash
azdata app create --spec <directory containing spec file>
```

Il comando seguente mostra un esempio di come potrebbe apparire questo comando:

```bash
azdata app create --spec ./addpy
```

Si presuppone che l'applicazione sia archiviata nella `addpy` cartella. Questa cartella deve inoltre contenere un file di specifica per l'applicazione, `spec.yaml`denominato. Per ulteriori informazioni sul `spec.yaml` file, vedere [la pagina](concept-application-deployment.md) relativa alla distribuzione di applicazioni.

Per distribuire l'app di esempio app, creare i file seguenti in una directory `addpy`denominata:

- `add.py` (Indici per tabelle con ottimizzazione per la memoria). Copiare il codice Python seguente in questo file:
   ```py
   #add.py
   def add(x,y):
        result = x+y
        return result
    result=add(x,y)
   ```
- `spec.yaml` (Indici per tabelle con ottimizzazione per la memoria). Copiare il codice seguente nel file:
   ```yaml
   #spec.yaml
   name: add-app #name of your python script
   version: v1  #version of the app
   runtime: Python #the language this app uses (R or Python)
   src: ./add.py #full path to the location of the app
   entrypoint: add #the function that will be called upon execution
   replicas: 1  #number of replicas needed
   poolsize: 1  #the pool size that you need your app to scale
   inputs:  #input parameters that the app expects and the type
     x: int
     y: int
   output: #output parameter the app expects and the type
     result: int
   ```

Eseguire quindi il comando seguente:

```bash
azdata app create --spec ./addpy
```

È possibile verificare se l'app viene distribuita usando il comando list:

```bash
azdata app list
```

Se la distribuzione non è completa `state` `WaitingforCreate` , verrà visualizzato il seguente esempio:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Una volta completata la distribuzione, verrà visualizzata la `state` `Ready` modifica dello stato:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>Elencare un'app

È possibile elencare tutte le app create correttamente con il `app list` comando.

Il comando seguente elenca tutte le applicazioni disponibili nel cluster Big Data:

```bash
azdata app list
```

Se si specifica un nome e una versione, vengono elencate l'app specifica e il relativo stato (creazione o preparazione):

```bash
azdata app list --name <app_name> --version <app_version>
```

Nell'esempio seguente viene illustrato questo comando:

```bash
azdata app list --name add-app --version v1
```

Verrà visualizzato un output simile all'esempio seguente:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>Eseguire un'app

Se l'app è in uno `Ready` stato, è possibile usarla eseguendola con i parametri di input specificati. Per eseguire un'app, usare la sintassi seguente:

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

Il comando di esempio seguente illustra il comando Run:

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

Se l'esecuzione ha avuto esito positivo, l'output dovrebbe essere visualizzato come specificato al momento della creazione dell'app. Di seguito è riportato un esempio.

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="create-an-app-skeleton"></a>Creare uno scheletro di app

Il comando init fornisce un patibolo con gli elementi rilevanti necessari per la distribuzione di un'app. Nell'esempio seguente viene creato Hello a tale scopo, eseguendo il comando seguente.

```bash
azdata app init --name hello --version v1 --template python
```

Verrà creata una cartella denominata Hello.  È possibile `cd` accedere alla directory ed esaminare i file generati nella cartella. spec. YAML definisce l'app, ad esempio il nome, la versione e il codice sorgente. È possibile modificare le specifiche per modificare nome, versione, input e output.

Di seguito è riportato un esempio di output del comando init che verrà visualizzato nella cartella

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>Descrivere un'app

Il comando Descrivi fornisce informazioni dettagliate sull'app, incluso l'endpoint nel cluster. Questa operazione viene in genere usata da uno sviluppatore di app per compilare un'app usando il client di spavalderia e usando il servizio Web per interagire con l'app in modo RESTful. Per ulteriori informazioni, vedere [utilizzo di applicazioni in cluster Big Data](big-data-cluster-consume-apps.md) .

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30777/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30777/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>Eliminare un'app

Per eliminare un'app dal cluster Big Data, usare la sintassi seguente:

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere come integrare le app distribuite in SQL Server cluster Big Data nelle proprie [Big Data](big-data-cluster-consume-apps.md) applicazioni. È anche possibile vedere esempi aggiuntivi in [esempi di distribuzione di app](https://aka.ms/sql-app-deploy).

Per ulteriori informazioni sui cluster SQL Server Big Data, vedere [che cosa sono SQL Server 2019 cluster Big Data?](big-data-cluster-overview.md).
