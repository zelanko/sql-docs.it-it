---
title: riferimento allo stato di controllo di mssqlctl integrazione applicativa dei dati
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi dello stato del controllo mssqlctl integrazione applicativa dei dati.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c87849f8539cbef18222a053ae17fae487194e93
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728594"
---
# <a name="mssqlctl-bdc-control-status"></a>stato del controllo mssqlctl integrazione applicativa dei dati

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **integrazione applicativa dei dati stato del controllo** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[Mostra lo stato di mssqlctl integrazione applicativa dei dati controllo](#mssqlctl-bdc-control-status-show) | Stato del controllo.
## <a name="mssqlctl-bdc-control-status-show"></a>Mostra lo stato di mssqlctl integrazione applicativa dei dati controllo
Stato del controllo.
```bash
mssqlctl bdc control status show 
```
### <a name="examples"></a>Esempi
Ottiene lo stato del controllo.
```bash
mssqlctl bdc control status show
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

Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).