---
title: sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
ms.openlocfilehash: f84cd1cbb9a49f0c13a93fdff721f430983088ca
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955972"
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

`@publication= 'publication'`  
Nome della pubblicazione in cui è stato inserito il token di traccia. Il tipo di dati viene **sysname**. Questo parametro è obbligatorio.

`[ @tracer_id= ] tracer_id`  
ID del token di traccia da eliminare. Il tipo di dati viene **int**. Il valore predefinito è *null*. Se *null*, vengono eliminati tutti i token di traccia appartenenti alla pubblicazione.

`[ @cutoff_date= ] cutoff_date`  
Token di traccia inseriti nella pubblicazione prima di tale data verranno eliminati. Il tipo di dati viene **datetime**. Il valore predefinito è *null*.

`[ @publisher= ] 'publisher'`  
Nome del server di pubblicazione. Il tipo di dati viene **sysname**. Il valore predefinito è *null*.

> [!NOTE]
> Questo parametro deve essere specificato solo per non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i server di pubblicazione o quando si esegue la stored procedure dal database di distribuzione.

`[ @publisher_db= ] 'publisher_db'`  
Nome del database di pubblicazione. Il tipo di dati viene **sysname**. Il valore predefinito è NULL. Questo parametro viene ignorato se la stored procedure viene eseguita nel server di pubblicazione.

> [!NOTE]
> Questo parametro deve essere specificato quando si esegue la stored procedure dal database di distribuzione.

## <a name="return-code-values"></a>Valori restituiti

**0** (esito positivo) o **1** (errore)

## <a name="remarks"></a>Note

**sp_deletetracertokenhistory** viene utilizzata nella replica transazionale.  

Si verifica un errore se si specificano entrambi i parametri *tracer_id* e *cutoff_date*.

Se non si esegue **sp_deletetracertokenhistory** per eliminare i metadati dei token di traccia, le informazioni verranno eliminate quando si verifica la pulizia della cronologia regolarmente pianificate.

Gli ID dei token di traccia può essere determinato eseguendo [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) oppure eseguendo una query il [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) tabella di sistema.

## <a name="permissions"></a>Permissions

Solo il personale della seguente dispongono di autorizzazioni sufficienti per eseguire **sp_deletetracertokenhistory**:

- I membri del **replmonitor** ruoli, nel database di distribuzione
- I membri del **sysadmin** ruolo predefinito del server.
- I membri del **db_owner** ruolo predefinito del database, nel database di pubblicazione.
- Il **db_owner** del database predefinito.

## <a name="see-also"></a>Vedere anche

[Misurazione della latenza e convalida delle connessioni per la replica transazionale](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
