---
title: riferimento di sezione Configurazione cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di sezione mssqlctl cluster config.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e0c4f543f349d166962e65ea91338595d25308ce
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800962"
---
# <a name="mssqlctl-cluster-config-section"></a>sezione configurazione cluster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **sezione di configurazione del cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[presentazione di sezione Configurazione cluster mssqlctl](#mssqlctl-cluster-config-section-show) | Ottiene una sezione da un file di configurazione.
[gruppo di sezione di configurazione di cluster mssqlctl](#mssqlctl-cluster-config-section-set) | Imposta una sezione per un file di configurazione.
## <a name="mssqlctl-cluster-config-section-show"></a>presentazione di sezione Configurazione cluster mssqlctl
Ottiene la sezione specificata nel file di configurazione selezionato in base al percorso json specificato.
```bash
mssqlctl cluster config section show --json-path -j 
                                     --config-file -c  
                                     [--target -t]  
                                     [--force -f]
```
### <a name="examples"></a>Esempi
Ottiene un valore alla fine del percorso di una chiave json semplice.
```bash
mssqlctl cluster config section show --config-file custom-config.json --json-path 'metadata.name' --target section.json
```
Ottiene un valore alla fine di un percorso di chiave json con un'istruzione condizionale
```bash
mssqlctl cluster config section show --config-file custom-config.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--json-path -j`
Il percorso json che comporta la sezione o il valore desiderato dal file di configurazione, vale a dire key1.key2.key3. Usa il linguaggio di query jsonpath https://github.com/h2non/jsonpath-ng, ad esempio: -j ' $. spec.pools [? ( @.spec.type = = "Master")]... degli endpoint
#### `--config-file -c`
Percorso del file di configurazione del cluster.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target -t`
Percorso del file di dove si desidera che il file sezione inserito. Valore predefinito: indirizzati a stdout.
#### `--force -f`
Forzare la sovrascrittura del file di destinazione.
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
Imposta la sezione specificata nel file di configurazione selezionato in base al percorso json specificato.  Examplesbelow tutti sono espressi in Bash.  Se si usa un'altra riga di comando, tenere presente che potrebbe essere necessario escapequotations in modo appropriato.  In alternativa, è possibile usare la funzionalità di file di patch.
```bash
mssqlctl cluster config section set --config-file -c 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="examples"></a>Esempi
Ad esempio, 1 (inline) - impostazione della porta di un singolo endpoint (Endpoint Controller).
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values '$.spec.controlPlane.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Ad esempio, 1 (patch): impostare la porta di un singolo endpoint (Endpoint Controller) con file di patch.
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Ad esempio, 2 (inline) - archiviazione piano dei Set di controllo.
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values 'spec.controlPlane.spec.storage=spec.controlPlane.spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ad esempio, 2 (patch): archiviazione di piano di controllo di Set con file di patch.
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"spec.controlPlane.spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3(inline) - impostare l'archiviazione del pool, inclusi le repliche (Pool di archiviazione).
```bash
mssqlctl cluster config section set --config-file custom-config.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
Ad esempio, 3 (patch): impostare archiviazione pool, incluse le repliche (Pool di archiviazione) con file di patch.
```bash
mssqlctl cluster config section set --config-file custom-config.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--config-file -c`
Percorso di file di configurazione di cluster di file di configurazione da impostare
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--json-values -j`
Un elenco di coppie di valore della chiave di percorsi json per i valori: key1.subkey1=value1,key2.subkey2=value2. È possibile fornire inline valori json, ad esempio: key ='{"tipo": "cluster", "name": "test-cluster"}' oppure specificare un percorso di file, ad esempio key=./values.json. Se si desidera impostare un valore che richiede un'istruzione condizionale, usare la notazione jsonpath da cui iniziare il percorso con un carattere $. In questo modo sarà possibile eseguire un'istruzione condizionale, ad esempio -j $. key1.key2 [? ( @.key3= = 'someValue'] .key4 = valore. È possibile riscontrare esempi riportati di seguito. Per altre informazioni, vedere: https://jsonpath.com/
#### `--patch-file -p`
Percorso di un file di patch json che si basa la libreria jsonpatch: http://jsonpatch.com/. È necessario avviare il file di patch json con una chiave denominata "patch", il cui valore è una matrice di operazioni patch che si intende eseguire. Per il percorso di un'operazione patch, è possibile usare la notazione, ad esempio key1.key2 per la maggior parte delle operazioni. Se si vuole eseguire un'operazione di sostituzione e si sostituisce un valore in una matrice che richiede un'istruzione condizionale, usare la notazione jsonpath da cui iniziare il percorso con un carattere $. In questo modo sarà possibile eseguire un'istruzione condizionale, ad esempio $. key1.key2 [? ( @.key3= = 'someValue'] .key4. Vedere gli esempi seguenti. Per altre informazioni, vedere: https://jsonpath.com/.
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