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
ms.openlocfilehash: 81b07c1eb33176533cedbf0d02a71a264419b11e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85052553"
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Categoria di eventi Security Audit (SQL Server Profiler)
  La categoria di eventi **Security Audit** include gli eventi relativi ai controlli di sicurezza.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Classe di evento Audit Add DB User](audit-add-db-user-event-class.md)|Indica che un account di accesso è stato aggiunto o rimosso dal database come utente di database.|  
|[Classe di evento Audit Add Login to Server Role](audit-add-login-to-server-role-event-class.md)|Indica che un account di accesso è stato aggiunto o rimosso da un ruolo predefinito del server.|  
|[Classe di evento Audit Add Member to DB Role](audit-add-member-to-db-role-event-class.md)|Indica che un account di accesso è stato aggiunto o rimosso da un ruolo.|  
|[Classe di evento Audit Add Role](audit-add-role-event-class.md)|Indica che un ruolo del database è stato aggiunto o rimosso da un database.|  
|[Classe di evento Audit Addlogin](audit-addlogin-event-class.md)|Indica che un account di accesso è stato aggiunto o rimosso.|  
|[Classe di evento Audit App Role Change Password](audit-app-role-change-password-event-class.md)|Indica che è stata modificata una password per un ruolo applicazione.|  
|[Classe di evento Audit Backup/Restore](audit-backup-and-restore-event-class.md)|Indica che è stata eseguita un'istruzione di backup o di ripristino.|  
|[Classe di evento Audit Broker Conversation](broker-conversation-event-class.md)|Segnala i messaggi di controllo correlati alla sicurezza del dialogo di Service Broker.|  
|[Classe di evento Audit Broker Login](audit-broker-login-event-class.md)|Segnala i messaggi di controllo correlati alla sicurezza del trasporto di Service Broker.|  
|[Classe di evento Audit Change Audit](audit-change-audit-event-class.md)|Indica che è stata apportata una modifica alla traccia di controllo.|  
|[Classe di evento Audit Change Database Owner](audit-change-database-owner-event-class.md)|Indica che le autorizzazioni necessarie per modificare il proprietario di un database sono state controllate.|  
|[Classe di evento Audit Database Management](audit-database-management-event-class.md)|Indica che un database è stato creato, modificato o eliminato.|  
|[Classe di evento Audit Database Mirroring Login](audit-database-mirroring-login-event-class.md)|Segnala i messaggi di controllo correlati alla sicurezza del trasporto del mirroring del database.|  
|[Classe di evento Audit Database Object Access](audit-database-object-access-event-class.md)|Indica che è stato effettuato l'accesso a un oggetto di database, ad esempio uno schema.|  
|[Classe di evento Audit Database Object GDR](audit-database-object-gdr-event-class.md)|Indica che si è verificato un evento GDR per un oggetto di database.|  
|[Classe di evento Audit Database Object Management](audit-database-object-management-event-class.md)|Indica che è stata eseguita un'istruzione CREATE, ALTER o DROP in un oggetto di database.|  
|[Classe di evento Audit Database Object Take Ownership](audit-database-object-take-ownership-event-class.md)|Indica che si è verificata una modifica di proprietario per oggetti nell'ambito del database.|  
|[Classe di evento Audit Database Operation](audit-database-operation-event-class.md)|Indica che si sono verificate varie operazioni, ad esempio i checkpoint o la sottoscrizione di notifica delle query.|  
|[Classe di evento Audit Database Principal Impersonation](audit-database-principal-impersonation-event-class.md)|Indica che all'interno dell'ambito del database si è verificata una rappresentazione.|  
|[Classe di evento Audit Database Principal Management](audit-database-principal-management-event-class.md)|Indica che sono state create, modificate o eliminate entità da un database.|  
|[Classe di evento Audit Database Scope GDR](audit-database-scope-gdr-event-class.md)|Indica che è stata eseguita un'istruzione GRANT, REVOKE o DENY per un'autorizzazione per le istruzioni da parte di un utente in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe di evento Audit DBCC](audit-dbcc-event-class.md)|Indica che è stato eseguito un comando DBCC.|  
|[Classe di evento Audit Fulltext](audit-fulltext-event-class.md)|Indica che si è verificato un evento full-text.|  
|[Classe di evento Audit Login Change Password](audit-login-change-password-event-class.md)|Indica che un utente ha modificato la password dell'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Classe di evento Audit Login Change Property](audit-login-change-property-event-class.md)|Indica che è stata usata **sp_defaultdb**, **sp_defaultlanguage**o ALTER LOGIN per modificare una proprietà di un account di accesso.|  
|[Classe di evento Audit Login](audit-login-event-class.md)|Indica che un utente è riuscito ad accedere correttamente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe di evento Audit Login Failed](audit-login-failed-event-class.md)|Indica che un utente ha tentato di accedere a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'operazione ha avuto esito negativo.|  
|[Classe di evento Audit Login GDR](audit-login-gdr-event-class.md)|Indica che un diritto di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows è stato aggiunto o rimosso.|  
|[Classe di evento Audit Logout](audit-logout-event-class.md)|Indica che un utente ha effettuato la disconnessione da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe di evento Audit Object Derived Permission](audit-object-derived-permission-event-class.md)|Indica che è stata eseguita un'istruzione CREATE, ALTER o DROP per un oggetto.|  
|[Classe di evento Audit Schema Object Access](audit-schema-object-access-event-class.md)|Indica che è stata utilizzata un'autorizzazione per gli oggetti, ad esempio SELECT.|  
|[Classe di evento Audit Schema Object GDR](audit-schema-object-gdr-event-class.md)|Indica che è stata eseguita un'istruzione GRANT, REVOKE o DENY per un'autorizzazione per un oggetto dello schema da parte di un utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe di evento Audit Schema Object Management](audit-schema-object-management-event-class.md)|Indica che un oggetto del server è stato creato, modificato o eliminato.|  
|[Classe di evento Audit Schema Object Take Ownership](audit-schema-object-take-ownership-event-class.md)|Indica che le autorizzazioni necessarie per modificare il proprietario di un oggetto dello schema sono state controllate.|  
|[Classe di evento Audit Server Alter Trace](audit-server-alter-trace-event-class.md)|Indica che l'autorizzazione ALTER TRACE è stata controllata.|  
|[Classe di evento Audit Server Object GDR](audit-server-object-gdr-event-class.md)|Indica che si è verificato un evento GDR per un oggetto dello schema.|  
|[Classe di evento Audit Server Object Management](audit-server-object-management-event-class.md)|Indica che si è verificato un evento CREATE, ALTER o DROP per un oggetto del server.|  
|[Classe di evento Audit Server Object Take Ownership](audit-server-object-take-ownership-event-class.md)|Indica che è stato modificato il proprietario di un oggetto del server.|  
|[Classe di evento Audit Server Operation](audit-server-operation-event-class.md)|Indica che nel server si sono verificate operazioni di controllo.|  
|[Classe di evento Audit Server Principal Impersonation](audit-server-principal-impersonation-event-class.md)|Indica che all'interno dell'ambito del server si è verificata una rappresentazione.|  
|[Classe di evento Audit Server Principal Management](audit-server-principal-management-event-class.md)|Indica che si è verificato un evento CREATE, ALTER o DROP per un'entità del server.|  
|[Classe di evento Audit Server Scope GDR](audit-server-scope-gdr-event-class.md)|Indica che si è verificato un evento GDR per le autorizzazioni del server.|  
|[Classe di evento Audit Server Starts and Stops](audit-server-starts-and-stops-event-class.md)|Indica che è stato modificato lo stato del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Classe di evento Audit Statement Permission](audit-statement-permission-event-class.md)|Indica che è stata utilizzata un'autorizzazione per le istruzioni.|  
  
## <a name="related-content"></a>Contenuto correlato  
 [Eventi estesi](../extended-events/extended-events.md)  
  
  
