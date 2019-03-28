---
title: sp_syscollector_start_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_start_collection_set_TSQL
- sp_syscollector_start_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_start_collection_set
ms.assetid: d8357180-f51e-4681-99f9-0596fe2d2b53
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2806d42e58bbd60b962f83e8ab58fbe4511e44b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526403"
---
# <a name="spsyscollectorstartcollectionset-transact-sql"></a>sp_syscollector_start_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Avvia un set di raccolta se l'agente di raccolta è già abilitato e il set di raccolta non è in esecuzione. Se l'agente di raccolta non è abilitato, abilitare l'agente di raccolta eseguendo [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) e quindi utilizzare questa stored procedure per avviare un set di raccolta.  

  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @collection_set_id = ] collection_set_id` È l'identificatore univoco locale del set di raccolta. *collection_set_id* viene **int** con un valore predefinito NULL. *collection_set_id* deve avere un valore se *nome* è NULL.  
  
`[ @name = ] 'name'` È il nome del set di raccolta. *nome* viene **sysname** con un valore predefinito NULL. *nome* deve avere un valore se *collection_set_id* è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 È necessario eseguire sp_syscollector_create_collection_set nel contesto del database di sistema msdb e SQL Server Agent deve essere abilitato.  
  
 Questa procedura ha esito negativo se viene eseguita in un set di raccolta che non include una pianificazione. Se il set di raccolta non dispone di una pianificazione (perché la modalità di raccolta è impostata non in cache, ad esempio), usare il [sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md) stored procedure per avviare il set di raccolta.  
  
 Questa procedura abilita i processi di raccolta e di caricamento per il set di raccolta specificato e avvierà immediatamente il processo dell'agente di raccolta se il set di raccolta è impostato sulla modalità cache (0). Per altre informazioni, vedere [sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
 Se il set di raccolta non contiene alcun elemento della raccolta, questa operazione non ha alcun effetto. Viene restituito l'errore 14685 come avviso.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa procedura, è necessaria l'appartenenza al ruolo predefinito del database dc_operator. Se al set di raccolta non è associato un account proxy, è richiesta l'appartenenza al ruolo predefinito del server sysadmin.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene avviato un set di raccolta utilizzando il relativo identificatore.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
