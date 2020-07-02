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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 82c26d20933562b05bb95796140dcc51bbc0777d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734329"
---
# <a name="sp_msx_get_account-transact-sql"></a>sp_msx_get_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Visualizza un elenco di informazioni sulle credenziali utilizzate dal server di destinazione per accedere al server master.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_msx_get_account  
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce il set di risultati seguente:  
  
|Nome colonna|Type|Descrizione|  
|-----------------|----------|-----------------|  
|msx_connection|**int**|Numero della connessione al server master.|  
|msx_credential_id|**int**|ID delle credenziali utilizzate per questa connessione al server master.|  
|msx_credential_name|**sysname**|Nome delle credenziali utilizzate per questa connessione al server master.|  
|msx_login_name|**nvarchar(4000)**|Nome del dominio e nome utente dell'utente di Windows per le credenziali.|  
  
## <a name="remarks"></a>Osservazioni  
 In assenza di credenziali specificate per questo server di destinazione, restituisce un set di risultati vuoto. Per impostare le credenziali, utilizzare sp_msx_set_account.  
  
## <a name="permissions"></a>Autorizzazioni  
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
 [Stored procedure di SQL Server Agent &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREAZIONE di credenziali &#40;&#41;Transact-SQL](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_set_account &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-msx-set-account-transact-sql.md)  
  
  
