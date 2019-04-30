---
title: riferimento di configurazione del cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3a4693c5ffb68ad555d97d02f983fadf4e6bbd9a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473302"
---
# <a name="mssqlctl-cluster-config"></a>configurazione cluster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **configurazione del cluster** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[configurazione di cluster mssqlctl ottenere](#mssqlctl-cluster-config-get) | Ottenere la configurazione di cluster - kube config è necessario nel sistema.
[mssqlctl cluster config init](#mssqlctl-cluster-config-init) | Inizializza una configurazione del cluster.
[elenco di configurazione di cluster mssqlctl](#mssqlctl-cluster-config-list) | Elenca le scelte di file di configurazione disponibili.
[sezione di configurazione del cluster mssqlctl](reference-mssqlctl-cluster-config-section.md) | Comandi per l'uso con le singole sezioni del file di configurazione.
## <a name="mssqlctl-cluster-config-get"></a>configurazione di cluster mssqlctl ottenere
Ottiene il file di configurazione corrente di SQL Server Big Data del Cluster.
```bash
mssqlctl cluster config get --name -n 
                            [--output-file -f]
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome del cluster, usata per lo spazio dei nomi kubernetes.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--output-file -f`
File di output per archiviare il risultato in. Valore predefinito: indirizzati a stdout.
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
Inizializza un file di configurazione del cluster per l'utente in base al tipo di valore predefinito specificato.
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target -t`
Percorso del file di dove si desidera che il file di configurazione posizionato, il valore predefinito è cwd con custom-config. JSON.
#### `--src -s`
Configurazione origine: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
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
mssqlctl cluster config list [--config-file -f] 
                             
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--config-file -f`
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