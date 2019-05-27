---
title: MIN_ACTIVE_ROWVERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MIN_ACTIVE_ROWVERSION
- MIN_ACTIVE_ROWVERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MIN_ACTIVE_ROWVERSION function [Transact-SQL]
ms.assetid: 87c89547-8ea1-4820-b75e-36be683e4e10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c4f21916de6c03c8e592702e58af481ef64cbb6d
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944219"
---
# <a name="minactiverowversion-transact-sql"></a>MIN_ACTIVE_ROWVERSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce il valore **rowversion** attivo più basso nel database corrente. Un valore **rowversion** è attivo se viene usato in una transazione di cui non è ancora stato eseguito il commit. Per altre informazioni, vedere [rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md).  
  
> [!NOTE]  
>  Il tipo di dati **rowversion** è anche noto come **timestamp**.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
MIN_ACTIVE_ROWVERSION  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 Restituisce un valore **binary(8)** .  
  
## <a name="remarks"></a>Remarks  
 MIN_ACTIVE_ROWVERSION è una funzione non deterministica che restituisce il valore di **rowversion** attivo più basso nel database corrente. Quando viene eseguita un'istruzione INSERT o UPDATE in una tabella contenente una colonna di tipo **rowversion** , viene solitamente generato un nuovo valore **rowversion**. Se nel database non sono presenti valori attivi, MIN_ACTIVE_ROWVERSION restituisce lo stesso valore di @@DBTS + 1.  
  
 MIN_ACTIVE_ROWVERSION è utile in scenari come la sincronizzazione dei dati che usano i valori di **rowversion** per raggruppare i set di modifiche. Se un'applicazione usa @@DBTS invece di MIN_ACTIVE_ROWVERSION, potrebbero andare perse modifiche attive al momento della sincronizzazione.  
  
 La funzione MIN_ACTIVE_ROWVERSION non è interessata dalle modifiche apportate ai livelli di isolamento delle transazioni.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituiti valori di **rowversion** usando `MIN_ACTIVE_ROWVERSION` e `@@DBTS`. Si noti che i valori sono diversi quando non vi sono transazioni attive nel database.  
  
```  
-- Create a table that has a ROWVERSION column in it.  
CREATE TABLE RowVersionTestTable (rv ROWVERSION)  
GO  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()   
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E2  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E3  
  
-- Insert a row.  
INSERT INTO RowVersionTestTable VALUES (DEFAULT)  
SELECT * FROM RowVersionTestTable  
GO  
---------------- Results ----------------  
--rv  
--0x00000000000007E3  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()  
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E3  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E4  
  
-- Insert a new row inside a transaction but do not commit.  
BEGIN TRAN  
INSERT INTO RowVersionTestTable VALUES (DEFAULT)  
SELECT * FROM RowVersionTestTable  
GO  
---------------- Results ----------------  
--rv  
--0x00000000000007E3  
--0x00000000000007E4  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()   
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E4  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E4  
  
-- Commit the transaction.  
COMMIT  
GO  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()  
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E4  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E5  
```  
  
## <a name="see-also"></a>Vedere anche  
 [@@DBTS &#40;Transact-SQL&#41;](../../t-sql/functions/dbts-transact-sql.md)   
 [rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)  
  
  
