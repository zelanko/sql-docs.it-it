---
title: sysmail_update_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profileaccount_sp_TSQL
- sysmail_update_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profileaccount_sp
ms.assetid: 92ca7488-29db-414e-8e36-08b0a8f542bb
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 96dc0a33c15f1547088c3fe7c79824da55cd1d35
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538123"
---
# <a name="sysmailupdateprofileaccountsp-transact-sql"></a>sysmail_update_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiorna il numero di sequenza di un account in un profilo di Posta elettronica database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_update_profileaccount_sp  { [ @profile_id = ] profile_id   
| [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' } ,  
    [ @sequence_number = ] sequence_number  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @profile_id = ] profile_id` L'ID del profilo del profilo da aggiornare. *profile_id* viene **int**, con un valore predefinito è NULL. Entrambi i *profile_id* o nella *profile_name* deve essere specificato.  
  
`[ @profile_name = ] 'profile_name'` Il nome del profilo del profilo da aggiornare. *profile_name* viene **sysname**, con un valore predefinito è NULL. Entrambi i *profile_id* o nella *profile_name* deve essere specificato.  
  
`[ @account_id = ] account_id` ID dell'account da aggiornare. *account_id* viene **int**, con un valore predefinito è NULL. Entrambi i *account_id* o nella *account_name* deve essere specificato.  
  
`[ @account_name = ] 'account_name'` Il nome dell'account da aggiornare. *account_name* viene **sysname**, con un valore predefinito è NULL. Entrambi i *account_id* o nella *account_name* deve essere specificato.  
  
`[ @sequence_number = ] sequence_number` Il nuovo numero di sequenza per l'account. *sequence_number* viene **int**, non prevede alcun valore predefinito. Il numero di sequenza determina l'ordine in cui gli account sono utilizzati nel profilo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Restituisce un errore se l'account specificato non è associato al profilo.  
  
 Il numero di sequenza determina l'ordine in cui Posta elettronica database utilizza gli account nel profilo. Per un nuovo messaggio di posta elettronica, Posta elettronica database inizia con l'account che ha il numero di sequenza più basso. Se l'invio del messaggio con tale account ha esito negativo, Posta elettronica database prova con l'account con il numero di sequenza successivo e così via, finché il messaggio non viene inviato o finché anche l'invio con l'account con il numero di sequenza più alto non ha esito negativo. Se l'account con il numero di sequenza più alto restituisce un errore, l'invio del messaggio non viene completato.  
  
 Se esistono più account con lo stesso numero di sequenza, Posta elettronica database utilizza solo uno di questi account per un messaggio di posta specifico. In questo caso, non viene garantito quale account viene utilizzato per quel numero di sequenza né che venga utilizzato lo stesso account per ogni messaggio.  
  
 La stored procedure **sysmail_update_profileaccount_sp** nel **msdb** database ed è di proprietà di **dbo** dello schema. La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni per questa routine per impostazione predefinita ai membri di esecuzione per il **sysadmin** ruolo predefinito del server.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente modifica il numero di sequenza dell'account `Admin-BackupServer` all'interno del profilo `AdventureWorks Administrator` nel **msdb** database. Dopo l'esecuzione del codice, il numero di sequenza dell'account è `3`, ad indicare che sarà utilizzato se i primi due account restituiscono un messaggio di errore.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@account_name = 'Admin-BackupServer',  
    ,@sequence_number = 3;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Creare un Account di posta elettronica Database](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Oggetti di configurazione di posta elettronica database](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Stored procedure di posta elettronica database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
