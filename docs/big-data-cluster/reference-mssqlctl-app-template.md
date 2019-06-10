---
title: riferimento di modello app mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi di modello app mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9e73b0ddf9e30c5e38fd54d34ab93526213fe061
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800967"
---
# <a name="mssqlctl-app-template"></a>modello di app mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **modello di app** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[elenco di modelli di app mssqlctl](#mssqlctl-app-template-list) | Modelli di recupero supportata.
[pull di modello app mssqlctl](#mssqlctl-app-template-pull) | Scaricare i modelli supportati.
## <a name="mssqlctl-app-template-list"></a>elenco di modelli di app mssqlctl
Modelli di recupero supportata disponibili nel repository di github [URL] specificato.
```bash
mssqlctl app template list [--url -u] 
                           
```
### <a name="examples"></a>Esempi
Recuperare tutti i modelli con il percorso predefinito dei repository di modelli.
```bash
mssqlctl app template list
```
Recuperare tutti i modelli in una posizione diversa del repository.
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--url -u`
Specificare un percorso del repository di modelli diversi. Valore predefinito: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-template-pull"></a>pull di modello app mssqlctl
Scaricare i modelli supportati disponibili nel repository di github [URL] specificato.
```bash
mssqlctl app template pull [--name -n] 
                           [--url -u]  
                           [--destination -d]
```
### <a name="examples"></a>Esempi
Scaricare tutti i modelli con il percorso predefinito dei repository di modelli.
```bash
mssqlctl app template pull
```
Scaricare tutti i modelli in una posizione diversa del repository.
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
Scaricare il modello di singole in base al nome.
```bash
mssqlctl app template pull --name ssis            
```
### <a name="optional-parameters"></a>Parametri facoltativi
#### `--name -n`
Nome del modello. Per un elenco completo off namesrun supportata del modello `mssqlctl app template list`
#### `--url -u`
Specificare un percorso del repository di modelli diversi. Valore predefinito: https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
Posizione in cui inserire il modello di struttura dell'applicazione.
`./templates`
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