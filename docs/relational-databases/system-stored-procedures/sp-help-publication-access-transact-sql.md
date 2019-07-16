---
title: sp_help_publication_access (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8af56ae768ca883e22d7c9e18150e75025086d63
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085259"
---
# <a name="sphelppublicationaccess-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco di tutti gli account di accesso a cui sono state concesse autorizzazioni per una pubblicazione. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione a cui accedere. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @return_granted = ] 'return_granted'` ID di accesso. *return_granted* viene **bit**, con un valore predefinito è 1. Se **0** è specificato e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene utilizzata l'autenticazione, vengono restituiti gli account di accesso disponibili visualizzati nel server di pubblicazione, ma non nel server di distribuzione. Se **0** specificato e viene utilizzata l'autenticazione di Windows, gli account di accesso negato non specificamente accedere al server di pubblicazione o un server di distribuzione vengono restituiti.  
  
`[ @login = ] 'login'` ID di accesso standard di sicurezza. *account di accesso* viene **sysname**, il valore predefinito è **%** .  
  
`[ @initial_list = ] initial_list` Specifica se restituire tutti i membri con accesso alla pubblicazione oppure solo i membri che avevano accesso prima che venissero aggiunti nuovi membri all'elenco. *initial_list* è di tipo bit e il valore predefinito **0**.  
  
 **1** restituisce informazioni per tutti i membri del **sysadmin** ruolo predefinito del server con un account di accesso validi nel server di distribuzione esistenti dal momento della creazione della pubblicazione, nonché l'account di accesso corrente.  
  
 **0** restituisce informazioni per tutti i membri del **sysadmin** ruolo predefinito del server con account di accesso validi nel server di distribuzione esistenti dal momento della pubblicazione è stata creata anche come tutti gli utenti nell'elenco di accesso alla pubblicazione che non dispongono appartenere al **sysadmin** ruolo predefinito del server.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**LoginName**|**nvarchar(256)**|Nome effettivo dell'account di accesso.|  
|**isntname**|**int**|**0** = account di accesso non è un utente di Windows.<br /><br /> **1** = account di accesso è un utente di Windows.|  
|**Isntgroup**|**int**|**0** = account di accesso non è un gruppo di Windows.<br /><br /> **1** = account di accesso è un gruppo di Windows.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_help_publication_access** viene utilizzata in tutti i tipi di replica.  
  
 Quando entrambe **Isntname** e **Isntgroup** nel risultato sono set **0**, si presuppone che l'account di accesso è un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_help_publication_access**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_grant_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
