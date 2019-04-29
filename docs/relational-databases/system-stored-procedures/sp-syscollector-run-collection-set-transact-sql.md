---
title: sp_syscollector_run_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2ad81b1d92bb45d9ab15ca11897804cc0d333a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001749"
---
# <a name="spsyscollectorruncollectionset-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Avvia un set di raccolta se l'agente di raccolta è già abilitato e set di raccolta è configurato per la modalità di raccolta non in cache.  
  
> [!NOTE]  
>  Questa procedura avrà esito negativo se eseguita in un set di raccolta configurato per la modalità di raccolta in modalità memorizzata nella cache.  
  
 sp_syscollector_run_collection_set consente a un utente di acquisire snapshot dei dati su richiesta.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @collection_set_id = ] collection_set_id` È l'identificatore univoco locale del set di raccolta. *collection_set_id* viene **int** e deve avere un valore se *nome* è NULL.  
  
`[ @name = ] 'name'` È il nome del set di raccolta. *nome* viene **sysname** e deve avere un valore se *collection_set_id* è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Entrambi *collection_set_id* oppure *nome* deve avere un valore, non possono essere entrambi NULL.  
  
 Questa procedura verrà avviare la raccolta e caricare i processi per set di raccolta specificata e avvierà immediatamente il processo dell'agente di raccolta se il set di raccolta ha relativi **@collection_mode** impostato su non in cache (1). Per altre informazioni, vedere [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
 È possibile utilizzare sp_sycollector_run_collection_set anche per eseguire un set di raccolta senza una pianificazione.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **dc_operator** (con autorizzazione EXECUTE) ruolo predefinito del database per eseguire questa procedura.  
  
## <a name="example"></a>Esempio  
 Avviare un set di raccolta utilizzandone l'identificatore.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
