---
title: riferimento di debug mssqlctl cluster
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di debug di mssqlctl cluster.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4eafc3838d153a2616e34e98aed041374c04292d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779397"
---
# <a name="mssqlctl-cluster-debug"></a>debug cluster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **debug cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[mssqlctl cluster debug-log di copia](#mssqlctl-cluster-debug-copy-logs) | Copiare i log.
[dump del debug mssqlctl cluster](#mssqlctl-cluster-debug-dump) | Dump di registrazione di trigger.
## <a name="mssqlctl-cluster-debug-copy-logs"></a>mssqlctl cluster debug-log di copia
Copiare i log di debug dal cluster: configurazione di kube è necessaria nel sistema.
```bash
mssqlctl cluster debug copy-logs --namespace -n 
                                 [--container -c]  
                                 [--target-folder -d]  
                                 [--pod -p]  
                                 [--timeout -t]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Nome del cluster, usata per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--container -c`
Copiare i log per i contenitori con nome simile, facoltativo, per impostazione predefinita la copia dei log per tutti i contenitori. Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare
#### `--target-folder -d`
Percorso della cartella di destinazione per copiare i registri per. Facoltativo, per impostazione predefinita viene creato il risultato nella cartella locale.  Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare
#### `--pod -p`
Copiare i log per i POD con nome simile. Facoltativo, per i log di copia predefinita per tutti i POD. Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare
#### `--timeout -t`
Il numero di secondi di attesa per il completamento del comando. Il valore predefinito è 0 che è illimitato
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.
## <a name="mssqlctl-cluster-debug-dump"></a>dump del debug mssqlctl cluster
Attivare i dump di registrazione e copiarlo dal contenitore: configurazione di kube è necessaria nel sistema.
```bash
mssqlctl cluster debug dump --namespace -n 
                            --container -c  
                            [--target-folder -d]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--namespace -n`
Nome del cluster, usata per lo spazio dei nomi kubernetes.
#### `--container -c`
Copiare i log per i contenitori con nome simile, facoltativo, per impostazione predefinita la copia dei log per tutti i contenitori. Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target-folder -d`
Percorso della cartella di destinazione per copiare i registri per. Facoltativo, per impostazione predefinita viene creato il risultato nella cartella locale.  Non è possibile specificare più volte. Se è specificato più volte, ultimo uno da utilizzare `./output/dump`
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).