---
title: riferimento di montaggio mssqlctl archiviazione
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di archiviazione mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3ad8a97bac1f708dcf01612368c76d584fa39f5c
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860292"
---
# <a name="mssqlctl-storage-mount"></a>montaggio archiviazione mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **montare archiviazione** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a id="commands"></a> Comandi

|||
|---|---|
| [create](#create) | Creare punti di montaggio di archivi remoti in HDFS. |
| [delete](#delete) | Eliminare i punti di montaggio del remoto archivia in HDFS. |
| [status](#status) | Stato di mount(s). |

## <a id="create"></a> montare archiviazione mssqlctl creare

Creare punti di montaggio di archivi remoti in HDFS.

```
mssqlctl storage mount create
   --local-path
   --remote-uri
   [--credential-file]
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **--local-path** | Percorso HDFS in cui deve essere montaggio creare (destinazione di montaggio). Obbligatorio. |
| **--remote-uri** | URI dell'archivio remoto che deve essere montati (di origine di montaggio). Obbligatorio. |
| **--credential-file** | File che contiene le credenziali per accedere all'archivio remoto. Le credenziali devono essere specificate come chiave = coppie valore con una chiave = valore per ogni riga. Qualsiasi è uguale in chiavi o valori sono necessario utilizzare caratteri di escape. Le credenziali non sono necessari per impostazione predefinita. Le chiavi necessarie variano a seconda del tipo di archivio remoto in cui vengono montato e il tipo di autorizzazione usata. |

### <a name="examples"></a>Esempi

Per montare "i dati del contenitore" nell'account Azure Data Lake Store generazione 2 "adlsv2example" nel percorso HDFS `/mounts/adlsv2/data` usando la chiave condivisa:

```
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/ --local-path /mounts/adlsv2/data --credentials credential_file
```

Per montare un cluster HDFS remoto (`hdfs://namenode1:8080/`) nel percorso HDFS locale `/mounts/hdfs/`:

```
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --local-path /mounts/hdfs/
```

## <a id="delete"></a> mssqlctl archiviazione montaggio delete

Eliminare i punti di montaggio del remoto archivia in HDFS.

```
mssqlctl storage mount delete
   --local-path
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **--local-path** | Il percorso HDFS corrispondente per il montaggio che deve essere eliminato. Obbligatorio. |

### <a name="examples"></a>Esempi

Eliminare montaggio creato alle /mounts/adlsv2/data per un account di archiviazione di Azure Data Lake Store generazione 2.

```
mssqlctl storage mount delete --local-path /mounts/adlsv2/data
```

## <a id="status"></a> stato montaggio dell'archiviazione mssqlctl

Stato di mount(s).

```
mssqlctl storage mount status
   --local-path
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **--mount-path** | Percorso di montaggio. Obbligatorio. |

### <a name="examples"></a>Esempi

Ottenere lo stato di montaggio per percorso

```
mssqlctl storage mount status --mount-path /mounts/hdfs
```

Ottiene lo stato di tutti i punti di montaggio.

```
mssqlctl storage mount status
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).