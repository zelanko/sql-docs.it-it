---
title: riferimento batch Spark azdata BDC
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi batch azdata BDC Spark.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6e242b26f439b49dbf0b3cf5ab50ea46c273f45f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426161"
---
# <a name="azdata-bdc-spark-batch"></a>batch Spark azdata BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi **batch Spark per integrazione applicativa** dei dati nello strumento **azdata** . Per ulteriori informazioni su altri comandi di **azdata** , vedere [riferimento azdata](reference-azdata.md)

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[creazione batch Spark azdata BDC](#azdata-bdc-spark-batch-create) | Creare un nuovo batch Spark.
[elenco di batch Spark di azdata BDC](#azdata-bdc-spark-batch-list) | Elencare tutti i batch in Spark.
[informazioni batch Spark azdata BDC](#azdata-bdc-spark-batch-info) | Ottenere informazioni su un batch Spark attivo.
[log del batch Spark azdata BDC](#azdata-bdc-spark-batch-log) | Ottenere i log di esecuzione per un batch Spark.
[stato batch Spark azdata BDC](#azdata-bdc-spark-batch-state) | Ottenere lo stato di esecuzione per un batch Spark.
[eliminazione batch Spark azdata BDC](#azdata-bdc-spark-batch-delete) | Eliminare un batch Spark.
## <a name="azdata-bdc-spark-batch-create"></a>creazione batch Spark azdata BDC
Viene creato un nuovo processo batch Spark che esegue il codice fornito.
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
Creare un nuovo batch Spark.
```bash
azdata spark batch create --code "2+2"
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--file -f`
Percorso del file da eseguire.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--class-name -c`
Nome della classe da eseguire quando si passano uno o più file con estensione jar.
#### `--arguments -a`
Elenco di argomenti.  Per passare un elenco JSON, codificare i valori.  Esempio:' ["ENTRY1", "Entry2"]'.
#### `--jar-files -j`
Elenco di percorsi di file jar.  Per passare un elenco JSON, codificare i valori.  Esempio:' ["ENTRY1", "Entry2"]'.
#### `--py-files -p`
Elenco di percorsi di file Python.  Per passare un elenco JSON, codificare i valori.  Esempio:' ["ENTRY1", "Entry2"]'.
#### `--files`
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
#### `--archives`
Elenco di percorsi degli archivi.  Per passare un elenco JSON, codificare i valori.  Esempio:' ["ENTRY1", "Entry2"]'.
#### `--queue -q`
Nome della coda di Spark in cui eseguire la sessione.
#### `--name -n`
Nome della sessione Spark.
#### `--config`
Elenco di coppie nome-valore contenenti i valori di configurazione di Spark.  Codificata come dizionario JSON.  Esempio:' {"Name": "value", "name2": "value2"}'.
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
## <a name="azdata-bdc-spark-batch-list"></a>elenco di batch Spark di azdata BDC
Elencare tutti i batch in Spark.
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
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  Valori consentiti: JSON, jsonc, Table, TSV.  Impostazione predefinita: JSON.
#### `--query -q`
Stringa di query JMESPath. Per [http://jmespath.org/](http://jmespath.org/]) ulteriori informazioni ed esempi, vedere.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
## <a name="azdata-bdc-spark-batch-info"></a>informazioni batch Spark azdata BDC
Ottiene le informazioni per un batch Spark con l'ID specificato.  L'ID batch viene restituito da "Spark batch create".
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>Esempi
Ottenere le informazioni sul batch per il batch con ID 0.
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--batch-id -i`
Numero ID batch Spark.
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
## <a name="azdata-bdc-spark-batch-log"></a>log del batch Spark azdata BDC
Ottiene le voci del log batch per un batch Spark con l'ID specificato.  L'ID batch viene restituito da "Spark batch create".
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>Esempi
Ottiene il log batch per il batch con ID 0.
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--batch-id -i`
Numero ID batch Spark.
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
## <a name="azdata-bdc-spark-batch-state"></a>stato batch Spark azdata BDC
Ottiene lo stato del batch per un batch Spark con l'ID specificato.  L'ID batch viene restituito da "Spark batch create".
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>Esempi
Ottiene lo stato del batch per il batch con ID 0.
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--batch-id -i`
Numero ID batch Spark.
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
## <a name="azdata-bdc-spark-batch-delete"></a>eliminazione batch Spark azdata BDC
Viene eliminato un batch Spark. L'ID batch viene restituito da "Spark batch create".
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>Esempi
Eliminare un batch.
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--batch-id -i`
Numero ID batch Spark.
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
