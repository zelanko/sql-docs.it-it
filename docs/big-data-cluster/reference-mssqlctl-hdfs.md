---
title: Fare riferimento a mssqlctl hdfs
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi hdfs mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9051c3630fce005572bc3b939ebef9ed8d111e07
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394213"
---
# <a name="mssqlctl-hdfs"></a>mssqlctl hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **hdfs** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[mssqlctl hdfs shell](#mssqlctl-hdfs-shell) | La shell HDFS è una shell dei comandi interattiva semplice per file system HDFS.
[mssqlctl hdfs ls](#mssqlctl-hdfs-ls) | Elenca lo stato del file specificato o della directory.
[hdfs mssqlctl esiste](#mssqlctl-hdfs-exists) | Determinare se esiste un file o directory.  Restituisce True se è presente e False in caso contrario.
[mssqlctl hdfs mkdir](#mssqlctl-hdfs-mkdir) | Creare una directory nel percorso specificato.
[mssqlctl hdfs mv](#mssqlctl-hdfs-mv) | Spostare il file specificato o il percorso nel percorso specificato.
[creare mssqlctl hdfs](#mssqlctl-hdfs-create) | Creare il file di testo nella posizione specificata.  È possibile aggiungere contenuto di testo semplice tramite il parametro dei dati.
[mssqlctl hdfs read](#mssqlctl-hdfs-read) | Leggere il contenuto di un file.  Offset e lunghezza in byte sono parametri facoltativi.
[mssqlctl hdfs rm](#mssqlctl-hdfs-rm) | Rimuovere un file o directory.
[mssqlctl hdfs rmr](#mssqlctl-hdfs-rmr) | Rimuovono in modo ricorsivo un file o directory.
[chmod hdfs mssqlctl](#mssqlctl-hdfs-chmod) | Modificare l'autorizzazione per il file o directory specificata.
[mssqlctl hdfs chown](#mssqlctl-hdfs-chown) | Modificare il proprietario o il gruppo di file specificato.
## <a name="mssqlctl-hdfs-shell"></a>shell hdfs mssqlctl
La shell HDFS è una shell dei comandi interattiva semplice per file system HDFS.
```bash
mssqlctl hdfs shell 
```
### <a name="examples"></a>Esempi
Avviare la shell.
```bash
mssqlctl hdfs shell
```
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
## <a name="mssqlctl-hdfs-ls"></a>mssqlctl hdfs ls
Elenca lo stato del file specificato o della directory.
```bash
mssqlctl hdfs ls --path -p 
                 
```
### <a name="examples"></a>Esempi
Elenca stato
```bash
mssqlctl hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Il percorso per lo stato dell'elenco.
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
## <a name="mssqlctl-hdfs-exists"></a>hdfs mssqlctl esiste
Determinare se esiste un file o directory.  Restituisce True se è presente e False in caso contrario.
```bash
mssqlctl hdfs exists --path -p 
                     
```
### <a name="examples"></a>Esempi
Cercare l'esistenza di file o directory.
```bash
mssqlctl hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Percorso per verificare la presenza di esistenza.
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
## <a name="mssqlctl-hdfs-mkdir"></a>mssqlctl hdfs mkdir
Creare una directory nel percorso specificato.
```bash
mssqlctl hdfs mkdir --path -p 
                    
```
### <a name="examples"></a>Esempi
Creare directory.
```bash
mssqlctl hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome della directory da creare.
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
## <a name="mssqlctl-hdfs-mv"></a>mssqlctl hdfs mv
Spostare il file specificato o il percorso nel percorso specificato.
```bash
mssqlctl hdfs mv --source-path -s 
                 --target-path -t
```
### <a name="examples"></a>Esempi
Sposta file o directory.
```bash
mssqlctl hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--source-path -s`
La directory da spostare.
#### `--target-path -t`
Il percorso in cui spostarsi.
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
## <a name="mssqlctl-hdfs-create"></a>creare mssqlctl hdfs
Creare il file di testo nella posizione specificata.  È possibile aggiungere contenuto di testo semplice tramite il parametro dei dati.
```bash
mssqlctl hdfs create --path -p 
                     --data -d
```
### <a name="examples"></a>Esempi
Creare file.
```bash
mssqlctl hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file da creare.
#### `--data -d`
Contenuto del file.  Pensate per il contenuto di testo semplice.
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
## <a name="mssqlctl-hdfs-read"></a>hdfs mssqlctl leggere
Leggere il contenuto di un file.  Offset e lunghezza in byte sono parametri facoltativi.
```bash
mssqlctl hdfs read --path -p 
                   --offset  
                   --length -l
```
### <a name="examples"></a>Esempi
Leggere il file.
```bash
mssqlctl hdfs read --path '/tmp/test.txt'
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
Aumentare il livello di dettaglio di registrazione per mostrare che tutti i registri di debug.
#### `--help -h`
Mostra questo messaggio della Guida e uscita.
#### `--output -o`
Formato di output.  I valori consentiti: json, jsonc, tabella, tsv.  Predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Visualizzare [ http://jmespath.org/ ](http://jmespath.org/]) per altre informazioni ed esempi.
#### `--verbose`
Aumentare il livello di dettaglio di registrazione. Usare--debug per i log di debug completi.
## <a name="mssqlctl-hdfs-rm"></a>mssqlctl hdfs rm
Rimuovere un file o directory.
```bash
mssqlctl hdfs rm --path -p 
                 
```
### <a name="examples"></a>Esempi
Rimuovere un file o directory.
```bash
mssqlctl hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file da rimuovere.
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
## <a name="mssqlctl-hdfs-rmr"></a>mssqlctl hdfs rmr
Rimuovono in modo ricorsivo un file o directory.
```bash
mssqlctl hdfs rmr --path -p 
                  
```
### <a name="examples"></a>Esempi
Rimuovi directory ricorsiva.
```bash
mssqlctl hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file da rimuovere in modo ricorsivo.
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
## <a name="mssqlctl-hdfs-chmod"></a>chmod hdfs mssqlctl
Modificare l'autorizzazione per il file o directory specificata.
```bash
mssqlctl hdfs chmod --path -p 
                    --permission
```
### <a name="examples"></a>Esempi
Modificare l'autorizzazione di file o directory.
```bash
mssqlctl hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file o directory per impostare le autorizzazioni su.
#### `--permission`
Ottetti di autorizzazione da impostare.  Esempio "775".
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
## <a name="mssqlctl-hdfs-chown"></a>mssqlctl hdfs chown
Modificare il proprietario o il gruppo di file specificato.
```bash
mssqlctl hdfs chown --path -p 
                    --owner  
                    --group -g
```
### <a name="examples"></a>Esempi
Modificare il proprietario e il gruppo.
```bash
mssqlctl hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--path -p`
Nome del file o directory per la modifica del proprietario.
#### `--owner`
Per impostare il nome del proprietario.
#### `--group -g`
Nome del gruppo per impostare su.
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

Per altre informazioni su come installare il **mssqlctl** dello strumento, vedere [installare mssqlctl per gestire i cluster di big data di SQL Server 2019](deploy-install-mssqlctl.md).