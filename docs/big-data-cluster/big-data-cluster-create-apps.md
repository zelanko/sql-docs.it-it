---
title: Come distribuire un'app
titleSuffix: SQL Server 2019 big data clusters
description: Distribuire uno script Python o R come un'applicazione nel cluster di big data 2019 Server SQL (anteprima).
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 12/11/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f37267083e0e56dd6e3c0e06c1d80ed79c0d9969
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241932"
---
# <a name="how-to-deploy-an-app-on-sql-server-2019-big-data-cluster-preview"></a>Come distribuire un'app nel cluster di big data 2019 Server SQL (anteprima)

Questo articolo descrive come distribuire e gestire lo script R e Python come un'applicazione all'interno di un cluster di big data di SQL Server 2019 (anteprima).

Le applicazioni di R e Python sono distribuite e gestite con il **mssqlctl-pre** utilità della riga di comando incluso in CTP 2.2. Questo articolo fornisce esempi su come distribuire questi script R e Python come le app dalla riga di comando.

## <a name="prerequisites"></a>Prerequisiti

È necessario disporre di un cluster di big data di SQL Server 2019 configurato. Per altre informazioni, vedere [come distribuire SQL Server del cluster di big data in Kubernetes](deployment-guidance.md). 

## <a name="installation"></a>Installazione

Il **mssqlctl-pre** utilità della riga di comando viene fornito per visualizzare in anteprima la funzionalità di distribuzione di applicazioni Python e R. Usare il comando seguente per installare l'utilità:

```cmd
pip install -r https://private-repo.microsoft.com/python/ctp-2.2/mssqlctlpre/mssqlctlpre.txt --trusted-host https://private-repo.microsoft.com
```

## <a name="capabilities"></a>Capabilities

CTP 2.2 che è possibile creare, eliminare, elencare ed eseguire un'applicazione di R o Python. La tabella seguente descrive i comandi di distribuzione dell'applicazione che è possibile usare con **mssqlctl-pre**.

| Comando | Descrizione |
|---|---|
| `mssqlctl-pre login` | Accedere a un cluster di big data di SQL Server |
| `mssqlctl-pre app create` | Creare un'app |
| `mssqlctl-pre app list` | Elencare le app distribuite |
| `mssqlctl-pre app delete` | Eliminare un'app |
| `mssqlctl-pre app run` | Elencare le App in esecuzione |

È possibile ottenere assistenza con la `--help` parametro come nell'esempio seguente:

```bash
mssqlctl-pre app create --help
```

Le sezioni seguenti descrivono questi comandi in modo più dettagliato.

## <a name="log-in"></a>Accedi

Prima di configurare applicazioni R e Python, prima accedere al Server SQL cluster dei big data con il `mssqlctl-pre login` comando. Specificare l'indirizzo IP esterno del `service-proxy-lb` oppure `service-proxy-nodeport` services (ad esempio: `https://ip-address:30777`) con il nome utente e la password per il cluster.

È possibile ottenere l'indirizzo IP del **service-proxy-lb** oppure **servizio-proxy-nodeport** servizio eseguendo questo comando in una finestra bash o cmd:

```bash 
kubectl get svc service-proxy-lb -n <name of your cluster>
```

```bash
mssqlctl-pre login -e https://<ip-address-of-service-proxy-lb>:30777 -u <user-name> -p <password>
```

## <a name="create-an-app"></a>Creare un'app

Per creare un'applicazione, si passano il file di codice Python o R da **mssqlctl-pre** con il `app create` comando. Questi file si trovano in locale nel computer che si sta creando l'app.

Usare la sintassi seguente per creare una nuova app nel cluster di big data:

```bash
mssqlctl-pre app create -n <app_name> -v <version_number> -r <runtime> -i <path_to_code_init> -c <path_to_code> --inputs <input_params> --outputs <output_params> 
```

Il comando seguente illustra un esempio di ciò che potrebbe essere simile questo comando:

```py
#add.py
def add(x,y):
        result = x+y
        return result;
result=add(x,y)
```
A questo scopo, salvare le righe di codice precedente nella directory locale come `add.py` ed eseguire il comando seguente

```bash
mssqlctl-pre app create --name add-app --version v1 --runtime Python --code ./add.py  --inputs x=int,y=int --outputs result=int 
```

È possibile controllare se l'app viene distribuita usando il comando di elenco:

```bash
mssqlctl-pre app list
```

Se la distribuzione non è stata completata dovrebbe essere "state" Mostra "Creazione": 

```
[
  {
    "name": "add-app",
    "state": "Creating",
    "version": "v1"
  }
]
```

Dopo la distribuzione ha esito positivo si dovrebbe vedere lo "stato" modifica allo stato "Ready":

```
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
mssqlctl-pre app list
```

Se si specifica un nome e la versione, verranno visualizzate app specifiche e il relativo stato (creazione in corso o Ready):

```bash
mssqlctl-pre app list --name <app_name> --version <app_version>
```

L'esempio seguente illustra questo comando:

```bash
mssqlctl-pre app list --name add-app --version v1
```

Si dovrebbe visualizzato un output simile all'esempio seguente:

```
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>Eseguire un'app

Se l'app è in uno stato "Pronto", è possibile usarlo eseguendolo con i parametri di input specificati. Usare la sintassi seguente per eseguire un'app:

```bash
mssqlctl-pre app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

Il comando seguente viene illustrato il comando di esecuzione:

```bash
mssqlctl-pre app run --name add-app --version v1 --inputs x=1,y=2
```

Se l'esecuzione ha avuto esito positivo, si verrà visualizzato l'output come specificato durante la creazione dell'app. Di seguito è riportato un esempio.

```
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

## <a name="delete-an-app"></a>Eliminare un'app

Per eliminare un'app dal cluster i big data, usare la sintassi seguente:

```bash
mssqlctl-pre app delete --name add-app --version v1
```

## <a name="next-steps"></a>Passaggi successivi

È anche possibile consultare esempi aggiuntivi in [ https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster). 

Per altre informazioni sui cluster dei big data a SQL Server, vedere [quali sono i cluster di SQL Server 2019 dei big data?](big-data-cluster-overview.md).
