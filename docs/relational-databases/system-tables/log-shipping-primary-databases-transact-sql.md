---
title: log_shipping_primary_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 893f016fba45d18947af376425012d21964709b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004725"
---
# <a name="logshippingprimarydatabases-transact-sql"></a>log_shipping_primary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Archivia un record per il database primario in una configurazione per il log shipping. Questa tabella è archiviata nel **msdb** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|ID del database primario nella configurazione per il log shipping.|  
|**primary_database**|**sysname**|Nome del database primario nella configurazione di log shipping.|  
|**backup_directory**|**nvarchar(500)**|Directory in cui vengono archiviati i file di backup del log delle transazioni dal server primario.|  
|**backup_share**|**nvarchar(500)**|Percorso di rete o UNC della directory di backup.|  
|**backup_retention_period**|**int**|Intervallo di tempo, espresso in minuti, di conservazione del file di backup dei log nella directory di backup trascorso il quale il file viene eliminato.|  
|**backup_job_id**|**uniqueidentifier**|Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID processo dell'agente associato con il processo di backup nel server primario.|  
|**monitor_server**|**sysname**|Il nome dell'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizzato come server di monitoraggio nella configurazione di log shipping.|  
|**monitor_server_security_mode**|**bit**|Modalità di sicurezza utilizzata per connettersi al server di monitoraggio.<br /><br /> 1 = Autenticazione di Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione.|  
|**last_backup_file**|**nvarchar(500)**|Percorso assoluto del backup del log delle transazioni più recente.|  
|**last_backup_date**|**datetime**|Data e ora dell'ultima operazione di backup dei log.|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database** e **sp_help_log_shipping_secondary_primary** usare questa colonna per controllare la visualizzazione delle impostazioni di monitoraggio in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].<br /><br /> 0 = richiamando una di queste due stored procedure, l'utente non specificava un valore esplicito per il **@monitor_server** parametro.<br /><br /> 1 = È stato specificato un valore esplicito.|  
|**backup_compression**|**tinyint**|Indica se la configurazione per il log shipping esegue l'override del comportamento della compressione dei backup a livello del server.<br /><br /> 0 = disabilitati. I backup del log non vengono mai compressi, indipendentemente dalle impostazioni di compressione dei backup configurate dal server.<br /><br /> 1 = abilitati. I backup del log vengono sempre compressi, indipendentemente dalle impostazioni di compressione dei backup configurate dal server.<br /><br /> 2 = viene utilizzata la configurazione del server per il [visualizzare o configurare l'opzione di configurazione del Server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) opzione di configurazione del server. Rappresenta il valore predefinito.<br /><br /> La compressione dei backup è supportata solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition.|  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
