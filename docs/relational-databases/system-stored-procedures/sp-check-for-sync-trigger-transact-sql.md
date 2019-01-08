---
title: sp_check_for_sync_trigger (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_for_sync_trigger
helpviewer_keywords:
- sp_check_for_sync_trigger
ms.assetid: 54a1e2fd-c40a-43d4-ac64-baed28ae4637
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ac0fe99f835dae638cb65b24e569857fb77b098
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52759960"
---
# <a name="spcheckforsynctrigger-transact-sql"></a>sp_check_for_sync_trigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Determina se una stored procedure definita dall'utente o un trigger definito dall'utente viene chiamato nel contesto di un trigger di replica utilizzato per sottoscrizioni ad aggiornamento immediato. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione o nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_check_for_sync_trigger [ @tabid = ] 'tabid'   
    [ , [ @trigger_op = ] 'trigger_output_parameters' OUTPUT ]  
    [ , [ @fonpublisher = ] fonpublisher ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@tabid =** ] '*tabid*'  
 ID di oggetto della tabella in cui vengono controllati i trigger per l'aggiornamento immediato. *tabid* viene **int** non prevede alcun valore predefinito.  
  
 [ **@trigger_op =** ] '*output_parameters*' OUTPUT  
 Specifica se il parametro di output restituisce il tipo di trigger da cui viene richiamato. *output_parameters* viene **char (10)** i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Componenti aggiuntivi**|Trigger INSERT|  
|**UPD**|Trigger UPDATE|  
|**CANC**|Trigger DELETE|  
|NULL (predefinito)||  
  
 [  **@fonpublisher =** ] *fonpublisher*  
 Specifica la posizione in cui viene eseguita la stored procedure. *fonpublisher* viene **bit**, valore predefinito pari a 0. 0 indica che l'esecuzione avviene nel Sottoscrittore, mentre 1 indica che avviene nel server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 indica che la stored procedure non viene richiamata nel contesto di un trigger per l'aggiornamento immediato. 1 indica che viene richiamata nel contesto di un trigger per l'aggiornamento immediato ed è il tipo di trigger restituito in *@trigger_op*.  
  
## <a name="remarks"></a>Note  
 **sp_check_for_sync_trigger** viene utilizzata nella replica snapshot e transazionale.  
  
 **sp_check_for_sync_trigger** viene utilizzata per coordinare la replica e trigger definiti dall'utente. Questa stored procedure determina se viene richiamata nel contesto di un trigger di replica. Ad esempio, è possibile chiamare la routine **sp_check_for_sync_trigger** nel corpo di un trigger definito dall'utente. Se **sp_check_for_sync_trigger** restituisce **0**, il trigger definito dall'utente continua l'elaborazione. Se **sp_check_for_sync_trigger** restituisce **1**, il trigger definito dall'utente viene chiusa. Ciò garantisce che il trigger definito dall'utente non venga attivato quando il trigger di replica aggiorna la tabella.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato il codice che può essere utilizzato in un trigger in una tabella del Sottoscrittore.  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int  
SELECT @table_id = object_id('tablename')  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT  
IF @retcode = 1  
RETURN  
```  
  
## <a name="example"></a>Esempio  
 Il codice può anche essere aggiunto a un trigger in una tabella nel server di pubblicazione; il codice è simile, ma la chiamata a **sp_check_for_sync_trigger** include un parametro aggiuntivo.  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int, @fonpublisher int  
SELECT @table_id = object_id('tablename')  
SELECT @fonpublisher = 1  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT, @fonpublisher  
IF @retcode = 1  
RETURN  
```  
  
## <a name="permissions"></a>Permissions  
 **sp_check_for_sync_trigger** stored procedure può essere eseguita da qualsiasi utente con autorizzazioni SELECT il [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) vista di sistema.  
  
## <a name="see-also"></a>Vedere anche  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
