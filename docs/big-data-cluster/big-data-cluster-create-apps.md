---
title: Distribuire le applicazioni usando mssqlctl
titleSuffix: SQL Server big data clusters
description: Distribuire uno script Python o R come un'applicazione nel cluster di big data 2019 Server SQL (anteprima).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: d7a61c97d3e1636cd6a11173e281c192d1533d93
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388747"
---
# <a name="how-to-deploy-an-app-on-sql-server-big-data-cluster-preview"></a>Come distribuire un'app nel cluster di big data di SQL Server (anteprima)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come distribuire e gestire lo script R e Python come un'applicazione all'interno di un cluster di big data di SQL Server 2019 (anteprima).

## <a name="whats-new-and-improved"></a>Che cos'è nuovo e migliorato

- Un'unica utilità della riga di comando per la gestione di cluster e l'app.
- Distribuzione dell'app semplificata, fornendo un controllo granulare tramite file di specifiche.
- Supporta l'hosting di tipi di applicazione aggiuntivi - SSIS e MLeap (novità di CTP 2.3)
- [Estensione di Visual Studio Code](app-deployment-extension.md) per gestire la distribuzione di applicazioni

Le applicazioni vengono distribuite e gestite usando `mssqlctl` utilità della riga di comando. Questo articolo fornisce esempi su come distribuire le app dalla riga di comando. Per informazioni su come usare in Visual Studio Code, vedere [estensione di Visual Studio Code](app-deployment-extension.md).

Sono supportati i tipi di App seguenti:
- App di R e Python (funzioni, i modelli e App)
- MLeap Serving
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Prerequisiti

- [Cluster di big data di SQL Server 2019](deployment-guidance.md)
- [utilità della riga di comando mssqlctl](deploy-install-mssqlctl.md)

## <a name="capabilities"></a>Capabilities

In SQL Server 2019 (anteprima) è possibile creare, eliminare, descrivere, inizializzare, elenco eseguire e aggiornare l'applicazione. La tabella seguente descrive i comandi di distribuzione dell'applicazione che è possibile usare con **mssqlctl**.

|Comando |Descrizione |
|:---|:---|
|`mssqlctl login` | Accedere a un cluster di big data di SQL Server |
|`mssqlctl app create` | Creare l'applicazione. |
|`mssqlctl app delete` | Eliminare l'applicazione. |
|`mssqlctl app describe` | Descrivere l'applicazione. |
|`mssqlctl app init` | Kickstart nuova struttura dell'applicazione. |
|`mssqlctl app list` | Elencare le applicazioni. |
|`mssqlctl app run` | Esegui l'applicazione. |
|`mssqlctl app update`| Aggiornare l'applicazione. |

È possibile ottenere assistenza con la `--help` parametro come nell'esempio seguente:

```bash
mssqlctl app create --help
```

Le sezioni seguenti descrivono questi comandi in modo più dettagliato.

## <a name="sign-in"></a>Accedi

Prima di distribuire o interagire con le applicazioni, accedere prima all'istanza di SQL Server del cluster di big data con il `mssqlctl login` comando. Specificare l'indirizzo IP esterno del `controller-svc-external` servizio (ad esempio: `https://ip-address:30080`) con il nome utente e la password per il cluster.

```bash
mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

Se si usa servizio contenitore di AZURE, è necessario eseguire il comando seguente per ottenere l'indirizzo IP del `mgmtproxy-svc-external` servizio eseguendo questo comando in una finestra bash o cmd:


```bash
kubectl get svc mgmtproxy-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm oppure Minikube

Se si usa Kubeadm oppure Minikube eseguire il comando seguente per ottenere l'indirizzo IP per l'accesso al cluster

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Creare un'app

Per creare un'applicazione, usare `mssqlctl` con il `app create` comando. Questi file si trovano in locale nel computer che si sta creando l'app.

Usare la sintassi seguente per creare una nuova app nel cluster di big data:

```bash
mssqlctl app create --spec <directory containing spec file>
```

Il comando seguente illustra un esempio di ciò che potrebbe essere simile questo comando:

```bash
mssqlctl app create --spec ./addpy
```

Ciò presuppone che si disponga dell'applicazione archiviato nel `addpy` cartella. Questa cartella deve contenere anche un file della specifica per l'applicazione, denominata chiamato `spec.yaml`. Vedi [la pagina distribuzione delle applicazioni](concept-application-deployment.md) per altre informazioni sul `spec.yaml` file.

Per distribuire questa app di esempio di app, creare i seguenti file in una directory denominata `addpy`:

- `add.py` (Indici per tabelle con ottimizzazione per la memoria). Copiare il seguente codice Python in questo file:
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

Quindi, eseguire il comando seguente:

```bash
mssqlctl app create --spec ./addpy
```

È possibile controllare se l'app viene distribuita usando il comando di elenco:

```bash
mssqlctl app list
```

Se la distribuzione non è stata completata dovrebbe essere il `state` mostrare `WaitingforCreate` come illustrato nell'esempio seguente:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Dopo la distribuzione ha esito positivo, viene visualizzato il `state` passare alla `Ready` stato:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>Pubblica un'app

È possibile elencare tutte le app che sono state create correttamente con il `app list` comando.

Il seguente comando Elenca tutte le applicazioni disponibili nel cluster di big data:

```bash
mssqlctl app list
```

Se si specifica un nome e la versione, elenca app specifici e il relativo stato (creazione in corso o pronta):

```bash
mssqlctl app list --name <app_name> --version <app_version>
```

L'esempio seguente illustra questo comando:

```bash
mssqlctl app list --name add-app --version v1
```

Si dovrebbe visualizzato un output simile all'esempio seguente:

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

Se l'app si trova in un `Ready` lo stato, è possibile usarlo eseguendolo con i parametri di input specificati. Usare la sintassi seguente per eseguire un'app:

```bash
mssqlctl app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

Il comando seguente viene illustrato il comando di esecuzione:

```bash
mssqlctl app run --name add-app --version v1 --inputs x=1,y=2
```

Se l'esecuzione ha avuto esito positivo, si verrà visualizzato l'output come specificato durante la creazione dell'app. Di seguito è riportato un esempio.

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

## <a name="create-an-app-skeleton"></a>Creare una struttura dell'app

Il comando init fornisce uno scaffold con gli elementi pertinenti che è necessario per la distribuzione di un'app. L'esempio seguente crea hello è possibile farlo eseguendo il comando seguente.

```bash
mssqlctl app init --name hello --version v1 --template python
```

Si creerà una cartella denominata hello.  È possibile `cd` nella directory ed esaminare i file generati nella cartella. Spec.yaml definisce l'app, ad esempio nome, versione e il codice sorgente. È possibile modificare la specifica per modificare nome, versione, input e output.

Di seguito è riportato l'output del comando init che verrà visualizzato nella cartella

```
hello.py
README.md
run-spec.yaml
spec.yaml

```

## <a name="describe-an-app"></a>Descrivere un'app

Il comando descrizione fornisce informazioni dettagliate sull'app tra cui il punto finale nel cluster. Ciò in genere viene usato da uno sviluppatore di app per compilare un'app usando il client di swagger e usando il servizio Web per interagire con l'app in modalità RESTful. Visualizzare [utilizzo di applicazioni nei cluster di big data](big-data-cluster-consume-apps.md) per altre informazioni.

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

Per eliminare un'app dal cluster i big data, usare la sintassi seguente:

```bash
mssqlctl app delete --name add-app --version v1
```

## <a name="next-steps"></a>Passaggi successivi

Scopri come integrare le app distribuite nel cluster di big data nelle proprie applicazioni in SQL Server [utilizzo di applicazioni nei cluster di big data](big-data-cluster-consume-apps.md) per altre informazioni. È anche possibile consultare esempi aggiuntivi in [esempi di distribuire App](https://aka.ms/sql-app-deploy).

Per altre informazioni sui cluster dei big data a SQL Server, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
