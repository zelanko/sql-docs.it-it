---
title: sp_check_dynamic_filters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b31249dda65f427ce53d3418e7a62f4bb0abf6d1
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124131"
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza informazioni sulle proprietà dei filtri di riga con parametri per una pubblicazione, specificando in particolare le funzioni utilizzate per generare una partizione di dati filtrati per una pubblicazione e se la pubblicazione consente l'utilizzo di partizioni pre-calcolate. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@publication**=] **'**_pubblicazione_**'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Se la pubblicazione consente l'utilizzo di partizioni pre-calcolate; in cui **1** significa che le partizioni calcolate possono essere utilizzate, e **0** significa che non possono essere utilizzate.|  
|**has_dynamic_filters**|**bit**|È se è stato definito il filtro di almeno una riga con parametri della pubblicazione; in cui **1** significa che esistono uno o più filtri di riga con parametri, e **0** significa che non esistono filtri dinamici.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Elenco delle funzioni utilizzate per filtrare gli articoli di una pubblicazione, separate con un punto e virgola.|  
|**validate_subscriber_info**|**nvarchar(500)**|Elenco delle funzioni utilizzate per filtrare gli articoli di una pubblicazione, separate con un segno più (+).|  
|**uses_host_name**|**bit**|Se il [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) funzione viene usata nei filtri di riga con parametri, dove **1** indica che questa funzione viene utilizzata per i filtri dinamici.|  
|**uses_suser_sname**|**bit**|Se il [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) funzione viene usata nei filtri di riga con parametri, dove **1** indica che questa funzione viene utilizzata per i filtri dinamici.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_check_dynamic_filters** viene utilizzata nella replica di tipo merge.  
  
 Se una pubblicazione è stata definita per utilizzare partizioni precalcolate **sp_check_dynamic_filters** verifica la presenza di eventuali violazioni delle restrizioni di partizioni pre-calcolate. Se viene rilevata una qualsiasi violazione, viene restituito un errore. Per altre informazioni, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 Se una pubblicazione è stata definita in modo da includere filtri di riga con parametri ma non viene rilevato alcun filtro, viene restituito un errore.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_check_dynamic_filters**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione delle partizioni di una pubblicazione di tipo Merge con filtri con parametri](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
