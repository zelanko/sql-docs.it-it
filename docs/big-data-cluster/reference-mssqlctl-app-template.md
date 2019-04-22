---
title: riferimento di modello app mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di modello app mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c67ed74750ac36d1a5c79503417414a9dd8ab6b5
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860102"
---
# <a name="mssqlctl-app-template"></a>modello di app mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **modello di app** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a id="commands"></a> Comandi

|||
|---|---|
| [list](#list) | Modelli di recupero supportata. |
| [pull](#pull) | Scaricare i modelli supportati. |

## <a id="list"></a> elenco di modelli di app mssqlctl

Modelli di recupero supportata.

```
mssqlctl app template list
   --url
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-url -u** | Specificare un percorso del repository di modelli diversi. Valore predefinito: https://github.com/Microsoft/sql-server-samples.git. |

### <a name="examples"></a>Esempi

Recuperare tutti i modelli con il percorso predefinito dei repository di modelli.

```
mssqlctl app template list
```

Recuperare tutti i modelli in una posizione diversa del repository.

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

## <a id="pull"></a> pull di modello app mssqlctl

Scaricare i modelli supportati.

```
mssqlctl app template pull
   --destination
   --name
   --url
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **--destination -d** | Posizione in cui inserire il modello di struttura dell'applicazione.  Valore predefinito:. / modelli. |
| **-Nome - n** | Nome del modello. Per un elenco completo di disattivare i nomi dei modelli supportati eseguire `mssqlctl app template list`. |
| **-url -u** | Specificare un percorso del repository di modelli diversi. Impostazione predefinita:
https://github.com/Microsoft/sql-server-samples.git (Indici per tabelle con ottimizzazione per la memoria). |

### <a name="examples"></a>Esempi

Scaricare tutti i modelli con il percorso predefinito dei repository di modelli.

```
mssqlctl app template pull
```

Scaricare tutti i modelli in una posizione diversa del repository.

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

Scaricare il modello di singole in base al nome.

```
mssqlctl app template pull --name ssis
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).