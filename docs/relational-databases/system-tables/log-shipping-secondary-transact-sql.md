---
title: log_shipping_secondary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary
- log_shipping_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary system table
ms.assetid: 69723419-4544-49c6-a517-adb30ffa5741
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5debab1572bc2f788c0dc13773d0dc140c693108
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82805948"
---
# <a name="log_shipping_secondary-transact-sql"></a>log_shipping_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Archivia un record per ogni ID secondario. Questa tabella è archiviata nel database **msdb** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**secondary_id**|**uniqueidentifier**|ID del server secondario nella configurazione per il log shipping.|  
|**primary_server**|**sysname**|Nome dell'istanza primaria del Motore di database di SQL Server nella configurazione di log shipping.|  
|**primary_database**|**sysname**|Nome del database primario nella configurazione di log shipping.|  
|**backup_source_directory**|**nvarchar (500)**|Directory in cui vengono archiviati i file di backup del log delle transazioni dal server primario.|  
|**backup_destination_directory**|**nvarchar (500)**|Directory nel server secondario in cui vengono copiati i file di backup.|  
|**file_retention_period**|**int**|Durata di tempo, in minuti, durante la quale un file di backup viene mantenuto nel server secondario prima di essere eliminato.|  
|**copy_job_id**|**uniqueidentifier**|ID associato al processo di copia nel server secondario.|  
|**restore_job_id**|**uniqueidentifier**|ID associato al processo di ripristino nel server secondario.|  
|**monitor_server**|**sysname**|Nome dell'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizzata come server di monitoraggio nella configurazione del log shipping.|  
|**monitor_server_security_mode**|**bit**|Modalità di sicurezza utilizzata per connettersi al server di monitoraggio.<br /><br /> 1 = Autenticazione di Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione di.|  
|**last_copied_file**|**nvarchar (500)**|Nome dell'ultimo file di backup copiato nel server secondario.|  
|**last_copied_date**|**datetime**|Data e ora dell'ultima operazione di copia nel server secondario.|  
  
## <a name="remarks"></a>Commenti  
 Più database secondari nello stesso server secondario per un determinato database primario condividono alcune impostazioni nella tabella **log_shipping_secondary** . Se una impostazione condivisa viene modificata per uno dei database, l'impostazione viene modificata per tutti i database.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul &#40;di log shipping SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
