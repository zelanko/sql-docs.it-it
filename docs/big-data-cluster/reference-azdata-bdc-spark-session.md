---
title: Informazioni di riferimento su azdata bdc spark session
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata bdc spark session.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1573c5b95eeaf314db08acc60d6fe5e1e2c4b753
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653423"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark session

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

L'articolo seguente fornisce informazioni di riferimento per i comandi **bdc spark session** nello strumento **azdata**. Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

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
azdata bdc spark session create --session-kind pyspark
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
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
azdata bdc spark session list
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
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark session info
Ottiene le informazioni sulla sessione per una sessione Spark attiva con l'ID specificato.  L'ID della sessione viene restituito da "spark session create".
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>Esempi
Ottenere informazioni sulla sessione con ID 0.
```bash
azdata bdc spark session info --session-id 0
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark session log
Ottiene le voci di log per una sessione Spark attiva con l'ID specificato.  L'ID della sessione viene restituito da "spark session create".
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>Esempi
Ottenere il log per la sessione con ID 0.
```bash
azdata bdc spark session log --session-id 0
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark session state
Ottiene lo stato di una sessione Spark attiva con l'ID specificato.  L'ID della sessione viene restituito da "spark session create".
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>Esempi
Ottenere lo stato della sessione con ID 0.
```bash
azdata bdc spark session state --session-id 0
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark session delete
Elimina una sessione Spark interattiva. L'ID della sessione viene restituito da "spark session create".
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>Esempi
Eliminare una sessione.
```bash
azdata bdc spark session delete --session-id 0
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
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org/]).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi **azdata**, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per ulteriori informazioni su come installare lo strumento **azdata** , vedere [Install azdata to Manage [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](deploy-install-azdata.md).
