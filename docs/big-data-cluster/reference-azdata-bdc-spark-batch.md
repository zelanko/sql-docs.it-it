---
title: Informazioni di riferimento su azdata bdc spark batch
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc spark batch.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fc3dc5a987ae55ba410ca64c15a3a4b776465b54
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531755"
---
# <a name="azdata-bdc-spark-batch"></a>azdata bdc spark batch

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md)

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[azdata bdc spark batch create](#azdata-bdc-spark-batch-create) | Crea un nuovo batch Spark.
[azdata bdc spark batch list](#azdata-bdc-spark-batch-list) | Elenca tutti i batch in Spark.
[azdata bdc spark batch info](#azdata-bdc-spark-batch-info) | Ottiene informazioni su un batch Spark attivo.
[azdata bdc spark batch log](#azdata-bdc-spark-batch-log) | Ottenere i log di esecuzione relativi a un batch Spark.
[azdata bdc spark batch state](#azdata-bdc-spark-batch-state) | Ottenere lo stato di esecuzione per un batch Spark.
[azdata bdc spark batch delete](#azdata-bdc-spark-batch-delete) | Elimina un batch Spark.
## <a name="azdata-bdc-spark-batch-create"></a>azdata bdc spark batch create
Crea un nuovo processo batch Spark che esegue il codice fornito.
```bash
azdata bdc spark batch create --file -f 
                              [--class-name -c]  
                              [--arguments -a]  
                              [--jar-files -j]  
                              [--py-files -p]  
                              [--files]  
                              [--driver-memory]  
                              [--driver-cores]  
                              [--executor-memory]  
                              [--executor-cores]  
                              [--executor-count]  
                              [--archives]  
                              [--queue -q]  
                              [--name -n]  
                              [--config]
```
### <a name="examples"></a>Esempi
Crea un nuovo batch Spark.
```bash
azdata spark batch create --code "2+2"
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--file -f`
Percorso del file da eseguire.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--class-name -c`
Nome della classe da eseguire quando si passa uno o più file con estensione JAR.
#### `--arguments -a`
Elenco di argomenti.  Per passare un elenco JSON, codificare i valori.  Esempio: '["entry1", "entry2"]'.
#### `--jar-files -j`
Elenco di percorsi di file JAR.  Per passare un elenco JSON, codificare i valori.  Esempio: '["entry1", "entry2"]'.
#### `--py-files -p`
Elenco di percorsi di file Python.  Per passare un elenco JSON, codificare i valori.  Esempio: '["entry1", "entry2"]'.
#### `--files`
Elenco di percorsi di file.  Per passare un elenco JSON, codificare i valori.  Esempio: '["entry1", "entry2"]'.
#### `--driver-memory`
Quantità di memoria da allocare al driver.  Specificare le unità come parte del valore.  Esempio: 512 M o 2 G.
#### `--driver-cores`
Quantità di core CPU da allocare al driver.
#### `--executor-memory`
Quantità di memoria da allocare all'esecutore.  Specificare le unità come parte del valore.  Esempio: 512 M o 2 G.
#### `--executor-cores`
Quantità di core CPU da allocare all'esecutore.
#### `--executor-count`
Numero di istanze dell'esecutore da eseguire.
#### `--archives`
Elenco di percorsi di archivi.  Per passare un elenco JSON, codificare i valori.  Esempio: '["entry1", "entry2"]'.
#### `--queue -q`
Nome della coda di Spark in cui eseguire la sessione.
#### `--name -n`
Nome della sessione Spark.
#### `--config`
Elenco di coppie nome-valore contenenti valori di configurazione Spark.  Codificati come dizionario JSON.  Esempio: '{"name":"value", "name2":"value2"}'.
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
## <a name="azdata-bdc-spark-batch-list"></a>azdata bdc spark batch list
Elenca tutti i batch in Spark.
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>Esempi
Elencare tutti i batch attivi.
```bash
azdata spark batch list
```
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
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark batch info
Ottiene le informazioni relative a un batch Spark con l'ID specificato.  L'ID del batch viene restituito da "spark batch create".
```bash
azdata bdc spark batch info --batch-id -i 
          ```
### Examples
Get batch info for batch with ID of 0.
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--batch-id -i`
Numero ID del batch Spark.
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
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark batch log
Ottiene le voci di log relative a un batch Spark con l'ID specificato.  L'ID del batch viene restituito da "spark batch create".
```bash
azdata bdc spark batch log --batch-id -i 
         ```
### Examples
Get batch log for batch with ID of 0.
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--batch-id -i`
Numero ID del batch Spark.
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
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark batch state
Ottiene lo stato di un batch Spark con l'ID specificato.  L'ID del batch viene restituito da "spark batch create".
```bash
azdata bdc spark batch state --batch-id -i 
           ```
### Examples
Get batch state for batch with ID of 0.
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--batch-id -i`
Numero ID del batch Spark.
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
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark batch delete
Elimina un batch Spark. L'ID del batch viene restituito da "spark batch create".
```bash
azdata bdc spark batch delete --batch-id -i 
            ```
### Examples
Delete a batch.
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--batch-id -i`
Numero ID del batch Spark.
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
