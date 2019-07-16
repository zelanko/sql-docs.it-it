---
title: riferimento ai pool lo stato di mssqlctl integrazione applicativa dei dati
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di stato mssqlctl integrazione applicativa dei dati del pool.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2a93fe8ba55b7b9508cff32d4272645fab7cb975
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958048"
---
# <a name="mssqlctl-bdc-pool-status"></a>stato del pool di mssqlctl integrazione applicativa dei dati

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **lo stato di integrazione applicativa dei dati del pool** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[Mostra lo stato del pool di mssqlctl integrazione applicativa dei dati](#mssqlctl-bdc-pool-status-show) | Stato del pool.
## <a name="mssqlctl-bdc-pool-status-show"></a>Mostra lo stato del pool di mssqlctl integrazione applicativa dei dati
Stato del pool.
```bash
mssqlctl bdc pool status show --kind -k 
                              [--name -n]
```
### <a name="examples"></a>Esempi
Ottiene lo stato del pool di archiviazione.
```bash
mssqlctl bdc pool status show --kind storage --name default
```
Ottiene lo stato del pool di dati.
```bash
mssqlctl bdc pool status show --kind data --name default
```
Ottiene lo stato del pool di calcolo.
```bash
mssqlctl bdc pool status show --kind compute --name default
```
Ottiene lo stato del pool master.
```bash
mssqlctl bdc pool status show --kind master --name default
```
Ottiene lo stato del pool di spark.
```bash
mssqlctl bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--kind -k`
Tipo di pool di integrazione applicativa dei dati.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome del pool di integrazione applicativa dei dati.
`default`
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

Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).