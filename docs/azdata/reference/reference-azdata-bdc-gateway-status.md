---
title: Informazioni di riferimento su azdata bdc gateway status
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc gateway status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 10fab7071a5e599b81ef65f3774ebf3a50507662
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914856"
---
# <a name="azdata-bdc-gateway-status"></a>azdata bdc gateway status

Si applica al `azdata`

L'articolo seguente fornisce informazioni di riferimento sui comandi **sql** dello strumento **azdata**. Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi

|Comando|Descrizione|
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). 

Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata](..\install\deploy-install-azdata.md).

