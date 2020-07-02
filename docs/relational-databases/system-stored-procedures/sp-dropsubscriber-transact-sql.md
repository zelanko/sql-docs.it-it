---
title: sp_dropsubscriber (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscriber_TSQL
- sp_dropsubscriber
helpviewer_keywords:
- sp_dropsubscriber
ms.assetid: 8c6eb282-81b5-4ec4-b691-aa061d9267dc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 093c04b63b9b99a777f7b20af70ea06677b0c917
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727199"
---
# <a name="sp_dropsubscriber-transact-sql"></a>sp_dropsubscriber (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Rimuove la designazione del Sottoscrittore da un server registrato. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  Questa stored procedure è deprecata. Non è più necessario registrare in modo esplicito un Sottoscrittore nel server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropsubscriber [ @subscriber= ] 'subscriber'   
    [ , [ @reserved= ] 'reserved' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @subscriber = ] 'subscriber'`Nome del Sottoscrittore da eliminare. *Subscriber* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_dropsubscriber** viene utilizzato in tutti i tipi di replica.  
  
 Questa stored procedure rimuove l'opzione del server **secondario** e rimuove il mapping dell'account di accesso remoto dell'amministratore di sistema a **repl_subscriber**.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_dropsubscriber**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare una sottoscrizione push](../../relational-databases/replication/delete-a-push-subscription.md)   
 [Eliminare una sottoscrizione pull](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addsubscriber &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
