---
title: Riferimento ad azdata arc resource-kind
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata arc resource-kind.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 68d6d4c30e43804c8c18a7dc36d0a9d53bcb5677
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358709"
---
# <a name="azdata-arc-resource-kind"></a>azdata arc resource-kind

Si applica al [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi **sql** dello strumento **azdata**. Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi

|Comando|Descrizione|
| --- | --- |
[azdata arc resource-kind list](#azdata-arc-resource-kind-list) | Elenca i tipi di risorse personalizzati disponibili per Arc che è possibile definire e creare.
[azdata arc resource-kind get](#azdata-arc-resource-kind-get) | Ottiene il file di modello del tipo di risorsa Arc.
## <a name="azdata-arc-resource-kind-list"></a>azdata arc resource-kind list
Elenca i tipi di risorse personalizzati disponibili per Arc che è possibile definire e creare. Dopo aver visualizzato l'elenco, è possibile procedere al recupero del file di modello necessario per definire o creare la risorsa personalizzata.
```bash
azdata arc resource-kind list 
```
### <a name="examples"></a>Esempi
Comando di esempio per elencare i tipi di risorse personalizzati disponibili per Arc.
```bash
azdata arc resource-kind list
```
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
## <a name="azdata-arc-resource-kind-get"></a>azdata arc resource-kind get
Ottiene il file di modello del tipo di risorsa Arc.
```bash
azdata arc resource-kind get --kind -k 
                             [--dest -d]
```
### <a name="examples"></a>Esempi
Comando di esempio per ottenere il file di modello CRD del tipo risorsa Arc.
```bash
azdata arc resource-kind get --kind sqldb
```
### <a name="required-parameters"></a>Parametri necessari
#### `--kind -k`
Tipo di risorsa Arc per cui si vuole ottenere il file di modello.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--dest -d`
Directory in cui si vogliono inserire i file di modello.
`template`
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

