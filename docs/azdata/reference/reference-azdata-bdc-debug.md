---
title: Informazioni di riferimento su azdata bdc debug
titleSuffix: SQL Server big data clusters
description: Usare questo articolo di riferimento per comprendere i comandi SQL dello strumento azdata, in particolare i comandi bdc debug.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e9d1f561666bf6aefdef6abf4b1daf568a5a89d8
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733816"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
| Comando | Descrizione |
| --- | --- |
[azdata bdc debug copy-logs](#azdata-bdc-debug-copy-logs) | Copia i log.
[azdata bdc debug dump](#azdata-bdc-debug-dump) | Attiva il dump della memoria.
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug copy-logs
Copia i log di debug dal cluster Big Data. È necessaria la configurazione di Kubernetes nel sistema in uso.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           
[--target-folder -d]  
                           
[--pod -p]  
                           
[--timeout -t]  
                           
[--skip-compress -sc]  
                           
[--exclude-dumps -ed]
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
#### `--skip-compress -sc`
Indica se ignorare o meno la compressione della cartella dei risultati. Il valore predefinito è False, ovvero la cartella dei risultati viene compressa.
#### `--exclude-dumps -ed`
Indica se escludere o meno i dump dalla cartella dei risultati. Il valore predefinito è False, ovvero i dump vengono inclusi.
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
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
Attiva il dump della memoria e lo copia dal contenitore. È necessaria la configurazione di Kubernetes nel sistema in uso.
```bash
azdata bdc debug dump --namespace -n 
                      [--container -c]  
                      
[--target-folder -d]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Nome del cluster Big Data, usato per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--container -c`
Contenitore di destinazione da attivare per il dump dei processi `controller` in esecuzione
#### `--target-folder -d`
Cartella di destinazione in cui copiare il dump. `./output/dump`
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
