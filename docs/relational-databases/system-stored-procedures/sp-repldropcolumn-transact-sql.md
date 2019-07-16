---
title: sp_repldropcolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldropcolumn_TSQL
- sp_repldropcolumn
helpviewer_keywords:
- sp_repldropcolumn
ms.assetid: fdc1ec5f-f108-42b4-a2d8-f06a71913ab8
author: stevestein
ms.author: sstein
ms.openlocfilehash: d18116f59b44e5e36e92d755c7a8ac7d7fdc683e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090020"
---
# <a name="sprepldropcolumn-transact-sql"></a>sp_repldropcolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina una colonna da un articolo di tabella esistente pubblicato. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]
>  Questa stored procedure è deprecata e viene supportata solo per motivi di compatibilità con le versioni precedenti. Deve essere utilizzata solo con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] server di pubblicazione e [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] sottoscrittori di ripubblicazione. Questa stored procedure non deve essere utilizzata nelle colonne con tipi di dati introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_repldropcolumn [ @source_object = ] 'source_object', [ @column = ] 'column'   
    [ , [ @from_agent = ] from_agent]   
    [ , [ @schema_change_script = ] 'schema_change_script' ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>Argomenti  
 [ @source_object =] '*source_object*'  
 Nome dell'articolo di tabella contenente la colonna da eliminare. *source_object* è nvarchar(258), non prevede alcun valore predefinito.  
  
 [ @column =] '*colonna*'  
 Nome della colonna nella tabella da eliminare. *colonna* è di tipo sysname e non prevede alcun valore predefinito.  
  
 [ @from_agent =] *from_agent*  
 Specifica se la stored procedure viene eseguita da un agente di replica. *from_agent* è int, valore predefinito 0, in cui viene utilizzato un valore pari a 1 quando questa stored procedure viene eseguita da un agente di replica e in tutti gli altri casi deve essere utilizzato il valore predefinito pari a 0.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 Specifica il nome e il percorso di uno script di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per modificare le stored procedure personalizzate generate dal sistema. *schema_change_script* è nvarchar (4000), con un valore predefinito è NULL. La replica consente di sostituire una o più stored procedure predefinite utilizzate per la replica transazionale con stored procedure personalizzate definite dall'utente. *schema_change_script* viene eseguito dopo una modifica dello schema viene eseguita in un articolo di tabella replicato utilizzando sp_repldropcolumn e può essere utilizzata per eseguire una delle operazioni seguenti:  
  
-   Se le stored procedure personalizzate vengono rigenerate automaticamente, *schema_change_script* può essere utilizzato per eliminare le stored procedure personalizzate e sostituirle con definito dall'utente stored procedure personalizzate che supportano il nuovo schema.  
  
-   Se le stored procedure personalizzate non vengono rigenerate automaticamente, *schema_change_script*può essere usato per rigenerare queste stored procedure o stored procedure di creazione personalizzate definite dall'utente.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 Abilita o disabilita la funzionalità che consente di invalidare uno snapshot. *force_invalidate_snapshot* è di tipo bit, con un valore predefinito è 1.  
  
 Il valore 1 specifica che le modifiche all'articolo possono invalidare lo snapshot. In tal caso, il valore 1 consente l'esecuzione del nuovo snapshot.  
  
 Il valore 0 specifica che le modifiche apportate all'articolo non invalidano lo snapshot.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 Abilita o disabilita la funzionalità che consente di reinizializzare la sottoscrizione. *force_reinit_subscription* è di tipo bit con valore predefinito è 0.  
  
 Il valore 0 specifica che le modifiche apportate all'articolo non causano la reinizializzazione della sottoscrizione.  
  
 Il valore 1 specifica che le modifiche apportate all'articolo possono causare la reinizializzazione della sottoscrizione. In tal caso, il valore 1 consente la reinizializzazione della sottoscrizione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server sysadmin sul server di pubblicazione o i membri dei ruoli predefiniti del database db_owner o db_ddladmin nel database di pubblicazione possono eseguire sp_repldropcolumn.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità deprecate nella replica di SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
