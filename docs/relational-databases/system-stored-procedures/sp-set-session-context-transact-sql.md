---
title: sp_set_session_context (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 25f9d67ee50f7c33391027d69c7db87aac8d7210
ms.sourcegitcommit: 869d4de6c807a37873b66e5479d2c5ceff9efb85
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2019
ms.locfileid: "67559430"
---
# <a name="spsetsessioncontext-transact-sql"></a>sp_set_session_context (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Imposta una coppia chiave-valore nel contesto della sessione.  
  

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_set_session_context [ @key= ] N'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @key=] N'key'  
 La chiave viene impostata, di tipo **sysname**. La dimensione massima della chiave è 128 byte.  
  
 [ @value=] 'value'  
 Il valore della chiave specificata, di tipo **sql_variant**. Impostazione di un valore null libera la memoria. Le dimensioni massime sono pari a 8.000 byte.  
  
 [ @read_only= ] { 0 | 1 }  
 Un flag di tipo **bit**. Se è 1, quindi il valore della chiave specificata non può essere più modificato in questa connessione logica. Se 0 (impostazione predefinita), quindi il valore può essere modificato.  
  
## <a name="permissions"></a>Permissions  
 Qualsiasi utente può impostare un contesto di sessione per la propria sessione.  
  
## <a name="remarks"></a>Note  
 Analogamente alle altre stored procedure, solo i valori letterali e variabili (chiamate di funzione o espressioni not) possono essere passate come parametri.  
  
 Le dimensioni totali del contesto della sessione sono limitata a 1 MB. Se si imposta un valore che determina il superamento del limite, l'istruzione ha esito negativo. È possibile monitorare l'utilizzo della memoria globale nel [DM os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).  
  
 È possibile monitorare l'utilizzo della memoria globale eseguendo una query [sys.dm_os_memory_cache_counters &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) come indicato di seguito: `SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come impostare e restituire quindi una chiave di contesto sessioni denominata linguaggio con un valore di lingua inglese.  
  
```  
EXEC sys.sp_set_session_context @key = N'language', @value = 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 Nell'esempio seguente viene illustrato l'utilizzo del flag di sola lettura facoltativo.  
  
```  
EXEC sys.sp_set_session_context @key = N'user_id', @value = 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [Sicurezza a livello di riga](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
