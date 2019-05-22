---
title: riferimento di configurazione del cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 984a3c50ac691df3759edc161baabc533bd9456f
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993340"
---
# <a name="mssqlctl-cluster-config"></a>configurazione cluster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **configurazione del cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[show config di mssqlctl cluster](#mssqlctl-cluster-config-show) | Ottiene la configurazione corrente di SQL Server Big Data del Cluster.
[mssqlctl cluster config init](#mssqlctl-cluster-config-init) | Consente di inizializzare creare un profilo di configurazione del cluster che può essere utilizzato con il cluster.
[elenco di configurazione di cluster mssqlctl](#mssqlctl-cluster-config-list) | Elenca le scelte di file di configurazione disponibili.
[sezione di configurazione del cluster mssqlctl](reference-mssqlctl-cluster-config-section.md) | Comandi per l'utilizzo di diverse sezioni del file di configurazione del cluster.
## <a name="mssqlctl-cluster-config-show"></a>show config di mssqlctl cluster
Ottiene il file di configurazione corrente di SQL Server Big Data del Cluster e lo invia al file di destinazione o piuttosto lo stampa nella console.
```bash
mssqlctl cluster config show [--target -t] 
                             [--force -f]
```
### <a name="examples"></a>Esempi
Mostra file di configurazione del cluster nella console di
```bash
mssqlctl cluster config show
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target -t`
File di output per archiviare il risultato in. Valore predefinito: indirizzati a stdout.
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
## <a name="mssqlctl-cluster-config-init"></a>mssqlctl cluster config init
Consente di inizializzare creare un profilo di configurazione del cluster che può essere utilizzato con il cluster. Gli argomenti da 3 scelte, è possibile specificare l'origine specifica del profilo di configurazione.
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]  
                             [--force -f]
```
### <a name="examples"></a>Esempi
PGO esperienza init di configurazione del cluster - si riceveranno istruzioni per i valori necessari.
```bash
mssqlctl cluster config init
```
Init di configurazione con gli argomenti del cluster, viene creato un profilo di configurazione del servizio contenitore di Azure-dev-test in. / custom.json.
```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target -t`
Percorso del file di dove si desidera che il profilo di configurazione posizionato, il valore predefinito è cwd con custom-config. JSON.
#### `--src -s`
Origine del profilo di configurazione: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
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
## <a name="mssqlctl-cluster-config-list"></a>elenco di configurazione di cluster mssqlctl
Vengono elencate le opzioni di file di configurazione disponibili per l'uso nel cluster config init
```bash
mssqlctl cluster config list [--config-file -c] 
                             
```
### <a name="examples"></a>Esempi
Mostra tutti i nomi dei profili di configurazione disponibili.
```bash
mssqlctl cluster config list
```
Mostra json di un profilo di configurazione specifica.
```bash
mssqlctl cluster config list --config-file aks-dev-test.json
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--config-file -c`
File di configurazione predefinito: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
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