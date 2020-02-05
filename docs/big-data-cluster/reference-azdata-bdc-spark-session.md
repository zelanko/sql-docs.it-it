---
title: Informazioni di riferimento su azdata bdc spark session
description: Articolo di riferimento per i comandi azdata bdc spark session.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6829ce474b2f2f0b000a8ded5cfae2e293e1c2da
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75258622"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark session

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

L'articolo seguente offre informazioni di riferimento sui comandi `bdc spark session` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md)

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[azdata bdc spark session create](#azdata-bdc-spark-session-create) | Crea una nuova sessione Spark.
[azdata bdc spark session list](#azdata-bdc-spark-session-list) | Elenca tutte le sessioni attive in Spark.
[azdata bdc spark session info](#azdata-bdc-spark-session-info) | Ottiene informazioni su una sessione Spark attiva.
[azdata bdc spark session log](#azdata-bdc-spark-session-log) | Ottiene i log di esecuzione per una sessione Spark attiva.
[azdata bdc spark session state](#azdata-bdc-spark-session-state) | Ottiene lo stato di esecuzione per una sessione Spark attiva.
[azdata bdc spark session delete](#azdata-bdc-spark-session-delete) | Elimina una sessione Spark.
## <a name="azdata-bdc-spark-session-create"></a>azdata bdc spark session create
Crea una nuova sessione Spark interattiva. Il chiamante deve specificare il tipo di sessione Spark. Questa sessione dura oltre la durata di un'esecuzione di azdata e deve essere eliminata con "spark session delete"
```bash
azdata bdc spark session create [--session-kind -k] 
                                [--jar-files -j]  
                                [--py-files -p]  
                                [--files -f]  
                                [--driver-memory]  
                                [--driver-cores]  
                                [--executor-memory]  
                                [--executor-cores]  
                                [--executor-count]  
                                [--archives -a]  
                                [--queue -q]  
                                [--name -n]  
                                [--config -c]  
                                [--timeout-seconds -t]
```
### <a name="examples"></a>Esempi
Crea una sessione.
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--session-kind -k`
Nome del tipo di sessione da creare.  Uno tra spark, pyspark, sparkr e sql.
#### `--jar-files -j`
Elenco di percorsi di file JAR.  Per passare un elenco JSON, codificare i valori.  Esempio: '["entry1", "entry2"]'.
#### `--py-files -p`
Elenco di percorsi di file Python.  Per passare un elenco JSON, codificare i valori.  Esempio: '["entry1", "entry2"]'.
#### `--files -f`
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
#### `--archives -a`
Elenco di percorsi di archivi.  Per passare un elenco JSON, codificare i valori.  Esempio: '["entry1", "entry2"]'.
#### `--queue -q`
Nome della coda di Spark in cui eseguire la sessione.
#### `--name -n`
Nome della sessione Spark.
#### `--config -c`
Elenco di coppie nome-valore contenenti valori di configurazione Spark.  Codificati come dizionario JSON.  Esempio: '{"name":"value", "name2":"value2"}'.
#### `--timeout-seconds -t`
Timeout di inattività sessione in secondi.
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
## <a name="azdata-bdc-spark-session-list"></a>azdata bdc spark session list
Elenca tutte le sessioni attive in Spark.
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>Esempi
Elenca tutte le sessioni attive.
```bash
azdata spark session list
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
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark session info
Ottiene le informazioni sulla sessione per una sessione Spark attiva con l'ID specificato.  L'ID della sessione viene restituito da "spark session create".
```bash
azdata bdc spark session info --session-id -i 
            ```
### Examples
Get session info for session with ID of 0.
```bash
azdata spark session info --session-id 0
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
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark session log
Ottiene le voci di log per una sessione Spark attiva con l'ID specificato.  L'ID della sessione viene restituito da "spark session create".
```bash
azdata bdc spark session log --session-id -i 
           ```
### Examples
Get session log for session with ID of 0.
```bash
azdata spark session log --session-id 0
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
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark session state
Ottiene lo stato di una sessione Spark attiva con l'ID specificato.  L'ID della sessione viene restituito da "spark session create".
```bash
azdata bdc spark session state --session-id -i 
             ```
### Examples
Get session state for session with ID of 0.
```bash
azdata spark session state --session-id 0
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
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark session delete
Elimina una sessione Spark interattiva. L'ID della sessione viene restituito da "spark session create".
```bash
azdata bdc spark session delete --session-id -i 
              ```
### Examples
Delete a session.
```bash
azdata spark session delete --session-id 0
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

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).
