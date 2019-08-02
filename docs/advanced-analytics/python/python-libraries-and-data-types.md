---
title: Conversioni dei tipi di dati da Python a SQL
description: Esaminare le conversioni di tipi di dati implicite ed esplicite tra Python e SQL Server nelle soluzioni di data science e machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 690126098bbbd3ab26add51a0484f735120351de
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715778"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Mapping dei tipi di dati tra Python e SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Per le soluzioni Python eseguite nella funzionalità di integrazione di Python in SQL Server Machine Learning Services, esaminare l'elenco dei tipi di dati non supportati e le conversioni dei tipi di dati che possono essere eseguite in modo implicito quando i dati vengono passati tra Python e SQL Server.

## <a name="python-version"></a>Versione di Python

Un subset della funzionalità RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, forse alcuni altri) viene fornito usando le API Python, usando un nuovo pacchetto python **revoscalepy**. È possibile usare questo pacchetto per lavorare con i dati usando i frame di dati Pandas, i file XDF o le query di dati SQL.

Per ulteriori informazioni, vedere il [modulo revoscalepy nella Guida di riferimento alle funzioni SQL Server](ref-py-revoscalepy.md) e [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

Python supporta un numero limitato di tipi di dati rispetto a SQL Server. Di conseguenza, ogni volta che si usano i dati di SQL Server negli script Python, i dati potrebbero essere convertiti in modo implicito in un tipo di dati compatibile. Tuttavia, spesso non è possibile eseguire automaticamente una conversione esatta e viene restituito un errore.

## <a name="python-and-sql-data-types"></a>Tipi di dati Python e SQL

In questa tabella sono elencate le conversioni implicite fornite. Altri tipi di dati non sono supportati.

|SQLtype|Tipo Python|
|-------|-----------|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**ntext**|`str`|
