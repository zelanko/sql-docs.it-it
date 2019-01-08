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
manager: craigg
ms.openlocfilehash: 4c04df4cb844faf42506c781607a220e98a7db17
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779113"
---
# <a name="spredirectpublisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Specifica un server di pubblicazione reindirizzato per una coppia server di pubblicazione/database esistente. Se il server di pubblicazione appartiene a un gruppo di disponibilità AlwaysOn, il server di pubblicazione reindirizzato è il nome del listener gruppo di disponibilità associato al gruppo di disponibilità.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@original_publisher** =] **'***original_publisher***'**  
 Il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ha pubblicato in origine il database. *original_publisher* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Il nome del database da pubblicare. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***'**  
 Il nome del listener del gruppo di disponibilità associato al gruppo di disponibilità che sarà il nuovo server di pubblicazione. *redirected_publisher* viene **sysname**, non prevede alcun valore predefinito. Quando il listener del gruppo di disponibilità è configurato per una porta non predefinita, specificare il numero della porta insieme al nome del listener, ad esempio `'Listenername,51433'`  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 **sp_redirect_publisher** viene usato per consentire a un server di pubblicazione di replica essere reindirizzati alla replica primaria corrente di un gruppo di disponibilità AlwaysOn associando la coppia server di pubblicazione/database con un listener gruppo di disponibilità. Eseguire **sp_redirect_publisher** dopo aver configurato il listener del gruppo di disponibilità per il gruppo di disponibilità che contiene il database pubblicato.  
  
 Se il database di pubblicazione nel server di pubblicazione originale viene rimosso da un gruppo di disponibilità nella replica primaria, eseguire **sp_redirect_publisher** senza specificare un valore per il *@redirected_publisher* parametro da rimuovere il reindirizzamento per la coppia server di pubblicazione/database. Per ulteriori informazioni sul reindirizzamento del server di pubblicazione, vedere [gestione di un Database di pubblicazione AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 Chiamante deve essere un membro del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database per database di distribuzione o un membro di un elenco accesso pubblicazione per una pubblicazione definita associati al database di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
