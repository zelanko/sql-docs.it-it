---
title: Informazioni di riferimento su azdata app template
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata app template.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 07911616659a29df7f7fa6ce4d356a9c82789ae2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153224"
---
# <a name="azdata-app-template"></a>azdata app template

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

Questo articolo è un articolo di riferimento per **azdata**. 

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata app template list](#azdata-app-template-list) | Recupera i modelli supportati.
[azdata app template pull](#azdata-app-template-pull) | Scarica i modelli supportati.
## <a name="azdata-app-template-list"></a>azdata app template list
Recupera i modelli supportati nel repository GitHub [URL] specificato.
```bash
azdata app template list 
```
### <a name="examples"></a>Esempi
Recuperare tutti i modelli nel percorso predefinito del repository di modelli.
```bash
azdata app template list
```
Recuperare tutti i modelli in un percorso di repository diverso.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
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
## <a name="azdata-app-template-pull"></a>azdata app template pull
Scarica i modelli supportati nel repository GitHub [URL] specificato.
```bash
azdata app template pull 
```
### <a name="examples"></a>Esempi
Scaricare tutti i modelli nel percorso predefinito del repository di modelli.
```bash
azdata app template pull
```
Scaricare tutti i modelli in un percorso di repository diverso.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
Scaricare un singolo modello per nome.
```bash
azdata app template pull --name ssis
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
