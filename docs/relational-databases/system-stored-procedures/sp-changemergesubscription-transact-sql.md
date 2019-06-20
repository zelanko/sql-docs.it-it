---
title: sp_changemergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergesubscription_TSQL
- sp_changemergesubscription
helpviewer_keywords:
- sp_changemergesubscription
ms.assetid: fd820f35-c189-4e2d-884d-b60c1c469f58
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b37e09147652e856ac0c4c8160c1d7d3caf6f6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62993113"
---
# <a name="spchangemergesubscription-transact-sql"></a>sp_changemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le proprietà selezionate di una sottoscrizione push di tipo merge. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]  
>  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changemergesubscription [ [ @publication= ] 'publication' ]  
    [ , [ @subscriber= ] 'subscriber'  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione da modificare. *pubblicazione* viene **sysname**, con un valore predefinito è NULL. La pubblicazione deve essere già esistente e conforme alle regole per gli identificatori.  
  
`[ @subscriber = ] 'subscriber'` È il nome del sottoscrittore. *Sottoscrittore* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'` È il nome del database di sottoscrizione. *subscriber_db*viene **sysname**, con un valore predefinito è NULL.  
  
`[ @property = ] 'property'` È la proprietà da modificare per la pubblicazione specificata. *proprietà* viene **sysname**, e può essere uno dei valori nella tabella.  
  
`[ @value = ] 'value'` Nuovo valore per l'oggetto specificato *proprietà*. *valore* viene **nvarchar(255**, e può essere uno dei valori nella tabella.  
  
|Proprietà|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**description**||Descrizione della sottoscrizione di tipo merge.|  
|**priority**||Priorità della sottoscrizione. La priorità viene utilizzata dal sistema di risoluzione predefinito per eseguire una selezione in caso di conflitti.|  
|**merge_job_login**||Account di accesso per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione dell'agente.|  
|**merge_job_password**||Password dell'account di Windows utilizzato per l'esecuzione dell'agente.|  
|**publisher_security_mode**|**1**|Esegue la connessione al server di pubblicazione utilizzando l'autenticazione di Windows.|  
||**0**|Esegue la connessione al server di pubblicazione utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_login**||Nome dell'account di accesso al server di pubblicazione.|  
|**publisher_password**||Password complessa per l'account di accesso fornito per il server di pubblicazione.|  
|**subscriber_security_mode**|**1**|Esegue la connessione al Sottoscrittore utilizzando l'autenticazione di Windows.|  
||**0**|Esegue la connessione al Sottoscrittore utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**subscriber_login**||Nome dell'account di accesso nel Sottoscrittore.|  
|**subscriber_password**||Password complessa per l'account di accesso fornito per il Sottoscrittore.|  
|**sync_type**|**automatic**|Lo schema e i dati iniziali per le tabelle pubblicate vengono trasferiti per primi nel Sottoscrittore.|  
||**Nessuno**|Il Sottoscrittore dispone già dello schema e dei dati iniziali per le tabelle pubblicate. Le tabelle di sistema e i dati vengono sempre trasferiti.|  
|**use_interactive_resolver**|**true**|Consente la risoluzione interattiva dei conflitti per tutti gli articoli che la prevedono.|  
||**false**|I conflitti vengono risolti automaticamente utilizzando un sistema di risoluzione predefinito o personalizzato.|  
|NULL (predefinito)|NULL (predefinito)||  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changemergesubscription** viene utilizzata nella replica di tipo merge.  
  
 Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_changemergesubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
