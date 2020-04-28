---
title: sp_syscollector_delete_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_collection_set_TSQL
- sp_syscollector_delete_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_delete_collecton_set
ms.assetid: 29c63a74-4db4-4068-bd57-9fb519b0c598
author: stevestein
ms.author: sstein
ms.openlocfilehash: e60fb13244d6740b7d52c568835e54155eeb8c46
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68000881"
---
# <a name="sp_syscollector_delete_collection_set-transact-sql"></a>sp_syscollector_delete_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina un set di raccolta definito dall'utente e tutti i relativi elementi della raccolta.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_delete_collection_set [[ @collection_set_id = ] collection_set_id OUTPUT ]  
    , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @collection_set_id = ] *collection_set_id*  
 Identificatore univoco del log del set di raccolta. *collection_set_id* è di **tipo int** e deve avere un valore se *Name* è null.  
  
 [ @name = ] '*Name*'  
 Nome del set di raccolta. *Name* è di **tipo sysname** e deve avere un valore se *collection_set_id* è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 È necessario eseguire sp_syscollector_delete_collection_set nel contesto del database di sistema msdb.  
  
 Il *collection_set_id* o il *nome* deve avere un valore e non può essere null. Per ottenere questi valori, eseguire una query sulla vista di sistema syscollector_collection_set.  
  
 Non è possibile eliminare set di raccolta definiti dal sistema.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire questa procedura, è richiesta l'appartenenza al ruolo predefinito del database dc_admin (con autorizzazione EXECUTE) .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato un set di raccolta definito dall'utente che specifica il *collection_set_id*.  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_delete_collection_set  
    @collection_set_id = 4;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure dell'agente di raccolta dati &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
