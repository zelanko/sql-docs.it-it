---
title: riferimento dell'app mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Articolo di riferimento per i comandi dell'app mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fa2b43c352fbab39cd00112b9646a87a2b752f5b
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018487"
---
# <a name="mssqlctl-app"></a>app mssqlctl

L'articolo seguente fornisce informazioni di riferimento per la **app** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a id="commands"></a> Comandi

|||
|---|---|
| [create](#create) | Creare l'applicazione. |
| [delete](#delete) | Eliminare l'applicazione. |
| [describe](#describe) | Descrivere l'applicazione. |
| [init](#init) | Kickstart nuova struttura dell'applicazione. |
| [list](#list) | Elencare le applicazioni. |
| [run](#run) | Esegui l'applicazione. |
| [update](#update) | Aggiornare l'applicazione. |
| [template](reference-mssqlctl-app-template.md) | Comandi di modello. |

## <a id="create"></a> creare app mssqlctl

Creare l'applicazione.

```
mssqlctl app create
   --assets
   --code
   --description
   --entrypoint
   --inputs
   --name
   --outputs
   --runtime
   --spec
   --version
   --yes
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **--assets -a** | Elenco degli asset di file dell'applicazione aggiuntivi da includere. |
| **--code -c** | Percorso file di codice R o Python. |
| **--description -d** | Descrizione dell'applicazione. |
| **--entrypoint** |  |
| **--inputs** | Schema dei parametri di input. |
| **-Nome - n** | Nome applicazione |
| **--outputs** | Schema dei parametri output. |
| **-r - runtime** | Fase di esecuzione dell'applicazione.  Valori consentiti: Mleap, Python, R, SSIS. |
| **-spec -s** | Percorso di una directory con un file YAML delle specifiche che descrive l'applicazione. |
| **--version -v** | Versione dell'applicazione. |
| **-Sì -y** | Non chiedere conferma quando si crea un'applicazione dal file spec.yaml del CWD. |

### <a name="examples"></a>Esempi

Creare una nuova applicazione tramite spec.yaml (scelta consigliata).

```
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```

Creare un nuovo inline app Python usando argomenti.

```
mssqlctl app create --name add --version v1 --inputs x=float, y=float --outputs result=float --runtime Python --code add.py  --init init.py
```

Creare una nuova inline di applicazione di R usando argomenti.

```
mssqlctl app create --name add --version v1 --inputs x=numeric, y=numeric --outputs result=numeric --runtime R --code add.R  --init init.R
```

Creare un nuovo inline di applicazione di R con gli asset di file aggiuntivi da includere.

```
mssqlctl app create --name add --version v1 --runtime R --code  add.R --assets file.RData,/path/to/more/files
```

## <a id="delete"></a> mssqlctl app delete

Eliminare l'applicazione.

```
mssqlctl app delete
   --name
   --version
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-Nome - n** | Nome applicazione |
| **--version -v** | Versione dell'applicazione. |

### <a name="examples"></a>Esempi

Eliminare l'applicazione per nome e versione.

```
mssqlctl app delete --name reduce --version v1
```

## <a id="describe"></a> Descrivere mssqlctl app

Descrivere l'applicazione.

```
mssqlctl app describe
   --name
   --spec
   --version
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-Nome - n** | Nome applicazione |
| **-spec -s** | Percorso di una directory con un file YAML delle specifiche che descrive l'applicazione. |
| **--version -v** | Versione dell'applicazione. |

### <a name="examples"></a>Esempi

Descrivere l'applicazione.

```
mssqlctl app describe --name reduce --version v1
```

## <a id="init"></a> mssqlctl app init

Kickstart nuova struttura dell'applicazione.

```
mssqlctl app init
   --destination
   --name
   --spec
   --template
   --url
   --version
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **--destination -d** | Posizione in cui posizionare lo scheletro dell'applicazione. Valore predefinito: directory di lavoro corrente. |
| **-Nome - n** | Nome applicazione |
| **-spec -s** | Generare solo un spec.yaml dell'applicazione. |
| **--template -t** | Nome del modello. Per un elenco completo di disattivare i nomi dei modelli supportati eseguire `mssqlctl app template list`. |
| **-url -u** | Specificare un percorso del repository di modelli diversi. Valore predefinito: https://github.com/Microsoft/sql-server-samples.git. |
| **--version -v** | Versione dell'applicazione. |

### <a name="examples"></a>Esempi

Eseguire lo scaffolding di una nuova applicazione `spec.yaml` solo.

```
mssqlctl app init --spec
```

Eseguire lo scaffolding di una struttura di applicazione dell'applicazione R nuova basata di `r` modello.

```
mssqlctl app init --name reduce --template r
```

Eseguire lo scaffolding di una struttura di applicazione dell'applicazione Python nuova basata di `python` modello.

```
mssqlctl app init --name reduce --template python
```

Eseguire lo scaffolding di una struttura di applicazione dell'applicazione SSIS nuova basata di `ssis` modello.

```
mssqlctl app init --name reduce --template ssis
```

## <a id="list"></a> elenco di app mssqlctl

Elencare le applicazioni.

```
mssqlctl app list
   --name
   --version
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-Nome - n** | Nome applicazione |
| **--version -v** | Versione dell'applicazione. |

### <a name="examples"></a>Esempi

Applicazione di elenco per nome e versione.

```
mssqlctl app list --name reduce  --version v1
```

Elencare tutte le versioni dell'applicazione in base al nome.

```
mssqlctl app list --name reduce
```

Elencare tutte le applicazioni.

```
mssqlctl app list
```

## <a id="run"></a> esecuzione dell'app mssqlctl

Esegui l'applicazione.

```
mssqlctl app run
   --name
   --version
   --inputs
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-Nome - n** | Nome applicazione |
| **--version -v** | Versione dell'applicazione. |
| **--inputs** | I parametri in un file CSV di input applicazione `name=value` formato. |

### <a name="examples"></a>Esempi

Eseguire l'applicazione senza parametri di input.

```
mssqlctl app run --name reduce --version v1
```

Eseguire l'applicazione con 1 parametro di input.

```
mssqlctl app run --name reduce --version v1 --inputs x=10
```

Esegui l'applicazione con più parametri di input.

```
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6
```

## <a id="update"></a> aggiornamento dell'app mssqlctl

Aggiornare l'applicazione.

```
mssqlctl app update
   --spec
   --yes
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-spec -s** | Percorso di una directory con un file YAML delle specifiche che descrive l'applicazione. |
| **-Sì -y** | Non chiedere conferma quando si aggiorna un'applicazione dal file spec.yaml del CWD. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).