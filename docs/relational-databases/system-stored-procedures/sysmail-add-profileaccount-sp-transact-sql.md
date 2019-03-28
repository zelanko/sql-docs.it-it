---
title: sysmail_add_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 44dc2d5341e536179fe0bf6ef152ef7d39afe966
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532103"
---
# <a name="sysmailaddprofileaccountsp-transact-sql"></a>sysmail_add_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un account di Posta elettronica database a un profilo di Posta elettronica database. Eseguire **sysmail_add_profileaccount_sp** dopo aver creato un Account di Database con [sysmail_add_account_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md), e viene creato un profilo di Database con [sysmail_add_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @profile_id = ] profile_id` Id del profilo a cui aggiungere l'account. *profile_id* viene **int**, con un valore predefinito è NULL. Entrambi i *profile_id* o nella *profile_name* deve essere specificato.  
  
`[ @profile_name = ] 'profile_name'` Il nome del profilo a cui aggiungere l'account. *profile_name* viene **sysname**, con un valore predefinito è NULL. Entrambi i *profile_id* o nella *profile_name* deve essere specificato.  
  
`[ @account_id = ] account_id` Id dell'account da aggiungere al profilo. *account_id* viene **int**, con un valore predefinito è NULL. Entrambi i *account_id* o nella *account_name* deve essere specificato.  
  
`[ @account_name = ] 'account_name'` Il nome dell'account da aggiungere al profilo. *account_name* viene **sysname**, con un valore predefinito è NULL. Entrambi i *account_id* o nella *account_name* deve essere specificato.  
  
`[ @sequence_number = ] sequence_number` Il numero di sequenza dell'account all'interno del profilo. *sequence_number* viene **int**, non prevede alcun valore predefinito. Il numero di sequenza determina l'ordine in cui gli account sono utilizzati nel profilo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 Sia il profilo che l'account devono esistere. In caso contrario, la stored procedure restituisce un errore.  
  
 Questa stored procedure non modifica il numero di sequenza di un account che è già associato al profilo specificato. Per altre informazioni sull'aggiornamento del numero di sequenza di un account, vedere [sysmail_update_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md).  
  
 Il numero di sequenza determina l'ordine in cui Posta elettronica database utilizza gli account nel profilo. Per un nuovo messaggio di posta elettronica, Posta elettronica database inizia con l'account che ha il numero di sequenza più basso. Se l'invio del messaggio con tale account ha esito negativo, Posta elettronica database prova con l'account con il numero di sequenza successivo e così via, finché il messaggio non viene inviato o finché anche l'invio con l'account con il numero di sequenza più alto non ha esito negativo. Se l'invio del messaggio con l'account con il numero di sequenza più alto non riesce, Posta elettronica database sospende i tentativi di invio del messaggio per il periodo di tempo specificato nel parametro *AccountRetryDelay* di **sysmail_configure_sp**. Trascorso questo periodo di tempo, Posta elettronica database prova di nuovo a inviare il messaggio, iniziando con l'account con il numero di sequenza più basso. Usare il parametro *AccountRetryAttempts* di **sysmail_configure_sp**per specificare quante volte il processo di posta elettronica esterno deve tentare di inviare il messaggio di posta elettronica usando ogni account indicato del profilo specificato.  
  
 Se esistono più account con lo stesso numero di sequenza, Posta elettronica database utilizzerà uno solo di tali account per un dato messaggio di posta elettronica. In questo caso, non viene garantito quale account viene utilizzato per quel numero di sequenza né che venga utilizzato lo stesso account per ogni messaggio.  
  
 La stored procedure **sysmail_add_profileaccount_sp** nel **msdb** database ed è di proprietà di **dbo** dello schema. La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni per questa routine per impostazione predefinita ai membri di esecuzione per il **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente il profilo `AdventureWorks Administrator` viene associato all'account `Audit Account`. Il numero di sequenza dell'account è 1.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Creare un Account di posta elettronica Database](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Oggetti di configurazione di posta elettronica database](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Stored procedure di posta elettronica database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
