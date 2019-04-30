---
title: Azioni e gruppi di azioni di SQL Server Audit | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- audit actions [SQL Server]
- audits [SQL Server], groups
- server-level audit actions [SQL Server]
- SQL Server Audit
- audit-level audit actions [SQL Server]
- database-level audit actions [SQL Server]
- audit action groups [SQL Server]
- audits [SQL Server], actions
ms.assetid: b7422911-7524-4bcd-9ab9-e460d5897b3d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e204a1865c2a928079fcd9b32b31a8ae0c0bd0a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63238138"
---
# <a name="sql-server-audit-action-groups-and-actions"></a>Azioni e gruppi di azioni di SQL Server Audit
  La funzionalità [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit consente di controllare gruppi di eventi ed eventi singoli a livello di server e di database. Per altre informazioni, vedere [SQL Server Audit &#40;Motore di database&#41;](sql-server-audit-database-engine.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono costituiti da zero o da più attività di controllo. Tali attività possono essere un gruppo di azioni, ad esempio Server_Object_Change_Group, oppure azioni singole, ad esempio operazioni SELECT da eseguire in una tabella.  
  
> [!NOTE]  
>  Server_Object_Change_Group include le operazioni CREATE, ALTER e DROP per qualsiasi oggetto server (database o endpoint).  
  
 Ai controlli possono essere associate le categorie di azioni seguenti:  
  
-   Azioni a livello di server, che includono operazioni server, ad esempio modifiche relative alla gestione e operazioni di accesso e di disconnessione.  
  
-   Azioni a livello di database, che includono operazioni DML (Data Manipulation Language) e DDL (Data Definition Language).  
  
-   Azioni a livello di controllo, ovvero le azioni del processo di controllo.  
  
 Alcune azioni eseguite sui componenti di controllo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono verificate in modo intrinseco in un controllo specifico. In questi casi gli eventi di controllo si verificano automaticamente poiché l'evento si è verificato nell'oggetto padre.  
  
 Di seguito sono elencate le azioni controllate in modo intrinseco:  
  
-   Modifica stato del controllo del server (impostazione dello stato su ON oppure OFF)  
  
 Di seguito sono elencati gli eventi non controllati in modo intrinseco:  
  
-   CREATE SERVER AUDIT SPECIFICATION  
  
-   ALTER SERVER AUDIT SPECIFICATION  
  
-   DROP SERVER AUDIT SPECIFICATION  
  
-   CREATE DATABASE AUDIT SPECIFICATION  
  
-   ALTER DATABASE AUDIT SPECIFICATION  
  
-   DROP DATABASE AUDIT SPECIFICATION  
  
 Al momento della creazione, tutti i controlli sono disabilitati.  
  
## <a name="server-level-audit-action-groups"></a>Gruppi di azioni di controllo a livello di server  
 I gruppi di azioni di controllo a livello di server sono analoghi alle classi degli eventi di controllo della sicurezza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [SQL Server Event Class Reference](../../event-classes/sql-server-event-class-reference.md).  
  
 Nella tabella seguente vengono descritti i gruppi di azioni di controllo a livello di server e, dove applicabile, viene specificata la classe di evento di SQL Server equivalente.  
  
|Nome del gruppo di azioni|Descrizione|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|Questo evento viene generato ogni volta che una password viene modificata per un ruolo applicazione. Equivale a [Audit App Role Change Password Event Class](../../event-classes/audit-app-role-change-password-event-class.md).|  
|AUDIT_CHANGE_GROUP|Questo evento viene generato ogni volta che un controllo viene creato, modificato o eliminato, nonché ogni volta che la specifica di un controllo viene creata, modificata o eliminata. Qualsiasi modifica al controllo viene verificata nel controllo stesso. Equivale a [Audit Change Audit Event Class](../../event-classes/audit-change-audit-event-class.md).|  
|BACKUP_RESTORE_GROUP|Questo evento viene generato ogni volta che viene eseguito un comando per il backup o il ripristino. Equivalente alla [classe di evento Audit Backup/Restore](../../event-classes/audit-backup-and-restore-event-class.md).|  
|BROKER_LOGIN_GROUP|Questo evento viene generato per segnalare i messaggi di controllo correlati alla sicurezza del trasporto Service Broker. Equivale a [Audit Broker Login Event Class](../../event-classes/audit-broker-login-event-class.md).|  
|DATABASE_CHANGE_GROUP|Questo evento viene generato quando un database viene creato, modificato o eliminato. viene creato, modificato o eliminato. Equivale a [Audit Database Management Event Class](../../event-classes/audit-database-management-event-class.md).|  
|DATABASE_LOGOUT_GROUP|Questo evento viene generato quando un utente del database indipendente si disconnette da un database. Equivale alla classe di evento Audit Database Logout.|  
|DATABASE_MIRRORING_LOGIN_GROUP|Questo evento viene generato per segnalare i messaggi di controllo correlati alla sicurezza del trasporto del mirroring del database. Equivale a [Audit Database Mirroring Login Event Class](../../event-classes/audit-database-mirroring-login-event-class.md).|  
|DATABASE_OBJECT_ACCESS_GROUP|Questo evento viene generato a ogni accesso a oggetti di database, ad esempio tipi di messaggio, assembly e contratti.<br /><br /> Questo evento viene generato per qualsiasi accesso a qualsiasi database. **Nota:**  Questa situazione potrebbe provocare ai record di controllo di dimensioni elevate. <br /><br /> Equivale a [Audit Database Object Access Event Class](../../event-classes/audit-database-object-access-event-class.md).|  
|DATABASE_OBJECT_CHANGE_GROUP|Questo evento viene generato quando si esegue un'istruzione CREATE, ALTER o DROP in oggetti di database, ad esempio schemi. L'evento viene generato ogni volta che un oggetto di database viene creato, modificato o eliminato. **Nota:**  Questo potrebbe causare una quantità molto elevate di record di controllo. <br /><br /> Equivale a [Audit Database Object Management Event Class](../../event-classes/audit-database-object-management-event-class.md).|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|Questo evento viene generato in caso di modifica del proprietario di oggetti nell'ambito del database. Questo evento viene generato in caso di qualsiasi modifica del proprietario di oggetti per qualsiasi database del server. Equivale a [Audit Database Object Take Ownership Event Class](../../event-classes/audit-database-object-take-ownership-event-class.md).|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|Questo evento viene generato quando è stata eseguita un'istruzione GRANT, REVOKE o DENY per oggetti di database, ad esempio assembly o schemi. Questo evento viene generato per qualsiasi modifica alle autorizzazioni per gli oggetti per qualsiasi database del server. Equivale a [Audit Database Object GDR Event Class](../../event-classes/audit-database-object-gdr-event-class.md).|  
|DATABASE_OPERATION_GROUP|Questo evento viene generato quando vengono effettuate operazioni in un database, ad esempio il checkpoint o la sottoscrizione di notifiche di query. nonché in caso di qualsiasi operazione effettuata su qualsiasi database. Equivale a [Audit Database Operation Event Class](../../event-classes/audit-database-operation-event-class.md).|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|Questo evento viene generato quando si utilizza l'istruzione ALTER AUTHORIZATION per modificare il proprietario di un database e quando vengono controllate le autorizzazioni necessarie a tale scopo. L'evento viene inoltre generato in caso di qualsiasi modifica del proprietario del database per qualsiasi database del server. Equivale a [Audit Change Database Owner Event Class](../../event-classes/audit-change-database-owner-event-class.md).|  
|DATABASE_PERMISSION_CHANGE_GROUP|Questo evento viene generato ogni volta che una qualsiasi entità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] emette GRANT, REVOKE o DENY per un'autorizzazione per le istruzioni. Questa situazione si applica ad eventi relativi esclusivamente a database, ad esempio la concessione di autorizzazioni in un database.<br /><br /> Questo evento viene generato per qualsiasi modifica alle autorizzazioni del database (evento GDR) per qualsiasi database del server. Equivale a [Audit Database Scope GDR Event Class](../../event-classes/audit-database-scope-gdr-event-class.md).|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|Questo evento viene generato quando in un database vengono create, modificate o eliminate entità, quali gli utenti. Equivale a [Audit Database Principal Management Event Class](../../event-classes/audit-database-principal-management-event-class.md). L'evento equivale anche alla classe di evento Audit Add DB Principal, generata in relazione alle stored procedure deprecate sp_grantdbaccess, sp_revokedbaccess, sp_addPrincipal e sp_dropPrincipal.<br /><br /> Questo evento viene generato ogni volta che un ruolo del database viene aggiunto o rimosso utilizzando le stored procedure sp_addrole e sp_droprole. nonché ogni volta che una qualsiasi entità di database viene creata, modificata o eliminata da un database. Equivale a [Classe di evento Audit Add Role](../../event-classes/audit-add-role-event-class.md).|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|Questo evento viene generato in presenza di un'operazione di rappresentazione nell'ambito del database, ad esempio EXECUTE AS \<entità> o SETPRINCIPAL. Questo evento viene generato per le rappresentazioni effettuate in qualsiasi database. Equivale a [Audit Database Principal Impersonation Event Class](../../event-classes/audit-database-principal-impersonation-event-class.md).|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|Questo evento viene generato ogni volta che un account di accesso viene aggiunto a un ruolo del database o rimosso. La classe di evento viene generata in relazione alle stored procedure sp_addrolemember, sp_changegroup e sp_droprolemember. Questo evento viene generato per qualsiasi modifica apportata ai membri del ruolo del database in qualsiasi database. Equivale a [Classe di evento Audit Add Member to DB Role](../../event-classes/audit-add-member-to-db-role-event-class.md).|  
|DBCC_GROUP|Questo evento viene generato ogni volta che un'entità esegue un comando DBCC. Equivale a [Audit DBCC Event Class](../../event-classes/audit-dbcc-event-class.md).|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|Viene indicato il tentativo fallito di accesso a un database indipendente da parte di un'entità. Gli eventi di questa classe vengono generati da connessioni nuove o riutilizzate da un pool di connessioni. Equivale a [Audit Login Failed Event Class](../../event-classes/audit-login-failed-event-class.md).|  
|FAILED_LOGIN_GROUP|Indica che un'entità ha tentato di accedere a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e l'operazione ha avuto esito negativo. Gli eventi di questa classe vengono generati da connessioni nuove o riutilizzate da un pool di connessioni. Equivale a [Audit Login Failed Event Class](../../event-classes/audit-login-failed-event-class.md).|  
|FULLTEXT_GROUP|Viene indicata l'occorrenza di un evento full-text. Equivale a [Audit Fulltext Event Class](../../event-classes/audit-fulltext-event-class.md).|  
|LOGIN_CHANGE_PASSWORD_GROUP|Questo evento viene generato ogni volta che una password di accesso viene modificata tramite l'istruzione ALTER LOGIN o la stored procedure sp_password. Equivale a [Audit Login Change Password Event Class](../../event-classes/audit-login-change-password-event-class.md).|  
|LOGOUT_GROUP|Viene indicata la disconnessione da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]da parte di un'entità. Gli eventi di questa classe vengono generati da connessioni nuove o riutilizzate da un pool di connessioni. Equivale a [Audit Logout Event Class](../../event-classes/audit-logout-event-class.md).|  
|SCHEMA_OBJECT_ACCESS_GROUP|Questo evento viene generato ogni volta che nello schema è stata utilizzata un'autorizzazione per gli oggetti. Equivale a [Audit Schema Object Access Event Class](../../event-classes/audit-schema-object-access-event-class.md).|  
|SCHEMA_OBJECT_CHANGE_GROUP|Questo evento viene generato quando si effettua un'operazione CREATE, ALTER o DROP in uno schema. Equivale a [Audit Schema Object Management Event Class](../../event-classes/audit-schema-object-management-event-class.md).<br /><br /> Questo evento viene generato negli oggetti dello schema. Equivale a [Audit Object Derived Permission Event Class](../../event-classes/audit-object-derived-permission-event-class.md).<br /><br /> Questo evento viene generato ogni volta che uno schema di un database viene modificato. Equivale a [Audit Statement Permission Event Class](../../event-classes/audit-statement-permission-event-class.md).|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|Questo evento viene generato quando vengono controllate le autorizzazioni per la modifica del proprietario dell'oggetto dello schema, ad esempio una tabella, una procedura o una funzione. Questa situazione si verifica quando si assegna un proprietario a un oggetto tramite l'istruzione ALTER AUTHORIZATION. Questo evento viene generato in caso di qualsiasi modifica del proprietario dello schema per qualsiasi database del server. Equivale a [Audit Schema Object Take Ownership Event Class](../../event-classes/audit-schema-object-take-ownership-event-class.md).|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|Questo evento viene generato ogni volta che un'istruzione GRANT, DENY o REVOKE viene eseguita per un oggetto dello schema. Equivale a [Audit Schema Object GDR Event Class](../../event-classes/audit-schema-object-gdr-event-class.md).|  
|SERVER_OBJECT_CHANGE_GROUP|Questo evento viene generato per operazioni CREATE, ALTER o DROP negli oggetti server. Equivale a [Audit Server Object Management Event Class](../../event-classes/audit-server-object-management-event-class.md).|  
|SERVER_OBJECT_OWNERSHIP_CHANGE_GROUP|Questo evento viene generato in caso di modifica del proprietario degli oggetti nell'ambito del server. Equivale a [Audit Server Object Take Ownership Event Class](../../event-classes/audit-server-object-take-ownership-event-class.md).|  
|SERVER_OBJECT_PERMISSION_CHANGE_GROUP|Questo evento viene generato ogni volta che una qualsiasi entità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]consente di eseguire un'istruzione GRANT, REVOKE o DENY in relazione a un'autorizzazione per l'oggetto server. Equivale a [Audit Server Object GDR Event Class](../../event-classes/audit-server-object-gdr-event-class.md).|  
|SERVER_OPERATION_GROUP|Questo evento viene generato quando si utilizzano operazioni di controllo della sicurezza, ad esempio la modifica di impostazioni, risorse, opzioni per l'accesso esterno o autorizzazioni. Equivale a [Audit Server Operation Event Class](../../event-classes/audit-server-operation-event-class.md).|  
|SERVER_PERMISSION_CHANGE_GROUP|Questo evento viene generato quando viene eseguita un'istruzione GRANT, REVOKE o DENY in relazione alle autorizzazioni nell'ambito del server, ad esempio in caso di creazione di un account di accesso. Equivale a [Audit Server Scope GDR Event Class](../../event-classes/audit-server-scope-gdr-event-class.md).|  
|SERVER_PRINCIPAL_CHANGE_GROUP|Questo evento viene generato in caso di creazione, modifica o eliminazione di entità del server. Equivale a [Audit Server Principal Management Event Class](../../event-classes/audit-server-principal-management-event-class.md).<br /><br /> Questo evento viene generato quando un'entità esegue la stored procedure sp_defaultdb o sp_defaultlanguage o l'istruzione ALTER LOGIN. Equivale a [Audit Addlogin Event Class](../../event-classes/audit-addlogin-event-class.md).<br /><br /> Questo evento viene generato in relazione alle stored procedure sp_addlogin e sp_droplogin. e a [Audit Login Change Property Event Class](../../event-classes/audit-login-change-property-event-class.md).<br /><br /> Questo evento viene generato per sp_grantlogin o sp_revokelogin stored procedure. Equivale a [Audit Login GDR Event Class](../../event-classes/audit-login-gdr-event-class.md).|  
|SERVER_PRINCIPAL_IMPERSONATION_GROUP|Questo evento viene generato in presenza di una rappresentazione nell'ambito del server, ad esempio EXECUTE AS \<account di accesso>. Equivale a [Audit Server Principal Impersonation Event Class](../../event-classes/audit-server-principal-impersonation-event-class.md).|  
|SERVER_ROLE_MEMBER_CHANGE_GROUP|Questo evento viene generato ogni volta che un account di accesso viene aggiunto a un ruolo predefinito del server o rimosso. L'evento viene generato in relazione alle stored procedure sp_addsrvrolemember e sp_dropsrvrolemember. Equivale a [Classe di evento Audit Add Login to Server Role](../../event-classes/audit-add-login-to-server-role-event-class.md).|  
|SERVER_STATE_CHANGE_GROUP|Questo evento viene generato quando lo stato del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene modificato. Equivale a [Audit Server Starts and Stops Event Class](../../event-classes/audit-server-starts-and-stops-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Viene indicato il corretto accesso a un database indipendente da parte di un'entità. Equivale alla classe di evento Audit Successful Database Authentication.|  
|SUCCESSFUL_LOGIN_GROUP|Viene indicato il corretto accesso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]da parte di un'entità. Gli eventi di questa classe vengono generati da connessioni nuove o riutilizzate da un pool di connessioni. Equivale a [Audit Login Event Class](../../event-classes/audit-login-event-class.md).|  
|TRACE_CHANGE_GROUP|Questo evento viene generato per tutte le istruzioni che consentono di controllare l'autorizzazione ALTER TRACE. Equivale a [Audit Server Alter Trace Event Class](../../event-classes/audit-server-alter-trace-event-class.md).|  
|USER_CHANGE_PASSWORD_GROUP|Questo evento viene generato ogni volta che la password di un utente del database indipendente viene modificata tramite l'istruzione ALTER USER.|  
|USER_DEFINED_AUDIT_GROUP|Questo gruppo consente di monitorare gli eventi generati usando [sp_audit_write &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-audit-write-transact-sql). In genere, nei trigger o nelle stored procedure sono incluse chiamate a `sp_audit_write` per abilitare il controllo di eventi importanti.|  
  
### <a name="considerations"></a>Considerazioni  
 Nei gruppi di azioni a livello di server sono comprese azioni relative a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Qualsiasi controllo dell'accesso agli oggetti dello schema in un database, ad esempio, viene registrato se il gruppo di azioni appropriato viene aggiunto a una specifica del controllo del server. In una specifica del controllo del database vengono registrati solo gli accessi agli oggetti dello schema del database specifico.  
  
 Le azioni a livello di server non consentono di applicare filtri dettagliati sulle azioni a livello di database. Per implementare l'applicazione di filtri dettagliati sull'azione, è necessario un controllo a livello di database, ad esempio un controllo di azioni SELECT nella tabella relativa ai clienti  per account di accesso nel gruppo relativo ai dipendenti. In una specifica del controllo di un database utente non includere oggetti con ambito server, ad esempio viste di sistema.  
  
## <a name="database-level-audit-action-groups"></a>Gruppi di azioni di controllo a livello di database  
 I gruppi di azioni di controllo a livello di database sono analoghi alle classi di eventi di controllo della sicurezza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per ulteriori informazioni sulle classi degli eventi, vedere [SQL Server Event Class Reference](../../event-classes/sql-server-event-class-reference.md).  
  
 Nella tabella seguente vengono descritti i gruppi di azioni di controllo a livello di database e, dove applicabile, viene specificata la classe di evento di SQL Server equivalente.  
  
|Nome del gruppo di azioni|Descrizione|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|Questo evento viene generato ogni volta che una password viene modificata per un ruolo applicazione. Equivale a [Audit App Role Change Password Event Class](../../event-classes/audit-app-role-change-password-event-class.md).|  
|AUDIT_CHANGE_GROUP|Questo evento viene generato ogni volta che un controllo viene creato, modificato o eliminato, nonché ogni volta che la specifica di un controllo viene creata, modificata o eliminata. Qualsiasi modifica al controllo viene verificata nel controllo stesso. Equivale a [Audit Change Audit Event Class](../../event-classes/audit-change-audit-event-class.md).|  
|BACKUP_RESTORE_GROUP|Questo evento viene generato ogni volta che viene eseguito un comando per il backup o il ripristino. Equivalente alla [classe di evento Audit Backup/Restore](../../event-classes/audit-backup-and-restore-event-class.md).|  
|DATABASE_CHANGE_GROUP|Questo evento viene generato quando un database viene creato, modificato o eliminato. Equivale a [Audit Database Management Event Class](../../event-classes/audit-database-management-event-class.md).|  
|DATABASE_LOGOUT_GROUP|Questo evento viene generato quando un utente del database indipendente si disconnette da un database. Equivalente alla [classe di evento Audit Backup/Restore](../../event-classes/audit-backup-and-restore-event-class.md).|  
|DATABASE_OBJECT_ACCESS_GROUP|Questo evento viene generato ogni volta che viene eseguito l'accesso a oggetti di database, ad esempio certificati e chiavi asimmetriche. Equivale a [Audit Database Object Access Event Class](../../event-classes/audit-database-object-access-event-class.md).|  
|DATABASE_OBJECT_CHANGE_GROUP|Questo evento viene generato quando si esegue un'istruzione CREATE, ALTER o DROP in oggetti di database, ad esempio schemi. Equivale a [Audit Database Object Management Event Class](../../event-classes/audit-database-object-management-event-class.md).|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|Questo evento viene generato in caso di modifica del proprietario di oggetti nell'ambito del database. Equivale a [Audit Database Object Take Ownership Event Class](../../event-classes/audit-database-object-take-ownership-event-class.md).|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|Questo evento viene generato quando è stata eseguita un'istruzione GRANT, REVOKE o DENY per oggetti di database, ad esempio assembly o schemi. Equivale a [Audit Database Object GDR Event Class](../../event-classes/audit-database-object-gdr-event-class.md).|  
|DATABASE_OPERATION_GROUP|Questo evento viene generato quando vengono effettuate operazioni in un database, ad esempio il checkpoint o la sottoscrizione di notifiche di query. Equivale a [Audit Database Operation Event Class](../../event-classes/audit-database-operation-event-class.md).|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|Questo evento viene generato quando si utilizza l'istruzione ALTER AUTHORIZATION per modificare il proprietario di un database e quando vengono controllate le autorizzazioni necessarie a tale scopo. Equivale a [Audit Change Database Owner Event Class](../../event-classes/audit-change-database-owner-event-class.md).|  
|DATABASE_PERMISSION_CHANGE_GROUP|Questo evento viene generato ogni volta che un qualsiasi utente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue un'istruzione GRANT, REVOKE o DENY in relazione a un'autorizzazione per eventi relativi esclusivamente a database, ad esempio la concessione di autorizzazioni in un database. Equivale a [Audit Database Scope GDR Event Class](../../event-classes/audit-database-scope-gdr-event-class.md).|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|Questo evento viene generato quando in un database vengono create, modificate o eliminate entità, quali gli utenti. Equivale a [Audit Database Principal Management Event Class](../../event-classes/audit-database-principal-management-event-class.md). Equivale anche alla [classe di evento Audit Add DB User](../../event-classes/audit-add-db-user-event-class.md), generata in relazione alle stored procedure deprecate sp_grantdbaccess, sp_revokedbaccess, sp_adduser e sp_dropuser.<br /><br /> Questo evento viene generato ogni volta che un ruolo del database viene aggiunto o rimosso utilizzando le stored procedure deprecate sp_addrole e sp_droprole. Equivale a [Classe di evento Audit Add Role](../../event-classes/audit-add-role-event-class.md).|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|Questo evento viene generato quando vi è una rappresentazione nell'ambito del database, ad esempio EXECUTE AS \<utente > o SETUSER. Equivale a [Audit Database Principal Impersonation Event Class](../../event-classes/audit-database-principal-impersonation-event-class.md).|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|Questo evento viene generato ogni volta che un account di accesso viene aggiunto a un ruolo del database o rimosso. Questa classe di evento viene usata con le stored procedure sp_addrolemember, sp_changegroup e sp_droprolemember. Equivale alla [classe di evento Audit Add Member to DB Role](../../event-classes/audit-add-member-to-db-role-event-class.md)|  
|DBCC_GROUP|Questo evento viene generato ogni volta che un'entità esegue un comando DBCC. Equivale a [Audit DBCC Event Class](../../event-classes/audit-dbcc-event-class.md).|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|Viene indicato il tentativo fallito di accesso a un database indipendente da parte di un'entità. Gli eventi di questa classe vengono generati da connessioni nuove o riutilizzate da un pool di connessioni. Viene generato questo evento.|  
|SCHEMA_OBJECT_ACCESS_GROUP|Questo evento viene generato ogni volta che nello schema è stata utilizzata un'autorizzazione per gli oggetti. Equivale a [Audit Schema Object Access Event Class](../../event-classes/audit-schema-object-access-event-class.md).|  
|SCHEMA_OBJECT_CHANGE_GROUP|Questo evento viene generato quando si effettua un'operazione CREATE, ALTER o DROP in uno schema. Equivale a [Audit Schema Object Management Event Class](../../event-classes/audit-schema-object-management-event-class.md).<br /><br /> Questo evento viene generato negli oggetti dello schema. Equivale a [Audit Object Derived Permission Event Class](../../event-classes/audit-object-derived-permission-event-class.md). e a [Audit Statement Permission Event Class](../../event-classes/audit-statement-permission-event-class.md).|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|Questo evento viene generato quando vengono controllate le autorizzazioni per la modifica del proprietario dell'oggetto dello schema, ad esempio una tabella, una procedura o una funzione. Questa situazione si verifica quando si assegna un proprietario a un oggetto tramite l'istruzione ALTER AUTHORIZATION. Equivale a [Audit Schema Object Take Ownership Event Class](../../event-classes/audit-schema-object-take-ownership-event-class.md).|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|Questo evento viene generato ogni volta che viene eseguita un'istruzione GRANT, DENY o REVOKE per un oggetto dello schema. Equivale a [Audit Schema Object GDR Event Class](../../event-classes/audit-schema-object-gdr-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Viene indicato il corretto accesso a un database indipendente da parte di un'entità. Equivale alla classe di evento Audit Successful Database Authentication.|  
|USER_CHANGE_PASSWORD_GROUP|Questo evento viene generato ogni volta che la password di un utente del database indipendente viene modificata tramite l'istruzione ALTER USER.|  
|USER_DEFINED_AUDIT_GROUP|Questo gruppo consente di monitorare gli eventi generati usando [sp_audit_write &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-audit-write-transact-sql).|  
  
## <a name="database-level-audit-actions"></a>Azioni di controllo a livello di database  
 Le azioni a livello di database supportano il controllo di azioni specifiche direttamente nello schema del database e negli oggetti dello schema, ad esempio tabelle, viste, stored procedure, funzioni, stored procedure estese, code e sinonimi. Tipi, raccolte di XML Schema, database e schemi non sono controllati. Il controllo di oggetti dello schema può essere configurato nello schema o nel database, ovvero tutti gli eventi sugli oggetti dello schema contenuti nello schema o nel database specificato verranno controllati. Nella tabella seguente vengono descritte le azioni di controllo a livello di database.  
  
|Azione|Descrizione|  
|------------|-----------------|  
|SELECT|Questo evento viene generato ogni volta che viene eseguita un'istruzione SELECT.|  
|UPDATE|Questo evento viene generato ogni volta che viene eseguita un'istruzione UPDATE.|  
|INSERT|Questo evento viene generato ogni volta che viene eseguita un'istruzione INSERT.|  
|DELETE|Questo evento viene generato ogni volta che viene eseguita un'istruzione DELETE.|  
|EXECUTE|Questo evento viene generato ogni volta che viene eseguita un'istruzione EXECUTE.|  
|RECEIVE|Questo evento viene generato ogni volta che viene eseguita un'istruzione RECEIVE.|  
|REFERENCES|Questo evento viene generato ogni volta che viene controllata un'autorizzazione REFERENCES.|  
  
### <a name="considerations"></a>Considerazioni  
*  Le azioni di controllo a livello di database non si applicano alle colonne.  
  
*  Quando Query Processor parametrizza la query, il parametro può apparire nel log degli eventi di controllo anziché nei valori di colonna della query. 
 
*  Le istruzioni RPC non vengono registrate.   
  
## <a name="audit-level-audit-action-groups"></a>Gruppi di azioni di controllo a livello di controllo  
 È possibile controllare le azioni anche durante il processo di controllo stesso. Questa operazione può essere eseguita sia nell'ambito del server che in quello del database. In quest'ultimo caso l'operazione può essere eseguita solo per le specifiche del controllo del database. Nella tabella seguente vengono descritti i gruppi di azioni di controllo a livello di controllo.  
  
|Nome del gruppo di azioni|Descrizione|  
|-----------------------|-----------------|  
|AUDIT_ CHANGE_GROUP|Questo evento viene generato ogni volta che viene eseguito uno dei comandi seguenti:<br /><br /> -CREATE SERVER AUDIT<br />-ALTER SERVER AUDIT<br />-DROP SERVER AUDIT<br />-CREA SPECIFICA CONTROLLO SERVER<br />-ALTER SERVER AUDIT SPECIFICATION<br />-DROP SERVER AUDIT SPECIFICATION<br />-CREA SPECIFICA CONTROLLO DATABASE<br />-ALTER DATABASE AUDIT SPECIFICATION<br />-DROP DATABASE AUDIT SPECIFICATION|  
  
## <a name="related-content"></a>Contenuto correlato  
 [Creazione di un controllo del server e di una specifica del controllo del server](create-a-server-audit-and-server-audit-specification.md)  
  
 [Creazione di un controllo del server e di una specifica del controllo del database](create-a-server-audit-and-database-audit-specification.md)  
  
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
  
  
