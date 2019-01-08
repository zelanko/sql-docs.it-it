---
title: sp_helpreplicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 29fcbe7f5e7b2b7e72c88390df9d5fe20c0f7352
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52812033"
---
# <a name="sphelpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indica se i database nel server di pubblicazione sono abilitati per la replica. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione. *Non è supportata per server di pubblicazione Oracle.*  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@dbname=**] **'***dbname***'**  
 Nome del database. *dbname* viene **sysname**, il valore predefinito è **%**. Se **%**, quindi il set di risultati contiene tutti i database nel server di pubblicazione, in caso contrario, sole nel database specificato vengono restituite informazioni. Non vengono restituite informazioni per gli eventuali database per cui l'utente non dispone delle autorizzazioni appropriate, come indicato di seguito.  
  
 [  **@type=**] **'***tipo***'**  
 Limita il set di risultati al database in cui l'opzione di replica specificato *tipo* valore è stato abilitato. *tipo di* viene **sysname**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**pubblicare**|È consentita la replica transazionale.|  
|**pubblicazione di tipo merge**|È consentita la replica di tipo merge.|  
|**è consentita la replica** (impostazione predefinita)|È consentita la replica transazionale o la replica di tipo merge.|  
  
 [  **@reserved=** ] *riservato*  
 Specifica se vengono restituite informazioni sulle pubblicazioni e sulle sottoscrizioni esistenti. *riservato* viene **bit**, valore predefinito pari a 0. Se **1**, il set di risultati include informazioni sul fatto che il database specificato ha eventuali pubblicazioni o sottoscrizioni esistenti.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome del database.|  
|**id**|**int**|Identificatore del database.|  
|**transpublish**|**bit**|Se il database è stato abilitato per la pubblicazione snapshot o transazionale; dove il valore **1** significa che è abilitata la pubblicazione transazionale o snapshot.|  
|**mergepublish**|**bit**|Se il database è stato abilitato per l'unione di pubblicazione; dove il valore **1** significa che la pubblicazione di tipo merge è abilitata.|  
|**dbowner**|**bit**|Se l'utente è membro del **db_owner** dove il valore del ruolo predefinito del database; **1** indica che l'utente è un membro di questo ruolo.|  
|**dbReadOnly**|**bit**|È se il database è contrassegnato come sola lettura. dove il valore **1** significa che il database è di sola lettura.|  
|**haspublications**|**bit**|È se il database presenta pubblicazioni esistenti dove il valore **1** significa che non esistono pubblicazioni esistenti.|  
|**haspullsubscriptions**|**bit**|Se il database dispone di tutte le sottoscrizioni pull esistenti; dove il valore **1** significa che sono presenti sottoscrizioni pull.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpreplicationdboption** viene utilizzata nella replica di tipo merge e snapshot, transazionale.  
  
## <a name="permissions"></a>Permissions  
 I membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_helpreplicationdboption** per qualsiasi database. I membri del **db_owner** ruolo predefinito del database possono eseguire **sp_helpreplicationdboption** per quel database.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
