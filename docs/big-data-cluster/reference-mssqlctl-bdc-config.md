---
title: riferimento di configurazione di integrazione applicativa dei dati mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di mssqlctl integrazione applicativa dei dati.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f6aee38bd11d226ba324153b76c750ba57eb9fb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958171"
---
# <a name="mssqlctl-bdc-config"></a>configurazione di integrazione applicativa dei dati mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **configurazione di integrazione applicativa dei dati** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[mssqlctl bdc config show](#mssqlctl-bdc-config-show) | Ottiene la Big Data configurazione del Cluster corrente.
[init di config mssqlctl integrazione applicativa dei dati](#mssqlctl-bdc-config-init) | Inizializza un Cluster di grandi dimensioni dati Crea profilo di configurazione che può essere utilizzato con il cluster.
[elenco di configurazione di integrazione applicativa dei dati mssqlctl](#mssqlctl-bdc-config-list) | Elenca le scelte del profilo di configurazione disponibili.
[sezione di configurazione di integrazione applicativa dei dati mssqlctl](reference-mssqlctl-bdc-config-section.md) | Comandi per l'utilizzo di diverse sezioni del profilo di configurazione del Cluster di Big Data.
## <a name="mssqlctl-bdc-config-show"></a>mssqlctl bdc config show
Ottiene il profilo di configurazione corrente del Cluster Big Data e lo invia a directory di destinazione o piuttosto lo stampa nella console.
```bash
mssqlctl bdc config show [--target -t] 
                         [--force -f]
```
### <a name="examples"></a>Esempi
Mostra la configurazione di integrazione applicativa dei dati nella console di
```bash
mssqlctl bdc config show
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target -t`
File di output per archiviare il risultato in. Valore predefinito: indirizzati a stdout.
#### `--force -f`
Forzare la sovrascrittura del file di destinazione.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
## <a name="mssqlctl-bdc-config-init"></a>init di config mssqlctl integrazione applicativa dei dati
Inizializza un Cluster di grandi dimensioni dati Crea profilo di configurazione che può essere utilizzato con il cluster. Gli argomenti da 3 scelte, è possibile specificare l'origine specifica del profilo di configurazione.
```bash
mssqlctl bdc config init [--target -t] 
                         [--source -s]  
                         [--force -f]
```
### <a name="examples"></a>Esempi
Esperienza guidata integrazione applicativa dei dati config init - si riceveranno istruzioni per i valori necessari.
```bash
mssqlctl bdc config init
```
Init di configurazione di integrazione applicativa dei dati con gli argomenti, crea un profilo di configurazione del servizio contenitore di Azure-dev-test in. / personalizzate.
```bash
mssqlctl bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--target -t`
Percorso del file di dove si desidera che il profilo di configurazione posizionato, il valore predefinito è cwd con custom-config. JSON.
#### `--source -s`
Origine del profilo di configurazione: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--force -f`
Forzare la sovrascrittura del file di destinazione.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
## <a name="mssqlctl-bdc-config-list"></a>elenco di configurazione di integrazione applicativa dei dati mssqlctl
Vengono elencate le opzioni di profilo di configurazione disponibili per l'utilizzo in `bdc config init`
```bash
mssqlctl bdc config list [--config-profile -c] 
                         
```
### <a name="examples"></a>Esempi
Mostra tutti i nomi dei profili di configurazione disponibili.
```bash
mssqlctl bdc config list
```
Mostra json di un profilo di configurazione specifica.
```bash
mssqlctl bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--config-profile -c`
Profilo di configurazione predefinito: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).