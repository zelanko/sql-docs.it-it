---
title: Record di SQL Server Audit | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audit records [SQL Server]
ms.assetid: 7a291015-df15-44fe-8d53-c6d90a157118
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3cc249ebfce796d7932e68d993ac98ede867845f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238385"
---
# <a name="sql-server-audit-records"></a>Record di SQL Server Audit
  La caratteristica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit consente di controllare gruppi di eventi ed eventi a livello di server e di database. Per altre informazioni, vedere [SQL Server Audit &#40;Motore di database&#41;](sql-server-audit-database-engine.md). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (Indici per tabelle con ottimizzazione per la memoria).  
  
 I controlli sono costituiti da zero o più attività di controllo, che vengono registrate in una *destinazione*del controllo. La destinazione del controllo può essere un file binario, il registro eventi applicazioni di Windows o il registro eventi di sicurezza di Windows. I record inviati alla destinazione possono contenere gli elementi descritti nella tabella seguente.  
  
|Nome colonna|Descrizione|Tipo|Sempre disponibile|  
|-----------------|-----------------|----------|----------------------|  
|**event_time**|Data e ora di generazione dell'azione controllabile.|`datetime2`|Yes|  
|**sequence_no**|Viene tenuta traccia della sequenza dei record all'interno di un singolo record di controllo con dimensioni troppo elevate per il buffer di scrittura dei controlli.|`int`|Yes|  
|**action_id**|ID dell'azione.<br /><br /> Suggerimento: Per utilizzare **action_id** come predicato, è necessario convertirlo da stringa di caratteri in valore numerico. Per altre informazioni, vedere [Filter SQL Server Audit on action_id / class_type predicate](https://blogs.msdn.com/b/sqlsecurity/archive/2012/10/03/filter-sql-server-audit-on-action-id-class-type-predicate.aspx)(Filtro di SQL Server Audit con il predicato action_id / class_type).|`varchar(4)`|Yes|  
|**succeeded**|Indica se l'azione che ha generato l'evento ha avuto esito positivo|`bit` -1 = esito positivo, 0 = esito negativo|Yes|  
|**permission_bitmask**|Se applicabile, visualizza le autorizzazioni concesse, negate o revocate.|`bigint`|No|  
|**is_column_permission**|Flag indicante un'autorizzazione a livello di colonna.|`bit` -1 = true, 0 = False|No|  
|**session_id**|ID della sessione in cui si è verificato l'evento.|`int`|Yes|  
|**server_principal_id**|ID del contesto dell'account di accesso utilizzato per eseguire l'azione.|`int`|Yes|  
|**database_principal_id**|ID del contesto dell'utente del database in cui viene eseguita l'azione.|`int`|No|  
|**object_id**|ID primario dell'entità in cui si è verificato il controllo. ad esempio:<br /><br /> oggetti server<br /><br /> database<br /><br /> oggetti di database<br /><br /> oggetti dello schema|`int`|No|  
|**target_server_principal_id**|Entità server cui si applica l'azione controllabile.|`int`|Yes|  
|**target_database_principal_id**|Entità di database cui si applica l'azione controllabile.|`int`|No|  
|**class_type**|Tipo di entità controllabile in cui si verifica il controllo.|`varchar(2)`|Yes|  
|**session_server_principal_name**|Entità server per la sessione.|`sysname`|Yes|  
|**server_principal_name**|Account di accesso corrente.|`sysname`|Yes|  
|**server_principal_sid**|SID dell'account di accesso corrente.|`varbinary`|Yes|  
|**database_principal_name**|Utente corrente.|`sysname`|No|  
|**target_server_principal_name**|Account di accesso di destinazione dell'azione.|`sysname`|No|  
|**target_server_principal_sid**|SID dell'account di accesso di destinazione.|`varbinary`|No|  
|**target_database_principal_name**|Utente di destinazione dell'azione.|`sysname`|no|  
|**server_instance_name**|Nome dell'istanza del server in cui si è verificato il controllo. Viene utilizzato il formato standard computer\istanza.|`nvarchar(120)`|Yes|  
|**database_name**|Contesto del database in cui si è verificata l'azione.|`sysname`|No|  
|**schema_name**|Contesto dello schema in cui si è verificata l'azione.|`sysname`|No|  
|**object_name**|Nome dell'entità in cui si è verificato il controllo. ad esempio:<br /><br /> oggetti server<br /><br /> database<br /><br /> oggetti di database<br /><br /> oggetti dello schema<br /><br /> istruzione TSQL (se presente)|`sysname`|No|  
|**istruzione**|istruzione TSQL (se presente)|`nvarchar(4000)`|No|  
|**additional_information**|Qualsiasi informazione aggiuntiva sull'evento, archiviata in formato XML.|`nvarchar(4000)`|No|  
  
## <a name="remarks"></a>Note  
 Alcune azioni non consentono l'inserimento di un valore di colonna perché il valore potrebbe non essere valido per l'azione.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit archivia 4000 caratteri di dati per ogni campo di tipo carattere in un record di controllo. Quando i valori **additional_information** e **statement** restituiti da un'azione controllabile sono costituiti da più di 4000 caratteri, viene usata la colonna **sequence_no** per scrivere più record nel report del controllo in modo che i dati vengano registrati da una singola azione di controllo. Il processo è il seguente:  
  
-   La colonna **statement** viene divisa in 4000 caratteri.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit scrive i dati parziali come prima riga del record di controllo. Tutti gli altri campi vengono duplicati in ogni riga.  
  
-   Viene incrementato il valore di **sequence_no** .  
  
-   Questo processo viene ripetuto fino a registrare tutti i dati.  
  
 È possibile connettere i dati leggendo le righe in sequenza con il valore **sequence_no** e le colonne **event_Time**, **action_id** e **session_id** per identificare l'azione.  
  
## <a name="related-content"></a>Contenuto correlato  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)  
  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-transact-sql)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-specification-transact-sql)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-transact-sql)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)  
  
  
