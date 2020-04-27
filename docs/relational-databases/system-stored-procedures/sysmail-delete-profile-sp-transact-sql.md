---
title: sysmail_delete_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profile_sp
- sysmail_delete_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profile_sp
ms.assetid: 71998653-4a02-446d-b6f7-50646a29e8a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9442f4d3637fcb7c891eacbe7546254708918ad3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67909206"
---
# <a name="sysmail_delete_profile_sp-transact-sql"></a>sysmail_delete_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina un profilo di posta utilizzato da Posta elettronica database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_delete_profile_sp  { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @profile_id = ] profile_id`ID del profilo da eliminare. *profile_id* è di **tipo int**e il valore predefinito è null. È necessario specificare *profile_id* o *profile_name* .  
  
`[ @profile_name = ] 'profile_name'`Nome del profilo da eliminare. *profile_name* è di **tipo sysname**e il valore predefinito è null. È necessario specificare *profile_id* o *profile_name* .  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="remarks"></a>Osservazioni  
 L'eliminazione di un profilo non comporta l'eliminazione degli account utilizzati dal profilo.  
  
 Questa stored procedure elimina il profilo indipendentemente dal fatto se gli utenti abbiano o meno accesso al profilo. Prestare attenzione quando si rimuove il profilo privato predefinito per un utente o il profilo pubblico predefinito per il database **msdb** . Quando non è disponibile alcun profilo predefinito, **sp_send_dbmail** richiede il nome di un profilo come argomento. Pertanto, la rimozione di un profilo predefinito può causare l'esito negativo delle chiamate a **sp_send_dbmail** . Per ulteriori informazioni, vedere [sp_send_dbmail &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).  
  
 Il stored procedure **sysmail_delete_profile_sp** si trova nel database **msdb** ed è di proprietà dello schema **dbo** . La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Autorizzazioni  
 Le autorizzazioni di esecuzione per questa procedura vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato il profilo `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Oggetti di configurazione Posta elettronica database](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Stored procedure di Posta elettronica database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
