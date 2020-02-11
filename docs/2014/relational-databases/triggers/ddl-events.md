---
title: Eventi DDL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c9c90dbb072ace600258edfb4ff13f99ecadf188
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196514"
---
# <a name="ddl-events"></a>Eventi DDL
  Nelle tabelle seguenti sono elencati gli eventi DDL che possono essere utilizzati per attivare un trigger DDL o generare una notifica degli eventi. Si noti che ogni evento corrisponde a una stored procedure o un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] , con la sintassi modificata per includere un carattere di sottolineatura (_) fra le parole chiave.  
  
> [!IMPORTANT]  
>  Le stored procedure di sistema che eseguono operazioni di tipo DDL possono inoltre generare trigger DDL e notifiche degli eventi. Testare i trigger DDL e le notifiche degli eventi per determinarne la risposta alle stored procedure di sistema eseguite. Ad esempio, l'istruzione CREATE TYPE e la stored procedure **sp_addtype** consentono entrambe di attivare un trigger DDL o una notifica degli eventi creata in un evento CREATE_TYPE.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>Istruzioni DDL di ambito server o database  
 È possibile creare le notifiche degli eventi o i trigger DDL in modo che vengano attivati in risposta agli eventi seguenti, qualora questi ultimi si verifichino nel database in cui la notifica degli eventi o il trigger è stato creato oppure in qualsiasi punto dell'istanza server.  
  
||||  
|-|-|-|  
|CREATE_APPLICATION_ROLE (si applica all'istruzione CREATE APPLICATION ROLE e **sp_addapprole**. Se viene creato un nuovo schema, questo evento attiva anche un evento CREATE_SCHEMA).|ALTER_APPLICATION_ROLE (si applica all'istruzione ALTER APPLICATION ROLE e **sp_approlepassword**).|DROP_APPLICATION_ROLE (si applica all'istruzione DROP APPLICATION ROLE e **sp_dropapprole**).|  
|CREATE_ASSEMBLY|ALTER_ASSEMBLY|DROP_ASSEMBLY|  
|CREATE_ASYMMETRIC_KEY|ALTER_ASYMMETRIC_KEY|DROP_ASYMMETRIC_KEY|  
|ALTER_AUTHORIZATION|ALTER_AUTHORIZATION_DATABASE (si applica all'istruzione ALTER AUTHORIZATION, quando è specificato ON DATABASE, e a **sp_changedbowner**).||  
|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|  
|CREATE_CERTIFICATE|ALTER_CERTIFICATE|DROP_CERTIFICATE|  
|CREATE_CONTRACT|DROP_CONTRACT||  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|GRANT_DATABASE|DENY_DATABASE|REVOKE_DATABASE|  
|CREATE_DATABASE_AUDIT_SPEFICIATION|ALTER_DATABASE_AUDIT_SPEFICIATION|DENY_DATABASE_AUDIT_SPEFICIATION|  
|CREATE_DATABASE_ENCRYPTION_KEY|ALTER_DATABASE_ENCRYPTION_KEY|DROP_DATABASE_ENCRYPTION_KEY|  
|CREATE_DEFAULT|DROP_DEFAULT||  
|BIND_DEFAULT (si applica a **sp_bindefault**).|UNBIND_DEFAULT (si applica a **sp_unbindefault**).||  
|CREATE_EVENT_NOTIFICATION|DROP_EVENT_NOTIFICATION||  
|CREATE_EXTENDED_PROPERTY (si applica a **sp_addextendedproperty**).|ALTER_EXTENDED_PROPERTY (si applica a **sp_updateextendedproperty**).|DROP_EXTENDED_PROPERTY (si applica a **sp_dropextendedproperty**).|  
|CREATE_FULLTEXT_CATALOG (si applica all'istruzione CREATE FULLTEXT CATALOG e **sp_fulltextcatalog** quando *create* è specificato).|ALTER_FULLTEXT_CATALOG (si applica all'istruzione ALTER FULLTEXT CATALOG, **sp_fulltextcatalog** quando è specificato *start_incremental*, *start_full*, *Stop*oppure *Rebuild* e **sp_fulltext_database** quando è specificato *enable* ).|DROP_FULLTEXT_CATALOG (si applica all'istruzione DROP FULLTEXT CATALOG e a **sp_fulltextcatalog** quando *drop* è specificato).|  
|CREATE_FULLTEXT_INDEX (si applica all'istruzione CREATE FULLTEXT INDEX e a **sp_fulltexttable** quando *create* è specificato).|ALTER_FULLTEXT_INDEX (si applica all'istruzione ALTER FULLTEXT INDEX, **sp_fulltextcatalog** quando è specificato *start_full*, *start_incremental*oppure *stop* , **sp_fulltext_column**e **sp_fulltext_table** quando è specificata qualunque azione diversa da *create* o *drop* ).|DROP_FULLTEXT_INDEX (si applica all'istruzione DROP FULLTEXT INDEX e a **sp_fulltexttable** quando *drop* è specificato).|  
|CREATE_FULLTEXT_STOPLIST|ALTER_FULLTEXT_STOPLIST|DROP_FULLTEXT_STOPLIST|  
|CREATE_FUNCTION|ALTER_FUNCTION|DROP_FUNCTION|  
|CREATE_INDEX|ALTER_INDEX (si applica all'istruzione ALTER INDEX e a **sp_indexoption**).|DROP_INDEX|  
|CREATE_MASTER_KEY|ALTER_MASTER_KEY|DROP_MASTER_KEY|  
|CREATE_MESSAGE_TYPE|ALTER_MESSAGE_TYPE|DROP_MESSAGE_TYPE|  
|CREATE_PARTITION_FUNCTION|ALTER_PARTITION_FUNCTION|DROP_PARTITION_FUNCTION|  
|CREATE_PARTITION_SCHEME|ALTER_PARTITION_SCHEME|DROP_PARTITION_SCHEME|  
|CREATE_PLAN_GUIDE (si applica a **sp_create_plan_guide**).|ALTER_PLAN_GUIDE (si applica a **sp_control_plan_guide** quando è specificato ENABLE, ENABLE ALL, DISABLE o DISABLE ALL).|DROP_PLAN_GUIDE (si applica a **sp_control_plan_guide** quando è specificato DROP o DROP ALL).|  
|CREATE_PROCEDURE|ALTER_PROCEDURE (si applica all'istruzione ALTER PROCEDURE e a **sp_procoption**).|DROP_PROCEDURE|  
|CREATE_QUEUE|ALTER_QUEUE|DROP_QUEUE|  
|CREATE_REMOTE_SERVICE_BINDING|ALTER_REMOTE_SERVICE_BINDING|DROP_REMOTE_SERVICE_BINDING|  
|CREATE_SPATIAL_INDEX|||  
|RENAME (si applica a **sp_rename**)|||  
|CREATE_ROLE (si applica all'istruzione CREATE ROLE, **sp_addrole**e **sp_addgroup**).|ALTER_ROLE|DROP_ROLE (si applica all'istruzione DROP ROLE, **sp_droprole**e **sp_dropgroup**).|  
|ADD_ROLE_MEMBER|DROP_ROLE_MEMBER||  
|CREATE_ROUTE|ALTER_ROUTE|DROP_ROUTE|  
|CREATE_RULE|DROP_RULE||  
|BIND_RULE (si applica a **sp_bindrule**).|UNBIND_RULE (si applica a **sp_unbindrule**).||  
|CREATE_SCHEMA (si applica all'istruzione CREATE SCHEMA, **sp_addrole**, **sp_adduser**, **sp_addgroup**e **sp_grantdbaccess**).|ALTER_SCHEMA (si applica all'istruzione ALTER SCHEMA e **sp_changeobjectowner**).|DROP_SCHEMA|  
|CREATE_SEARCH_PROPERTY_LIST|ALTER_SEARCH_PROPERTY_LIST|DROP_SEARCH_PROPERTY_LIST|  
|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|  
|CREATE_SERVER_ROLE|ALTER_SERVER_ROLE|DROP_SERVER_ROLE|  
|CREATE_SERVICE|ALTER_SERVICE|DROP_SERVICE|  
|ALTER_SERVICE_MASTER_KEY|BACKUP_SERVICE_MASTER_KEY|RESTORE_SERVICE_MASTER_KEY|  
|ADD_SIGNATURE (per operazioni di firma su oggetti con ambito non schema, cioè database, assembly, trigger)|DROP_SIGNATURE||  
|ADD_SIGNATURE_SCHEMA_OBJECT (per oggetti con ambito schema, cioè stored procedure, funzioni)|DROP_SIGNATURE_SCHEMA_OBJECT||  
|CREATE_SPATIAL_INDEX|ALTER_INDEX può essere utilizzato per gli indici spaziali.|DROP_INDEX può essere usato per gli indici spaziali.|  
|CREATE_STATISTICS|DROP_STATISTICS|UPDATE_STATISTICS|  
|CREATE_SYMMETRIC_KEY|ALTER_SYMMETRIC_KEY|DROP_SYMMETRIC_KEY|  
|CREATE_SYNONYM|DROP_SYNONYM||  
|CREATE_TABLE|ALTER_TABLE (si applica all'istruzione ALTER TABLE e **sp_tableoption**).|DROP_TABLE|  
|CREATE_TRIGGER|ALTER_TRIGGER (si applica all'istruzione ALTER TRIGGER e **sp_settriggerorder**).|DROP_TRIGGER|  
|CREATE_TYPE (si applica all'istruzione CREATE TYPE e **sp_addtype**).|DROP_TYPE (si applica all'istruzione DROP TYPE e **sp_droptype**).||  
|CREATE_USER (si applica all'istruzione CREATE USER, **sp_adduser**e **sp_grantdbaccess**).|ALTER_USER (si applica all'istruzione ALTER USER e **sp_change_user_login**).|DROP_USER (si applica all'istruzione DROP USER, **sp_dropuser**e **sp_revokedbaccess**).|  
|CREATE_VIEW|ALTER_VIEW|DROP_VIEW|  
|CREATE_XML_INDEX|ALTER_INDEX può essere utilizzato per gli indici XML.|DROP_INDEX può essere usato per gli indici XML.|  
|CREATE_XML_SCHEMA_COLLECTION|ALTER_XML_SCHEMA_COLLECTION|DROP_XML_SCHEMA_COLLECTION|  
  
## <a name="ddl-statements-that-have-server-scope"></a>Istruzioni DDL di ambito server  
 È possibile creare le notifiche degli eventi o i trigger DDL in modo che vengano attivati in risposta agli eventi seguenti, qualora questi ultimi si verifichino in qualsiasi punto dell'istanza del server.  
  
||||  
|-|-|-|  
|ALTER_AUTHORIZATION_SERVER|ALTER_SERVER_CONFIGURATION|ALTER_INSTANCE (si applica a **sp_configure** e **sp_addserver** quando è specificata un'istanza del server locale).|  
|CREATE_AVAILABILITY_GROUP|ALTER_AVAILABILITY_GROUP|DROP_AVAILABILITY_GROUP|  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|CREATE_CRYPTOGRAPHIC_PROVIDER|ALTER_CRYPTOGRAPHIC_PROVIDER|DROP_CRYPTOGRAPHIC_PROVIDER|  
|CREATE_DATABASE|ALTER_DATABASE (si applica all'istruzione ALTER DATABASE e a **sp_fulltext_database**).|DROP_DATABASE|  
|CREATE_ENDPOINT|ALTER_ENDPOINT|DROP_ENDPOINT|  
|CREATE_EVENT_SESSION|ALTER_EVENT_SESSION|DROP_EVENT_SESSION|  
|CREATE_EXTENDED_PROCEDURE (si applica a **sp_addextendedproc**).|DROP_EXTENDED_PROCEDURE (si applica a **sp_dropextendedproc**).||  
|CREATE_LINKED_SERVER (si applica a **sp_addlinkedserver**).|ALTER_LINKED_SERVER (si applica a **sp_serveroption**).|DROP_LINKED_SERVER (si applica a **sp_dropserver** quando è specificato un server collegato).|  
|CREATE_LINKED_SERVER_LOGIN (si applica a **sp_addlinkedsrvlogin**).|DROP_LINKED_SERVER_LOGIN (si applica a **sp_droplinkedsrvlogin**).||  
|CREATE_LOGIN (si applica all'istruzione CREATE LOGIN, **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin**e **sp_denylogin** quando vengono usati su un account di accesso che deve essere creato implicitamente).|ALTER_LOGIN (si applica all'istruzione ALTER LOGIN, **sp_defaultdb**, **sp_defaultlanguage**, **sp_password**e **sp_change_users_login** quando si specifica *Auto_Fix* ).|DROP_LOGIN (si applica all'istruzione DROP LOGIN, **sp_droplogin**, **sp_revokelogin**e **xp_revokelogin**).|  
|CREATE_MESSAGE (si applica a **sp_addmessage**).|ALTER_MESSAGE (si applica a **sp_altermessage**).|DROP_MESSAGE (si applica a **sp_dropmessage**).|  
|CREATE_REMOTE_SERVER (si applica a **sp_addserver**).|ALTER_REMOTE_SERVER (si applica a **sp_setnetname**).|DROP_REMOTE_SERVER (si applica a **sp_dropserver** quando è specificato un server remoto).|  
|CREATE_RESOURCE_POOL|ALTER_RESOURCE_POOL|DROP_RESOURCE_POOL|  
|GRANT_SERVER|DENY_SERVER|REVOKE_SERVER|  
|ADD_SERVER_ROLE_MEMBER|DROP_SERVER_ROLE_MEMBER||  
|CREATE_SERVER_AUDIT|ALTER_SERVER_AUDIT|DROP_SERVER_AUDIT|  
|CREATE_SERVER_AUDIT_SPECIFICATION|ALTER_SERVER_AUDIT_SPECIFICATION|DROP_SERVER_AUDIT_SPECIFICATION|  
|CREATE_WORKLOAD_GROUP|CREATE_WORKLOAD_GROUP|CREATE_WORKLOAD_GROUP|  
  
## <a name="see-also"></a>Vedere anche  
 [Trigger DDL](ddl-triggers.md)   
 [Notifiche degli eventi](../service-broker/event-notifications.md)   
 [Gruppi di eventi DDL](ddl-event-groups.md)  
  
  
