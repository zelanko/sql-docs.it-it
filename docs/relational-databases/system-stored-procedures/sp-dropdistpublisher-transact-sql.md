---
title: sp_dropdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ee7d2a6a50e03f6b0029e69dbf2b5c211004fe18
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813023"
---
# <a name="spdropdistpublisher-transact-sql"></a>sp_dropdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina un server di pubblicazione di distribuzione. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher=** ] **'***publisher***'**  
 Nome del server di pubblicazione da eliminare. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@no_checks=** ] *no_checks*  
 Specifica se **sp_dropdistpublisher** verifica che il server di pubblicazione sia stato disinstallato il server come server di distribuzione. *no_checks* viene **bit**, il valore predefinito è **0**.  
  
 Se **0**, replica viene verificato che il server di pubblicazione remoto sia stato disinstallato il server locale come server di distribuzione. Se il server di pubblicazione è locale, durante la replica viene verificato che nel server locale non siano più presenti oggetti di pubblicazione o di distribuzione.  
  
 Se **1**, tutti gli oggetti di replica associati alla distribuzione del server di pubblicazione vengono eliminati anche se non è possibile raggiungere un server di pubblicazione remoto. Dopo questa operazione, il server di pubblicazione remoto è necessario disinstallare la replica tramite [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) con **@ignore_distributor**  =  **1**.  
  
 [  **@ignore_distributor=** ] *ignore_distributor*  
 Specifica se gli oggetti di distribuzione vengono mantenuti nel server di distribuzione quando il server di pubblicazione viene rimosso. *ignore_distributor* viene **bit** i possibili valori sono i seguenti:  
  
 **1** = gli oggetti di distribuzione che appartengono al *server di pubblicazione* rimangono nel server di distribuzione.  
  
 **0** = gli oggetti di distribuzione per il *server di pubblicazione* vengono pulite nel server di distribuzione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_dropdistpublisher** viene utilizzata in tutti i tipi di replica.  
  
 Durante l'eliminazione di un server di pubblicazione Oracle, se non è possibile eliminare il server di pubblicazione **sp_dropdistpublisher** restituisce un errore e gli oggetti di database di distribuzione per il server di pubblicazione vengono rimossi.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_dropdistpublisher**.  
  
## <a name="see-also"></a>Vedere anche  
 [Disabilitare la pubblicazione e la distribuzione](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
