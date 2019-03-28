---
title: sp_mergemetadataretentioncleanup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1797200ce5369f49035f1a950d606e34e584edc2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526223"
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esegue una pulizia manuale dei metadati nel [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_ mapping](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), e [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) tabelle di sistema. Questa stored procedure viene eseguita in ogni server di pubblicazione e in ogni Sottoscrittore incluso nella topologia.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT` Restituisce il numero di righe rimosse dal [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) tabella. *num_genhistory_rows* viene **int**, il valore predefinito è **0**.  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT` Restituisce il numero di righe rimosse dal [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) tabella. *num_contents_rows* viene **int**, il valore predefinito è **0**.  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT` Restituisce il numero di righe rimosse dal [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) tabella. *num_tombstone_rows* viene **int**, il valore predefinito è **0**.  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only` Solo uso interno.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
  
> [!IMPORTANT]  
>  Se sono presenti più pubblicazioni in un database e una di esse viene utilizzato un periodo di memorizzazione infinito, in esecuzione **sp_mergemetadataretentioncleanup** non pulire il rilevamento delle modifiche di tipo merge della replica metadati per il database. È pertanto opportuno utilizzare il periodo di memorizzazione infinito con cautela. Per determinare se una pubblicazione di tipo ha un periodo di conservazione infinito, eseguire [sp_helpmergepublication &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) nel server di pubblicazione e nota delle pubblicazioni nel risultato impostato con il valore **0** per **conservazione**.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** corrette del database o gli utenti nell'elenco di accesso alla pubblicazione per un database pubblicato possono eseguire **sp_mergemetadataretentioncleanup**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
