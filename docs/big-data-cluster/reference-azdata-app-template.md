---
title: riferimento al modello di app azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi del modello di app azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3b257a2bacc56a7907ab0d25f492ed0ebd605543
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426331"
---
# <a name="azdata-app-template"></a>modello di app azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi del **modello app** nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[elenco dei modelli di app azdata](#azdata-app-template-list) | Recuperare i modelli supportati.
[pull del modello di app azdata](#azdata-app-template-pull) | Scaricare i modelli supportati.
## <a name="azdata-app-template-list"></a>elenco dei modelli di app azdata
Recuperare i modelli supportati nel repository GitHub [URL] specificato.
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>Esempi
Recuperare tutti i modelli nel percorso predefinito del repository del modello.
```bash
azdata app template list
```
Recuperare tutti i modelli in un percorso di repository diverso.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>Parametri facoltativi
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
## <a name="azdata-app-template-pull"></a>pull del modello di app azdata
Scaricare i modelli supportati nel repository GitHub [URL] specificato.
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         [--destination -d]
```
### <a name="examples"></a>Esempi
Scaricare tutti i modelli nel percorso predefinito del repository del modello.
```bash
azdata app template pull
```
Scaricare tutti i modelli in un percorso di repository diverso.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
Scaricare il singolo modello in base al nome.
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome del modello. Per un elenco completo del modello supportato namesrun`azdata app template list`
#### `--url -u`
Specificare un percorso del repository di modelli diverso. Predefinita https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
Posizione in cui posizionare il modello di scheletro dell'applicazione.
`./templates`
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
