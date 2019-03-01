---
title: riferimento di modello app mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Articolo di riferimento per i comandi di modello app mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 16583ba970bfc13312864ea2e9d2571b04c20fcb
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018497"
---
# <a name="mssqlctl-app-template"></a>modello di app mssqlctl

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