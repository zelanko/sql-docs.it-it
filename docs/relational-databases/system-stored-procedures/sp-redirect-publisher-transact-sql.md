---
title: sp_redirect_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6062522ca6c5c3a311ba2f2c796f791c47e874ab
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252119"
---
# <a name="sp_redirect_publisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Specifica un server di pubblicazione reindirizzato per una coppia server di pubblicazione/database esistente. Se il database del server di pubblicazione appartiene a un gruppo di disponibilità Always On, il server di pubblicazione reindirizzato è il nome del listener del gruppo di disponibilità associato al gruppo di disponibilità.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @original_publisher = ] 'original_publisher'` il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ha pubblicato originariamente il database. *original_publisher* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @publisher_db = ] 'publisher_db'` il nome del database da pubblicare. *publisher_db* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @redirected_publisher = ] 'redirected_publisher'` il nome del listener del gruppo di disponibilità associato al gruppo di disponibilità che sarà il nuovo server di pubblicazione. *redirected_publisher* è di **tipo sysname**e non prevede alcun valore predefinito. Quando il listener del gruppo di disponibilità è configurato per una porta non predefinita, specificare il numero della porta insieme al nome del listener, ad esempio `'Listenername,51433'`  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 **sp_redirect_publisher** viene utilizzato per consentire il reindirizzamento di un server di pubblicazione della replica al database primario corrente di un gruppo di disponibilità always on associando la coppia server di pubblicazione/database al listener di un gruppo di disponibilità. Eseguire **sp_redirect_publisher** dopo che il listener del gruppo di disponibilità è stato configurato per il gruppo di disponibilità che contiene il database pubblicato.  
  
 Se il database di pubblicazione nel server di pubblicazione originale viene rimosso da un gruppo di disponibilità nella replica primaria, eseguire **sp_redirect_publisher** senza specificare un valore per il parametro *\@redirected_publisher* per rimuovere Reindirizzamento per la coppia server di pubblicazione/database. Per ulteriori informazioni sul reindirizzamento del server di pubblicazione quando, vedere [gestione di un database &#40;di pubblicazione&#41;AlwaysOn SQL Server](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 Il chiamante deve essere un membro del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** per il database di distribuzione oppure un membro di un elenco di accesso alla pubblicazione per una pubblicazione definita associata al database del server di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
