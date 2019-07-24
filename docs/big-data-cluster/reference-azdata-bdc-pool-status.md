---
title: informazioni di riferimento sullo stato del pool BDC azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di stato del pool BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0a5925af4f16f2147988b2318880d9acec664c3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426131"
---
# <a name="azdata-bdc-pool-status"></a>stato pool BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi di **stato del pool BDC** nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[visualizzazione dello stato del pool BDC azdata](#azdata-bdc-pool-status-show) | Stato del pool.
## <a name="azdata-bdc-pool-status-show"></a>visualizzazione dello stato del pool BDC azdata
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
Ottenere lo stato del pool di risorse di calcolo.
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
Tipo di pool di cluster Big Data.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome del pool di cluster Big Data.
`default`
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  Valori consentiti: JSON, jsonc, Table, TSV.  Impostazione predefinita: JSON.
#### `--query -q`
Stringa di query JMESPath. Per [http://jmespath.org/](http://jmespath.org/]) ulteriori informazioni ed esempi, vedere.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su come installare lo strumento **azdata** , vedere [Install azdata to manage SQL Server 2019 Big Data Clusters](deploy-install-azdata.md).
