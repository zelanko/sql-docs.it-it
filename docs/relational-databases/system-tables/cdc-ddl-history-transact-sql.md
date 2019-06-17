---
title: cdc.ddl_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.ddl_history_TSQL
- cdc.ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.ddl_history
ms.assetid: cb97ea71-da2f-441a-bbd2-db1f5f48ab49
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b68bace89b49ba11fe7744229a5f7b9500ec6cdf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471394"
---
# <a name="cdcddlhistory-transact-sql"></a>cdc.ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni modifica DDL (Data Definition Language) apportata a tabelle abilitate per l'acquisizione dei dati delle modifiche. È possibile utilizzare questa tabella per determinare quando si è verificata una modifica DDL su una tabella di origine e la modifica effettuata. Per le tabelle di origine per cui non sono state eseguite modifiche DDL non esistono voci in questa tabella.  
  
 È consigliabile non eseguire una query direttamente sulle tabelle di sistema. Eseguire invece i [sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) stored procedure.  
   
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**source_object_id**|**int**|ID della tabella di origine alla quale è stata applicata la modifica DDL.|  
|**object_id**|**int**|ID della tabella delle modifiche associata a un'istanza di acquisizione per la tabella di origine.|  
|**required_column_update**|**bit**|Indica che il tipo di dati di una colonna acquisita è stato modificato nella tabella di origine. Questa modifica ha modificato la colonna nella tabella delle modifiche.|  
|**ddl_command**|**nvarchar(max)**|Istruzione DDL applicata alla tabella di origine.|  
|**ddl_lsn**|**binary(10)**|Il numero di sequenza del file di log (LSN) associato all'impegno della modifica DDL.|  
|**ddl_time**|**datetime**|Data e ora di esecuzione della modifica DDL nella tabella di origine.|  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
