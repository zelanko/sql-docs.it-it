---
title: CDC. index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c2dac6ec3b2799a4489d660c9467000b27391236
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833080"
---
# <a name="cdcindex_columns-transact-sql"></a>cdc.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni colonna dell'indice associata a una tabella delle modifiche. Le colonne dell'indice vengono utilizzate da Change Data Capture per identificare in modo univoco le righe della tabella di origine. Per impostazione predefinita, vengono incluse le colonne della chiave primaria della tabella di origine. Se tuttavia viene specificato un indice univoco nella tabella di origine quando Change Data Capture è abilitato nella tabella di origine, vengono utilizzate le colonne di tale indice. Nella tabella di origine viene richiesto un indice univoco o una chiave primaria se è abilitato il rilevamento delle modifiche totali. Per ulteriori informazioni, vedere [sys. sp_cdc_enable_table &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 È consigliabile non eseguire una query direttamente sulle tabelle di sistema. Eseguire invece il stored procedure [sys. sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) .  

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID della tabella delle modifiche.|  
|**column_name**|**sysname**|Nome della colonna dell'indice.|  
|**index_ordinal**|**tinyint**|Ordinale (in base 1) della colonna all'interno dell'indice.|  
|**column_id**|**int**|ID della colonna della tabella di origine.|  
  
## <a name="see-also"></a>Vedere anche  
 [CDC. change_tables &#40;&#41;Transact-SQL](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
