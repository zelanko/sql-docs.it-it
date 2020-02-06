---
title: Informazioni di riferimento su azdata bdc spark statement
description: Articolo di riferimento per i comandi azdata bdc spark statement.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38d556944db9e8c269fb8acf8f3089050fb8b1d8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75258607"
---
# <a name="azdata-bdc-spark-statement"></a>azdata bdc spark statement

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

L'articolo seguente offre informazioni di riferimento sui comandi `bdc spark statement` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md)

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata bdc spark statement list](#azdata-bdc-spark-statement-list) | Elenca tutte le istruzioni nella sessione Spark specificata.
[azdata bdc spark statement create](#azdata-bdc-spark-statement-create) | Crea una nuova istruzione Spark nella sessione specificata.
[azdata bdc spark statement info](#azdata-bdc-spark-statement-info) | Ottiene informazioni sull'istruzione richiesta nella sessione Spark specificata.
[azdata bdc spark statement cancel](#azdata-bdc-spark-statement-cancel) | Annulla un'istruzione all'interno della sessione Spark specificata.
## <a name="azdata-bdc-spark-statement-list"></a>azdata bdc spark statement list
Elenca tutte le istruzioni nella sessione Spark specificata.
```bash
azdata bdc spark statement list --session-id -i 
              ```
### Examples
List all the session statements.
```bash
azdata spark statement list --session-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--session-id -i`
Numero ID sessione Spark.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-spark-statement-create"></a>azdata bdc spark statement create
Questo comando crea ed esegue una nuova istruzione nella sessione specificata.  Se l'esecuzione è rapida, il risultato contiene l'output dell'esecuzione.  In caso contrario, il risultato può essere recuperato usando "spark session info" dopo il completamento dell'istruzione.
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
Stringa che contiene il codice da eseguire nell'ambito dell'istruzione.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-spark-statement-info"></a>azdata bdc spark statement info
Questo comando ottiene lo stato e i risultati dell'esecuzione, se l'istruzione è stata completata. L'ID di istruzione viene restituito dal comando "spark statement create".
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>Esempi
Ottenere informazioni sull'istruzione per la sessione con ID 0 e ID di istruzione 0.
```bash
azdata spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--session-id -i`
Numero ID sessione Spark.
#### `--statement-id -s`
Numero ID di istruzione Spark all'interno dell'ID di sessione specificato.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-spark-statement-cancel"></a>azdata bdc spark statement cancel
Annulla un'istruzione all'interno della sessione Spark specificata. L'ID di istruzione viene restituito dal comando "spark statement create".
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
Numero ID di istruzione Spark all'interno dell'ID di sessione specificato.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).
