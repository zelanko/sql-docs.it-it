---
title: Categoria di eventi Security Audit (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [SQL Server], Security Audit event category
- SQL Server event classes, Security Audit event category
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f2f854c7a6dbd0d1ab569f87bf053a5b9f45058
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044218"
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Categoria di eventi Security Audit (SQL Server Profiler)
  La categoria di eventi **controllo di sicurezza** contiene gli eventi di controllo di sicurezza.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Audit Add DB User - classe di evento](audit-add-db-user-event-class.md)|Indica che un account di accesso è stato aggiunto o rimosso dal database come utente di database.|  
|[Audit Add Login to Server Role - classe di evento](audit-add-login-to-server-role-event-class.md)|Indica che un account di accesso è stato aggiunto o rimosso da un ruolo predefinito del server.|  
|[Audit Add Member to DB Role - classe di evento](audit-add-member-to-db-role-event-class.md)|Indica che un account di accesso è stato aggiunto o rimosso da un ruolo.|  
|[Audit Add Role - classe di evento](audit-add-role-event-class.md)|Indica che un ruolo del database è stato aggiunto o rimosso da un database.|  
|[Audit Addlogin - classe di evento](audit-addlogin-event-class.md)|Indica che un account di accesso è stato aggiunto o rimosso.|  
|[Audit App Role Change Password - classe di evento](audit-app-role-change-password-event-class.md)|Indica che è stata modificata una password per un ruolo applicazione.|  
|[Classe di evento Audit Backup/Restore](audit-backup-and-restore-event-class.md)|Indica che è stata eseguita un'istruzione di backup o di ripristino.|  
|[Audit Broker Conversation - classe di evento](broker-conversation-event-class.md)|Segnala i messaggi di controllo correlati alla sicurezza del dialogo di Service Broker.|  
|[Audit Broker Login - classe di evento](audit-broker-login-event-class.md)|Segnala i messaggi di controllo correlati alla sicurezza del trasporto di Service Broker.|  
|[Audit Change Audit - classe di evento](audit-change-audit-event-class.md)|Indica che è stata apportata una modifica alla traccia di controllo.|  
|[Audit Change Database Owner - classe di evento](audit-change-database-owner-event-class.md)|Indica che le autorizzazioni necessarie per modificare il proprietario di un database sono state controllate.|  
|[Audit Database Management - classe di evento](audit-database-management-event-class.md)|Indica che un database è stato creato, modificato o eliminato.|  
|[Classe di evento Audit Database Mirroring Login](audit-database-mirroring-login-event-class.md)|Segnala i messaggi di controllo correlati alla sicurezza del trasporto del mirroring del database.|  
|[Audit Database Object Access - classe di evento](audit-database-object-access-event-class.md)|Indica che è stato effettuato l'accesso a un oggetto di database, ad esempio uno schema.|  
|[Audit Database Object GDR - classe di evento](audit-database-object-gdr-event-class.md)|Indica che si è verificato un evento GDR per un oggetto di database.|  
|[Audit Database Object Management - classe di evento](audit-database-object-management-event-class.md)|Indica che è stata eseguita un'istruzione CREATE, ALTER o DROP in un oggetto di database.|  
|[Audit Database Object Take Ownership - classe di evento](audit-database-object-take-ownership-event-class.md)|Indica che si è verificata una modifica di proprietario per oggetti nell'ambito del database.|  
|[Audit Database Operation - classe di evento](audit-database-operation-event-class.md)|Indica che si sono verificate varie operazioni, ad esempio i checkpoint o la sottoscrizione di notifica delle query.|  
|[Audit Database Principal Impersonation - classe di evento](audit-database-principal-impersonation-event-class.md)|Indica che all'interno dell'ambito del database si è verificata una rappresentazione.|  
|[Audit Database Principal Management - classe di evento](audit-database-principal-management-event-class.md)|Indica che sono state create, modificate o eliminate entità da un database.|  
|[Audit Database Scope GDR - classe di evento](audit-database-scope-gdr-event-class.md)|Indica che è stata eseguita un'istruzione GRANT, REVOKE o DENY per un'autorizzazione per l'istruzione da un utente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in.|  
|[Audit DBCC - classe di evento](audit-dbcc-event-class.md)|Indica che è stato eseguito un comando DBCC.|  
|[Classe di evento Audit Fulltext](audit-fulltext-event-class.md)|Indica che si è verificato un evento full-text.|  
|[Audit Login Change Password _- classe di evento](audit-login-change-password-event-class.md)|Indica che un utente ha modificato la password dell'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Audit Login Change Property - classe di evento](audit-login-change-property-event-class.md)|Indica che è stata usata **sp_defaultdb**, **sp_defaultlanguage**o ALTER LOGIN per modificare una proprietà di un account di accesso.|  
|[Audit Login - classe di evento](audit-login-event-class.md)|Indica che un utente è riuscito ad accedere correttamente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Audit Login Failed - classe di evento](audit-login-failed-event-class.md)|Indica che un utente ha tentato di accedere a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'operazione ha avuto esito negativo.|  
|[Audit Login GDR - classe di evento](audit-login-gdr-event-class.md)|Indica che un diritto di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows è stato aggiunto o rimosso.|  
|[Audit Logout - classe di evento](audit-logout-event-class.md)|Indica che un utente ha effettuato la disconnessione da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Audit Object Derived Permission - classe di evento](audit-object-derived-permission-event-class.md)|Indica che è stata eseguita un'istruzione CREATE, ALTER o DROP per un oggetto.|  
|[Audit Schema Object Access - classe di evento](audit-schema-object-access-event-class.md)|Indica che è stata utilizzata un'autorizzazione per gli oggetti, ad esempio SELECT.|  
|[Audit Schema Object GDR - classe di evento](audit-schema-object-gdr-event-class.md)|Indica che è stata eseguita un'istruzione GRANT, REVOKE o DENY per un'autorizzazione per un oggetto dello schema da parte di un utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Audit Schema Object Management - classe di evento](audit-schema-object-management-event-class.md)|Indica che un oggetto del server è stato creato, modificato o eliminato.|  
|[Audit Schema Object Take Ownership - classe di evento](audit-schema-object-take-ownership-event-class.md)|Indica che le autorizzazioni necessarie per modificare il proprietario di un oggetto dello schema sono state controllate.|  
|[Audit Server Alter Trace - classe di evento](audit-server-alter-trace-event-class.md)|Indica che l'autorizzazione ALTER TRACE è stata controllata.|  
|[Audit Server Object GDR - classe di evento](audit-server-object-gdr-event-class.md)|Indica che si è verificato un evento GDR per un oggetto dello schema.|  
|[Audit Server Object Management - classe di evento](audit-server-object-management-event-class.md)|Indica che si è verificato un evento CREATE, ALTER o DROP per un oggetto del server.|  
|[Audit Server Object Take Ownership - classe di evento](audit-server-object-take-ownership-event-class.md)|Indica che è stato modificato il proprietario di un oggetto del server.|  
|[Audit Server Operation - classe di evento](audit-server-operation-event-class.md)|Indica che nel server si sono verificate operazioni di controllo.|  
|[Audit Server Principal Impersonation - classe di evento](audit-server-principal-impersonation-event-class.md)|Indica che all'interno dell'ambito del server si è verificata una rappresentazione.|  
|[Audit Server Principal Management - classe di evento](audit-server-principal-management-event-class.md)|Indica che si è verificato un evento CREATE, ALTER o DROP per un'entità del server.|  
|[Audit Server Scope GDR - classe di evento](audit-server-scope-gdr-event-class.md)|Indica che si è verificato un evento GDR per le autorizzazioni del server.|  
|[Audit Server Starts and Stops - classe di evento](audit-server-starts-and-stops-event-class.md)|Indica che è stato modificato lo stato del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Audit Statement Permission - classe di evento](audit-statement-permission-event-class.md)|Indica che è stata utilizzata un'autorizzazione per le istruzioni.|  
  
## <a name="related-content"></a>Contenuto correlato  
 [Eventi estesi](../extended-events/extended-events.md)  
  
  
