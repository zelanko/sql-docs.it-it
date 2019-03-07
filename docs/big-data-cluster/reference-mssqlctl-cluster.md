---
title: riferimento cluster mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Articolo di riferimento per i comandi di cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 130d3019d49deb7851696f6a1db2f77040734b31
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527214"
---
# <a name="mssqlctl-cluster"></a>cluster mssqlctl

L'articolo seguente fornisce informazioni di riferimento per la **cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a id="commands"></a> Comandi

|||
|---|---|
| [create](#create) | Creare cluster. |
| [delete](#delete) | Eliminare il cluster. |
| [config](reference-mssqlctl-cluster-config.md) | Comandi di configurazione del cluster. |
| [debug](reference-mssqlctl-cluster-debug.md) | I comandi di debug. |

## <a id="create"></a> creare cluster mssqlctl

Creare cluster.

```
mssqlctl cluster create
   --name
   --accept-eula
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-Nome - n** | Nome del cluster, usata per lo spazio dei nomi kubernetes. |
| **--accept-eula -e** | Si accettano le condizioni di licenza? \[yes/no\].  I valori consentiti: no, Sì. Obbligatorio. |

## <a id="delete"></a> eliminazione del cluster mssqlctl

Eliminare il cluster.

```
mssqlctl cluster delete
   --name
   [--force]
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **-Nome - n** | Nome del cluster, usata per lo spazio dei nomi kubernetes. Obbligatorio. |
| **-force -f** | Cluster di eliminazione forzata. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).