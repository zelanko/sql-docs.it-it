---
title: riferimento al debug BDC azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di debug BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38c327287273ae6596326d88d9e0d67c8e014d47
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426231"
---
# <a name="azdata-bdc-debug"></a>debug BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi di **debug BDC** nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata di debug BDC-log di copia](#azdata-bdc-debug-copy-logs) | Copiare i log.
[dump del debug BDC azdata](#azdata-bdc-debug-dump) | Attivare il dump della registrazione.
## <a name="azdata-bdc-debug-copy-logs"></a>azdata di debug BDC-log di copia
Copiare i log di debug dal cluster di Big Data-la configurazione KUBE è necessaria nel sistema.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Nome del cluster di Big Data usato per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--container -c`
Copiare i log per i contenitori con nome simile, facoltativo, per impostazione predefinita copia i log per tutti i contenitori. Non può essere specificato più volte. Se specificato più volte, verrà utilizzato l'ultimo
#### `--target-folder -d`
Percorso della cartella di destinazione in cui copiare i log. Facoltativo, per impostazione predefinita crea il risultato nella cartella locale.  Non può essere specificato più volte. Se specificato più volte, verrà utilizzato l'ultimo
#### `--pod -p`
Copiare i log per i pod con un nome simile. Facoltativo, per impostazione predefinita copia i log per tutti i pod. Non può essere specificato più volte. Se specificato più volte, verrà utilizzato l'ultimo
#### `--timeout -t`
Numero di secondi di attesa per il completamento del comando. Il valore predefinito è 0, che è illimitato
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
## <a name="azdata-bdc-debug-dump"></a>dump del debug BDC azdata
Attivare il dump della registrazione e copiarlo dalla configurazione di container-KUBE è necessario nel sistema.
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Nome del cluster di Big Data usato per lo spazio dei nomi kubernetes.
#### `--container -c`
Copiare i log per i contenitori con nome simile, facoltativo, per impostazione predefinita copia i log per tutti i contenitori. Non può essere specificato più volte. Se specificato più volte, verrà utilizzato l'ultimo
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target-folder -d`
Percorso della cartella di destinazione in cui copiare i log. Facoltativo, per impostazione predefinita crea il risultato nella cartella locale.  Non può essere specificato più volte. Se specificato più volte, verrà utilizzato l'ultimo`./output/dump`
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

Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento **azdata** , vedere [Install azdata to manage SQL Server 2019 Big Data Clusters](deploy-install-azdata.md).
