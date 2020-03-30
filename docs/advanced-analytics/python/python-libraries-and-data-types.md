---
title: Convertire tipi di dati Python e SQL
description: Esaminare le conversioni dei tipi di dati implicite ed esplicite tra Python e SQL Server nelle soluzioni di data science e Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f22f838bc78d4791e73a1d107cd253aae314d205
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727520"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Mapping dei tipi di dati tra Python e SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Per le soluzioni Python eseguite nella funzionalità di integrazione di Python in Machine Learning Services per SQL Server, esaminare l'elenco dei tipi di dati non supportati e le conversioni dei tipi di dati che possono essere eseguite in modo implicito quando i dati vengono passati tra Python e SQL Server.

## <a name="python-version"></a>Versione di Python

Un subset della funzionalità RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees e poche altre funzioni) è disponibile con le API Python, se si usa il nuovo pacchetto Python **revoscalepy**. Con questo pacchetto è possibile lavorare con i dati usando frame di dati Pandas, file XDF o query di dati SQL.

Per altre informazioni, vedere [Modulo revoscalepy in SQL Server](ref-py-revoscalepy.md) e [Informazioni di riferimento per le funzioni di revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

Python supporta un numero limitato di tipi di dati rispetto a SQL Server. Di conseguenza, ogni volta che si usano dati di SQL Server all'interno di script Python, i dati possono essere convertiti in modo implicito in un tipo di dati compatibile. Spesso, tuttavia, non è possibile eseguire automaticamente una conversione esatta e viene restituito un errore.

## <a name="python-and-sql-data-types"></a>Tipi di dati Python e SQL

Questa tabella elenca le conversioni implicite disponibili. Altri tipi di dati non sono supportati.

|Tipo SQL|Tipo Python|
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
