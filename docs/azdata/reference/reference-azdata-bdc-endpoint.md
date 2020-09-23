---
title: Informazioni di riferimento su azdata bdc endpoint
titleSuffix: SQL Server big data clusters
description: Usare questo articolo di riferimento per comprendere i comandi SQL dello strumento azdata, in particolare i comandi bdc endpoint.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 06d910dd241a567e4b7f01281fdf403e646c6845
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733813"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc endpoint

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
| Comando | Descrizione |
| --- | --- |
[azdata bdc endpoint list](#azdata-bdc-endpoint-list) | Elenca gli endpoint per il cluster di Big Data.
## <a name="azdata-bdc-endpoint-list"></a>azdata bdc endpoint list
Elenca gli endpoint per il cluster di Big Data.
```bash
azdata bdc endpoint list [--endpoint-name -e] 
                         
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--endpoint-name -e`
Nome dell'endpoint del cluster di Big Data.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](../install/deploy-install-azdata.md).
