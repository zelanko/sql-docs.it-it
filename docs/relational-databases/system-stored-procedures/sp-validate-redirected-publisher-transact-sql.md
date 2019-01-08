---
title: sp_validate_redirected_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47bf5c0ada106a11bdef72debf401de0640ff11f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818923"
---
# <a name="spvalidateredirectedpublisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Verifica che l'host corrente per il database del server di pubblicazione sia in grado di supportare la replica. Deve essere eseguito da un database di distribuzione. Questa procedura viene chiamata da **sp_get_redirected_publisher**.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@original_publisher** =] **'***original_publisher***'**  
 Il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ha pubblicato in origine il database. *original_publisher* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Il nome del database da pubblicare. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***'**  
 La destinazione di reindirizzamento specificato quando **sp_redirect_publisher** è stato chiamato per la coppia server di pubblicazione/database. *redirected_publisher* viene **sysname**, non prevede alcun valore predefinito.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna.  
  
## <a name="remarks"></a>Note  
 Se non esiste alcuna voce per il server di pubblicazione e il database di pubblicazione **sp_validate_redirected_publisher** restituisce null nel parametro di output *@redirected_publisher*. Se una voce esiste, viene restituita nel parametro di output sia nei casi di esito positivo che di esito negativo.  
  
 Se la convalida ha esito positivo, **sp_validate_redirected_publisher** restituisce un'indicazione di esito positivo.  
  
 Se la convalida non riesce, vengono generati gli errori con la relativa descrizione.  
  
## <a name="permissions"></a>Permissions  
 Chiamante deve essere un membro del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database per database di distribuzione o un membro di un elenco accesso pubblicazione per una pubblicazione definita associati al database di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
