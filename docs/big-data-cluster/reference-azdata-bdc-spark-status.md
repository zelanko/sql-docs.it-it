---
title: Informazioni di riferimento su azdata bdc spark status
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc spark status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 59dee7b9c7262233ec6e80097105b1fbd6b4d7ea
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531753"
---
# <a name="azdata-bdc-spark-status"></a>azdata bdc spark status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md)

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[azdata bdc spark status show](#azdata-bdc-spark-status-show) | Stato del servizio Spark.
## <a name="azdata-bdc-spark-status-show"></a>azdata bdc spark status show
Stato del servizio Spark.
```bash
azdata bdc spark status show [--resource -r] 
                             [--all -a]
```
### <a name="examples"></a>Esempi
Recupero dello stato del servizio Spark.
```bash
azdata bdc spark status show
```
Recupero dello stato del servizio Spark con tutte le istanze.
```bash
azdata bdc spark status show --all
```
Recupero dello stato della risorsa di archiviazione all'interno del servizio Spark.
```bash
azdata bdc spark status show --resource storage-0
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--resource -r`
Consente di ottenere la risorsa specificata in questo servizio.
#### `--all -a`
Visualizza tutte le istanze di ogni risorsa all'interno del servizio.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).
