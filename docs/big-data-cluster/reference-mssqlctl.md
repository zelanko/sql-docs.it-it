---
title: riferimento mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ebd3b63d641c77dae1afbff21264ec4fe34df4d0
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473465"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **mssqlctl** dello strumento per [cluster di big data 2019 Server SQL (anteprima)](big-data-cluster-overview.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
|[app mssqlctl](reference-mssqlctl-app.md) | Creare, eliminare, eseguire e gestire le applicazioni. |
|[cluster mssqlctl](reference-mssqlctl-cluster.md) | Selezionare, gestire e operare i cluster. |
[account di accesso mssqlctl](#mssqlctl-login) | Accedere al cluster.
[disconnessione mssqlctl](#mssqlctl-logout) | Disconnettersi dal cluster.
|[archiviazione mssqlctl](reference-mssqlctl-storage.md) | Gestire l'archiviazione del cluster. |
## <a name="mssqlctl-login"></a>account di accesso mssqlctl
Accedere al cluster.
```bash
mssqlctl login [--username -u] 
               [--password -p]  
               [--endpoint -e]
```
### <a name="examples"></a>Esempi
Accedere in modo interattivo.
```bash
mssqlctl login
```
Accedere con nome utente e password.
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret
```
Accedere con l'endpoint del cluster, nome utente e password.
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--username -u`
Account utente.
#### `--password -p`
Credenziali password.
#### `--endpoint -e`
Cluster host e porta (es) "http://host:port".
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.
## <a name="mssqlctl-logout"></a>disconnessione mssqlctl
Disconnettersi dal cluster.
```bash
mssqlctl logout 
```
### <a name="examples"></a>Esempi
Disconnettere l'utente.
```bash
mssqlctl logout
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).