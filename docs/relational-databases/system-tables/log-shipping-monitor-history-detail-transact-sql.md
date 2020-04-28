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
ms.openlocfilehash: 0f0a304020b972b29d521bd32da3f98b8d3fdfc9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67990000"
---
# <a name="log_shipping_monitor_history_detail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Archivia i dettagli della cronologia relativi ai processi di log shipping. Questa tabella è archiviata nel database **msdb** .  
  
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
  
## <a name="remarks"></a>Osservazioni  
 Questa tabella contiene i dettagli della cronologia per gli agenti per il log shipping. Per identificare una sessione di Agent, utilizzare le colonne **agent_id**, **agent_type**e **session_id**. Per visualizzare i dettagli della cronologia per la sessione dell'agente, Ordina per **log_time**.  
  
 Oltre a essere archiviate sul server di monitoraggio remoto, le informazioni relative al server primario vengono archiviate nel server primario nella tabella **log_shipping_monitor_history_detail** e le informazioni relative a un server secondario vengono inoltre archiviate nel server secondario nella tabella **log_shipping_monitor_history_detail** .  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul &#40;di log shipping SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_delete_log_shipping_primary_database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Tabelle di sistema &#40;&#41;Transact-SQL](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [log_shipping_monitor_error_detail &#40;&#41;Transact-SQL](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
