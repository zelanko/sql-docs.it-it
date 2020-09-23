---
description: DBCC SHRINKLOG (Parallel Data Warehouse)
title: DBCC SHRINKLOG (Parallel Data Warehouse)
ms.custom: ''
ms.date: 03/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bae2ef1468110ba89d77d5f7a6360aecb324abd0
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076700"
---
# <a name="dbcc-shrinklog-parallel-data-warehouse"></a>DBCC SHRINKLOG (Parallel Data Warehouse)

[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

Riduce le dimensioni del log delle transazioni *nell'appliance* per il database [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. I dati vengono deframmentati per compattare il log delle transazioni. Nel corso del tempo, il log delle transazioni del database può diventare frammentato e inefficiente. Usare DBCC SHRINKLOG per ridurre la frammentazione e le dimensioni del log.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  

## <a name="arguments"></a>Argomenti

SIZE = { *target_size* [ MB \| **GB** \| TB ]  } \| **DEFAULT**.  
*target_size* è la dimensione desiderata per il log delle transazioni, in tutti i nodi di calcolo, al termine dell'esecuzione di DBCC SHRINKLOG. Si tratta di un valore intero maggiore di 0.  
Le dimensioni del log vengono misurate in megabyte (MB), gigabyte (GB) o terabyte (TB). Il valore rappresenta le dimensioni complessive del log delle transazioni in tutti i nodi di calcolo.  
Per impostazione predefinita, DBCC SHRINKLOG consente di ridurre il log delle transazioni alle dimensioni archiviate nei metadati per il database. Le dimensioni del log nei metadati sono determinate dal parametro LOG_SIZE in [CREATE DATABASE &#40;Azure Synapse Analytics&#41; ](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) o [ALTER DATABASE &#40;Azure Synapse Analytics&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md). DBCC SHRINKLOG riduce le dimensioni del log delle transazioni alle dimensioni predefinite quando è stato specificato `SIZE=DEFAULT`, oppure quando la clausola `SIZE` viene omessa.
  
WITH NO_INFOMSGS  
Nei risultati DBCC SHRINKLOG non vengono visualizzati i messaggi informativi.  
  
## <a name="permissions"></a>Autorizzazioni

È necessario avere l'autorizzazione ALTER SERVER STATE.

## <a name="general-remarks"></a>Osservazioni generali

DBCC SHRINKLOG non modifica le dimensioni del log archiviate nei metadati per il database. I metadati continuano a contenere il parametro LOG_SIZE specificato nell'istruzione CREATE DATABASE o ALTER DATABASE.
  
## <a name="examples"></a>Esempi

### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>R. Ridurre il log delle transazioni alle dimensioni originali specificate da CREATE DATABASE.  
Si supponga che il log delle transazioni per il database Addresses sia stato impostato su 100 MB quando il database è stato creato. In altre parole, l'istruzione CREATE DATABASE per il database Addresses era LOG_SIZE = 100 MB. A questo punto, si supponga che il file di log abbia raggiunto i 150 MB che e lo si voglia riportare nuovamente a 100 MB.
  
Ognuna delle istruzioni seguenti tenterà di ridurre il log delle transazioni per il database di Addresses fino a riportarlo alle dimensioni predefinite pari a 100 MB. Se la riduzione del log a 100 MB comporta la perdita di dati, DBCC SHRINKLOG riduce il log alle dimensioni più piccole possibili, superiori a 100 MB, senza perdere dati.

```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```
