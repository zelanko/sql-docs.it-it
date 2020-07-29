---
title: Informazioni di riferimento su azdata sql
titleSuffix: SQL Server big data clusters
description: Articolo di riferimento per i comandi azdata sql.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb7dd195d489be289cf434e8e4651ac17c6a6709
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242983"
---
# <a name="azdata-sql"></a>azdata sql

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

L'articolo seguente offre informazioni di riferimento sui comandi `sql` dello strumento `azdata`. Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md).

## <a name="commands"></a>Comandi:
| Comando | Descrizione |
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | L'interfaccia della riga di comando dei database SQL consente agli utenti di interagire con SQL Server tramite T-SQL.
[azdata sql query](#azdata-sql-query) | Il comando di query consente l'esecuzione di una query T-SQL.
## <a name="azdata-sql-shell"></a>azdata sql shell
L'interfaccia della riga di comando dei database SQL consente agli utenti di interagire con SQL Server tramite T-SQL.
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
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.
## <a name="azdata-sql-query"></a>azdata sql query
Il comando di query consente l'esecuzione di una query T-SQL.
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>Esempi
Selezionare l'elenco dei nomi di tabelle.  Il valore predefinito per il database è "master".
```bash
azdata sql query "SELECT name FROM SYS.TABLES"
```
### <a name="required-parameters"></a>Parametri obbligatori
#### `--database -d`
Database in cui eseguire la query.  Il valore predefinito è "master".
#### `-q`
Query SQL da eseguire.
### <a name="global-arguments"></a>Argomenti globali
#### `--debug`
Aumenta il livello di dettaglio della registrazione per mostrare tutti i log di debug.
#### `--help -h`
Visualizza questo messaggio della guida ed esce.
#### `--output -o`
Formato di output.  Valori consentiti: json, jsonc, table, tsv.  Valore predefinito: json.
#### `--query -q`
Stringa di query JMESPath. Per altre informazioni ed esempi, vedere [http://jmespath.org/](http://jmespath.org).
#### `--verbose`
Aumenta il livello di dettaglio della registrazione. Usare --debug per log di debug completi.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su altri comandi `azdata`, vedere [Informazioni di riferimento su azdata](reference-azdata.md). Per altre informazioni su come installare lo strumento `azdata`, vedere [Installare azdata per gestire i cluster Big Data di SQL Server 2019](deploy-install-azdata.md).
