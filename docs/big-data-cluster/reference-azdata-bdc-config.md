---
title: informazioni di riferimento sulla configurazione BDC azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed777391af3695da69e04c0e2693cff912c76771
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426291"
---
# <a name="azdata-bdc-config"></a>azdata configurazione BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi di **configurazione di integrazione applicativa** dei dati nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[init configurazione BDC azdata](#azdata-bdc-config-init) | Inizializza un profilo di configurazione del cluster di Big data che può essere usato con la creazione del cluster.
[azdata elenco di configurazione BDC](#azdata-bdc-config-list) | Elenca le scelte del profilo di configurazione disponibili.
[visualizzazione configurazione BDC azdata](#azdata-bdc-config-show) | Mostra la configurazione corrente di BDC o la configurazione di un file locale specificato, ovvero Custom/cluster. JSON.
[Aggiunta configurazione BDC azdata](#azdata-bdc-config-add) | Aggiungere un valore per un percorso JSON in un file di configurazione.
[rimozione configurazione BDC azdata](#azdata-bdc-config-remove) | Rimuovere un valore per un percorso JSON in un file di configurazione.
[sostituzione configurazione BDC azdata](#azdata-bdc-config-replace) | Sostituire un valore per un percorso JSON in un file di configurazione.
[patch di configurazione BDC azdata](#azdata-bdc-config-patch) | Patch di un file di configurazione in base a un file di patch JSON.
## <a name="azdata-bdc-config-init"></a>init configurazione BDC azdata
Inizializza un profilo di configurazione del cluster di Big data che può essere usato con la creazione del cluster. È possibile specificare l'origine specifica del profilo di configurazione negli argomenti da 3 scelte.
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Esempi
Esperienza di configurazione di integrazione applicativa dei dati
```bash
azdata bdc config init
```
Configurazione BDC init con argomenti, crea un profilo di configurazione di AKS-dev-test in./Custom.
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target -t`
Percorso del file in cui si vuole inserire il profilo di configurazione. il valore predefinito è CWD con Custom-config. JSON.
#### `--source -s`
Origine del profilo di configurazione: [' AKS-dev-test ',' kubeadm-dev-test ',' minikube-dev-test ']
#### `--force -f`
Forza la sovrascrittura del file di destinazione.
#### `--accept-eula -a`
Si accettano le condizioni di licenza? [Sì/No]. Se non si vuole usare questo arg, è possibile impostare la variabile di ambiente ACCEPT_EULA su "Yes". Le condizioni di licenza per questo prodotto possono essere visualizzate https://aka.ms/azdata-eula all'indirizzo.
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
## <a name="azdata-bdc-config-list"></a>azdata elenco di configurazione BDC
Elenca le scelte del profilo di configurazione disponibili per l'uso in`bdc config init`
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Esempi
Mostra tutti i nomi dei profili di configurazione disponibili.
```bash
azdata bdc config list
```
Mostra JSON di un profilo di configurazione specifico.
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--config-profile -c`
Profilo di configurazione predefinito: [' AKS-dev-test ',' kubeadm-dev-test ',' minikube-dev-test ']
#### `--type -t`
Il tipo di configurazione che si desidera visualizzare.
`cluster`
#### `--accept-eula -a`
Si accettano le condizioni di licenza? [Sì/No]. Se non si vuole usare questo arg, è possibile impostare la variabile di ambiente ACCEPT_EULA su "Yes". Le condizioni di licenza per questo prodotto possono essere visualizzate https://aka.ms/azdata-eula all'indirizzo.
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
## <a name="azdata-bdc-config-show"></a>visualizzazione configurazione BDC azdata
Mostra la configurazione corrente di BDC o la configurazione di un file locale specificato, ovvero Custom/cluster. JSON. Il comando può inoltre assumere un percorso JSON se si desidera ottenere solo una sezione.  È anche possibile specificare un file di destinazione in cui eseguire l'output.  Se non si specifica un file di destinazione, verrà semplicemente restituito al terminale.
```bash
azdata bdc config show [--config-file -c] 
                       [--target -t]  
                       [--json-path -j]  
                       [--force -f]
```
### <a name="examples"></a>Esempi
Mostra la configurazione di integrazione applicativa dei dati nella console
```bash
azdata bdc config show
```
In un file di configurazione locale ottenere un valore alla fine di un semplice percorso della chiave JSON.
```bash
azdata bdc config show --config-file custom-config/cluster.json --json-path 'metadata.name' --target section.json
```
In un file di configurazione locale, ottiene un valore alla fine di un percorso della chiave JSON con un oggetto condizionale
```bash
azdata bdc config show --config-file custom-config/cluster.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--config-file -c`
Percorso del file di configurazione del cluster di Big data se non si vuole che la configurazione del cluster a cui si currentlylogged, ad esempio Custom/cluster. JSON
#### `--target -t`
File di output in cui archiviare il risultato. Impostazione predefinita: indirizzato a stdout.
#### `--json-path -j`
Il percorso della chiave JSON che conduce alla sezione o al valore desiderato dalla configurazione, ad esempio Key1. Key2. Key3. Usa il linguaggio di query jsonpath https://jsonpath.com/ ,, ad esempio:-j ' $. spec. Pools [? ( @.spec.type = = "Master")].. endpoint
#### `--force -f`
Forza la sovrascrittura del file di destinazione.
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
## <a name="azdata-bdc-config-add"></a>Aggiunta configurazione BDC azdata
Aggiunge il valore nel percorso JSON nel file config.  Tutti gli esempi riportati di seguito sono forniti in bash.  Se si utilizza un'altra riga di comando, tenere presente che potrebbe essere necessario escapequotations in modo appropriato.  In alternativa, è possibile usare la funzionalità file di patch.
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>Esempi
Ex 1: aggiungere un archivio del piano di controllo.
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--config-file -c`
Percorso del file di configurazione del cluster di Big Data della configurazione che si vuole impostare, ad esempio Custom/cluster. JSON
#### `--json-values -j`
Elenco di coppie chiave-valore dei percorsi JSON dei valori: key1. SubKey1 = value1, Key2. SubKey2 = value2. È possibile specificare valori JSON inline quali: Key =' {"Kind": "cluster", "Name": "test-cluster"} "o fornire un percorso di file, ad esempio Key =./Values.JSON. Add non supporta le istruzioni condizionali.  Per esempi http://jsonpatch.com/ relativi all'aspetto del percorso, vedere.  Se si desidera accedere a una matrice, è necessario indicare l'indice, ad esempio Key. 0 = value
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
## <a name="azdata-bdc-config-remove"></a>rimozione configurazione BDC azdata
Rimuove il valore nel percorso JSON nel file config.  Tutti gli esempi riportati di seguito sono forniti in bash.  Se si utilizza un'altra riga di comando, tenere presente che potrebbe essere necessario escapequotations in modo appropriato.  In alternativa, è possibile usare la funzionalità file di patch.
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>Esempi
Ex 1: rimuovere l'archiviazione del piano di controllo.
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--config-file -c`
Percorso del file di configurazione del cluster di Big Data della configurazione che si vuole impostare, ad esempio Custom/cluster. JSON
#### `--json-path -j`
Elenco di percorsi JSON basati sulla libreria jsonpatch che indica i valori da rimuovere, ad esempio: key1. SubKey1, Key2. SubKey2. Remove non supporta le istruzioni condizionali. Per esempi http://jsonpatch.com/ relativi all'aspetto del percorso, vedere.  Se si desidera accedere a una matrice, è necessario indicare l'indice, ad esempio Key. 0 = value
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
## <a name="azdata-bdc-config-replace"></a>sostituzione configurazione BDC azdata
Sostituisce il valore in corrispondenza del percorso JSON nel file config.  Tutti i examplesbelow vengono forniti in bash.  Se si utilizza un'altra riga di comando, tenere presente che potrebbe essere necessario escapequotations in modo appropriato.  In alternativa, è possibile usare la funzionalità file di patch.
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>Esempi
Ex 1: sostituire la porta di un singolo endpoint (endpoint controller).
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Ex 2: sostituire l'archiviazione del piano di controllo.
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ex 3: sostituire lo spazio di archiviazione del pool, incluse le repliche (pool di archiviazione).
```bash
azdata bdc config replace --config-file custom/cluster.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--config-file -c`
Percorso del file di configurazione del cluster di Big Data della configurazione che si vuole impostare, ad esempio Custom/cluster. JSON
#### `--json-values -j`
Elenco di coppie chiave-valore dei percorsi JSON dei valori: key1. SubKey1 = value1, Key2. SubKey2 = value2. È possibile specificare valori JSON inline quali: Key =' {"Kind": "cluster", "Name": "test-cluster"} "o fornire un percorso di file, ad esempio Key =./Values.JSON. Replace supporta le istruzioni condizionali tramite la libreria jsonpath.  Per usarlo, avviare il percorso con $. Ciò consentirà di eseguire un'operazione condizionale, ad esempio-j $. Key1. Key2 [? ( @.key3= =' SomeValue ']. key4 = value. È possibile visualizzare gli esempi seguenti. Per ulteriori informazioni, vedere: https://jsonpath.com/
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
## <a name="azdata-bdc-config-patch"></a>patch di configurazione BDC azdata
Patch il file di configurazione in base al file di patch specificato. Per comprendere http://jsonpatch.com/ meglio le modalità di composizione dei percorsi, vedere. L'operazione Replace può utilizzare le istruzioni condizionali nel percorso a causa della libreria https://jsonpath.com/ jsonpath. Tutti i file JSON della patch devono iniziare con una chiave "patch" con una matrice di patch con la relativa op (Add, Replace, Remove), il percorso e il valore corrispondenti. L'operazione "Remove" non richiede un valore, ma solo un percorso. Vedere gli esempi seguenti.
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>Esempi
Ex 1: sostituire la porta di un singolo endpoint (endpoint controller) con il file di patch.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Ex 2: sostituire l'archiviazione del piano di controllo con il file di patch.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3: sostituire lo spazio di archiviazione del pool, incluse le repliche (pool di archiviazione) con file di correzione.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--config-file -c`
Percorso del file di configurazione del cluster di Big Data della configurazione che si vuole impostare, ad esempio Custom/cluster. JSON
#### `--patch-file -p`
Percorso di un file JSON patch basato sulla libreria jsonpatch: http://jsonpatch.com/. È necessario avviare il file JSON della patch con una chiave denominata "patch", il cui valore è una matrice di operazioni di patch che si intende eseguire. Per il percorso di un'operazione patch, è possibile usare la notazione del punto, ad esempio Key1. Key2 per la maggior parte delle operazioni. Se si vuole eseguire un'operazione di sostituzione e si sostituisce un valore in una matrice che richiede un condizionale, usare la notazione jsonpath iniziando il percorso con $. Ciò consentirà di eseguire una condizione condizionale, ad esempio $. Key1. Key2 [? ( @.key3= =' SomeValue ']. key4. Vedere gli esempi seguenti. Per ulteriori informazioni sulle condizioni, vedere: https://jsonpath.com/.
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