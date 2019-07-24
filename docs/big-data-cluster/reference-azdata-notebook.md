---
title: informazioni di riferimento su azdata notebook
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di azdata notebook.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b96c5e06ec51f53964a28cac86f385d6b42c1dc4
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426011"
---
# <a name="azdata-notebook"></a>Notebook di azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi del **notebook** nello strumento **azdata** . Per ulteriori informazioni su altri comandi di **azdata** , vedere [riferimento azdata](reference-azdata.md)

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[Visualizzazione del notebook di azdata](#azdata-notebook-view) | Visualizzare un notebook.  Opzione per arrestare il primo errore di esecuzione della cella.
[esecuzione di azdata notebook](#azdata-notebook-run) | Eseguire un notebook.  L'esecuzione viene arrestata al primo errore.
## <a name="azdata-notebook-view"></a>Visualizzazione del notebook di azdata
Questo comando può prendere un file notebook e convertire il Markdown, il codice e l'output in formato terminale colori.
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>Esempi
Visualizza notebook.  Vengono visualizzate tutte le celle.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
Visualizza notebook.  Vengono visualizzate tutte le celle a meno che non venga rilevata una cella con errore nell'output.  In tal caso, l'output viene arrestato.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Percorso del notebook da visualizzare.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--continue-on-error -c`
Continua a visualizzare le celle aggiuntive ignorando eventuali errori di celle trovati nell'output del notebook.  Il comportamento predefinito prevede l'arresto in errore.  L'arresto di rende più semplice la visualizzazione della prima cella che ha rilevato un errore.
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
## <a name="azdata-notebook-run"></a>esecuzione di azdata notebook
Questo comando crea una directory temporanea ed esegue il notebook specificato al suo interno come directory di lavoro.
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]
```
### <a name="examples"></a>Esempi
Eseguire notebook.
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Percorso del file del notebook da eseguire.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--output-path`
Percorso della directory da usare per l'output del notebook.  Il notebook con i dati di output e i file generati dal notebook vengono generati in relazione a questa directory.
#### `--output-html`
Flag facoltativo indicatingg se convertire ulteriormente il notebook di output in formato HTML.  Crea un secondo file di output.
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

Per altre informazioni su come installare lo strumento **azdata** , vedere [Install azdata to manage SQL Server 2019 Big Data Clusters](deploy-install-azdata.md).
