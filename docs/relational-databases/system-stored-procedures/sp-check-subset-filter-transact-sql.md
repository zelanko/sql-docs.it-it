---
title: sp_check_subset_filter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords:
- sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d3e6ad6a0cf8ed5c84279b621badc939b1e97a8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791713"
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa stored procedure viene utilizzata per controllare una clausola di filtro in qualsiasi tabella per determinarne la validità per la tabella e per restituire informazioni sul filtro specificato, incluso se il filtro può essere utilizzato con partizioni pre-calcolate. Questa stored procedure viene eseguita nel database contenente la pubblicazione nel server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@filtered_table**=] **'***filtered_table***'**  
 Nome della tabella filtrata. *filtered_table* viene **nvarchar(400)**, non prevede alcun valore predefinito.  
  
 [ **@subset_filterclause** =] **'***subset_filterclause***'**  
 Clausola di filtro sottoposta a verifica. *subset_filterclause* viene **nvarchar(1000)**, non prevede alcun valore predefinito.  
  
 [ **@has_dynamic_filters**=] *has_dynamic_filters*  
 Indica se la clausola di filtro è un filtro di riga con parametri. *has_dynamic_filters* viene **bit**, con un valore predefinito è NULL ed è un parametro di output. Restituisce un valore pari **1** quando la clausola di filtro è un filtro di riga con parametri.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Se la pubblicazione consente l'utilizzo di partizioni pre-calcolate; in cui **1** significa che le partizioni calcolate possono essere utilizzate, e **0** significa che non possono essere utilizzate.|  
|**has_dynamic_filters**|**bit**|Se la clausola di filtro include almeno un filtro di riga con parametri; in cui **1** significa che viene utilizzato un filtro di riga con parametri, e **0** significa che tale funzione non viene utilizzata.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Elenca le funzioni nella clausola di filtro che filtrano dinamicamente un articolo. Ogni funzione è separata da un punto e virgola.|  
|**uses_host_name**|**bit**|Se il [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) funzione viene utilizzata nella clausola di filtro, in cui **1** indica che questa funzione viene utilizzata.|  
|**uses_suser_sname**|**bit**|Se il [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) funzione viene utilizzata nella clausola di filtro, in cui **1** indica che questa funzione viene utilizzata.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_check_subset_filter** viene utilizzata nella replica di tipo merge.  
  
 **sp_check_subset_filter** può essere eseguita in qualsiasi tabella anche se la tabella non è pubblicata. Questa stored procedure può essere utilizzata per verificare una clausola di filtro prima di definire un articolo filtrato.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_check_subset_filter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
