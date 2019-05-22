---
title: riferimento dell'app mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi dell'app mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fb0bd30eb591efbf43f2a4503ce6467bf79ccd60
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993390"
---
# <a name="mssqlctl-app"></a>app mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **app** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[modello di app mssqlctl](reference-mssqlctl-app-template.md) | modelli.
[mssqlctl app init](#mssqlctl-app-init) | Kickstart nuova struttura dell'applicazione.
[creare app mssqlctl](#mssqlctl-app-create) | Creare l'applicazione.
[aggiornamento dell'app mssqlctl](#mssqlctl-app-update) | Aggiornare l'applicazione.
[elenco di app mssqlctl](#mssqlctl-app-list) | Elencare le applicazioni.
[mssqlctl app delete](#mssqlctl-app-delete) | Eliminare l'applicazione.
[esecuzione dell'app mssqlctl](#mssqlctl-app-run) | Esegui l'applicazione.
[Descrivere mssqlctl app](#mssqlctl-app-describe) | Descrivere l'applicazione.
## <a name="mssqlctl-app-init"></a>mssqlctl app init
Consente di passare a scheletro di kickstart nuova applicazione e/o file di specifiche basati sugli ambienti di runtime.
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>Esempi
Eseguire lo scaffolding di una nuova applicazione `spec.yaml` solo.
```bash
mssqlctl app init --spec
```
Eseguire lo scaffolding di una struttura di applicazione dell'applicazione R nuova basata di `r` modello.
```bash
mssqlctl app init --name reduce --template r
```
Eseguire lo scaffolding di una struttura di applicazione dell'applicazione Python nuova basata di `python` modello.
```bash
mssqlctl app init --name reduce --template python
```
Eseguire lo scaffolding di una struttura di applicazione dell'applicazione SSIS nuova basata di `ssis` modello.
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--spec -s`
Generare solo un spec.yaml dell'applicazione.
#### `--name -n`
Nome applicazione
#### `--version -v`
Versione dell'applicazione.
#### `--template -t`
Nome del modello. Per un elenco completo di disattivare i nomi dei modelli supportati eseguire `mssqlctl app template list`
#### `--destination -d`
Posizione in cui posizionare lo scheletro dell'applicazione. Valore predefinito: directory di lavoro corrente.
#### `--url -u`
Specificare un percorso del repository di modelli diversi. Valore predefinito: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-create"></a>creare app mssqlctl
Creare un'applicazione.
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>Esempi
Creare una nuova applicazione da una directory che contiene una specifica distribuzione spec.yaml valido.
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--spec -s`
Percorso di una directory con un file YAML delle specifiche che descrive l'applicazione.
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
## <a name="mssqlctl-app-update"></a>aggiornamento dell'app mssqlctl
Aggiornare un'applicazione.
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>Esempi
Aggiornare un'applicazione esistente da una directory che contiene una specifica distribuzione spec.yaml valido.
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--spec -s`
Percorso di una directory con un file YAML delle specifiche che descrive l'applicazione.
#### `--yes -y`
Non chiedere conferma quando si aggiorna un'applicazione dal file spec.yaml del CWD.
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
## <a name="mssqlctl-app-list"></a>elenco di app mssqlctl
Elencare un'applicazione o le applicazioni.,
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>Esempi
Applicazione di elenco per nome e versione.
```bash
mssqlctl app list --name reduce  --version v1
```
Elencare tutte le versioni dell'applicazione in base al nome.
```bash
mssqlctl app list --name reduce
```
Elencare tutte le versioni dell'applicazione in base al nome.
```bash
mssqlctl app list
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome applicazione
#### `--version -v`
Versione dell'applicazione.
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
## <a name="mssqlctl-app-delete"></a>mssqlctl app delete
Eliminare un'applicazione.
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>Esempi
Eliminare l'applicazione per nome e versione.
```bash
mssqlctl app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome applicazione
#### `--version -v`
Versione dell'applicazione.
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
## <a name="mssqlctl-app-run"></a>esecuzione dell'app mssqlctl
Eseguire un'applicazione.
```bash
mssqlctl app run --name -n 
                 --version -v  
                 [--inputs]
```
### <a name="examples"></a>Esempi
Eseguire l'applicazione senza parametri di input.
```bash
mssqlctl app run --name reduce --version v1
```
Eseguire l'applicazione con 1 parametro di input.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
Esegui l'applicazione con più parametri di input.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome applicazione
#### `--version -v`
Versione dell'applicazione.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--inputs`
I parametri in un file CSV di input applicazione `name=value` formato.
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
## <a name="mssqlctl-app-describe"></a>Descrivere mssqlctl app
Descrivere un'applicazione.
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>Esempi
Descrivere l'applicazione.
```bash
mssqlctl app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--spec -s`
Percorso di una directory con un file YAML delle specifiche che descrive l'applicazione.
#### `--name -n`
Nome applicazione
#### `--version -v`
Versione dell'applicazione.
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