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
ms.openlocfilehash: 28589be83c62f705457e990b328be98e88905568
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771267"
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Consente di verificare un filtro di join tra due tabelle per determinare se la relativa clausola è valida. Questa stored procedure restituisce inoltre informazioni sul filtro di join specificato e indica se può essere utilizzato con partizioni pre-calcolate per la tabella specificata. Questa stored procedure viene eseguita nella pubblicazione del server di pubblicazione. Per altre informazioni, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @filtered_table = ] 'filtered_table'`Nome di una tabella filtrata. *filtered_table* è di **tipo nvarchar (400)** e non prevede alcun valore predefinito.  
  
`[ @join_table = ] 'join_table'`Nome di una tabella che viene unita in join a *filtered_table*. *join_table* è di **tipo nvarchar (400)** e non prevede alcun valore predefinito.  
  
`[ @join_filterclause = ] 'join_filterclause'`Clausola del filtro di join sottoposta a test. *join_filterclause* è di **tipo nvarchar (1000)** e non prevede alcun valore predefinito.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|Indica se la pubblicazione è idonea per le partizioni pre-calcolate. dove **1** indica che è possibile usare le partizioni valore e **0** indica che non possono essere usate.|  
|**has_dynamic_filters**|**bit**|Indica se la clausola di filtro fornita include almeno una funzione di filtro con parametri. dove **1** indica che viene utilizzata una funzione di filtro con parametri e **0** indica che tale funzione non viene utilizzata.|  
|**dynamic_filters_function_list**|**nvarchar(500)**|Elenco delle funzioni nella clausola di filtro che definiscono un filtro con parametri per un articolo, separate con un punto e virgola.|  
|**uses_host_name**|**bit**|Se nella clausola di filtro viene utilizzata la funzione [HOST_NAME ()](../../t-sql/functions/host-name-transact-sql.md) , dove **1** indica che questa funzione è presente.|  
|**uses_suser_sname**|**bit**|Se nella clausola di filtro viene utilizzata la funzione [SUSER_SNAME ()](../../t-sql/functions/suser-sname-transact-sql.md) , dove **1** indica che questa funzione è presente.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_check_join_filter** viene utilizzata per la replica di tipo merge.  
  
 **sp_check_join_filter** può essere eseguito su tutte le tabelle correlate anche se non sono pubblicate. Questa stored procedure può essere utilizzata per verificare una clausola di filtro di join prima della definizione di un filtro di join tra due articoli.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_check_join_filter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
