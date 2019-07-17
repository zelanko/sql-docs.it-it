---
title: sp_register_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: c10451148c6f9b2fda231691b770bca3928517f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075753"
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La replica consente di sostituire una o più stored procedure predefinite utilizzate per la replica transazionale con stored procedure personalizzate definite dall'utente. Quando viene apportata una modifica dello schema a una tabella replicata, queste stored procedure vengono ricreate. **sp_register_custom_scripting** registra una stored procedure o [!INCLUDE[tsql](../../includes/tsql-md.md)] file script che viene eseguito quando viene apportata una modifica dello schema per uno script la definizione di una nuovo utente-stored procedure personalizzata definita. Questa nuova stored procedure personalizzata definita dall'utente deve riflettere il nuovo schema della tabella. **sp_register_custom_scripting** viene eseguita nel database di pubblicazione, server di pubblicazione e la stored procedure o un file script registrato viene eseguita nel Sottoscrittore quando viene apportata una modifica dello schema.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @type = ] 'type'` Il tipo di stored procedure personalizzata o script viene registrato. *tipo di* viene **varchar(16)** e non prevede alcun valore predefinito e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**insert**|La stored procedure personalizzata registrata viene eseguita quando viene replicata un'istruzione INSERT.|  
|**update**|La stored procedure personalizzata registrata viene eseguita quando viene replicata un'istruzione UPDATE.|  
|**delete**|La stored procedure personalizzata registrata viene eseguita quando viene replicata un'istruzione DELETE.|  
|**custom_script**|Lo script viene eseguito alla fine del trigger DDL (Data Definition Language).|  
  
`[ @value = ] 'value'` Nome di una stored procedure o nome e percorso completo per il [!INCLUDE[tsql](../../includes/tsql-md.md)] file script da registrare. *valore* viene **nvarchar(1024)** , non prevede alcun valore predefinito.  
  
> [!NOTE]  
>  Specificando NULL per *valore*parametro verrà annullata la registrazione di uno script registrato in precedenza, ovvero lo stesso che [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md).  
  
 Quando il valore di *tipo* viene **custom_script**, il nome e percorso completo di un [!INCLUDE[tsql](../../includes/tsql-md.md)] file script, è necessario. In caso contrario, *valore* deve essere il nome di una stored procedure registrata.  
  
`[ @publication = ] 'publication'` Nome della pubblicazione per cui viene registrato la stored procedure o script personalizzati. *pubblicazione* viene **sysname**, il valore predefinito è **NULL**.  
  
`[ @article = ] 'article'` Nome dell'articolo per cui viene registrato la stored procedure o script personalizzati. *articolo* viene **sysname**, il valore predefinito è **NULL**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_register_custom_scripting** viene utilizzata nella replica snapshot e transazionale.  
  
 Questa stored procedure deve essere eseguita prima di apportare una modifica dello schema a una tabella replicata. Per altre informazioni sull'uso di questa stored procedure, vedere [rigenerare procedure transazionali personalizzate per riflettere le modifiche dello Schema](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database, o la **db_ddladmin** ruolo predefinito del database possono eseguire **sp _ register_custom_scripting**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_unregister_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
