---
title: Tipi di dati (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a03da24fe18f0d910f5054d8cfb321c42d633db8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113736"
---
# <a name="data-types-transact-sql"></a>Tipi di dati (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ogni colonna, variabile locale, espressione e parametro è associato un tipo di dati. Un tipo di dati è un attributo che specifica il tipo di dati che l'oggetto può contenere, ovvero numeri interi, caratteri, valute, date e ore, stringhe binarie e così via.
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile un set di tipi di dati di sistema che definisce tutti i tipi di dati utilizzabili con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È anche possibile definire tipi di dati personalizzati in [!INCLUDE[tsql](../../includes/tsql-md.md)] o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. I tipi di dati alias sono basati sui tipi di dati di sistema. Per altre informazioni sui tipi di dati alias, vedere [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md). I tipi definiti dall'utente derivano le loro caratteristiche dai metodi e dagli operatori di una classe che viene creata utilizzando uno dei linguaggi di programmazione supportati da [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].
  
Quando due espressioni con tipi di dati, regole di confronto, precisione, scala o lunghezza diversi vengono combinati mediante un operatore, le caratteristiche del risultato vengono determinate come descritto di seguito.
-   Il tipo di dati del risultato viene determinato applicando le regole sulla precedenza dei tipi di dati ai tipi di dati delle espressioni di input. Per altre informazioni, vedere [Precedenza dei tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
-   Le regole di confronto del risultato sono determinate dalle regole di precedenza delle regole di confronto quando il tipo di dati del risultato è **char**, **varchar**, **text**, **nchar**, **nvarchar** o **ntext**. Per altre informazioni, vedere [Precedenza delle regole di confronto &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md).  
-   La precisione, la scala e la lunghezza del risultato dipendono dalla precisione, dalla scala e dalla lunghezza delle espressioni di input. Per altre informazioni, vedere [Precisione, scala e lunghezza &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono disponibili sinonimi dei tipi di dati per la compatibilità con ISO. Per altre informazioni, vedere [Sinonimi dei tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
## <a name="data-type-categories"></a>Categorie dei tipi di dati
I tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono organizzati nelle categorie seguenti:
  
|||  
|-|-|  
|Dati numerici esatti|Stringhe di testo Unicode|  
|Numerici approssimati|Stringhe binarie|  
|Date e Time|Altri tipi di dati|  
|Stringhe di caratteri||  
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a seconda delle caratteristiche relative all'archiviazione, alcuni tipi di dati appartengono ai gruppi seguenti:
-   Tipi di dati per valori di grandi dimensioni: **varchar(max)** e **nvarchar(max)**  
-   Tipi di dati per oggetti di grandi dimensioni: **text**, **ntext**, **image**, **varbinary(max)** e **xml**  
  
    > [!NOTE]  
    >  sp_help restituisce -1 per la lunghezza dei tipi di dati per valori di grandi dimensioni e **xml**.  
  
### <a name="exact-numerics"></a>Dati numerici esatti
  
|||  
|-|-|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|[smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)||  
  
### <a name="approximate-numerics"></a>Numerici approssimati
  
|||  
|-|-|  
|[float](../../t-sql/data-types/float-and-real-transact-sql.md)|[real](../../t-sql/data-types/float-and-real-transact-sql.md)|  
  
### <a name="date-and-time"></a>Date e Time
  
|||  
|-|-|  
|[data](../../t-sql/data-types/date-transact-sql.md)|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|[time](../../t-sql/data-types/time-transact-sql.md)|  
  
### <a name="character-strings"></a>Stringhe di caratteri
  
|||  
|-|-|  
|[char](../../t-sql/data-types/char-and-varchar-transact-sql.md)|[varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|[text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="unicode-character-strings"></a>Stringhe di testo Unicode
  
|||  
|-|-|  
|[nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|[nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
|[ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="binary-strings"></a>Stringhe binarie
  
|||  
|-|-|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|[image](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="other-data-types"></a>Altri tipi di dati
  
|||  
|-|-|  
|[cursor](../../t-sql/data-types/cursor-transact-sql.md)|[rowversion](../../t-sql/data-types/rowversion-transact-sql.md)|  
|[hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)|  
|[sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)|[xml](../../t-sql/xml/xml-transact-sql.md)|  
|[Tipi di geometria spaziale](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) |[Tipi di geografia spaziale](../../t-sql/spatial-geography/spatial-types-geography.md)|  
|[table](../../t-sql/data-types/table-transact-sql.md) | |
  
## <a name="see-also"></a>Vedere anche
[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[Espressioni &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funzioni &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  
