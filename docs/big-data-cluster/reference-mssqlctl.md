---
title: riferimento mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Articolo di riferimento per i comandi mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: be1ece46bd171370a91273c832bf89a0bf426cd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018367"
---
# <a name="mssqlctl"></a>mssqlctl

L'articolo seguente fornisce informazioni di riferimento per la **mssqlctl** dello strumento per i cluster di big data di SQL Server 2019 (anteprima).

## <a id="commands"></a> Comandi

|||
|---|---|
| [app](reference-mssqlctl-app.md) | Creare, eliminare, eseguire e gestire le applicazioni. |
| [cluster](reference-mssqlctl-cluster.md) | Selezionare, gestire e operare i cluster. |
| [login](#login) | Accedere al cluster. |
| [logout](#logout) | Disconnettersi dal cluster. |
| [storage](reference-mssqlctl-storage.md) | Gestire l'archiviazione del cluster. |

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
|**--endpoint -e**| Cluster host e porta (ex) `http://host:port"`. |
|**--password -p**| Credenziali password. |
|**-- username -u**| Account utente. |

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
| **-- username -u** | Account utente, se mancanti, disconnessione, l'account attivo corrente. |

### <a name="examples"></a>Esempi

Disconnettere l'utente.

```
mssqlctl logout --username admin
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).