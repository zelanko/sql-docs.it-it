---
title: Sys. systypes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.systypes_TSQL
- systypes_TSQL
- sys.systypes
- systypes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.systypes compatibility view
- systypes system table
ms.assetid: 1b0b1d0c-5f7b-470b-bd52-8bfa922d7889
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5533e521ba28c0190a5be57ed7637632213d7447
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018086"
---
# <a name="syssystypes-transact-sql"></a>sys.systypes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce una riga per ogni tipo di dati di sistema o definito dall'utente nel database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome del tipo di dati.|  
|**tipoX**|**tinyint**|Tipo di dati per l'archiviazione fisica.|  
|**status**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|Tipo di dati esteso definito dall'utente. Causa un errore di overflow o restituisce NULL se il numero di tipi di dati è maggiore di 32.767.|  
|**length**|**smallint**|Lunghezza fisica del tipo di dati.|  
|**xprec**|**tinyint**|Precisione interna utilizzata dal server, da non utilizzare nelle query.|  
|**XScale**|**tinyint**|Scala interna utilizzata dal server, da non utilizzare nelle query.|  
|**TImpossibile**|**int**|ID della stored procedure che include i controlli di integrità per questo tipo di dati.|  
|**domain**|**int**|ID della stored procedure che include i controlli di integrità per questo tipo di dati.|  
|**uid**|**smallint**|ID dello schema del proprietario del tipo.<br /><br /> Per i database aggiornati da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'ID dello schema corrisponde all'ID utente del proprietario.<br /><br /> **\*\* Importanti \* \***  se si usa uno dei seguenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istruzioni DDL, è necessario usare il [Sys. Types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) invece di vista del catalogo **Sys. systypes**.<br /><br /> ALTER AUTHORIZATION ON TYPE<br /><br /> CREATE TYPE<br /><br /> Causa un errore di overflow o restituisce NULL se il numero di utenti e ruoli è maggiore di 32.767.|  
|**reserved**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**collationid**|**int**|Se di tipo carattere, **collationid** è l'id delle regole di confronto del database corrente; in caso contrario, è NULL.|  
|**usertype**|**smallint**|ID tipo utente. Causa un errore di overflow o restituisce NULL se il numero di tipi di dati è maggiore di 32.767.|  
|**variable**|**bit**|Tipo di dati a lunghezza variabile.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**AllowNulls**|**bit**|Indica l'impostazione predefinita relativa al supporto dei valori Null per questo tipo di dati. Questo valore predefinito viene ignorato, se è specificato con valori null [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) oppure [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).|  
|**type**|**tinyint**|Tipo di dati per l'archiviazione fisica.|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Prec**|**smallint**|Livello di precisione per il tipo di dati.<br /><br /> -1 = **xml** o tipi di valori di grandi dimensioni.|  
|**scala**|**tinyint**|Scala per il tipo di dati, basata sulla precisione.<br /><br /> NULL = Tipo di dati non numerico.|  
|**regole di confronto**|**sysname**|Se di tipo carattere, **regole di confronto** regole di confronto del database corrente; in caso contrario, è NULL.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
