---
title: riferimento dello stato di integrazione applicativa dei dati mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di mssqlctl integrazione applicativa dei dati dello stato.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f1b7f7c635b621c1c85953e63acc8f80bb52b01
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728561"
---
# <a name="mssqlctl-bdc-status"></a>stato di integrazione applicativa dei dati mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **lo stato di integrazione applicativa dei dati** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[Mostra lo stato di integrazione applicativa dei dati mssqlctl](#mssqlctl-bdc-status-show) | Mostra lo stato del Cluster di Big Data.
## <a name="mssqlctl-bdc-status-show"></a>Mostra lo stato di integrazione applicativa dei dati mssqlctl
Mostra lo stato del Cluster di Big Data.
```bash
mssqlctl bdc status show 
```
### <a name="examples"></a>Esempi
Stato di integrazione applicativa dei dati in cui l'utente è connesso.
```bash
mssqlctl bdc status show
```
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

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).