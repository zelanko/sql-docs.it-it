---
title: PARSENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs:
- TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9867f73e382dbf59290844b0a7597eece7d4399a
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944282"
---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Restituisce la parte specificata del nome di un oggetto. Le parti di un oggetto che è possibile recuperare sono il nome dell'oggetto, il nome del proprietario, il nome del database e il nome del server.  
  
> [!NOTE]  
>  La funzione PARSENAME non indica se esiste un oggetto avente il nome specificato. PARSENAME restituisce solo la parte specificata del nome di oggetto specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>Argomenti  
 '*object_name*'  
 Nome dell'oggetto per cui recuperare la parte specificata. *object_name* è di tipo **sysname**. Questo parametro rappresenta un nome di oggetto che può essere qualificato facoltativamente. Se vengono qualificate tutte le parti del nome dell'oggetto, il nome può essere costituito da quattro parti, ovvero nome del server, nome del database, nome del proprietario e nome dell'oggetto.  
  
 *object_piece*  
 Parte dell'oggetto da restituire. *object_piece* è di tipo **int**. I possibili valori sono i seguenti:  
  
 1 = nome dell'oggetto  
  
 2 = nome dello schema  
  
 3 = nome del database  
  
 4 = nome del server  
  
## <a name="return-types"></a>Tipi restituiti  
 **sysname**  
  
## <a name="remarks"></a>Remarks  
 PARSENAME restituisce NULL se si verifica una delle condizioni seguenti:  
  
-   *object_name* o *object_piece* è NULL.  
  
-   Si verifica un errore di sintassi.  
  
 La lunghezza della parte dell'oggetto richiesta è uguale a 0 e la parte dell'oggetto non è un identificatore di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido. Se la lunghezza del nome dell'oggetto è pari a 0, il nome completo risulta non valido.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato `PARSENAME` per restituire informazioni sulla tabella `Person` nel database `AdventureWorks2012`.  
  
```  
-- Uses AdventureWorks  
  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
Object Name
------------------------------
DimCustomer

(1 row(s) affected)

Schema Name
------------------------------
dbo

(1 row(s) affected)

Database Name
------------------------------
AdventureWorksPDW2012

(1 row(s) affected)

Server Name
------------------------------
(null)

(1 row(s) affected)
```
  
## <a name="see-also"></a>Vedere anche  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

