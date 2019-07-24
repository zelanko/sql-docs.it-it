---
title: riferimento alla sessione di azdata BDC
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi della sessione di Spark BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20b7ac3dcf72482e80278ce0f0df922026232a6d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426101"
---
# <a name="azdata-bdc-spark-session"></a>sessione di Spark BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

L'articolo seguente fornisce informazioni di riferimento sui comandi della **sessione di Spark BDC** nello strumento **azdata** . Per ulteriori informazioni su altri comandi di **azdata** , vedere [riferimento azdata](reference-azdata.md)

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[creazione della sessione di Spark BDC azdata](#azdata-bdc-spark-session-create) | Creare una nuova sessione di Spark.
[elenco di sessioni di Spark BDC azdata](#azdata-bdc-spark-session-list) | Elencare tutte le sessioni attive in Spark.
[informazioni sulla sessione di Spark azdata BDC](#azdata-bdc-spark-session-info) | Ottenere informazioni su una sessione Spark attiva.
[log della sessione di Spark BDC azdata](#azdata-bdc-spark-session-log) | Ottenere i log di esecuzione per una sessione Spark attiva.
[stato sessione di Spark BDC azdata](#azdata-bdc-spark-session-state) | Ottenere lo stato di esecuzione per una sessione Spark attiva.
[eliminazione della sessione di Spark BDC azdata](#azdata-bdc-spark-session-delete) | Eliminare una sessione di Spark.
## <a name="azdata-bdc-spark-session-create"></a>creazione della sessione di Spark BDC azdata
Viene creata una nuova sessione Spark interattiva. Il chiamante deve specificare il tipo di sessione Spark. Questa sessione si trova oltre la durata di un'esecuzione di azdata e deve essere eliminata con ' Spark Session Delete '
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
Creare una sessione.
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--session-kind -k`
Nome del tipo di sessione da creare.  Uno di Spark, pyspark, sparkr o SQL.
#### `--jar-files -j`
Elenco di percorsi di file jar.  Per passare un elenco JSON, codificare i valori.  Esempio:' ["ENTRY1", "Entry2"]'.
#### `--py-files -p`
Elenco di percorsi di file Python.  Per passare un elenco JSON, codificare i valori.  Esempio:' ["ENTRY1", "Entry2"]'.
#### `--files -f`
Elenco di percorsi di file.  Per passare un elenco JSON, codificare i valori.  Esempio:' ["ENTRY1", "Entry2"]'.
#### `--driver-memory`
Quantità di memoria da allocare al driver.  Specificare le unità come parte del valore.  Esempio di 512M o 2G.
#### `--driver-cores`
Quantità di core CPU da allocare al driver.
#### `--executor-memory`
Quantità di memoria da allocare all'executor.  Specificare le unità come parte del valore.  Esempio di 512M o 2G.
#### `--executor-cores`
Quantità di core CPU da allocare all'executor.
#### `--executor-count`
Numero di istanze dell'Executor da eseguire.
#### `--archives -a`
Elenco di percorsi degli archivi.  Per passare un elenco JSON, codificare i valori.  Esempio:' ["ENTRY1", "Entry2"]'.
#### `--queue -q`
Nome della coda di Spark in cui eseguire la sessione.
#### `--name -n`
Nome della sessione Spark.
#### `--config -c`
Elenco di coppie nome-valore contenenti i valori di configurazione di Spark.  Codificata come dizionario JSON.  Esempio:' {"Name": "value", "name2": "value2"}'.
#### `--timeout-seconds -t`
Timeout di inattività della sessione in secondi.
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
## <a name="azdata-bdc-spark-session-list"></a>elenco di sessioni di Spark BDC azdata
Elencare tutte le sessioni attive in Spark.
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>Esempi
Elencare tutte le sessioni attive.
```bash
azdata spark session list
```
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
## <a name="azdata-bdc-spark-session-info"></a>informazioni sulla sessione di Spark azdata BDC
Ottiene le informazioni sulla sessione per una sessione Spark attiva con l'ID specificato.  L'ID sessione viene restituito da' Spark session create '.
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>Esempi
Ottenere le informazioni sulla sessione per la sessione con ID 0.
```bash
azdata spark session info --session-id 0
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
## <a name="azdata-bdc-spark-session-log"></a>log della sessione di Spark BDC azdata
Ottiene le voci del log di sessione per una sessione Spark attiva con l'ID specificato.  L'ID sessione viene restituito da' Spark session create '.
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>Esempi
Ottenere il log della sessione per la sessione con ID 0.
```bash
azdata spark session log --session-id 0
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
## <a name="azdata-bdc-spark-session-state"></a>stato sessione di Spark BDC azdata
Ottiene lo stato della sessione per una sessione Spark attiva con l'ID specificato.  L'ID sessione viene restituito da' Spark session create '.
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>Esempi
Ottenere lo stato della sessione per la sessione con ID 0.
```bash
azdata spark session state --session-id 0
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
## <a name="azdata-bdc-spark-session-delete"></a>eliminazione della sessione di Spark BDC azdata
In questo modo viene eliminata una sessione Spark interattiva. L'ID sessione viene restituito da' Spark session create '.
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>Esempi
Eliminare una sessione.
```bash
azdata spark session delete --session-id 0
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

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento **azdata** , vedere [Install azdata to manage SQL Server 2019 Big Data Clusters](deploy-install-azdata.md).
