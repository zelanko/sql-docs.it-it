---
title: Conversioni - SQL Server Machine Learning di tipi di dati Python-to-SQL
description: Esaminare il converstions tipo di dati implicite ed esplicite tra codice Python e SQL Server in analisi scientifica dei dati e soluzioni di machine learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9578f81146f0dab42e7a607b9e8ab410313958d4
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431977"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Mapping dei tipi di dati tra codice Python e SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Per le soluzioni di Python che eseguono la funzionalità di integrazione di Python in SQL Server Machine Learning Services, esaminare l'elenco dei tipi di dati non supportati e conversioni di tipi di dati che potrebbero essere eseguite in modo implicito quando i dati vengono passati tra codice Python e SQL Server.

## <a name="python-version"></a>Versione di Python

Distribuzione di SQL Server 2017 Anaconda 4.2 e in Python 3.6.

Un sottoinsieme delle funzionalità RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, forse alcuni altri) viene fornito tramite le API Python, usando un nuovo pacchetto di Python **revoscalepy**. È possibile usare questo pacchetto per lavorare con i dati usando query di dati SQL, file XDF o frame di dati Pandas.

Per altre informazioni, vedere [modulo revoscalepy in SQL Server](ref-py-revoscalepy.md) e [revoscalepy di riferimento alle funzioni](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

Python supporta un numero limitato di tipi di dati rispetto a SQL Server. Di conseguenza, ogni volta che si utilizzano dati da SQL Server negli script di Python, i dati potrebbero essere implicitamente convertiti in un tipo di dati compatibile. Tuttavia, spesso una conversione esatta non può essere eseguita automaticamente e viene restituito un errore.

## <a name="python-and-sql-data-types"></a>Tipi di dati SQL e Python

Questa tabella elenca le conversioni implicite che vengono fornite. Non sono supportati altri tipi di dati.

|SQLtype|Tipo di Python|
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

## <a name="see-also"></a>Vedere anche

