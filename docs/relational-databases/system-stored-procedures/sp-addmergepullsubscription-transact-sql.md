---
title: sp_addmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: stevestein
ms.author: sstein
ms.openlocfilehash: ef860a30ba5994e25a9d532445af0ec2c39f9e1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042736"
---
# <a name="spaddmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge una sottoscrizione pull a una pubblicazione di tipo merge. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addmergepullsubscription [ @publication= ] 'publication'   
    [ , [ @publisher= ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @subscriber_type= ] 'subscriber_type' ]   
    [ , [ @subscription_priority= ] subscription_priority ]   
    [ , [ @sync_type= ] 'sync_type' ]   
    [ , [ @description= ] 'description' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *Server di pubblicazione* viene **sysname**, con un valore predefinito del nome del server locale. Il server di pubblicazione deve essere un server valido.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del server di pubblicazione. *publisher_db* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subscriber_type = ] 'subscriber_type'` È il tipo di sottoscrittore. *subscriber_type* viene **nvarchar(15)** e può essere **globale**, **locale** oppure **anonimo**. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive le sottoscrizioni locali vengono dette sottoscrizioni client e le sottoscrizioni globali vengono dette sottoscrizioni server.  
  
`[ @subscription_priority = ] subscription_priority` È la priorità della sottoscrizione. *subscription_priority*viene **reale**, con un valore predefinito è NULL. Per le sottoscrizioni locali e anonime, la priorità è **0,0**. La priorità viene utilizzata dal sistema di risoluzione predefinito per eseguire una selezione in caso di conflitti. Per i Sottoscrittori globali, la priorità della sottoscrizione deve essere minore di 100, che corrisponde al livello di priorità del server di pubblicazione.  
  
`[ @sync_type = ] 'sync_type'` È il tipo di sincronizzazione della sottoscrizione. *sync_type*viene **nvarchar(15)** , il valore predefinito è **automatica**. Può essere **automatici** oppure **none**. Se **automatica**, lo schema e i dati iniziali per le tabelle pubblicate vengono trasferiti nel Sottoscrittore prima di tutto. Se **none**, si presuppone il sottoscrittore dispone già dello schema e i dati iniziali per le tabelle pubblicate. Le tabelle e i dati di sistema vengono sempre trasferiti.  
  
> [!NOTE]  
>  Non è consigliabile specificare un valore di **none**.  
  
`[ @description = ] 'description'` È una breve descrizione della sottoscrizione pull. *Descrizione*viene **nvarchar(255**, con un valore predefinito è NULL. Questo valore viene visualizzato da Monitoraggio replica nella **soprannome** colonna, che può essere usato per ordinare le sottoscrizioni per una pubblicazione monitorata.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addmergepullsubscription** viene usato per la replica di tipo merge.  
  
 Se si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente per sincronizzare la sottoscrizione, il [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) stored procedure deve essere eseguita nel Sottoscrittore per creare un agente e processo per la sincronizzazione con la pubblicazione.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addmergepullsubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una sottoscrizione pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
