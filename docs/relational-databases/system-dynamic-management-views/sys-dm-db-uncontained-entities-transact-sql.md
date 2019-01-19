---
title: sys.dm_db_uncontained_entities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_uncontained_entities
- dm_db_uncontained_entities_TSQL
- sys.dm_db_uncontained_entities_TSQL
- dm_db_uncontained_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_uncontained_entities dynamic management view
ms.assetid: f417efd4-8c71-4f81-bc9c-af13bb4b88ad
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bb3351abb75827c3eac7f48687823ffeed76986c
ms.sourcegitcommit: 2e8783e6bedd9597207180941be978f65c2c2a2d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2019
ms.locfileid: "54405611"
---
# <a name="sysdmdbuncontainedentities-transact-sql"></a>sys.dm_db_uncontained_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Mostra qualsiasi oggetto non contenuto utilizzato nel database. Gli oggetti non contenuti sono oggetti che superano il limite del database in un database indipendente. Questa vista è accessibile sia da un database indipendente che da un database non indipendente. Se db_uncontained_entities è vuoto, il database non utilizza entità non contenute.  
  
 Se un modulo supera il limite del database più di una volta, viene riportato solo il primo superamento individuato.  
  
||||  
|-|-|-|  
|**Nome colonna**|**Tipo**|**Descrizione**|  
|*class*|**int**|1 = Oggetto o colonna (include moduli, XP, viste, sinonimi e tabelle).<br /><br /> 4 = Entità di database<br /><br /> 5 = Assembly<br /><br /> 6 = Tipo<br /><br /> 7 = Indice (indice full-text)<br /><br /> 12 = Trigger DDL database<br /><br /> 19 = Route<br /><br /> 30 = Specifica del controllo|  
|*class_desc*|**nvarchar(120)**|Descrizione della classe dell'entità. Uno dei seguenti in base alla classe:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **DATABASE_PRINCIPAL**<br /><br /> **ASSEMBLY**<br /><br /> **TYPE**<br /><br /> **INDEX**<br /><br /> **DATABASE_DDL_TRIGGER**<br /><br /> **ROUTE**<br /><br /> **AUDIT_SPECIFICATION**|  
|*major_id*|**int**|ID dell'entità.<br /><br /> Se *classe* = 1, quindi object_id<br /><br /> Se *classe* = 4, quindi principal_id.<br /><br /> Se *classe* = 5, allora assembly_id.<br /><br /> Se *classe* = 6, allora user_type_id.<br /><br /> Se *classe* = 7 then index_id.<br /><br /> Se *classe* = 12, quindi OBJECT_ID.<br /><br /> Se *classe* = 19, Route_ID.<br /><br /> Se *classe* = 30, allora sys. database_audit_specifications.database_specification_id.|  
|*statement_line_number*|**int**|Se la classe è un modulo, restituisce il numero di riga in cui si trova l'utilizzo non contenuto.  In caso contrario, il valore è Null.|  
|*statement_ offset_begin*|**int**|Se la classe è un modulo, indica la posizione iniziale dell'utilizzo non contenuto partendo da 0. Il valore viene espresso in byte. In caso contrario, il valore restituito è Null.|  
|*statement_ offset_end*|**int**|Se la classe è un modulo, indica la posizione finale dell'utilizzo non contenuto partendo da 0. Il valore viene espresso in byte. Il valore -1 indica la fine del modulo. In caso contrario, il valore restituito è Null.|  
|*statement_type*|**nvarchar(512)**|Tipo di istruzione.|  
|*nome feature_*|**nvarchar(256)**|Restituisce il nome esterno dell'oggetto.|  
|*feature_type_name*|**nvarchar(256)**|Restituisce il tipo di funzionalità.|  
  
## <a name="remarks"></a>Note  
 db_uncontained_entities Mostra le entità che potenzialmente possono superare il limite del database. Restituirà le entità utente che possono utilizzare gli oggetti al di fuori del database.  
  
 I tipi di funzionalità seguenti vengono segnalati.  
  
-   Comportamento di indipendenza sconosciuto (SQL dinamico o risoluzione dei nomi posticipata)  
  
-   Comando DBCC  
  
-   Stored procedure di sistema  
  
-   Funzione scalare di sistema  
  
-   Funzione con valori di tabella di sistema  
  
-   Funzione predefinita di sistema  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 db_uncontained_entities restituisce solo oggetti per cui l'utente dispone di un tipo di autorizzazione. Per una valutazione completa di indipendenza del database, questa funzione deve essere usata da un utente con privilegi elevati, ad esempio un membro del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata una procedura denominata P1, quindi viene eseguita una query su `sys.dm_db_uncontained_entities`. Nella query viene segnalato che P1 utilizza **sys.endpoints** , che si trova all'esterno del database.  
  
```sql  
CREATE DATABASE Test;  
GO  
  
USE Test;  
GO  
CREATE PROC P1  
AS   
SELECT * FROM sys.endpoints ;  
GO  
SELECT SO.name, UE.* FROM sys.dm_db_uncontained_entities AS UE  
LEFT JOIN sys.objects AS SO  
    ON UE.major_id = SO.object_id;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Database indipendenti](../../relational-databases/databases/contained-databases.md)  
  
  
