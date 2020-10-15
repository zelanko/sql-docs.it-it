---
description: cdc.captured_columns (Transact-SQL)
title: cdc.captured_columns (Transact-SQL) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3337ab3e4b4c2221c018c326762251ff954b329d
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081490"
---
# <a name="cdccaptured_columns-transact-sql"></a>cdc.captured_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce una riga per ogni colonna registrata in un'istanza di acquisizione. Per impostazione predefinita, sono acquisite tutte le colonne della tabella di origine. Tuttavia, le colonne possono essere incluse o escluse quando la tabella di origine è abilitata per l'acquisizione dei dati delle modifiche specificando un elenco di colonne. Per ulteriori informazioni, vedere [sys.sp_cdc_enable_table &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 Si consiglia di **non eseguire una query direttamente sulle tabelle di sistema**. Eseguire invece il [sys.sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md) stored procedure.  
   
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID della tabella delle modifiche a cui appartiene la colonna acquisita.|  
|**column_name**|**sysname**|Nome della colonna acquisita.|  
|**column_id**|**int**|ID della colonna acquisita all'interno della tabella di origine.|  
|**column_type**|**sysname**|Tipo della colonna acquisita.|  
|**column_ordinal**|**int**|Numero ordinale di colonna (in base 1) della tabella delle modifiche. Sono escluse le colonne di metadati nella tabella delle modifiche. Il numero ordinale 1 è assegnato alla prima colonna acquisita.|  
|**is_computed**|**bit**|Indica che la colonna acquisita è una colonna calcolata nella tabella di origine.|  
  
## <a name="see-also"></a>Vedere anche  
 [cdc.change_tables &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
