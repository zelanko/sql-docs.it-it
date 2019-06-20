---
title: log_shipping_monitor_primary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_primary
- log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_primary system table
ms.assetid: 5f629a29-1a62-40e6-ae33-6f6b7dd09a36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 650fb8c3b043940658bcc50720c0e5dd1da822db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62719473"
---
# <a name="logshippingmonitorprimary-transact-sql"></a>log_shipping_monitor_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Archivia un record di monitoraggio per database primario in ogni configurazione per il log shipping. Questa tabella è archiviata nel **msdb** database.  
  
 Le tabelle correlate alla cronologia e al monitoraggio vengono utilizzate anche nel server primario e nei server secondari.   
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|ID del database primario nella configurazione per il log shipping.|  
|**primary_server**|**sysname**|Il nome dell'istanza primaria del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nella configurazione di log shipping.|  
|**primary_database**|**sysname**|Nome del database primario nella configurazione di log shipping.|  
|**backup_threshold**|**int**|Numero di minuti consentiti tra le operazioni di backup prima che venga generato un avviso.|  
|**threshold_alert**|**int**|Avviso da generare quando viene superata la soglia per il backup.|  
|**threshold_alert_enabled**|**bit**|Determina se sono abilitati gli avvisi relativi alla soglia per il backup. 1 = abilitati.<br /><br /> 0 = disabilitati.|  
|**last_backup_file**|**nvarchar(500)**|Percorso assoluto del backup del log delle transazioni più recente.|  
|**last_backup_date**|**datetime**|Data e ora dell'ultima operazione di backup del log delle transazioni nel database primario.|  
|**last_backup_date_utc**|**datetime**|Data e ora dell'ultima operazione di backup del log delle transazioni nel database primario in base all'ora UTC (Coordinated Universal Time).|  
|**history_retention_period**|**int**|Intervallo di tempo, espresso in minuti, di conservazione dei record relativi alla cronologia di log shipping per un database primario specifico trascorso il quale i record vengono eliminati.|  
  
## <a name="remarks"></a>Note  
 Oltre a essere archiviate sul server di monitoraggio remoto, le informazioni correlate al server primario vengono archiviate nel server primario nel relativo **log_shipping_monitor_primary** tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_change_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_help_log_shipping_monitor_primary &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)   
 [sp_delete_log_shipping_alert_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
