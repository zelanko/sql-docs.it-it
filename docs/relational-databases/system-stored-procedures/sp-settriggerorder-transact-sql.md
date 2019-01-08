---
title: sp_settriggerorder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: acbdb4b406d3ec0c2820e2be7988c32af249379c
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590315"
---
# <a name="spsettriggerorder-transact-sql"></a>sp_settriggerorder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Specifica il primo o l'ultimo trigger AFTER attivato. I trigger AFTER compresi fra il primo e l'ultimo vengono eseguiti in base a un ordine non definito.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@triggername=** ] **'**[ _triggerschema_**.**] _triggername_**'**  
 Nome del trigger e schema al quale appartiene, se applicabile, il cui ordine deve essere impostato o modificato. [_triggerschema_**.**] *triggername* viene **sysname**. Se il nome specificato non corrisponde a un trigger oppure corrisponde a un trigger INSTEAD OF, viene restituito un errore. *triggerschema* non è possibile specificare per i trigger DDL o logon.  
  
 [ **@order=** ] **'**_value_**'**  
 Impostazione del nuovo ordine del trigger. *valore* viene **varchar (10)** e può essere uno dei valori seguenti.  
  
> [!IMPORTANT]  
>  Il **primo** e **ultima** trigger devono essere due trigger distinti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Primo**|Trigger avviato per primo.|  
|**Ultimo**|Trigger avviato per ultimo.|  
|**None**|Il trigger viene attivato in base a un ordine non definito.|  
  
 [  **@stmttype=** ] **'**_statement_type_**'**  
 Specifica l'istruzione SQL che attiva il trigger. *statement_type* viene **varchar (50)** e può essere INSERT, UPDATE, DELETE, LOGON o qualsiasi [!INCLUDE[tsql](../../includes/tsql-md.md)] elencato nell'evento dell'istruzione [eventi DDL](../../relational-databases/triggers/ddl-events.md). Non è possibile specificare gruppi di eventi.  
  
 Un trigger può essere designato come il **primo** oppure **ultima** trigger per un tipo di istruzione solo dopo che tale trigger è stato definito come trigger per tale tipo di istruzione. Ad esempio, attivare **TR1** può essere designato **primo** per l'inserimento nella tabella **T1** se **TR1** è definito come trigger INSERT. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] restituisce un errore se **TR1**, che è stata definita solo come trigger INSERT, viene impostato come una **prima**, oppure **ultimo**, trigger per un'istruzione UPDATE. Per altre informazioni, vedere la sezione Osservazioni.  
  
 **@namespace=** { **'DATABASE'** | **'SERVER'** | NULL}  
 Quando *triggername* è un trigger DDL, **@namespace** specifica se *triggername* è stata creata con ambito database o ambito server. Se *triggername* un trigger logon, è necessario specificare SERVER. Per altre informazioni sull'ambito del trigger DDL, vedere [trigger DDL](../../relational-databases/triggers/ddl-triggers.md). Se non specificato o se viene specificato NULL, *triggername* è un trigger DML.  
  
||  
|-|  
|SERVER si applica alle versioni da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
  
## <a name="dml-triggers"></a>Trigger DML  
 Può esistere un solo **primo** e una **ultima** trigger per ogni istruzione in una singola tabella.  
  
 Se un **primo** trigger è già definito nel database, di tabella o server, non è possibile definire un nuovo trigger **primo** per la stessa tabella, database o server per lo stesso *statement_type* . Questa restrizione si applica anche **ultimo** trigger.  
  
 La replica genera automaticamente un primo trigger per ogni tabella inclusa in una sottoscrizione ad aggiornamento in coda o ad aggiornamento immediato. La replica richiede che il proprio trigger sia il primo trigger. La replica genera un errore se si cerca di includere una tabella con un primo trigger in una sottoscrizione ad aggiornamento immediato o ad aggiornamento in coda. Se si prova a impostare un trigger come primo dopo l'inclusione di una tabella in una sottoscrizione, **sp_settriggerorder** restituisce un errore. Se si utilizza ALTER TRIGGER nel trigger di replica, o **sp_settriggerorder** per modificare il trigger di replica a un **ultima** oppure **None** trigger, la sottoscrizione viene non funzionare correttamente.  
  
## <a name="ddl-triggers"></a>Trigger DDL  
 Se un trigger DDL con ambito database e un trigger DDL con ambito server esistono sullo stesso evento, è possibile specificare che entrambi i trigger sono un **primo** trigger o una **ultima** trigger. Tuttavia, i trigger con ambito server vengono sempre generati per primi. In generale, l'ordine di esecuzione dei trigger DDL che esistono sullo stesso evento è il seguente:  
  
1.  Il trigger a livello di server contrassegnato **primo**.  
  
2.  Altri trigger a livello del server  
  
3.  Il trigger a livello di server contrassegnato **ultimo**.  
  
4.  Il trigger a livello di database contrassegnato **primo**.  
  
5.  Altri trigger a livello del database  
  
6.  Il trigger a livello di database contrassegnato **ultimo**.  
  
## <a name="general-trigger-considerations"></a>Considerazioni generali sui trigger  
 Se un'istruzione ALTER TRIGGER viene modificato un primo o ultimo trigger, il **primo** o **ultima** attributo originariamente impostato per il trigger viene eliminato e il valore viene sostituito con **None**. Il valore di ordine deve essere reimpostato tramite **sp_settriggerorder**.  
  
 Se lo stesso trigger deve essere designato come primo o ultimo ordine per più di un tipo di istruzione, **sp_settriggerorder** deve essere eseguita per ogni tipo di istruzione. Inoltre, il trigger deve essere prima definito per un tipo di istruzione prima può essere designato come il **primo** oppure **ultima** trigger da attivare per tale tipo di istruzione.  
  
## <a name="permissions"></a>Permissions  
 Per impostare l'ordine di un trigger DDL con ambito server (creato ON ALL SERVER) o un trigger LOGON è necessaria l'autorizzazione CONTROL SERVER nel server.  
  
 Per impostare l'ordine di attivazione di un trigger DDL nell'ambito del database (creato tramite l'istruzione ON DATABASE), è necessario disporre dell'autorizzazione ALTER ANY DATABASE DDL TRIGGER.  
  
 Per impostare l'ordine di attivazione di un trigger DML, è necessario disporre dell'autorizzazione ALTER per la tabella o vista in cui è stato definito il trigger.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>A. Impostazione dell'ordine di attivazione per un trigger DML  
 Nell'esempio seguente il trigger `uSalesOrderHeader` viene definito come primo trigger da attivare dopo l'esecuzione di un'operazione `UPDATE` nella tabella `Sales.SalesOrderHeader`.  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>b. Impostazione dell'ordine di attivazione per un trigger DDL  
 Nell'esempio seguente il trigger `ddlDatabaseTriggerLog` viene definito come primo trigger da attivare dopo che si è verificato un evento `ALTER_TABLE` nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
