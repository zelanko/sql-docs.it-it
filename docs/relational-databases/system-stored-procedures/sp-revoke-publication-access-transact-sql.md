---
description: sp_revoke_publication_access (Transact-SQL)
title: sp_revoke_publication_access (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_revoke_publication_access_TSQL
- sp_revoke_publication_access
helpviewer_keywords:
- sp_revoke_publication_access
ms.assetid: 84ed9e77-991f-4fa5-a21f-7c6bfec1b3e3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0be8037325faba0cecb0988903677c14260b8a47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446788"
---
# <a name="sp_revoke_publication_access-transact-sql"></a>sp_revoke_publication_access (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Rimuove l'account di accesso da un elenco di accesso per la pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_revoke_publication_access [ @publication = ] 'publication' , [ @login = ] 'login'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` Nome della pubblicazione a cui accedere. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @login = ] 'login'` ID di accesso. *login* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_revoke_publication_access** viene utilizzata per la replica snapshot, transazionale e di tipo merge.  
  
 **sp_revoke_publication_access** possono essere chiamate ripetutamente.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_revoke_publication_access**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_grant_publication_access &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_help_publication_access &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)   
 [Proteggere il server di pubblicazione](../../relational-databases/replication/security/secure-the-publisher.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
