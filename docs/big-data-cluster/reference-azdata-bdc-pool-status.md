---
title: Informazioni di riferimento su azdata bdc pool status
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc pool status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ee49ee09107c98047bd5aea849b9ae486eb6736a
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153116"
---
# <a name="azdata-bdc-pool-status"></a>azdata bdc pool status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

Questo articolo è un articolo di riferimento per **azdata**. 

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata bdc pool status show](#azdata-bdc-pool-status-show) | Stato del pool.
## <a name="azdata-bdc-pool-status-show"></a>azdata bdc pool status show
Stato del pool.
```bash
azdata bdc pool status show --kind -k 
                            [--name -n]
```
### <a name="examples"></a>Esempi
Ottenere lo stato del pool di archiviazione.
```bash
azdata bdc pool status show --kind storage --name default
```
Ottenere lo stato del pool di dati.
```bash
azdata bdc pool status show --kind data --name default
```
Ottenere lo stato del pool di calcolo.
```bash
azdata bdc pool status show --kind compute --name default
```
Ottenere lo stato del pool master.
```bash
azdata bdc pool status show --kind master --name default
```
Ottenere lo stato del pool Spark.
```bash
azdata bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--kind -k`
Tipo di pool del cluster Big Data.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome del pool del cluster Big Data.
`default`
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). 

- Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).
