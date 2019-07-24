---
title: informazioni di riferimento sull'istruzione azdata BDC Spark
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di azdata BDC Spark.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 778980ac6b93e7db79d59182fbd18ab4cfdb8b75
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426091"
---
# <a name="azdata-bdc-spark-statement"></a>azdata istruzione Spark BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

L'articolo seguente fornisce informazioni di riferimento sui comandi dell' **istruzione Spark di integrazione applicativa** dei dati nello strumento **azdata** . Per ulteriori informazioni su altri comandi di **azdata** , vedere [riferimento azdata](reference-azdata.md)

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[elenco di istruzioni Spark per azdata BDC](#azdata-bdc-spark-statement-list) | Elenca tutte le istruzioni nella sessione Spark specificata.
[creazione istruzione azdata BDC Spark](#azdata-bdc-spark-statement-create) | Crea una nuova istruzione Spark nella sessione specificata.
[informazioni sull'istruzione azdata BDC Spark](#azdata-bdc-spark-statement-info) | Ottenere informazioni sull'istruzione richiesta nella sessione Spark specificata.
[annullamento dell'istruzione azdata BDC Spark](#azdata-bdc-spark-statement-cancel) | Annulla un'istruzione all'interno della sessione Spark specificata.
## <a name="azdata-bdc-spark-statement-list"></a>elenco di istruzioni Spark per azdata BDC
Elenca tutte le istruzioni nella sessione Spark specificata.
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>Esempi
Elencare tutte le istruzioni della sessione.
```bash
azdata spark statement list --session-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--session-id -i`
Numero ID sessione Spark.
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
## <a name="azdata-bdc-spark-statement-create"></a>creazione istruzione azdata BDC Spark
Verrà creata ed eseguita una nuova istruzione nella sessione specificata.  Se l'esecuzione è rapida, il risultato contiene l'output dell'esecuzione.  In caso contrario, il risultato può essere recuperato utilizzando "informazioni sessione Spark" dopo il completamento dell'istruzione.
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>Esempi
Eseguire un'istruzione.
```bash
azdata spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--session-id -i`
Numero ID sessione Spark.
#### `--code -c`
Stringa che contiene il codice da eseguire come parte dell'istruzione.
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
## <a name="azdata-bdc-spark-statement-info"></a>informazioni sull'istruzione azdata BDC Spark
In questo modo si ottiene lo stato di esecuzione e i risultati dell'esecuzione se l'istruzione è stata completata. L'ID istruzione viene restituito da "Spark Statement create".
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>Esempi
Ottenere informazioni sull'istruzione per la sessione con ID 0 e ID istruzione 0.
```bash
azdata spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--session-id -i`
Numero ID sessione Spark.
#### `--statement-id -s`
Numero ID dell'istruzione Spark all'interno dell'ID di sessione specificato.
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
## <a name="azdata-bdc-spark-statement-cancel"></a>annullamento dell'istruzione azdata BDC Spark
Viene annullata un'istruzione all'interno della sessione Spark specificata. L'ID istruzione viene restituito da "Spark Statement create".
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>Esempi
Annulla un'istruzione.
```bash
azdata spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--session-id -i`
Numero ID sessione Spark.
#### `--statement-id -s`
Numero ID dell'istruzione Spark all'interno dell'ID di sessione specificato.
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
