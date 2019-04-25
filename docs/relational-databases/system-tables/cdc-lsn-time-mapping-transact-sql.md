---
title: cdc.lsn_time_mapping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3118a814d18013a4360dd9afdcd1e09dcc483545
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471114"
---
# <a name="cdclsntimemapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni transazione per la quale sono presenti righe in una tabella delle modifiche. Questa tabella viene utilizzata per eseguire il mapping tra valori di commit di numero di sequenza del file di log (LSN) e l'ora in cui è stato eseguito il commit della transazione. È possibile che vengano registrate anche le voci per le quali non esistono voci nelle tabelle delle modifiche. Questo consente alla tabella di registrare il completamento dell'elaborazione del numero LSN in periodi in cui le attività di modifica sono poche o inesistenti.  
  
 È consigliabile non eseguire una query direttamente sulle tabelle di sistema. Eseguire invece i [fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) e [Sys. fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) funzioni di sistema.  
    
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|Numero LSN della transazione completata.|  
|**tran_begin_time**|**datetime**|Ora in cui ha avuto inizio la transazione associata al numero LSN.|  
|**tran_end_time**|**datetime**|Ora di fine della transazione.|  
|**tran_id**|**varbinary(10)**|ID della transazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Log delle transazioni &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [cdc.&#60;capture_instance&#62;_CT &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
