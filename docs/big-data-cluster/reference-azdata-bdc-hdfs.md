---
title: riferimento HDFS BDC azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata BDC HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e892c2d501902ef915a297440ae5a6ffda83bce
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426181"
---
# <a name="azdata-bdc-hdfs"></a>azdata BDC HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento sui comandi **HDFS BDC** nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[Shell azdata BDC HDFS](#azdata-bdc-hdfs-shell) | HDFS Shell è una semplice shell dei comandi interattiva per HDFS file system.
[azdata BDC HDFS ls](#azdata-bdc-hdfs-ls) | Elenca lo stato del file o della directory specificata.
[azdata BDC HDFS esistente](#azdata-bdc-hdfs-exists) | Determinare se esiste un file o una directory.  Restituisce true se esiste e false in caso contrario.
[azdata BDC HDFS mkdir](#azdata-bdc-hdfs-mkdir) | Crea una directory nel percorso specificato.
[azdata BDC HDFS MV](#azdata-bdc-hdfs-mv) | Spostare il file o il percorso specificato nel percorso specificato.
[creazione di azdata BDC HDFS](#azdata-bdc-hdfs-create) | Creare il file di testo nel percorso specificato.  Il contenuto di testo semplice può essere aggiunto tramite il parametro data.
[azdata BDC HDFS Cat](#azdata-bdc-hdfs-cat) | Leggere il contenuto di un file.  Offset e lunghezza in byte sono parametri facoltativi.
[azdata BDC HDFS RM](#azdata-bdc-hdfs-rm) | Rimuovere un file o una directory.
[azdata BDC HDFS RMR](#azdata-bdc-hdfs-rmr) | Rimuovere in modo ricorsivo un file o una directory.
[azdata BDC HDFS chmod](#azdata-bdc-hdfs-chmod) | Modificare l'autorizzazione per il file o la directory specificata.
[azdata BDC HDFS chown](#azdata-bdc-hdfs-chown) | Modificare il proprietario o il gruppo del file specificato.
[azdata BDC HDFS Mount](reference-azdata-bdc-hdfs-mount.md) | Gestire il montaggio di archivi remoti in HDFS.
## <a name="azdata-bdc-hdfs-shell"></a>Shell azdata BDC HDFS
HDFS Shell è una semplice shell dei comandi interattiva per HDFS file system.
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>Esempi
Avviare la Shell.
```bash
azdata bdc hdfs shell
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
## <a name="azdata-bdc-hdfs-ls"></a>azdata BDC HDFS ls
Elenca lo stato del file o della directory specificata.
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>Esempi
Stato elenco
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Percorso dello stato dell'elenco.
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
## <a name="azdata-bdc-hdfs-exists"></a>azdata BDC HDFS esistente
Determinare se esiste un file o una directory.  Restituisce true se esiste e false in caso contrario.
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>Esempi
Verificare la presenza di file o directory.
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Percorso di cui verificare l'esistenza.
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
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata BDC HDFS mkdir
Crea una directory nel percorso specificato.
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>Esempi
Creare la directory.
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome della directory da creare.
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
## <a name="azdata-bdc-hdfs-mv"></a>azdata BDC HDFS MV
Spostare il file o il percorso specificato nel percorso specificato.
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>Esempi
Spostare il file o la directory.
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--source-path -s`
Directory da spostare.
#### `--target-path -t`
Posizione in cui spostarsi.
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
## <a name="azdata-bdc-hdfs-create"></a>creazione di azdata BDC HDFS
Creare il file di testo nel percorso specificato.  Il contenuto di testo semplice può essere aggiunto tramite il parametro data.
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>Esempi
Creare il file.
```bash
azdata bdc hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file da creare.
#### `--data -d`
Contenuto del file.  Progettato per contenuto di testo semplice.
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
## <a name="azdata-bdc-hdfs-cat"></a>azdata BDC HDFS Cat
Leggere il contenuto di un file.  Offset e lunghezza in byte sono parametri facoltativi.
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    --length -l
```
### <a name="examples"></a>Esempi
Leggere il file.
```bash
azdata bdc hdfs cat --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file da leggere.
#### `--offset`
Numero di byte di offset all'interno del file da leggere.
#### `--length -l`
Lunghezza dei dati da leggere.
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
## <a name="azdata-bdc-hdfs-rm"></a>azdata BDC HDFS RM
Rimuovere un file o una directory.
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>Esempi
Rimuovere un file o una directory.
```bash
azdata bdc hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file da rimuovere.
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
## <a name="azdata-bdc-hdfs-rmr"></a>azdata BDC HDFS RMR
Rimuovere in modo ricorsivo un file o una directory.
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>Esempi
Directory di rimozione ricorsiva.
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file da rimuovere in modo ricorsivo.
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
## <a name="azdata-bdc-hdfs-chmod"></a>azdata BDC HDFS chmod
Modificare l'autorizzazione per il file o la directory specificata.
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>Esempi
Modificare le autorizzazioni di file o directory.
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file o della directory in cui impostare le autorizzazioni.
#### `--permission`
Ottetti delle autorizzazioni da impostare.  Esempio "775".
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
## <a name="azdata-bdc-hdfs-chown"></a>azdata BDC HDFS chown
Modificare il proprietario o il gruppo del file specificato.
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      --group -g
```
### <a name="examples"></a>Esempi
Modificare il proprietario e il gruppo.
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file o della directory di cui modificare il proprietario.
#### `--owner`
Nome del proprietario su cui impostare.
#### `--group -g`
Nome del gruppo da impostare su.
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
