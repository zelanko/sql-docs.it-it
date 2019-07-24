---
title: riferimento per il montaggio di HDFS BDC azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di montaggio azdata BDC HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f0b259a3ac4ac0850fa05de3867e928b035307b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426271"
---
# <a name="azdata-bdc-hdfs-mount"></a>azdata BDC HDFS Mount

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi di **montaggio BDC HDFS** nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[creazione di azdata BDC HDFS montaggio](#azdata-bdc-hdfs-mount-create) | Creare montaggi di archivi remoti in HDFS.
[azdata BDC HDFS Mount Delete](#azdata-bdc-hdfs-mount-delete) | Elimina i montaggi degli archivi remoti in HDFS.
[stato di montaggio azdata BDC HDFS](#azdata-bdc-hdfs-mount-status) | Stato del montaggio/i.
[aggiornamento montaggio azdata BDC HDFS](#azdata-bdc-hdfs-mount-refresh) | Aggiornare il contenuto di un montaggio in HDFS.
## <a name="azdata-bdc-hdfs-mount-create"></a>creazione di azdata BDC HDFS montaggio
Creare montaggi di archivi remoti in HDFS. Le credenziali per l'accesso all'archivio remoto, se presente, devono essere specificate usando la variabile di ambiente MOUNT_CREDENTIALS come elenco delimitato da virgole di coppie chiave = valore. Qualsiasi virgola nelle chiavi o nei valori deve essere preceduta da un carattere di escape.
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>Esempi
Per montare il contenitore "data" nell'account ADLS gen 2 "adlsv2example" nel percorso HDFS/Mounts/adlsv2/data usando la chiave condivisa
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
Per montare una HDFS BDC remota (hdfs://namenode1:8080/) nel percorso HDFS locale/Mounts/HDFS/
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--remote-uri -r`
URI dell'archivio remoto da montare (origine del montaggio).
#### `--mount-path -m`
Percorso HDFS in cui è necessario creare il montaggio (destinazione del montaggio).
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
## <a name="azdata-bdc-hdfs-mount-delete"></a>azdata BDC HDFS Mount Delete
Elimina i montaggi degli archivi remoti in HDFS.
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>Esempi
Eliminare il montaggio creato in/Mounts/adlsv2/data per un account di archiviazione ADLS di generazione 2.
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--mount-path -m`
percorso HDFS che corrisponde al montaggio da eliminare.
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
## <a name="azdata-bdc-hdfs-mount-status"></a>stato di montaggio azdata BDC HDFS
Stato del montaggio/i.
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>Esempi
Ottenere lo stato di montaggio per percorso
```bash
azdata bdc hdfs mount status --mount-path /mounts/hdfs
```
Ottenere lo stato di tutti i montaggi.
```bash
azdata bdc hdfs mount status
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--mount-path -m`
Percorso di montaggio.
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
## <a name="azdata-bdc-hdfs-mount-refresh"></a>aggiornamento montaggio azdata BDC HDFS
Aggiornare il contenuto di un montaggio in HDFS.
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>Esempi
Aggiornamento del montaggio creato alle/Mounts/adlsv2/data.
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--mount-path -m`
Percorso HDFS che corrisponde al montaggio da aggiornare.
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
