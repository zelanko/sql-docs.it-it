---
title: captured_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.captured_columns
- cdc.captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.captured_columns
ms.assetid: 7bb4d408-d764-4ef6-802c-f271c8d39c2a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96927e2c0a773674cbc4b8dabee804870d6559e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119262"
---
# <a name="cdccapturedcolumns-transact-sql"></a>cdc.captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni colonna registrata in un'istanza di acquisizione. Per impostazione predefinita, sono acquisite tutte le colonne della tabella di origine. Tuttavia, le colonne possono essere incluse o escluse quando la tabella di origine è abilitata per l'acquisizione dei dati delle modifiche specificando un elenco di colonne. Per altre informazioni, vedere [Sys. sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 È consigliabile che si **eseguono query direttamente le tabelle di sistema**. Eseguire invece i [sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md) stored procedure.  
   
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID della tabella di origine alla quale appartiene la colonna acquisita.|  
|**column_name**|**sysname**|Nome della colonna acquisita.|  
|**column_id**|**int**|ID della colonna acquisita all'interno della tabella di origine.|  
|**COLUMN_TYPE**|**sysname**|Tipo della colonna acquisita.|  
|**column_ordinal**|**int**|Numero ordinale di colonna (in base 1) della tabella delle modifiche. Sono escluse le colonne di metadati nella tabella delle modifiche. Il numero ordinale 1 è assegnato alla prima colonna acquisita.|  
|**is_computed**|**bit**|Indica che la colonna acquisita è una colonna calcolata nella tabella di origine.|  
  
## <a name="see-also"></a>Vedere anche  
 [cdc.change_tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
