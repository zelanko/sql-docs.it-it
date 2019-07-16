---
title: sp_repladdcolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords:
- sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b01a48e15c06f021b41b3bded35a0cd2739313c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006922"
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge una colonna a un articolo di tabella esistente che è stato pubblicato. È possibile aggiungere la nuova colonna in tutti i server di pubblicazione che pubblicano la tabella specificata oppure solo in una pubblicazione specifica della tabella. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
> [!IMPORTANT]
>  Questa stored procedure è deprecata e viene supportata per motivi di compatibilità con le versioni precedenti. Deve essere utilizzata solo con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] server di pubblicazione e [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] sottoscrittori di ripubblicazione. Questa stored procedure non deve essere utilizzata nelle colonne con tipi di dati introdotti in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versioni successive.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_repladdcolumn [ @source_object = ] 'source_object', [ @column = ] 'column' ]  
    [ , [ @typetext = ] 'typetext' ]  
    [ , [ @publication_to_add = ] 'publication_to_add' ]  
    [ , [ @from_agent = ] from_agent ]  
    [ , [ @schema_change_script = ] 'schema_change_script' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @source_object =] '*source_object*'  
 Nome dell'articolo di tabella che contiene la nuova colonna da aggiungere. *source_object* è **nvarchar (358**), non prevede alcun valore predefinito.  
  
 [ @column =] '*colonna*'  
 Nome della colonna della tabella da aggiungere per la replica. *colonna* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ @typetext =] '*typetext*'  
 Definizione della colonna da aggiungere. *TypeText* viene **nvarchar(3000)** , non prevede alcun valore predefinito. Ad esempio, se la colonna order_filled viene aggiunto ed è un singolo campo, non NULL di caratteri e ha un valore predefinito di **N**, order_filled le *colonna* parametro, mentre la definizione del colonna **char (1) non NULL CONSTRAINT nome_vincolo DEFAULT ' n'** sarebbe il *typetext* valore del parametro.  
  
 [ @publication_to_add =] '*publication_to_add*'  
 Nome della pubblicazione cui si desidera aggiungere la nuova colonna. *publication_to_add* viene **nvarchar (4000)** , il valore predefinito è **tutti**. Se **tutti**, quindi tutte le pubblicazioni che contiene la tabella sono interessate. Se *publication_to_add* è specificato, solo questa pubblicazione è la nuova colonna aggiunta.  
  
 [ @from_agent =] *from_agent*  
 Specifica se la stored procedure viene eseguita da un agente di replica. *from_agent* viene **int**, il valore predefinito è **0**, dove il valore **1** viene usato quando viene eseguita questa stored procedure da un agente di replica e in ogni altro caso, il valore predefinito di **0**deve essere utilizzato.  
  
 [ @schema_change_script =] '*schema_change_script*'  
 Specifica il nome e il percorso di uno script di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per modificare le stored procedure personalizzate generate dal sistema. *schema_change_script* viene **nvarchar (4000)** , con un valore predefinito è NULL. La replica consente di sostituire una o più stored procedure predefinite utilizzate per la replica transazionale con stored procedure personalizzate definite dall'utente. *schema_change_script* viene eseguito dopo una modifica dello schema in un articolo di tabella replicato utilizzando sp_repladdcolumn e può essere utilizzata per eseguire una delle operazioni seguenti:  
  
-   Se le stored procedure personalizzate vengono rigenerate automaticamente, *schema_change_script* può essere utilizzato per eliminare le stored procedure personalizzate e sostituirle con definito dall'utente stored procedure personalizzate che supportano il nuovo schema.  
  
-   Se le stored procedure personalizzate non vengono rigenerate automaticamente, *schema_change_script*può essere usato per rigenerare queste stored procedure o stored procedure di creazione personalizzate definite dall'utente.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 Abilita o disabilita la funzionalità che consente di invalidare uno snapshot. *force_invalidate_snapshot* è un **bit**, il valore predefinito è **1**.  
  
 **1** specifica che le modifiche apportate all'articolo possono invalidare lo snapshot non è valido, e se è il caso, il valore **1** concede l'autorizzazione per il nuovo snapshot.  
  
 **0** specifica che le modifiche apportate all'articolo non invalidano lo snapshot non è valido.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 Abilita o disabilita la funzionalità che consente di reinizializzare la sottoscrizione. *force_reinit_subscription* è un **bit** con valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non causano la reinizializzazione della sottoscrizione.  
  
 **1** specifica che le modifiche apportate all'articolo possono causare la reinizializzazione della sottoscrizione e se è il caso, il valore **1** concede l'autorizzazione per la reinizializzazione della sottoscrizione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server sysadmin e del ruolo predefinito del database db_owner possono eseguire sp_repladdcolumn.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità deprecate nella replica di SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
