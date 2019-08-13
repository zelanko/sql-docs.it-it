---
title: Informazioni di riferimento su azdata bdc debug
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc debug.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38c327287273ae6596326d88d9e0d67c8e014d47
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426231"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi **bdc debug** dello strumento **azdata**. Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[azdata bdc debug copy-logs](#azdata-bdc-debug-copy-logs) | Copia i log.
[azdata bdc debug dump](#azdata-bdc-debug-dump) | Attiva il dump di registrazione.
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug copy-logs
Copia i log di debug dal cluster Big Data: è necessaria la configurazione kube nel sistema.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Nome del cluster Big Data, usato per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--container -c`
Copia i log relativi ai contenitori con nome simile. Facoltativo; per impostazione predefinita, vengono copiati i log di tutti i contenitori. Questo parametro non può essere specificato più volte. In caso contrario, verrà usato l'ultimo parametro specificato.
#### `--target-folder -d`
Percorso della cartella di destinazione in cui copiare i log. Facoltativo; per impostazione predefinita, il risultato viene creato nella cartella locale.  Questo parametro non può essere specificato più volte. In caso contrario, verrà usato l'ultimo parametro specificato.
#### `--pod -p`
Copia i log relativi ai pod con nome simile. Facoltativo; per impostazione predefinita, vengono copiati i log di tutti i pod. Questo parametro non può essere specificato più volte. In caso contrario, verrà usato l'ultimo parametro specificato.
#### `--timeout -t`
Numero di secondi di attesa per il completamento del comando. Il valore predefinito è 0, ovvero illimitato.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
Attiva il dump della registrazione e lo copia dal contenitore: è necessaria la configurazione kube nel sistema.
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Nome del cluster Big Data, usato per lo spazio dei nomi kubernetes.
#### `--container -c`
Copia i log relativi ai contenitori con nome simile. Facoltativo; per impostazione predefinita, vengono copiati i log di tutti i contenitori. Questo parametro non può essere specificato più volte. In caso contrario, verrà usato l'ultimo parametro specificato.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target-folder -d`
Percorso della cartella di destinazione in cui copiare i log. Facoltativo; per impostazione predefinita, il risultato viene creato nella cartella locale.  Questo parametro non può essere specificato più volte. In caso contrario, verrà usato l'ultimo parametro specificato. `./output/dump`
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).
