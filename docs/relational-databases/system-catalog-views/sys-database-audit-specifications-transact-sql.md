---
description: sys.database_audit_specifications (Transact-SQL)
title: sys. database_audit_specifications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_audit_specifications_TSQL
- sys.database_audit_specifications_TSQL
- sys.database_audit_specifications
- database_audit_specifications
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_audit_specifications catalog view
ms.assetid: bf80e5c6-0588-4eb7-86ff-aa7c73461335
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c2a8125bd67a5de2a3e88dab7e108b6e570f4bf9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469933"
---
# <a name="sysdatabase_audit_specifications-transact-sql"></a>sys.database_audit_specifications (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene informazioni sulle specifiche del controllo del database in un controllo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un'istanza del server. Per altre informazioni, vedere [SQL Server Audit &#40;Motore di database&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|Nome|**sysname**|Nome della specifica del controllo.|  
|database_specification_id|**int**|ID della specifica del database.|  
|create_date|**datetime**|Data di creazione della specifica del controllo.|  
|modified_date|**datetime**|Data dell'ultima modifica della specifica del controllo.|  
|is_state_enabled|**bit**|Stato della specifica del controllo:<br /><br /> 0-DISABILITATO<br /><br /> 1: ABILITATO|  
|audit_GUID|**uniqueidentifer**|GUID del controllo che contiene questa specifica. Viene utilizzato durante l'enumerazione delle specifiche del controllo del database membro durante l'avvio o il collegamento del database.|  
  
## <a name="remarks"></a>Osservazioni  
 Se un database è in modalità di sola lettura, la funzionalità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit non può aggiungere specifiche del controllo del database.  
  
## <a name="permissions"></a>Autorizzazioni  
 Le entità con autorizzazioni **ALTER ANY database audit** o **View definition** , il ruolo dbo e i membri del ruolo predefinito del database db_owners possono accedere a questa vista del catalogo. Inoltre, all'entità non deve essere negata l'autorizzazione **View definition** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]. Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Creazione di un controllo del server e di una specifica del controllo del server](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
