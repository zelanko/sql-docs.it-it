---
title: sp_droppullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d003270b0856da0c833b6e96e8adf54a014d4b9b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830000"
---
# <a name="sp_droppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Elimina una sottoscrizione nel database corrente del Sottoscrittore. Questa stored procedure viene eseguita nel database di sottoscrizione pull del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'`Nome del server remoto. *Publisher* è di **tipo sysname**e non prevede alcun valore predefinito. Se è **All**, la sottoscrizione viene eliminata in tutti i Publisher.  
  
`[ @publisher_db = ] 'publisher_db'`Nome del database del server di pubblicazione. *publisher_db* è di **tipo sysname**e non prevede alcun valore predefinito. **All** indica tutti i database del server di pubblicazione.  
  
`[ @publication = ] 'publication'`Nome della pubblicazione. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito. Se è **All**, la sottoscrizione viene eliminata in tutte le pubblicazioni.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_droppullsubscription** viene utilizzata nella replica snapshot e nella replica transazionale.  
  
 **sp_droppullsubscription** Elimina la riga corrispondente nel [MSreplication_subscriptions &#40;tabella&#41;Transact-SQL](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) e l'agente di distribuzione corrispondente nel Sottoscrittore. Se non viene lasciata alcuna riga in [MSreplication_subscriptions &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md), la tabella viene eliminata.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o dell'utente che ha creato la sottoscrizione pull possono eseguire **sp_droppullsubscription**. Il ruolo predefinito del database **db_owner** è in grado di eseguire **sp_droppullsubscription** solo se l'utente che ha creato la sottoscrizione pull appartiene a questo ruolo.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare una sottoscrizione pull](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
