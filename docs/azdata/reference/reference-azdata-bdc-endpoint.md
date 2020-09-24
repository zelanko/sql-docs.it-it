---
title: Informazioni di riferimento su azdata bdc endpoint
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc endpoint.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 52c82dc741e987bbd31f5328ab1cbc4f4bd84e68
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914867"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc endpoint

Si applica al `azdata`

L'articolo seguente fornisce informazioni di riferimento sui comandi **sql** dello strumento **azdata**. Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi

|Comando|Descrizione|
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

Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). 

Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata](..\install\deploy-install-azdata.md).

