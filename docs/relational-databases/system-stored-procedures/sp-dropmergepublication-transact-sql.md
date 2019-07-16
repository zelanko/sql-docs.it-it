---
title: sp_dropmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
author: stevestein
ms.author: sstein
ms.openlocfilehash: b675b07466464f706b6503f3d017acd34822b2c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933909"
---
# <a name="spdropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina una pubblicazione di tipo merge e l'agente snapshot associato. Prima di eliminare una pubblicazione di tipo merge, è necessario eliminare tutte le sottoscrizioni. Gli articoli della pubblicazione vengono eliminati automaticamente. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione da eliminare. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito. Se **tutti**, tutte le pubblicazioni di tipo merge esistenti vengono rimosse, nonché il processo dell'agente Snapshot associato. Se si specifica un valore specifico per *publication*, vengono eliminati solo tale pubblicazione e il processo dell'agente Snapshot associato.  
  
`[ @ignore_distributor = ] ignore_distributor` Consente di eliminare una pubblicazione senza eseguire attività di pulizia nel server di distribuzione. *ignore_distributor* viene **bit**, il valore predefinito è **0**. Questo parametro viene utilizzato anche quando si reinstalla il server di distribuzione.  
  
`[ @reserved = ] reserved` è riservato per utilizzi futuri. *riservato* viene **bit**, il valore predefinito è **0**.  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` Solo uso interno.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_dropmergepublication** viene utilizzata nella replica di tipo merge.  
  
 **sp_dropmergepublication** in modo ricorsivo Elimina tutti gli articoli che sono associati a una pubblicazione e quindi elimina la pubblicazione stessa. Non è possibile rimuovere una pubblicazione per cui esistono una o più sottoscrizioni. Per informazioni su come rimuovere le sottoscrizioni, vedere [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) e [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 L'esecuzione **sp_dropmergepublication** per eliminare una pubblicazione non rimuove gli oggetti pubblicati dal database di pubblicazione né degli oggetti corrispondenti dal database di sottoscrizione. Utilizzare DROP \<oggetto > per rimuovere questi oggetti manualmente se necessario.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_dropmergepublication**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminazione di una pubblicazione](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
