---
title: riferimento di configurazione del cluster mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Articolo di riferimento per i comandi di cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 26e93151a1150bbbbd1798b38486ca5b01aaab1d
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527204"
---
# <a name="mssqlctl-cluster-config"></a>configurazione di cluster mssqlctl

L'articolo seguente fornisce informazioni di riferimento per la **configurazione del cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a id="commands"></a> Comandi

|||
|---|---|
| [get](#get) | Get cluster. |

## <a id="get"></a> configurazione di cluster mssqlctl ottenere

Get cluster.

```
mssqlctl cluster config get
   --name
   --output-file
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-Nome - n** | Nome del cluster, usata per lo spazio dei nomi kubernetes. Obbligatorio. |
| **--output-file -f** | File di output per archiviare il risultato in. Obbligatorio. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).