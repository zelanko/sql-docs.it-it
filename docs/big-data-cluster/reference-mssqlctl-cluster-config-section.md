---
title: riferimento di sezione Configurazione cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di sezione mssqlctl cluster config.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5a793e7d0fcaf782a09a4981491ef0a8d90ab5a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759138"
---
# <a name="mssqlctl-cluster-config-section"></a>sezione configurazione cluster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **sezione di configurazione del cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[sezione di configurazione del cluster mssqlctl ottenere](#mssqlctl-cluster-config-section-get) | Ottiene una sezione da un file di configurazione.
[gruppo di sezione di configurazione di cluster mssqlctl](#mssqlctl-cluster-config-section-set) | Imposta una sezione per un file di configurazione.
## <a name="mssqlctl-cluster-config-section-get"></a>sezione di configurazione del cluster mssqlctl ottenere
Ottiene la sezione specificata nel file di configurazione selezionato in base al percorso json specificato.
```bash
mssqlctl cluster config section get --json-path -j 
                                    --config-file -f  
                                    [--target -t]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--json-path -j`
Il percorso json che comporta la sezione o il valore desiderato dal file di configurazione, vale a dire key1.key2.key3. Usa il linguaggio di query jsonpath https://github.com/h2non/jsonpath-ng, ad esempio: -j ' $. spec.pools [? ( @.spec.type = = "Master")]... degli endpoint
#### `--config-file -f`
Percorso del file di configurazione del cluster.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target -t`
Percorso del file di dove si desidera che il file sezione inserito.
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
## <a name="mssqlctl-cluster-config-section-set"></a>gruppo di sezione di configurazione di cluster mssqlctl
Imposta la sezione specificata nel file di configurazione selezionato in base al percorso json specificato.
```bash
mssqlctl cluster config section set --config-file -f 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--config-file -f`
Percorso di file di configurazione di cluster di file di configurazione da impostare
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--json-values -j`
Un elenco di coppie di valore della chiave di percorsi json per i valori: key1.subkey1=value1,key2.subkey2=value2. È possibile fornire inline valori json, ad esempio: key ='{"tipo": "cluster", "name": "test-cluster"}' oppure specificare un percorso di file, ad esempio key=./values.json
#### `--patch-file -p`
Percorso di un file di patch json che si basa la libreria di jsonpatch e jsonpath: https://github.com/stefankoegl/python-json-patch , https://github.com/h2non/jsonpath-ng -un semplice esempio: {"patch": [{"op": "Aggiungi", "path": "metadata.name", "value": "test"}, {"op": "Aggiungi", "path": "metadata.array", "value": [1, 2, 3]}]} . Includere la chiave "patch" e ha il valore da una matrice delle patch che si intende eseguire.  Verrà eseguito di conseguenza. Un esempio più complesso: {"patch": [{"op": "replace", "path": "$. spec.pools [? ( @.spec.type = = 'Master')]... endpoint di","value": {"name": "Nuovo Endpoint"}}]}
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