---
title: riferimento sql mssqlctl
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi sql mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 536d4712a6ccb288ca60c038a37e99c2be8a5eba
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394203"
---
# <a name="mssqlctl-sql"></a>mssqlctl sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per la **sql** comandi nel **mssqlctl** dello strumento. Per altre informazioni sulle altre **mssqlctl** comandi, vedere [mssqlctl riferimento](reference-mssqlctl.md).

## <a name="commands"></a>Comandi
|     |     |
| --- | --- |
[mssqlctl sql shell](#mssqlctl-sql-shell) | L'interfaccia CLI DB SQL consente all'utente di interagire con SQL Server tramite T-SQL.
[query sql mssqlctl](#mssqlctl-sql-query) | Il comando di query consente l'esecuzione di una query T-SQL.
## <a name="mssqlctl-sql-shell"></a>mssqlctl sql shell
L'interfaccia CLI DB SQL consente all'utente di interagire con SQL Server tramite T-SQL.
```bash
mssqlctl sql shell 
```
### <a name="examples"></a>Esempi
Riga di comando di esempio per avviare l'esperienza interattiva.
```bash
mssqlctl sql shell
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
## <a name="mssqlctl-sql-query"></a>query sql mssqlctl
Il comando di query consente l'esecuzione di una query T-SQL.
```bash
mssqlctl sql query --database -d 
                   -q
```
### <a name="examples"></a>Esempi
Selezionare l'elenco di nomi di tabelle.  Impostazioni predefinite del database master.
```bash
mssqlctl sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--database -d`
Database per eseguire query in.  Valore predefinito è master.
#### `-q`
Query T-SQL da eseguire.
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