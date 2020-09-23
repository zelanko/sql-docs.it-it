---
title: Informazioni di riferimento su azdata bdc app status
titleSuffix: SQL Server big data clusters
description: Usare questo articolo di riferimento per comprendere i comandi SQL dello strumento azdata, in particolare il comando bdc app status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fd6288649db641bc846b8ebed3b997aa0092d36e
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733831"
---
# <a name="azdata-bdc-app-status"></a>azdata bdc app status

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
| Comando | Descrizione |
| --- | --- |
[azdata bdc app status show](#azdata-bdc-app-status-show) | Stato del servizio app.
## <a name="azdata-bdc-app-status-show"></a>azdata bdc app status show
Stato del servizio app.
```bash
azdata bdc app status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>Esempi
Recupero dello stato del servizio app.
```bash
azdata bdc app status show
```
Recupero dello stato del servizio app con tutte le istanze.
```bash
azdata bdc app status show --all
```
Recupero dello stato della risorsa appproxy all'interno del servizio app.
```bash
azdata bdc app status show --resource appproxy
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](../install/deploy-install-azdata.md).
