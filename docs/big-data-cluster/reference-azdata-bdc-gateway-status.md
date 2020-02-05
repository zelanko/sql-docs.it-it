---
title: Informazioni di riferimento su azdata bdc gateway status
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc gateway status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1c74439be0a696197f35a86a0d493a8ad01e28ff
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "74820928"
---
# <a name="azdata-bdc-gateway-status"></a>azdata bdc gateway status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

L'articolo seguente offre informazioni di riferimento sui comandi `bdc gateway status` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md)

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata bdc gateway status show](#azdata-bdc-gateway-status-show) | Stato del servizio gateway.
## <a name="azdata-bdc-gateway-status-show"></a>azdata bdc gateway status show
Stato del servizio gateway.
```bash
azdata bdc gateway status show [--resource -r] 
                               [--all -a]
```
### <a name="examples"></a>Esempi
Recupero dello stato del servizio gateway.
```bash
azdata bdc gateway status show
```
Recupero dello stato del servizio gateway con tutte le istanze.
```bash
azdata bdc gateway status show --all
```
Recupero dello stato della risorsa gateway all'interno del servizio gateway.
```bash
azdata bdc gateway status show --resource gateway
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
