---
title: sp_msx_get_account (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_get_account_TSQL
- sp_msx_get_account
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_get_account
ms.assetid: 7b478049-e2d0-4bac-865a-b97fd1d8dfbc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3dab15a076200e464e82d0b01ef6a156447a537f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108037"
---
# <a name="spmsxgetaccount-transact-sql"></a>sp_msx_get_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza un elenco di informazioni sulle credenziali utilizzate dal server di destinazione per accedere al server master.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_msx_get_account  
```  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce il set di risultati seguente:  
  
|Nome colonna|type|Descrizione|  
|-----------------|----------|-----------------|  
|msx_connection|**int**|Numero della connessione al server master.|  
|msx_credential_id|**int**|ID delle credenziali utilizzate per questa connessione al server master.|  
|msx_credential_name|**sysname**|Nome delle credenziali utilizzate per questa connessione al server master.|  
|msx_login_name|**nvarchar(4000)**|Nome del dominio e nome utente dell'utente di Windows per le credenziali.|  
  
## <a name="remarks"></a>Note  
 In assenza di credenziali specificate per questo server di destinazione, restituisce un set di risultati vuoto. Per impostare le credenziali, utilizzare sp_msx_set_account.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server sysadmin.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene visualizzato un elenco di informazioni per le credenziali utilizzate dal server di destinazione per accedere al server master.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_get_account ;  
GO  
```  
  
 Quello che segue è un esempio di set dei risultati:  
  
 `msx_connection msx_credential_id msx_credential_name  msx_login_name`  
  
 `-------------- ----------------- -------------------- ------------------------------`  
  
 `1              65538             MsxAccount           AdventureWorks2012\MsxAccount`  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_set_account &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-set-account-transact-sql.md)  
  
  
