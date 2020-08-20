---
description: Eventi DDL
title: Eventi DDL | Microsoft Docs
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 25cdef293ced7b58ea41f71f78a1046c6b5dd0ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463800"
---
# <a name="ddl-events"></a>Eventi DDL
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Nelle tabelle seguenti sono elencati gli eventi DDL che possono essere utilizzati per attivare un trigger DDL o generare una notifica degli eventi. Si noti che ogni evento corrisponde a una stored procedure o un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] , con la sintassi modificata per includere un carattere di sottolineatura (_) fra le parole chiave.  
  
> [!IMPORTANT]  
>  Le stored procedure di sistema che eseguono operazioni di tipo DDL possono inoltre generare trigger DDL e notifiche degli eventi. Testare i trigger DDL e le notifiche degli eventi per determinarne la risposta alle stored procedure di sistema eseguite. Ad esempio, l'istruzione CREATE TYPE e la stored procedure **sp_addtype** consentono entrambe di attivare un trigger DDL o una notifica degli eventi creata in un evento CREATE_TYPE.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>Istruzioni DDL di ambito server o database  
 È possibile creare le notifiche degli eventi o i trigger DDL in modo che vengano attivati in risposta agli eventi seguenti, qualora questi ultimi si verifichino nel database in cui la notifica degli eventi o il trigger è stato creato oppure in qualsiasi punto dell'istanza server.  
  
:::row:::
    :::column:::
        CREATE_APPLICATION_ROLE (si applica all'istruzione CREATE APPLICATION ROLE e **sp_addapprole**. Se viene creato un nuovo schema, questo evento attiva anche un evento CREATE_SCHEMA).
    :::column-end:::
    :::column:::
        ALTER_APPLICATION_ROLE (si applica all'istruzione ALTER APPLICATION ROLE e **sp_approlepassword**).
    :::column-end:::
    :::column:::
        DROP_APPLICATION_ROLE (si applica all'istruzione DROP APPLICATION ROLE e **sp_dropapprole**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASSEMBLY
    :::column-end:::
    :::column:::
        ALTER_ASSEMBLY
    :::column-end:::
    :::column:::
        DROP_ASSEMBLY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_ASYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION
    :::column-end:::
    :::column:::
        ALTER_AUTHORIZATION_DATABASE (si applica all'istruzione ALTER AUTHORIZATION, quando è specificato ON DATABASE, e a **sp_changedbowner**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CERTIFICATE
    :::column-end:::
    :::column:::
        ALTER_CERTIFICATE
    :::column-end:::
    :::column:::
        DROP_CERTIFICATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CONTRACT
    :::column-end:::
    :::column:::
        DROP_CONTRACT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_DATABASE
    :::column-end:::
    :::column:::
        DENY_DATABASE
    :::column-end:::
    :::column:::
        REVOKE_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        ALTER_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        DENY_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        ALTER_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        DROP_DATABASE_ENCRYPTION_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DEFAULT
    :::column-end:::
    :::column:::
        DROP_DEFAULT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_DEFAULT (si applica a **sp_bindefault**).
    :::column-end:::
    :::column:::
        UNBIND_DEFAULT (si applica a **sp_unbindefault**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
        DROP_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROPERTY (si applica a **sp_addextendedproperty**).
    :::column-end:::
    :::column:::
        ALTER_EXTENDED_PROPERTY (si applica a **sp_updateextendedproperty**).
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROPERTY (si applica a **sp_dropextendedproperty**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_CATALOG (si applica all'istruzione CREATE FULLTEXT CATALOG e **sp_fulltextcatalog** quando *create* è specificato).
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_CATALOG (si applica all'istruzione ALTER FULLTEXT CATALOG, **sp_fulltextcatalog** quando è specificato *start_incremental*, *start_full*, *Stop*oppure *Rebuild* e **sp_fulltext_database** quando è specificato *enable* ).
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_CATALOG (si applica all'istruzione DROP FULLTEXT CATALOG e a **sp_fulltextcatalog** quando *drop* è specificato).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_INDEX (si applica all'istruzione CREATE FULLTEXT INDEX e a **sp_fulltexttable** quando *create* è specificato).
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_INDEX (si applica all'istruzione ALTER FULLTEXT INDEX, **sp_fulltextcatalog** quando è specificato *start_full*, *start_incremental*oppure *stop* , **sp_fulltext_column**e **sp_fulltext_table** quando è specificata qualunque azione diversa da *create* o *drop* ).
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_INDEX (si applica all'istruzione DROP FULLTEXT INDEX e a **sp_fulltexttable** quando *drop* è specificato).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_STOPLIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_FUNCTION
    :::column-end:::
    :::column:::
        DROP_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX (si applica all'istruzione ALTER INDEX e a **sp_indexoption**).
    :::column-end:::
    :::column:::
        DROP_INDEX
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MASTER_KEY
    :::column-end:::
    :::column:::
        ALTER_MASTER_KEY
    :::column-end:::
    :::column:::
        DROP_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        ALTER_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        DROP_MESSAGE_TYPE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        DROP_PARTITION_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        ALTER_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        DROP_PARTITION_SCHEME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PLAN_GUIDE (si applica a **sp_create_plan_guide**).
    :::column-end:::
    :::column:::
        ALTER_PLAN_GUIDE (si applica a **sp_control_plan_guide** quando è specificato ENABLE, ENABLE ALL, DISABLE o DISABLE ALL).
    :::column-end:::
    :::column:::
        DROP_PLAN_GUIDE (si applica a **sp_control_plan_guide** quando è specificato DROP o DROP ALL).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PROCEDURE
    :::column-end:::
    :::column:::
        ALTER_PROCEDURE (si applica all'istruzione ALTER PROCEDURE e a **sp_procoption**).
    :::column-end:::
    :::column:::
        DROP_PROCEDURE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_QUEUE
    :::column-end:::
    :::column:::
        ALTER_QUEUE
    :::column-end:::
    :::column:::
        DROP_QUEUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVICE_BINDING
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        RENAME (si applica a **sp_rename**)
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROLE (si applica all'istruzione CREATE ROLE, **sp_addrole**e **sp_addgroup**).
    :::column-end:::
    :::column:::
        ALTER_ROLE
    :::column-end:::
    :::column:::
        DROP_ROLE (si applica all'istruzione DROP ROLE, **sp_droprole**e **sp_dropgroup**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROUTE
    :::column-end:::
    :::column:::
        ALTER_ROUTE
    :::column-end:::
    :::column:::
        DROP_ROUTE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RULE
    :::column-end:::
    :::column:::
        DROP_RULE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_RULE (si applica a **sp_bindrule**).
    :::column-end:::
    :::column:::
        UNBIND_RULE (si applica a **sp_unbindrule**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SCHEMA (si applica all'istruzione CREATE SCHEMA, **sp_addrole**, **sp_adduser**, **sp_addgroup**e **sp_grantdbaccess**).
    :::column-end:::
    :::column:::
        ALTER_SCHEMA (si applica all'istruzione ALTER SCHEMA e **sp_changeobjectowner**).
    :::column-end:::
    :::column:::
        DROP_SCHEMA
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        ALTER_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        DROP_SEARCH_PROPERTY_LIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_ROLE
    :::column-end:::
    :::column:::
        ALTER_SERVER_ROLE
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVICE
    :::column-end:::
    :::column:::
        ALTER_SERVICE
    :::column-end:::
    :::column:::
        DROP_SERVICE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        BACKUP_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        RESTORE_SERVICE_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE (per operazioni di firma su oggetti con ambito non schema, cioè database, assembly, trigger)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE_SCHEMA_OBJECT (per oggetti con ambito schema, cioè stored procedure, funzioni)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE_SCHEMA_OBJECT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX può essere utilizzato per gli indici spaziali.
    :::column-end:::
    :::column:::
        DROP_INDEX può essere usato per gli indici spaziali.
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_STATISTICS
    :::column-end:::
    :::column:::
        DROP_STATISTICS
    :::column-end:::
    :::column:::
        UPDATE_STATISTICS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_SYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYNONYM
    :::column-end:::
    :::column:::
        DROP_SYNONYM
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TABLE
    :::column-end:::
    :::column:::
        ALTER_TABLE (si applica all'istruzione ALTER TABLE e **sp_tableoption**).
    :::column-end:::
    :::column:::
        DROP_TABLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TRIGGER
    :::column-end:::
    :::column:::
        ALTER_TRIGGER (si applica all'istruzione ALTER TRIGGER e **sp_settriggerorder**).
    :::column-end:::
    :::column:::
        DROP_TRIGGER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TYPE (si applica all'istruzione CREATE TYPE e **sp_addtype**).
    :::column-end:::
    :::column:::
        DROP_TYPE (si applica all'istruzione DROP TYPE e **sp_droptype**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_USER (si applica all'istruzione CREATE USER, **sp_adduser**e **sp_grantdbaccess**).
    :::column-end:::
    :::column:::
        ALTER_USER (si applica all'istruzione ALTER USER e **sp_change_user_login**).
    :::column-end:::
    :::column:::
        DROP_USER (si applica all'istruzione DROP USER, **sp_dropuser**e **sp_revokedbaccess**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_VIEW
    :::column-end:::
    :::column:::
        ALTER_VIEW
    :::column-end:::
    :::column:::
        DROP_VIEW
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX può essere utilizzato per gli indici XML.
    :::column-end:::
    :::column:::
        DROP_INDEX può essere usato per gli indici XML.
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        ALTER_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        DROP_XML_SCHEMA_COLLECTION
    :::column-end:::
:::row-end:::
 
## <a name="ddl-statements-that-have-server-scope"></a>Istruzioni DDL di ambito server  
 È possibile creare le notifiche degli eventi o i trigger DDL in modo che vengano attivati in risposta agli eventi seguenti, qualora questi ultimi si verifichino in qualsiasi punto dell'istanza del server.  
  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION_SERVER
    :::column-end:::
    :::column:::
        ALTER_SERVER_CONFIGURATION
    :::column-end:::
    :::column:::
        ALTER_INSTANCE (si applica a **sp_configure** e **sp_addserver** quando è specificata un'istanza del server locale).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        ALTER_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        DROP_AVAILABILITY_GROUP
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        ALTER_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        DROP_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE
    :::column-end:::
    :::column:::
        ALTER_DATABASE (si applica all'istruzione ALTER DATABASE e a **sp_fulltext_database**).
    :::column-end:::
    :::column:::
        DROP_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ENDPOINT
    :::column-end:::
    :::column:::
        ALTER_ENDPOINT
    :::column-end:::
    :::column:::
        DROP_ENDPOINT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_SESSION
    :::column-end:::
    :::column:::
        ALTER_EVENT_SESSION
    :::column-end:::
    :::column:::
        DROP_EVENT_SESSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROCEDURE (si applica a **sp_addextendedproc**).
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROCEDURE (si applica a **sp_dropextendedproc**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER (si applica a **sp_addlinkedserver**).
    :::column-end:::
    :::column:::
        ALTER_LINKED_SERVER (si applica a **sp_serveroption**).
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER (si applica a **sp_dropserver** quando è specificato un server collegato).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER_LOGIN (si applica a **sp_addlinkedsrvlogin**).
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER_LOGIN (si applica a **sp_droplinkedsrvlogin**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LOGIN (si applica all'istruzione CREATE LOGIN, **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin**e **sp_denylogin** quando vengono usati su un account di accesso che deve essere creato implicitamente).
    :::column-end:::
    :::column:::
        ALTER_LOGIN (si applica all'istruzione ALTER LOGIN, **sp_defaultdb**, **sp_defaultlanguage**, **sp_password**e **sp_change_users_login** quando si specifica *Auto_Fix* ).
    :::column-end:::
    :::column:::
        DROP_LOGIN (si applica all'istruzione DROP LOGIN, **sp_droplogin**, **sp_revokelogin**e **xp_revokelogin**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE (si applica a **sp_addmessage**).
    :::column-end:::
    :::column:::
        ALTER_MESSAGE (si applica a **sp_altermessage**).
    :::column-end:::
    :::column:::
        DROP_MESSAGE (si applica a **sp_dropmessage**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVER (si applica a **sp_addserver**).
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVER (si applica a **sp_setnetname**).
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVER (si applica a **sp_dropserver** quando è specificato un server remoto).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RESOURCE_POOL
    :::column-end:::
    :::column:::
        ALTER_RESOURCE_POOL
    :::column-end:::
    :::column:::
        DROP_RESOURCE_POOL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_SERVER
    :::column-end:::
    :::column:::
        DENY_SERVER
    :::column-end:::
    :::column:::
        REVOKE_SERVER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        ALTER_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        DROP_WORKLOAD_GROUP
    :::column-end:::
:::row-end:::
 
## <a name="see-also"></a>Vedere anche  
 [Trigger DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Notifiche degli eventi](../../relational-databases/service-broker/event-notifications.md)   
 [Gruppi di eventi DDL](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
