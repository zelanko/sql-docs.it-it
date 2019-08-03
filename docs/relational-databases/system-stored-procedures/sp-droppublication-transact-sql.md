---
title: sp_droppublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppublication_TSQL
- sp_droppublication
helpviewer_keywords:
- sp_droppublication
ms.assetid: b52b37e6-4fec-40cf-abba-7dce4ff395fd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2bbcd4c8c70d2d381df77ccf8a4a99cec82d3e49
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768233"
---
# <a name="spdroppublication-transact-sql"></a>sp_droppublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Elimina una pubblicazione e l'agente snapshot associato. Prima di eliminare una pubblicazione, è necessario eliminare tutte le sottoscrizioni. Gli articoli della pubblicazione vengono eliminati automaticamente. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_droppublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione da eliminare. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito. Se si specifica **All** , tutte le pubblicazioni vengono eliminate dal database di pubblicazione, ad eccezione di quelle con sottoscrizioni.  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_droppublication** viene utilizzato nella replica snapshot e nella replica transazionale.  
  
 **sp_droppublication** Elimina in modo ricorsivo tutti gli articoli associati a una pubblicazione e quindi Elimina la pubblicazione stessa. Non è possibile rimuovere una pubblicazione per cui esistono una o più sottoscrizioni. Per informazioni su come rimuovere le sottoscrizioni, vedere [eliminare una sottoscrizione push](../../relational-databases/replication/delete-a-push-subscription.md) ed [eliminare una sottoscrizione pull](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 L'esecuzione di **sp_droppublication** per eliminare una pubblicazione non comporta la rimozione degli oggetti pubblicati dal database di pubblicazione o degli oggetti corrispondenti dal database di sottoscrizione. Utilizzare DROP \<Object > per rimuovere questi oggetti manualmente, se necessario.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_droppublication**.  
  
## <a name="examples"></a>Esempi  
 [!code-sql[HowTo#sp_droppublication](../../relational-databases/replication/codesnippet/tsql/sp-droppublication-trans_1.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare una pubblicazione](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
