---
title: Informazioni di riferimento su azdata bdc status
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: daf3115a7ccdd73f86dbaa9766049cd5be1e1eb9
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733690"
---
# <a name="azdata-bdc-status"></a>azdata bdc status

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
| Comando | Descrizione |
| --- | --- |
[azdata bdc status show](#azdata-bdc-status-show) | Visualizza lo stato del cluster Big Data.
## <a name="azdata-bdc-status-show"></a>azdata bdc status show
Visualizza lo stato del cluster Big Data.
```bash
azdata bdc status show [--resource -r] 
                       [--all -a]
```
### <a name="examples"></a>Esempi
Stato del cluster Big Data a cui l'utente ha eseguito l'accesso.
```bash
azdata bdc status show
```
Stato del cluster Big Data con tutte le istanze delle risorse incluse.
```bash
azdata bdc status show --all
```
Stato del cluster Big Data dei servizi che includono la risorsa di controllo.
```bash
azdata bdc status show --resource control
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--resource -r`
Consente di ottenere i servizi associati alla risorsa.
#### `--all -a`
Visualizza tutte le istanze di ogni risorsa all'interno dei servizi.
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
