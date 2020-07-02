---
title: sp_msx_set_account (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_set_account
- sp_msx_set_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_set_account
ms.assetid: 314ec720-3a37-48f7-bb6b-8d5b894bf843
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 27c5b993817e063caf08ca55e03a31ebaacc17b2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731607"
---
# <a name="sp_msx_set_account-transact-sql"></a>sp_msx_set_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Imposta il nome account e la password del server master di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel server di destinazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_msx_set_account [ @credential_name = ] 'credential_name'  | [ @credential_id = ] credential_id  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @credential_name = ] 'credential_name'`Nome delle credenziali da utilizzare per accedere al server master. Il nome specificato deve corrispondere al nome di una credenziale esistente. È necessario specificare *credential_name* o *credential_id* .  
  
`[ @credential_id = ] credential_id`Identificatore della credenziale da utilizzare per accedere al server master. L'identificatore deve corrispondere a un identificatore di credenziali già esistenti. È necessario specificare *credential_name* o *credential_id* .  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 No.  
  
## <a name="remarks"></a>Osservazioni  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza le credenziali per archiviare le informazioni relative al nome utente e alla password utilizzate da un server di destinazione per accedere a un server master. Questa procedura imposta le credenziali utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per questo server di destinazione per accedere al server master.  
  
 Le credenziali specificate devono corrispondere a delle credenziali esistenti. Per ulteriori informazioni sulla creazione di una credenziale, vedere [create credential &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_msx_set_account** per impostazione predefinita ai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene impostato il server per utilizzare le credenziali `MsxAccount` per accedere al server master.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_set_account @credential_name = MsxAccount ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di SQL Server Agent &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREAZIONE di credenziali &#40;&#41;Transact-SQL](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_get_account &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)  
  
  
