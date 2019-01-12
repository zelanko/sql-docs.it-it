---
title: sp_changeqreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changeqreader_agent_TSQL
- sp_changeqreader_agent
helpviewer_keywords:
- sp_changeqreader_agent
ms.assetid: d3fe79c5-31ef-4565-bf38-b476b5fb16f7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21da0ca61d2d9075fe7c962156443fd85f3ebefd
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135132"
---
# <a name="spchangeqreaderagent-transact-sql"></a>sp_changeqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di modificare le proprietà di sicurezza di un agente di lettura coda. Questa stored procedure viene eseguita nel database di distribuzione del server di distribuzione o nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changeqreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@job_login**=] **'**_job_login_**'**  
 Account di accesso per l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizzato per l'esecuzione dell'agente. *job_login* viene **nvarchar(257)**, con un valore predefinito è NULL.  
  
 [ **@job_password**=] **'**_job_password_**'**  
 Password dell'account di Windows utilizzato per l'esecuzione dell'agente. *job_password* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@frompublisher=** ] *frompublisher*  
 Specifica se la procedura viene eseguita nel server di pubblicazione. *frompublisher* è di tipo bit e il valore predefinito **0**. Un valore pari **1** significa che la procedura viene eseguita dal server di pubblicazione nel database di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changeqreader_agent** viene utilizzata nella replica transazionale.  
  
 **sp_changeqreader_agent** viene utilizzato per modificare l'account di Windows con cui viene eseguito un agente di lettura coda. È possibile cambiare la password di un account di accesso di Windows esistente oppure specificare un nuovo account di accesso di Windows e la password.  
  
 Dopo la modifica dell'account di accesso o della password di un agente, è necessario arrestare e riavviare l'agente per rendere effettiva la modifica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_changeqreader_agent**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
  
