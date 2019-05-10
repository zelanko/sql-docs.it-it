---
title: riferimento di montaggio mssqlctl archiviazione
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di montaggio archiviazione mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 523253e8d1ff2d621d9f7a5ef90dbc957fba82ec
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774692"
---
# <a name="mssqlctl-storage-mount"></a>montaggio archiviazione mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **montare archiviazione** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[montare archiviazione mssqlctl creare](#mssqlctl-storage-mount-create) | Creare punti di montaggio di archivi remoti in HDFS.
[mssqlctl archiviazione montaggio delete](#mssqlctl-storage-mount-delete) | Eliminare i punti di montaggio del remoto archivia in HDFS.
[stato montaggio dell'archiviazione mssqlctl](#mssqlctl-storage-mount-status) | Stato di mount(s).
## <a name="mssqlctl-storage-mount-create"></a>montare archiviazione mssqlctl creare
Creare punti di montaggio di archivi remoti in HDFS.
```bash
mssqlctl storage mount create --remote-uri 
                              --mount-path  
                              [--credential-file]
```
### <a name="examples"></a>Esempi
Montare contenitore "dati" nella generazione 2 di Azure Data Lake Store account "adlsv2example" su /mounts/adlsv2/data percorso HDFS usando la chiave condivisa
```bash
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data --credentials credential_file
```
Per montare un cluster HDFS remoto (hdfs://namenode1:8080 /) in locale HDFS percorso /mounts/hdfs /
```bash
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--remote-uri`
URI dell'archivio remoto che deve essere montati (di origine di montaggio).
#### `--mount-path`
Percorso HDFS in cui deve essere creato (destinazione di montaggio) montaggio.
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--credential-file`
File che contiene le credenziali per accedere all'archivio remoto. Le credenziali devono essere specificate come chiave = coppie valore con una chiave = valore per ogni riga. Qualsiasi è uguale in chiavi o valori sono necessario utilizzare caratteri di escape. Le credenziali non sono necessari per impostazione predefinita. Le chiavi necessarie variano a seconda del tipo di archivio remoto in cui vengono montato e il tipo di autorizzazione usata.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.
## <a name="mssqlctl-storage-mount-delete"></a>mssqlctl archiviazione montaggio delete
Eliminare i punti di montaggio del remoto archivia in HDFS.
```bash
mssqlctl storage mount delete --mount-path 
                              
```
### <a name="examples"></a>Esempi
Eliminare montaggio creato alle /mounts/adlsv2/data per un account di archiviazione di Azure Data Lake Store generazione 2.
```bash
mssqlctl storage mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--mount-path`
Il percorso HDFS corrispondente per il montaggio che deve essere eliminato.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.
## <a name="mssqlctl-storage-mount-status"></a>stato montaggio dell'archiviazione mssqlctl
Stato di mount(s).
```bash
mssqlctl storage mount status [--mount-path] 
                              
```
### <a name="examples"></a>Esempi
Ottenere lo stato di montaggio per percorso
```bash
mssqlctl storage mount status --mount-path /mounts/hdfs
```
Ottiene lo stato di tutti i punti di montaggio.
```bash
mssqlctl storage mount status
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--mount-path`
Percorso di montaggio.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md). Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).