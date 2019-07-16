---
title: riferimento all'endpoint di mssqlctl integrazione applicativa dei dati
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi dell'endpoint di mssqlctl integrazione applicativa dei dati.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ae9a5ad79f388f260494c18448dd80e815b3ac02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958083"
---
# <a name="mssqlctl-bdc-endpoint"></a>endpoint di integrazione applicativa dei dati mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **endpoint di integrazione applicativa dei dati** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[elenco di endpoint mssqlctl integrazione applicativa dei dati](#mssqlctl-bdc-endpoint-list) | Vengono elencati gli endpoint per il Cluster Big Data.
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
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).