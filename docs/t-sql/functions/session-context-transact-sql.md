---
title: SESSION_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d875024e6f227c6ba0d65ab0346092c02e860385
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945232"
---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Restituisce il valore della chiave specificata nel contesto della sessione corrente. Il valore viene impostato usando la procedura [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>Argomenti  
 'key'  
 Chiave (tipo sysname) del valore da recuperare.  
  
## <a name="return-type"></a>Tipo restituito  
 **sql_variant**  
  
## <a name="return-value"></a>Valore restituito  
 Valore associato alla chiave specificata nel contesto della sessione oppure NULL se non è stato impostato alcun valore per tale chiave.  
  
## <a name="permissions"></a>Autorizzazioni  
 Qualsiasi utente può leggere il contesto della sessione per la propria sessione.  
  
## <a name="remarks"></a>Remarks  
 Il comportamento di MARS per SESSION_CONTEXT è simile a quello per CONTEXT_INFO. Se un batch MARS imposta una coppia chiave-valore, il nuovo valore non viene restituito in altri batch MARS nella stessa connessione, salvo se l'operazione è iniziata dopo il completamento del batch che ha impostato il nuovo valore. Se su una connessione sono attivi più batch MARS non è possibile impostare i valori come "read_only" (sola lettura). Questo comportamento impedisce le race condition e il non determinismo relativo al valore che "ottiene la precedenza".  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene impostato il valore di contesto della sessione per la chiave `user_id` su 4, quindi viene usata la funzione **SESSION_CONTEXT** per recuperare il valore.  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [Sicurezza a livello di riga](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
