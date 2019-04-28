---
title: log_shipping_monitor_history_detail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_history_detail_TSQL
- log_shipping_monitor_history_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_history_detail system table
ms.assetid: 7080c888-323b-4206-a1ab-e6c51f9e2579
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f8968661442adabe4c04608ca5a5bb5362341c4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719623"
---
# <a name="logshippingmonitorhistorydetail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Archivia i dettagli della cronologia relativi ai processi di log shipping. Questa tabella è archiviata nel **msdb** database.  
  
 Le tabelle correlate alla cronologia e al monitoraggio vengono utilizzate anche nel server primario e nei server secondari.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|ID primario per il backup o ID secondario per la copia o il ripristino.|  
|**agent_type**|**tinyint**|Tipo di processo di log shipping.<br /><br /> 0 = backup.<br /><br /> 1 = copia.<br /><br /> 2 = ripristino.|  
|**session_id**|**int**|ID della sessione per il processo di backup/copia/ripristino.|  
|**database_name**|**sysname**|Nome del database associato a questo record. Database primario per il backup, database secondario per il ripristino, o vuoto per la copia.|  
|**session_status**|**tinyint**|Stato della sessione.<br /><br /> 0 = In fase di avvio.<br /><br /> 1 = In fase di esecuzione.<br /><br /> 2 = Esito positivo.<br /><br /> 3 = Errore.<br /><br /> 4 = Avviso.|  
|**log_time**|**datetime**|Data e ora di creazione del record.|  
|**log_time_utc**|**datetime**|Data e ora UTC (Coordinated Universal Time o ora di Greenwich) di creazione del record.|  
|**message**|**nvarchar(max)**|Testo del messaggio.|  
  
## <a name="remarks"></a>Note  
 Questa tabella contiene i dettagli della cronologia per gli agenti per il log shipping. Per identificare una sessione di agente, utilizzare le colonne **agent_id**, **agent_type**, e **session_id**. Per visualizzare i dettagli della cronologia per la sessione dell'agente, per ordinare **log_time**.  
  
 Oltre a essere archiviate sul server di monitoraggio remoto, le informazioni correlate al server primario vengono archiviate nel server primario nel relativo **log_shipping_monitor_history_detail** tabella e informazioni relative a un database secondario Server verrà archiviato anche nel server secondario nel relativo **log_shipping_monitor_history_detail** tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [log_shipping_monitor_error_detail &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
