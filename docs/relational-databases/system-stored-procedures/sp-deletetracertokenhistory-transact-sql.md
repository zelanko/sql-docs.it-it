---
title: sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f8f1a91210cbd263a9225cef54bcf27a81bf2bf4
ms.sourcegitcommit: dc3543e81e32451568133e9b1b560f7ee76d7fb5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2019
ms.locfileid: "55428598"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove i record di token di traccia dal [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) e [MStracer_history &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md) le tabelle di sistema. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione o nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_deletetracertokenhistory [ @publication = ] 'publication'   
    [ , [ @tracer_id = ] tracer_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@publication=** ] **'***publication***'**  
 Nome della pubblicazione in cui è stato inserito il token di traccia. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@tracer_id=** ] *tracer_id*  
 ID del token di traccia da eliminare. *tracer_id* viene **int**, con un valore predefinito NULL. Se **null**, quindi vengono eliminati tutti i token di traccia appartenenti alla pubblicazione.  
  
 [ **@cutoff_date=** ] *cutoff_date*  
 Specifica un valore di cambio data in modo che tutti i token di traccia inseriti nella pubblicazione prima di tale data vengano rimossi. *cutoff_date* è di tipo datetime, un valore predefinito NULL.  
  
 [ **@publisher=** ] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]
>  Questo parametro deve essere specificato solo per non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione o quando si esegue la stored procedure dal database di distribuzione.  
  
 [ **@publisher_db=** ] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* viene **sysname**, con un valore predefinito NULL. Questo parametro viene ignorato se la stored procedure viene eseguita nel server di pubblicazione.  
  
> [!NOTE]
>  Questo parametro deve essere specificato quando si esegue la stored procedure dal database di distribuzione.  

## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_deletetracertokenhistory** viene utilizzata nella replica transazionale.  
  
 Quando si esegue **sp_deletetracertokenhistory**, è possibile specificare solo uno dei *tracer_id* oppure *cutoff_date*. Se si specificano entrambi i parametri, viene generato un errore.  
  
 Se non si esegue **sp_deletetracertokenhistory** per rimuovere i metadati dei token di traccia, le informazioni verranno rimossi quando si verifica la pulizia della cronologia regolarmente pianificate.  
  
 Gli ID dei token di traccia può essere determinato eseguendo [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) oppure eseguendo una query il [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) tabella di sistema.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database nel database di pubblicazione, o **db_owner** predefiniti del database o  **replmonitor** nel database di distribuzione possono eseguire **sp_deletetracertokenhistory**.  
  
## <a name="see-also"></a>Vedere anche  
 [Misurare la latenza e convalidare le connessioni per la replica transazionale](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)  
  
  
