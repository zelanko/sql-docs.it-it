---
title: riferimento di montaggio mssqlctl integrazione applicativa dei dati del pool di archiviazione
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di montaggio mssqlctl integrazione applicativa dei dati del pool di archiviazione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b6a412c6d7cab9fb869a9aa8ee1b62ae0ed3f717
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958006"
---
# <a name="mssqlctl-bdc-storage-pool-mount"></a>montaggio di pool di archiviazione mssqlctl integrazione applicativa dei dati

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **montaggio di integrazione applicativa dei dati del pool di archiviazione** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[creazione di montaggio di pool di archiviazione mssqlctl integrazione applicativa dei dati](#mssqlctl-bdc-storage-pool-mount-create) | Creare punti di montaggio di archivi remoti in HDFS.
[eliminazione di montaggio mssqlctl integrazione applicativa dei dati del pool di archiviazione](#mssqlctl-bdc-storage-pool-mount-delete) | Eliminare i punti di montaggio del remoto archivia in HDFS.
[stato di montaggio mssqlctl integrazione applicativa dei dati del pool di archiviazione](#mssqlctl-bdc-storage-pool-mount-status) | Stato di mount(s).
## <a name="mssqlctl-bdc-storage-pool-mount-create"></a>creazione di montaggio di pool di archiviazione mssqlctl integrazione applicativa dei dati
Creare punti di montaggio di archivi remoti in HDFS. Le credenziali per l'accesso all'archivio remoto, se presente, devono essere specificate utilizzando la variabile di ambiente MOUNT_CREDENTIALS come elenco delimitato da virgole di chiave = coppie di valore. Le virgole nel chiavi o i valori devono essere evitate.
```bash
mssqlctl bdc storage-pool mount create --remote-uri 
                                       --mount-path
```
### <a name="examples"></a>Esempi
Montare contenitore "dati" nella generazione 2 di Azure Data Lake Store account "adlsv2example" su /mounts/adlsv2/data percorso HDFS usando la chiave condivisa
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
mssqlctl bdc storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
Per montare un BDC HDFS remoto (hdfs://namenode1:8080 /) in locale HDFS percorso /mounts/hdfs /
```bash
mssqlctl bdc storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--remote-uri`
URI dell'archivio remoto che deve essere montati (di origine di montaggio).
#### `--mount-path`
Percorso HDFS in cui deve essere creato (destinazione di montaggio) montaggio.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
## <a name="mssqlctl-bdc-storage-pool-mount-delete"></a>eliminazione di montaggio mssqlctl integrazione applicativa dei dati del pool di archiviazione
Eliminare i punti di montaggio del remoto archivia in HDFS.
```bash
mssqlctl bdc storage-pool mount delete --mount-path 
                                       
```
### <a name="examples"></a>Esempi
Eliminare montaggio creato alle /mounts/adlsv2/data per un account di archiviazione di Azure Data Lake Store generazione 2.
```bash
mssqlctl bdc storage-pool mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--mount-path`
Il percorso HDFS corrispondente per il montaggio che deve essere eliminato.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.
## <a name="mssqlctl-bdc-storage-pool-mount-status"></a>stato di montaggio mssqlctl integrazione applicativa dei dati del pool di archiviazione
Stato di mount(s).
```bash
mssqlctl bdc storage-pool mount status [--mount-path] 
                                       
```
### <a name="examples"></a>Esempi
Ottenere lo stato di montaggio per percorso
```bash
mssqlctl bdc storage-pool mount status --mount-path /mounts/hdfs
```
Ottiene lo stato di tutti i punti di montaggio.
```bash
mssqlctl bdc storage-pool mount status
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--mount-path`
Percorso di montaggio.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio di registrazione per mostrare tutti i log di debug.
#### `--help -h`
Mostra questo messaggio della Guida e l'uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumenta il livello di dettaglio di registrazione. Usare --debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).