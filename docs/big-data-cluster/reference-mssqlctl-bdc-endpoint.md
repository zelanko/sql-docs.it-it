---
title: riferimento all'endpoint di mssqlctl integrazione applicativa dei dati
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi dell'endpoint di mssqlctl integrazione applicativa dei dati.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bdca9bb137fdaccbfa5e24deca1b22492678c1c9
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394323"
---
# <a name="mssqlctl-bdc-endpoint"></a>mssqlctl bdc endpoint

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **endpoint di integrazione applicativa dei dati** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[mssqlctl bdc endpoint list](#mssqlctl-bdc-endpoint-list) | Vengono elencati gli endpoint per il Cluster Big Data.
## <a name="mssqlctl-bdc-endpoint-list"></a>elenco di endpoint mssqlctl integrazione applicativa dei dati
Vengono elencati gli endpoint per il Cluster Big Data.
```bash
mssqlctl bdc endpoint list [--endpoint-name -e] 
                           
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--endpoint-name -e`
Nome dell'endpoint di integrazione applicativa dei dati.
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

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).