---
title: sys. server_audits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_audits_TSQL
- sys.server_audits_TSQL
- sys.server_audits
- server_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_audits catalog view
ms.assetid: c2c4a000-1127-46a8-b1e9-947fd1136e1e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 67f25c6f4d39eb8cbd3b09d2e7710462f91ed397
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821593"
---
# <a name="sysserver_audits-transact-sql"></a>sys.server_audits (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni controllo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un'istanza del server. Per altre informazioni, vedere [SQL Server Audit &#40;Motore di database&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|ID del controllo.|  
|**name**|**sysname**|Nome del controllo.|  
|**audit_guid**|**uniqueidentifier**|GUID per il controllo utilizzato per enumerare i controlli con server membro&#124;specifiche del controllo del database durante le operazioni di avvio del server e di connessione del database.|  
|**create_date**|**datetime**|Data UTC di creazione del controllo.|  
|**modify_date**|**datetime**|Data UTC dell'ultima modifica del controllo.|  
|**principal_id**|**int**|ID del proprietario del controllo registrato nel server.|  
|**type**|**char(2)**|Tipo di controllo:<br /><br /> SL-NT registro eventi di sicurezza<br /><br /> Log eventi dell'applicazione AL-NT<br /><br /> File FL file system|  
|**type_desc**|**nvarchar(60)**|SECURITY LOG<br /><br /> APPLICATION LOG<br /><br /> FILE|  
|**on_failure**|**tinyint**|Voce in condizione di errore:<br /><br /> 0-continua<br /><br /> 1-arrestare un'istanza del server<br /><br /> 2-operazione non riuscita|  
|**on_failure_desc**|**nvarchar(60)**|Voce in condizione di errore:<br /><br /> CONTINUE<br /><br /> SHUTDOWN SERVER INSTANCE<br /><br /> FAIL_OPERATION|  
|**is_state_enabled**|**tinyint**|0 - Disabilitata<br /><br /> 1: abilitato|  
|**queue_delay**|**int**|Tempo massimo di attesa, in millisecondi, prima della scrittura su disco. Se il valore è 0, il controllo garantirà una scrittura prima che un evento possa continuare.|  
|**predicato**|**nvarchar (3000)**|Espressione del predicato applicata all'evento.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Le entità con l'autorizzazione **ALTER ANY Server Audit** o **View any Definition** possono accedere a questa vista del catalogo. Non è inoltre necessario negare l'autorizzazione **View any Definition** per l'entità.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREAZIONE della specifica del controllo del SERVER &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREARE una specifica del controllo del DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys. fn_get_audit_file &#40;&#41;Transact-SQL](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys. server_file_audits &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys. server_audit_specifications &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys. server_audit_specification_details &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys. database_audit_specifications &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys. database_audit_specification_details &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys. dm_server_audit_status &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys. dm_audit_actions &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys. dm_audit_class_type_map &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Creazione di un controllo del server e di una specifica del controllo del server](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
