---
description: sp_helpremotelogin (Transact-SQL)
title: sp_helpremotelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpremotelogin_TSQL
- sp_helpremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpremotelogin
ms.assetid: 93f50869-2627-4642-899f-8f626f8833f4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b35458a0c99eb14db60a058ef72e98df529c217
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547982"
---
# <a name="sp_helpremotelogin-transact-sql"></a>sp_helpremotelogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce informazioni sugli account di accesso remoti per un determinato server remoto o per tutti i server remoti definiti nel server locale.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Utilizzare i server collegati e le stored procedure per i server collegati in alternativa.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpremotelogin [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @remoteserver **=** ] **'***RemoteServer***'**  
 Server remoto per il quale vengono restituite informazioni sugli account di accesso remoti. *RemoteServer* è di **tipo sysname**e il valore predefinito è null. Se *RemoteServer* non è specificato, vengono restituite informazioni su tutti i server remoti definiti nel server locale.  
  
 [ @remotename **=** ] **'***remote_name***'**  
 Account di accesso remoto specifico nel server remoto. *remote_name* è di **tipo sysname**e il valore predefinito è null. Se *remote_name* viene omesso, vengono restituite informazioni su tutti gli utenti remoti definiti per *RemoteServer* .  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|server|**sysname**|Nome di un server remoto definito nel server locale.|  
|local_user_name|**sysname**|Account di accesso del server locale a cui è stato eseguito il mapping degli account di accesso remoti del server.|  
|remote_user_name|**sysname**|Account di accesso nel server remoto sul quale viene eseguito il mapping a local_user_name.|  
|opzioni|**sysname**|Trusted = Quando l'account di accesso remoto si connette al server locale dal server remoto, non viene richiesta alcuna password.<br /><br /> Untrusted (o vuoto) = Quando l'account di accesso remoto si connette al server locale dal server remoto, viene sempre richiesta una password.|  
  
## <a name="remarks"></a>Osservazioni  
 Per recuperare un elenco dei nomi dei server remoti definiti nel server locale, eseguire sp_helpserver.  
  
## <a name="permissions"></a>Autorizzazioni  
 Le autorizzazioni non vengono controllate.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-reporting-help-on-a-single-server"></a>R. Visualizzazione di informazioni su un solo server  
 Nell'esempio seguente vengono visualizzate informazioni su tutti gli utenti remoti nel server remoto `Accounts`.  
  
```  
EXEC sp_helpremotelogin 'Accounts';  
```  
  
### <a name="b-reporting-help-on-all-remote-users"></a>B. Visualizzazione di informazioni su tutti gli utenti remoti  
 Nell'esempio seguente vengono visualizzate informazioni su tutti gli utenti remoti disponibili in tutti i server remoti noti al server locale.  
  
```  
EXEC sp_helpremotelogin;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_addremotelogin &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_dropremotelogin &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
