---
title: informazioni di riferimento sullo stato del controllo BDC azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di stato del controllo BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d1f7e2e5931ec55cd2fd2632072de223db252b84
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426251"
---
# <a name="azdata-bdc-control-status"></a>stato del controllo BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi di **stato del controllo BDC** nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[visualizzazione dello stato del controllo BDC azdata](#azdata-bdc-control-status-show) | Stato del controllo.
## <a name="azdata-bdc-control-status-show"></a>visualizzazione dello stato del controllo BDC azdata
Stato del controllo.
```bash
azdata bdc control status show 
```
### <a name="examples"></a>Esempi
Ottenere lo stato del controllo.
```bash
azdata bdc control status show
```
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
