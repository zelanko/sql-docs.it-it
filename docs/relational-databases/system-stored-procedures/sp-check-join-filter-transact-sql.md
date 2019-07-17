---
title: sp_check_join_filter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
author: stevestein
ms.author: sstein
ms.openlocfilehash: f180e2b3478ce136fa16d82084d46b79e6152957
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070418"
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di verificare un filtro di join tra due tabelle per determinare se la relativa clausola è valida. Questa stored procedure restituisce inoltre informazioni sul filtro di join specificato e indica se può essere utilizzato con partizioni pre-calcolate per la tabella specificata. Questa stored procedure viene eseguita nella pubblicazione del server di pubblicazione. Per altre informazioni, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @filtered_table = ] 'filtered_table'` È il nome di una tabella filtrata. *filtered_table* viene **nvarchar(400)** , non prevede alcun valore predefinito.  
  
`[ @join_table = ] 'join_table'` È il nome di una tabella da unire in join *filtered_table*. *join_table* viene **nvarchar(400)** , non prevede alcun valore predefinito.  
  
`[ @join_filterclause = ] 'join_filterclause'` Si sta testando la clausola di filtro di join. *join_filterclause* viene **nvarchar(1000)** , non prevede alcun valore predefinito.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Se la pubblicazione consente le partizioni pre-calcolate. in cui **1** significa che è possono utilizzare le partizioni di valore, e **0** significa che non possono essere utilizzate.|  
|**has_dynamic_filters**|**bit**|Se la clausola di filtro include almeno una funzione di filtro con parametri; in cui **1** indica che viene utilizzata una funzione di filtro con parametri, e **0** significa che tale funzione non viene utilizzata.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Elenco delle funzioni nella clausola di filtro che definiscono un filtro con parametri per un articolo, separate con un punto e virgola.|  
|**uses_host_name**|**bit**|Se il [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) funzione viene utilizzata nella clausola di filtro, in cui **1** indica che questa funzione viene utilizzata.|  
|**uses_suser_sname**|**bit**|Se il [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) funzione viene utilizzata nella clausola di filtro, in cui **1** indica che questa funzione viene utilizzata.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_check_join_filter** viene utilizzata nella replica di tipo merge.  
  
 **sp_check_join_filter** può essere eseguito su tutte le tabelle correlate anche se non è pubblicata. Questa stored procedure può essere utilizzata per verificare una clausola di filtro di join prima della definizione di un filtro di join tra due articoli.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_check_join_filter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
