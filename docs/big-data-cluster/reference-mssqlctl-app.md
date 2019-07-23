---
title: riferimento all'app mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi dell'app mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0df3e9ca007fb6546310236f4c23d1775687cc5
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388393"
---
# <a name="mssqlctl-app"></a>app mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per i comandi dell' **app** nello strumento **mssqlctl** . Per ulteriori informazioni su altri comandi **mssqlctl** , vedere [riferimento mssqlctl](reference-mssqlctl.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[modello di app mssqlctl](reference-mssqlctl-app-template.md) | Modelli.
[mssqlctl app init](#mssqlctl-app-init) | Avvia la nuova ossatura dell'applicazione.
[creazione dell'app mssqlctl](#mssqlctl-app-create) | Creare un'applicazione.
[aggiornamento dell'app mssqlctl](#mssqlctl-app-update) | Aggiornare l'applicazione.
[elenco di app mssqlctl](#mssqlctl-app-list) | Elencare le applicazioni.
[eliminazione dell'app mssqlctl](#mssqlctl-app-delete) | Eliminare l'applicazione.
[esecuzione dell'app mssqlctl](#mssqlctl-app-run) | Eseguire l'applicazione.
[Descrizione dell'app mssqlctl](#mssqlctl-app-describe) | Descrivere l'applicazione.
## <a name="mssqlctl-app-init"></a>mssqlctl app init
Consente di eseguire il Kickstart dei nuovi file di scheletro e/o speci dell'applicazione basati su ambienti di Runtime.
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>Esempi
Impalcatura di una `spec.yaml` nuova applicazione.
```bash
mssqlctl app init --spec
```
Impalcatura di un nuovo scheletro dell'applicazione R `r` basato sul modello.
```bash
mssqlctl app init --name reduce --template r
```
Impalcatura di una nuova ossatura dell'applicazione Python `python` basata sul modello.
```bash
mssqlctl app init --name reduce --template python
```
Impalcatura di una nuova ossatura dell'applicazione SSIS `ssis` basata sul modello.
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--spec -s`
Generare solo un'applicazione spec. yaml.
#### `--name -n`
Nome applicazione
#### `--version -v`
Versione dell'applicazione.
#### `--template -t`
Nome del modello. Per un elenco completo dei nomi di modello supportati, eseguire`mssqlctl app template list`
#### `--destination -d`
Posizione in cui posizionare la struttura dell'applicazione. Impostazione predefinita: directory di lavoro corrente.
#### `--url -u`
Specificare un percorso del repository di modelli diverso. Predefinita https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-create"></a>creazione dell'app mssqlctl
Creare un'applicazione.
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>Esempi
Creare una nuova applicazione da una directory contenente una specifica di distribuzione di spec. YAML valida.
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--spec -s`
Percorso di una directory con un file di specifica YAML che descrive l'applicazione.
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
## <a name="mssqlctl-app-update"></a>aggiornamento dell'app mssqlctl
Aggiornare un'applicazione.
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>Esempi
Aggiornare un'applicazione esistente da una directory contenente una specifica di distribuzione di spec. YAML valida.
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--spec -s`
Percorso di una directory con un file di specifica YAML che descrive l'applicazione.
#### `--yes -y`
Non richiedere conferma quando si aggiorna un'applicazione dal file spec. YAML di CWD.
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
## <a name="mssqlctl-app-list"></a>elenco di app mssqlctl
Elencare un'applicazione o le applicazioni.
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>Esempi
Elencare l'applicazione in base al nome e alla versione.
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
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  Valori consentiti: JSON, jsonc, Table, TSV.  Impostazione predefinita: JSON.
#### `--query -q`
Stringa di query JMESPath. Per [http://jmespath.org/](http://jmespath.org/]) ulteriori informazioni ed esempi, vedere.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
## <a name="mssqlctl-app-delete"></a>eliminazione dell'app mssqlctl
Eliminare un'applicazione.
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>Esempi
Elimina l'applicazione in base al nome e alla versione.
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
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  Valori consentiti: JSON, jsonc, Table, TSV.  Impostazione predefinita: JSON.
#### `--query -q`
Stringa di query JMESPath. Per [http://jmespath.org/](http://jmespath.org/]) ulteriori informazioni ed esempi, vedere.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
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
Eseguire un'applicazione con più parametri di input.
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
Parametri di input dell'applicazione in `name=value` formato CSV.
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
## <a name="mssqlctl-app-describe"></a>Descrizione dell'app mssqlctl
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
Percorso di una directory con un file di specifica YAML che descrive l'applicazione.
#### `--name -n`
Nome applicazione
#### `--version -v`
Versione dell'applicazione.
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

Per ulteriori informazioni su altri comandi **mssqlctl** , vedere [riferimento mssqlctl](reference-mssqlctl.md). Per altre informazioni su come installare lo strumento **mssqlctl** , vedere [Install mssqlctl to manage SQL Server 2019 Big Data Clusters](deploy-install-mssqlctl.md).