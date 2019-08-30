---
title: Informazioni di riferimento su azdata app
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata app.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ec7e461705138905713b803e2f0f96934044d971
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155299"
---
# <a name="azdata-app"></a>azdata app

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

Questo articolo è un articolo di riferimento per **azdata**. 

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata app template](reference-azdata-app-template.md) | Modelli.
[azdata app init](#azdata-app-init) | Avvia un nuovo scheletro dell'applicazione.
[azdata app create](#azdata-app-create) | Crea un'applicazione.
[azdata app update](#azdata-app-update) | Aggiorna un'applicazione.
[azdata app list](#azdata-app-list) | Elenca le applicazioni.
[azdata app delete](#azdata-app-delete) | Elimina un'applicazione.
[azdata app run](#azdata-app-run) | Esegue un'applicazione.
[azdata app describe](#azdata-app-describe) | Descrive un'applicazione.
## <a name="azdata-app-init"></a>azdata app init
Consente di avviare lo scheletro di una nuova applicazione e/o file specifici basati su ambienti di runtime.
```bash
azdata app init 
```
### <a name="examples"></a>Esempi
Eseguire lo scaffolding solo di una nuova applicazione `spec.yaml`.
```bash
azdata app init --spec
```
Impalcatura di una nuova ossatura dell'applicazione R basata `r` sul modello.
```bash
azdata app init --name reduce --template r
```
Impalcatura di una nuova applicazione Python applicazione basata sul `python` modello.
```bash
azdata app init --name reduce --template python
```
Impalcatura di una nuova struttura di applicazione SSIS basata `ssis` sul modello.
```bash
azdata app init --name reduce --template ssis            
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-app-create"></a>azdata app create
Crea un'applicazione.
```bash
azdata app create 
```
### <a name="examples"></a>Esempi
Creare una nuova applicazione da una directory contenente specifiche di distribuzione di spec.yaml valide.
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-app-update"></a>azdata app update
Aggiorna un'applicazione.
```bash
azdata app update 
```
### <a name="examples"></a>Esempi
Aggiornare un'applicazione esistente da una directory contenente specifiche di distribuzione di spec.yaml valide.
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-app-list"></a>azdata app list
Elenca le applicazioni.
```bash
azdata app list 
```
### <a name="examples"></a>Esempi
Elencare le applicazioni per nome e versione.
```bash
azdata app list --name reduce  --version v1
```
Elencare tutte le versioni dell'applicazione in base al nome.
```bash
azdata app list --name reduce
```
Elencare tutte le versioni dell'applicazione in base al nome.
```bash
azdata app list
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-app-delete"></a>azdata app delete
Elimina un'applicazione.
```bash
azdata app delete 
```
### <a name="examples"></a>Esempi
Eliminare le applicazioni per nome e versione.
```bash
azdata app delete --name reduce --version v1    
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-app-run"></a>azdata app run
Esegue un'applicazione.
```bash
azdata app run 
```
### <a name="examples"></a>Esempi
Eseguire l'applicazione senza parametri di input.
```bash
azdata app run --name reduce --version v1
```
Eseguire l'applicazione con 1 parametro di input.
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
Eseguire l'applicazione con più parametri di input.
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-app-describe"></a>azdata app describe
Descrive un'applicazione.
```bash
azdata app describe 
```
### <a name="examples"></a>Esempi
Descrivere un'applicazione.
```bash
azdata app describe --name reduce --version v1    
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). 

- Per altre informazioni su come installare lo strumento **azdata**, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).
