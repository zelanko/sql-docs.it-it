---
title: Informazioni di riferimento su azdata extension
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata extension.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e2585a77c3117df8514622728d0f09df93d7bc2
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242998"
---
# <a name="azdata-extension"></a>azdata extension

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi
| Comando | Descrizione |
| --- | --- |
[azdata extension add](#azdata-extension-add) | Aggiunge un'estensione.
[azdata extension remove](#azdata-extension-remove) | Rimuove un'estensione.
[azdata extension list](#azdata-extension-list) | Elenca le estensioni installate.
## <a name="azdata-extension-add"></a>azdata extension add
Aggiunge un'estensione.
```bash
azdata extension add --source -s 
                     [--index]  
                     
[--pip-proxy]  
                     
[--pip-extra-index-urls]  
                     
[--yes -y]
```
### <a name="examples"></a>Esempi
Aggiungere un'estensione dall'URL.
```bash
azdata extension add --source https://contoso.com/some_ext-0.0.1-py2.py3-none-any.whl
```
Aggiungere un'estensione dal disco locale.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl
```
Aggiungere un'estensione dal disco locale e usare pip proxy per le dipendenze.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl --pip-proxy https://user:pass@proxy.server:8080
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--source -s`
Percorso di un file wheel dell'estensione sul disco o URL di un'estensione
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--index`
URL di base dell'indice di pacchetti Python (impostazione predefinita https://pypi.org/simple). Dovrebbe puntare a un repository conforme a PEP 503 (API del repository semplice) o a una directory locale con lo stesso formato.
#### `--pip-proxy`
Proxy per pip da usare per le dipendenze dell'estensione nel formato [utente:passwd@]server.proxy:porta
#### `--pip-extra-index-urls`
Elenco separato da spazi di URL aggiuntivi degli indici di pacchetti da usare. Dovrebbe puntare a un repository conforme a PEP 503 (API del repository semplice) o a una directory locale con lo stesso formato.
#### `--yes -y`
Indica che non è richiesta la conferma.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-extension-remove"></a>azdata extension remove
Rimuove un'estensione.
```bash
azdata extension remove --name -n 
                        [--yes -y]
```
### <a name="examples"></a>Esempi
Rimuovere un'estensione.
```bash
azdata extension remove --name some-ext
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--name -n`
Nome dell'estensione
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--yes -y`
Indica che non è richiesta la conferma.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-extension-list"></a>azdata extension list
Elenca le estensioni installate.
```bash
azdata extension list 
```
### <a name="examples"></a>Esempi
Elencare le estensioni.
```bash
azdata extension list
```
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).
