---
title: sp_db_vardecimal_storage_format (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_vardecimal_storage_format
- sp_db_vardecimal_storage_format_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_vardecimal_storage_format
- decimal data type, compressing
- compressing decimal data
- numeric data type, compressing
- database compression [SQL Server]
- table compression [SQL Server]
ms.assetid: 9920b2f7-b802-4003-913c-978c17ae4542
author: stevestein
ms.author: sstein
ms.openlocfilehash: 28628ee5dc8ff1bde7906dfea7fca60470720e11
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108217"
---
# <a name="spdbvardecimalstorageformat-transact-sql"></a>sp_db_vardecimal_storage_format (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce lo stato corrente del formato di archiviazione vardecimal di un database oppure abilita il formato di archiviazione vardecimal per un database.  A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], i database utente sono sempre abilitati. L'abilitazione del formato di archiviazione vardecimal per i database è necessaria solo in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
> [!IMPORTANT]  
>  La modifica dello stato del formato di archiviazione vardecimal di un database può influire su backup e recupero, mirroring del database, sp_attach_db, log shipping e replica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_db_vardecimal_storage_format [ [ @dbname = ] 'database_name']   
    [ , [ @vardecimal_storage_format = ] { 'ON' | 'OFF' } ]   
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @dbname=] '*nome_database*'  
 Nome del database per il quale deve essere modificato il formato di archiviazione. *database_name* viene **sysname**, non prevede alcun valore predefinito. Se il nome del database viene omesso, viene restituito lo stato del formato di archiviazione vardecimal di tutti i database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [ @vardecimal_storage_format=] {'ON' |' DISATTIVARE '}  
 Specifica se il formato di archiviazione vardecimal è abilitato. @vardecimal_storage_format può essere ON oppure OFF. Il parametro è **varchar(3)** , non prevede alcun valore predefinito. Se viene specificato il nome di un database ma viene omesso @vardecimal_storage_format, viene restituita l'impostazione corrente del database specificato. Questo argomento non ha effetto in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versioni successive.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Se il formato di archiviazione del database non può essere modificato, sp_db_vardecimal_storage_format restituisce un errore. Se lo stato corrente del database corrisponde a quello specificato, la stored procedure non produce alcun effetto.  
  
 Se il @vardecimal_storage_format argomento non viene specificato, vengono restituite le colonne Database Name e Vardecimal State.  
  
## <a name="remarks"></a>Note  
 sp_db_vardecimal_storage_format restituisce lo stato di vardecimal ma non consente di modificare tale stato.  
  
 sp_db_vardecimal_storage_format avrà esito negativo nelle circostanze seguenti:  
  
-   Non sono presenti utenti attivi nel database.  
  
-   È abilitato il mirroring del database.  
  
-   L'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta il formato di archiviazione vardecimal.  
  
 Per modificare lo stato del formato di archiviazione vardecimal in OFF, è necessario che un database sia impostato sulla modalità di recupero con registrazione minima. In caso di impostazione di un database su tale modalità, la catena di log è interrotta. Dopo aver impostato lo stato del formato di archiviazione vardecimal su OFF, eseguire un backup completo del database.  
  
 La modifica dello stato in OFF avrà esito negativo se sono presenti tabelle in cui viene utilizzata la compressione di database di tipo vardecimal. Per modificare il formato di archiviazione di una tabella, usare [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Per determinare le tabelle di un database in cui viene utilizzato il formato di archiviazione vardecimal, utilizzare la funzione `OBJECTPROPERTY` e cercare la proprietà `TableHasVarDecimalStorageFormat`, come illustrato nell'esempio seguente.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT name, object_id, type_desc  
FROM sys.objects   
 WHERE OBJECTPROPERTY(object_id,   
   N'TableHasVarDecimalStorageFormat') = 1 ;  
GO  
```  
  
## <a name="examples"></a>Esempi  
 Tramite il codice seguente viene abilitata la compressione nel database `AdventureWorks2012`, viene verificato lo stato e quindi vengono compresse le colonne decimal e numeric della tabella `Sales.SalesOrderDetail`.  
  
```  
USE master ;  
GO  
  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON' ;  
GO  
  
-- Check the vardecimal storage format state for  
-- all databases in the instance.  
EXEC sp_db_vardecimal_storage_format ;  
GO  
  
USE AdventureWorks2012 ;  
GO  
  
EXEC sp_tableoption 'Sales.SalesOrderDetail', 'vardecimal storage format', 1 ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
