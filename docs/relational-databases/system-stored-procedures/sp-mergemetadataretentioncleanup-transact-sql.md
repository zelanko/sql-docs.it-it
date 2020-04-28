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
ms.openlocfilehash: 41c3a6848d71d7ba8f22667c117686485bb569b6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68019969"
---
# <a name="sp_mergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esegue una pulizia manuale dei metadati nelle tabelle di sistema [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)e [MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md) . Questa stored procedure viene eseguita in ogni server di pubblicazione e in ogni Sottoscrittore incluso nella topologia.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT`Restituisce il numero di righe rimosse dalla tabella [MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md) . *num_genhistory_rows* è di **tipo int**e il valore predefinito è **0**.  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT`Restituisce il numero di righe rimosse dalla tabella [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) . *num_contents_rows* è di **tipo int**e il valore predefinito è **0**.  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT`Restituisce il numero di righe rimosse dalla tabella [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) . *num_tombstone_rows* è di **tipo int**e il valore predefinito è **0**.  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only`Solo per uso interno.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
  
> [!IMPORTANT]  
>  Se in un database sono presenti più pubblicazioni e una di queste pubblicazioni utilizza un periodo di memorizzazione infinito, l'esecuzione di **sp_mergemetadataretentioncleanup** non comporta la pulizia dei metadati del rilevamento delle modifiche della replica di tipo merge per il database. È pertanto opportuno utilizzare il periodo di memorizzazione infinito con cautela. Per determinare se una pubblicazione ha un periodo di conservazione infinito, eseguire [sp_helpmergepublication &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md) nel server di pubblicazione e prendere nota di eventuali pubblicazioni nel set di risultati con un valore pari a **0** per la **conservazione**.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del **db_owner** ruolo predefinito del database o gli utenti nell'elenco di accesso alla pubblicazione di un database pubblicato possono eseguire **sp_mergemetadataretentioncleanup**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
