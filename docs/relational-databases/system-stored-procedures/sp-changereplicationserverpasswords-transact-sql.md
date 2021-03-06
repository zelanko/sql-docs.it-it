---
description: sp_changereplicationserverpasswords (Transact-SQL)
title: sp_changereplicationserverpasswords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0d0e07afbf3837768ac2b57e3dfaa7d0c8c0d0af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481478"
---
# <a name="sp_changereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Modifica le password archiviate per l' [!INCLUDE[msCoName](../../includes/msconame-md.md)] account di Windows o l'account [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di accesso utilizzato dagli agenti di replica durante la connessione ai server in una topologia di replica. Di norma sarebbe necessario modificare la password per ogni singolo agente in esecuzione nel server, anche se tutti utilizzano lo stesso account o lo stesso account di accesso. Questa stored procedure consente di modificare la password per tutte le istanze di un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un account di Windows specifico utilizzato da tutti gli agenti di replica in esecuzione in un server. Questa stored procedure viene eseguita in qualsiasi server della topologia di replica nel database master.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @login_type = ] login_type` Tipo di autenticazione per le credenziali specificate. *LOGIN_TYPE* è di **tinyint**e non prevede alcun valore predefinito.  
  
 **1** = autenticazione integrata di Windows  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione 0  
  
`[ @login = ] 'login'` Nome dell'account di Windows o dell'account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso da modificare. *login* è di **tipo nvarchar (257)** e non prevede alcun valore predefinito  
  
`[ @password = ] 'password'` Nuova password da archiviare per l' *account di accesso*specificato. *password* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
> [!NOTE]  
>  Dopo aver modificato una password per la replica è necessario arrestare e riavviare ogni agente che utilizza la password prima che la modifica abbia effetto per tale agente.  
  
`[ @server = ] 'server'` Connessione al server per cui viene modificata la password archiviata. il *Server* è di **tipo sysname**. i possibili valori sono i seguenti:  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**distribuzione**|Tutte le connessioni di agenti al server di distribuzione.|  
|**pubblicazione**|Tutte le connessioni di agenti al server di pubblicazione.|  
|**Sottoscrittore**|Tutte le connessioni di agenti al Sottoscrittore.|  
|**%** predefinita|Tutte le connessioni di agenti a tutti i server di una topologia di replica.|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_changereplicationserverpasswords** viene utilizzato con tutti i tipi di replica.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_changereplicationserverpasswords**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
