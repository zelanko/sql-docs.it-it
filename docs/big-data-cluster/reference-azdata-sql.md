---
title: riferimento SQL azdata
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi SQL azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 90512592901fcf83e4697b5eefc80a6df7aeb032
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426021"
---
# <a name="azdata-sql"></a>azdata SQL

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

L'articolo seguente fornisce informazioni di riferimento per i comandi **SQL** nello strumento **azdata** . Per ulteriori informazioni su altri comandi **azdata** , vedere [riferimento azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
|     |     |
| --- | --- |
[Shell SQL azdata](#azdata-sql-shell) | L'interfaccia della riga di comando di SQL database consente all'utente di interagire con SQL Server tramite T-SQL.
[query SQL di azdata](#azdata-sql-query) | Il comando di query consente l'esecuzione di una query T-SQL.
## <a name="azdata-sql-shell"></a>Shell SQL azdata
L'interfaccia della riga di comando di SQL database consente all'utente di interagire con SQL Server tramite T-SQL.
```bash
azdata sql shell 
```
### <a name="examples"></a>Esempi
Esempio di riga di comando per avviare l'esperienza interattiva.
```bash
azdata sql shell
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
## <a name="azdata-sql-query"></a>query SQL di azdata
Il comando di query consente l'esecuzione di una query T-SQL.
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>Esempi
Consente di selezionare l'elenco dei nomi delle tabelle.  Il valore predefinito del database è master.
```bash
azdata sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--database -d`
Database in cui eseguire la query.  Il valore predefinito è master.
#### `-q`
Query T-SQL da eseguire.
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

Per altre informazioni su come installare lo strumento **azdata** , vedere [Install azdata to manage SQL Server 2019 Big Data Clusters](deploy-install-azdata.md).
