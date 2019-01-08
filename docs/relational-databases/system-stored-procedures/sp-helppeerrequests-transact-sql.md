---
title: sp_helppeerrequests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fde5daf72455af7c4c46c9ef19e4975a3f87a2dc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802233"
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni su tutte le richieste di stato ricevute dai partecipanti in una topologia di replica peer-to-peer, in cui queste richieste sono state iniziate eseguendo [sp_requestpeerresponse &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) in corrispondenza di qualsiasi database pubblicato della topologia. Questa stored procedure viene eseguita nel database di pubblicazione di un server di pubblicazione che partecipa a una topologia di replica peer-to-peer. Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@publication**=] **'***pubblicazione***'**  
 Nome della pubblicazione in una topologia peer-to-peer per cui sono state inviate richieste dello stato. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@description**=] **'***descrizione***'**  
 Valore che può essere usato per identificare richieste dello stato individuali, che consente di filtrare le risposte restituite in base all'utente definite le informazioni fornite durante la chiamata [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). *Descrizione* viene **nvarchar (4000)**, il valore predefinito è **%**. Per impostazione predefinita, tutte le richieste dello stato per la pubblicazione vengono restituite. Questo parametro viene utilizzato per restituire solo le richieste di stato con una descrizione corrispondente al valore specificato nel *description*, in cui vengono confrontate le stringhe di caratteri tramite un [come &#40;Transact-SQL&#41; ](../../t-sql/language-elements/like-transact-sql.md)clausola.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica una richiesta.|  
|**pubblicazione**|**sysname**|Nome della pubblicazione per cui è stata inviata la richiesta dello stato.|  
|**sent_date**|**datetime**|Data e ora dell'invio della richiesta dello stato.|  
|**description**|**nvarchar(4000)**|Informazioni definite dall'utente che possono essere utilizzate per identificare richieste dello stato individuali.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helppeerrequests** viene utilizzata nella replica transazionale peer-to-peer.  
  
 **sp_helppeerrequests** viene usato quando si ripristina un database pubblicato in una topologia peer-to-peer.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_helppeerrequests**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
