---
title: riferimento mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b050638ee0ca600c5df0ecdbe5616b801f41e7a8
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860353"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **mssqlctl** dello strumento per [cluster di big data 2019 Server SQL (anteprima)](big-data-cluster-overview.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).

## <a id="commands"></a> Comandi

|||
|---|---|
| [app](reference-mssqlctl-app.md) | Creare, eliminare, eseguire e gestire le applicazioni. |
| [cluster](reference-mssqlctl-cluster.md) | Selezionare, gestire e operare i cluster. |
| [login](#login) | Accedere al cluster. |
| [logout](#logout) | Disconnettersi dal cluster. |
| [archiviazione](reference-mssqlctl-storage.md) | Gestire l'archiviazione del cluster. |

## <a id="login"></a> account di accesso mssqlctl

Accedere al cluster.

```
mssqlctl login
   --endpoint
   --password
   --username
```

### <a name="parameters"></a>Parametri

| Parametro | Descrizione |
|---|---|
|**-endpoint -e**| Cluster host e porta (ex) `http://host:port"`. |
|**-password -p**| Credenziali password. |
|**--username -u**| Account utente. |

### <a name="examples"></a>Esempi

Accedere in modo interattivo.

```
mssqlctl login
```

Accedere con nome utente e password.

```
mssqlctl login -u johndoe@contoso.com -p VerySecret
```

Accedere con l'endpoint del cluster, nome utente e password.

```
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```

## <a id="logout"></a> disconnessione mssqlctl

Disconnettersi dal cluster.

```
mssqlctl logout
   --username
```

### <a name="parameters"></a>Parametri

| Parametri | Descrizione |
|---|---|
| **--username -u** | Account utente, se mancanti, disconnessione, l'account attivo corrente. |

### <a name="examples"></a>Esempi

Disconnettere l'utente.

```
mssqlctl logout --username admin
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).