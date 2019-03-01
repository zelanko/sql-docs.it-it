---
title: riferimento di debug mssqlctl cluster
titleSuffix: SQL Server 2019 big data clusters
description: Articolo di riferimento per i comandi di cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9312e972dfcb439f4ef19a4e72d8d66454622096
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018157"
---
# <a name="mssqlctl-cluster-debug"></a>debug di cluster mssqlctl

L'articolo seguente fornisce informazioni di riferimento per la **debug cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a id="commands"></a> Comandi

|||
|---|---|
| [copy-logs](#copy-logs) | Copiare i log. |
| [dump](#dump) | Dump di registrazione di trigger. |

## <a id="copy-logs"></a> Copia-log di debug di cluster

Copiare i log.

```
mssqlctl cluster debug copy-logs
   --namespace
   [--container]
   [--pod]
   [--target-folder]
   [--timeout]
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-n - spazio dei nomi** | Nome del cluster, usata per lo spazio dei nomi kubernetes. Obbligatorio. |
| **--container -c** | Copiare i log per i contenitori con nome simile, facoltativo, per impostazione predefinita la copia dei log per tutti i contenitori. Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare. |
| **-pod -p** | Copiare i log per i POD con nome simile. Facoltativo, per i log di copia predefinita per tutti i POD. Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare. |
| **--target-folder -d** | Percorso della cartella di destinazione per copiare i registri per. Facoltativo, per impostazione predefinita viene creato il risultato nella cartella locale.  Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare. |
| **--timeout -t** | Il numero di secondi di attesa per il completamento del comando. Il valore predefinito è 0 che è illimitato. |

## <a id="dump"></a> dump del debug del cluster

Dump di registrazione di trigger.

```
mssqlctl cluster debug dump
   [--container]
   [--namespace]
   --target-folder
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **--container -c** | Copiare i log per i contenitori con nome simile, facoltativo, per impostazione predefinita la copia dei log per tutti i contenitori. Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare.  I valori consentiti: mssql-controller. |
| **-n - spazio dei nomi** | Nome del cluster, usata per lo spazio dei nomi kubernetes. Obbligatorio. |
| **--target-folder -d** | Percorso della cartella di destinazione per copiare i registri per. Facoltativo, per impostazione predefinita viene creato il risultato nella cartella locale.  Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare.  Valore predefinito: `./output/dump`. Obbligatorio. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).