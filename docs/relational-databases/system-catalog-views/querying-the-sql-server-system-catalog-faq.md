---
title: L'esecuzione di query nel catalogo di sistema SQL Server domande frequenti | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], examples
- metadata [SQL Server], frequently asked questions
- metadata [SQL Server], example queries
- system catalogs [SQL Server], example queries
- catalog views [SQL Server], frequently asked questions
ms.assetid: ca202580-c37e-4ccd-9275-77ce79481f64
author: stevestein
ms.author: sstein
ms.openlocfilehash: c16bc1e0c8d8d6b5a62e2823aa011b58520b1d00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018360"
---
# <a name="querying-the-sql-server-system-catalog-faq"></a>Domande frequenti sull'esecuzione di query sul catalogo di sistema di SQL Server
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In questo argomento è incluso un elenco di domande frequenti. Le risposte a queste domande sono query basate sulle viste del catalogo.  
  
##  <a name="_TOP"></a> Domande frequenti  
 Nelle sezioni seguenti sono elencate le domande frequenti per categoria.  
  
### <a name="data-types"></a>Tipi di dati  
  
-   [Ricerca per categorie di tipi di dati delle colonne di una tabella specificata?](#_FAQ7)  
  
-   [Ricerca per categorie di tipi di dati LOB di una tabella specificata?](#_FAQ14)  
  
-   [Come trovo le colonne che dipendono da un tipo di dati specificato?](#_FAQ22)  
  
-   [Come trovo le colonne calcolate che dipendono da un tipo definito dall'utente CLR specificato o un tipo di dati alias?](#_FAQ23)  
  
-   [Come è possibile trovare i parametri che dipendono da un tipo definito dall'utente CLR specificato o un tipo alias?](#_FAQ24)  
  
-   [Come è possibile trovare i vincoli CHECK che dipendono da un tipo definito dall'utente CLR specificato?](#_FAQ25)  
  
-   [Come individuare le viste, funzioni Transact-SQL e le procedure di Transact-SQL archiviate che dipendono da un tipo definito dall'utente CLR specificato o un tipo alias?](#_FAQ26)  
  
### <a name="tables-indexes-views-and-constraints"></a>Tabelle, indici, viste e vincoli  
  
-   [Come individuare tutte le tabelle definite dall'utente in un database specificato?](#_FAQ31)  
  
-   [Come è trovare tutte le tabelle che non dispongono di un indice cluster in un database specificato?](#_FAQ1)  
  
-   [Come è trovare tutte le tabelle che non dispongono di un indice?](#_FAQ4)  
  
-   [Come è trovare tutte le tabelle che non è una chiave primaria?](#_FAQ3)  
  
-   [Come è trovare tutte le tabelle che dispongono di una colonna identity?](#_FAQ5)  
  
-   [Come individuare tutte le tabelle e indici partizionati?](#_FAQ32)  
  
-   [Come trovare tutte le visualizzazioni in un database?](#_FAQ13)  
  
-   [Come individuare la definizione di una vista?](#_FAQ35)  
  
-   [Come è possibile trovare tutte le entità che sono state modificate negli ultimi N giorni?](#_FAQ6)  
  
-   [Come trovo le colonne di una chiave primaria per una tabella specificata?](#_FAQ16)  
  
-   [Come trovo le colonne di una chiave esterna per una tabella specificata?](#_FAQ17)  
  
-   [Come è possibile determinare se una colonna viene utilizzata in un'espressione di colonna calcolata?](#_FAQ20)  
  
-   [Come individuare tutte le colonne utilizzate in un'espressione di colonna calcolata?](#_FAQ21)  
  
-   [Come individuare tutti i vincoli per una tabella specificata?](#_FAQ27)  
  
-   [Come individuare tutti gli indici per una tabella specificata?](#_FAQ28)  
  
-   [Come trovare tutte le tabelle con un nome di colonna specificato?](#_FAQ30)  
  
-   [Come trovare tutte le statistiche su un oggetto specificato?](#_FAQ33)  
  
-   [Come individuare tutte le statistiche e le colonne delle statistiche su un oggetto specificato?](#_FAQ34)  
  
### <a name="modules-stored-procedures-user-defined-functions-and-triggers"></a>Moduli (stored procedure, funzioni definite dall'utente e trigger)  
  
-   [Come trovare tutte le stored procedure in un database?](#_FAQ9)  
  
-   [Come individuare tutte le funzioni definite dall'utente in un database?](#_FAQ12)  
  
-   [Come trovare i parametri per una stored procedure o una funzione?](#_FAQ10)  
  
-   [Come trovare le dipendenze in una funzione specificata?](#_FAQ8)  
  
-   [Come è possibile visualizzare la definizione di un modulo?](#_FAQ15)  
  
-   [Come è possibile visualizzare la definizione di un trigger a livello di server?](#_FAQ19)  
  
### <a name="schemas-users-roles-and-permissions"></a>Schemi, utenti, ruoli e autorizzazioni  
  
-   [Come trovare tutti i proprietari delle entità contenute in un determinato schema?](#_FAQ2)  
  
-   [Come trovare le autorizzazioni concesse o negate per un'entità specificata?](#_FAQ18)  
  
## <a name="answers"></a>Risposte  
  
###  <a name="_FAQ1"></a> Come è trovare tutte le tabelle che non dispongono di un indice cluster in un database specificato?  
 Prima di eseguire le query seguenti, sostituire `<database_name>` con un nome di database valido.  
  
```  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name, t.name AS table_name  
FROM sys.tables AS t  
WHERE NOT EXISTS   
   (  
     SELECT * FROM sys.indexes AS i  
     WHERE i.object_id = t.object_id  
     AND i.type = 1  -- or type_desc = 'CLUSTERED'  
   )  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 In alternativa, è possibile utilizzare la funzione `OBJECTPROPERTY`, come illustrato nell'esempio seguente.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name, name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasClustIndex') = 0  
ORDER BY schema_id, name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ2"></a> Come trovare tutti i proprietari delle entità contenute in un determinato schema?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT 'OBJECT' AS entity_type  
    ,USER_NAME(OBJECTPROPERTY(object_id, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.objects WHERE SCHEMA_NAME(schema_id) = '<schema_name>'  
UNION   
SELECT 'TYPE' AS entity_type  
    ,USER_NAME(TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.types WHERE SCHEMA_NAME(schema_id) = '<schema_name>'   
UNION  
SELECT 'XML SCHEMA COLLECTION' AS entity_type   
    ,COALESCE(USER_NAME(xsc.principal_id),USER_NAME(s.principal_id)) AS owner_name  
    ,xsc.name   
FROM sys.xml_schema_collections AS xsc JOIN sys.schemas AS s  
    ON s.schema_id = xsc.schema_id  
WHERE s.name = '<schema_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ3"></a> Come è trovare tutte le tabelle che non è una chiave primaria?  
 Prima di eseguire le query seguenti, sostituire `<database_name>` con un nome di database valido.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name  
    ,t.name AS table_name  
FROM sys.tables t   
WHERE object_id NOT IN   
   (  
    SELECT parent_object_id   
    FROM sys.key_constraints   
    WHERE type_desc = 'PRIMARY_KEY_CONSTRAINT' -- or type = 'PK'  
    );  
GO  
  
```  
  
 In alternativa, è possibile eseguire la query seguente.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ4"></a> Come è trovare tutte le tabelle che non dispongono di un indice?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome di database valido.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'IsIndexed') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ5"></a> Come è trovare tutte le tabelle che dispongono di una colonna identity?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome di database valido.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    , t.name AS table_name  
    , c.name AS column_name  
FROM sys.tables AS t  
JOIN sys.identity_columns c ON t.object_id = c.object_id  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 In alternativa, è possibile eseguire la query seguente.  
  
> [!NOTE]  
>  Questa query non restituisce il nome delle colonne.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasIdentity') = 1  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ7"></a> Ricerca per categorie di tipi di dati delle colonne di una tabella specificata?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.table_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT c.name AS column_name  
    ,c.column_id  
    ,SCHEMA_NAME(t.schema_id) AS type_schema  
    ,t.name AS type_name  
    ,t.is_user_defined  
    ,t.is_assembly_type  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
FROM sys.columns AS c   
JOIN sys.types AS t ON c.user_type_id=t.user_type_id  
WHERE c.object_id = OBJECT_ID('<schema_name.table_name>')  
ORDER BY c.column_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ8"></a> Come trovare le dipendenze in una funzione specificata?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.function_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS referencing_object_name  
    ,COALESCE(COL_NAME(object_id, column_id), '(n/a)') AS referencing_column_name  
    ,*  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.function_name>')  
ORDER BY OBJECT_NAME(object_id), COL_NAME(object_id, column_id);  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ9"></a> Come trovare tutte le stored procedure in un database?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido.  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS procedure_name   
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
FROM sys.procedures;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ10"></a> Come trovare i parametri per una stored procedure o una funzione?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.object_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,o.name AS object_name  
    ,o.type_desc  
    ,p.parameter_id  
    ,p.name AS parameter_name  
    ,TYPE_NAME(p.user_type_id) AS parameter_type  
    ,p.max_length  
    ,p.precision  
    ,p.scale  
    ,p.is_output  
FROM sys.objects AS o  
INNER JOIN sys.parameters AS p ON o.object_id = p.object_id  
WHERE o.object_id = OBJECT_ID('<schema_name.object_name>')  
ORDER BY schema_name, object_name, p.parameter_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ12"></a> Come individuare tutte le funzioni definite dall'utente in un database?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome di database valido.  
  
```  
USE <database_name>;  
GO  
SELECT name AS function_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE type_desc LIKE '%FUNCTION%';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ13"></a> Come trovare tutte le visualizzazioni in un database?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome di database valido.  
  
```  
USE <database_name>;  
GO  
SELECT name AS view_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,OBJECTPROPERTYEX(object_id,'IsIndexed') AS IsIndexed  
  ,OBJECTPROPERTYEX(object_id,'IsIndexable') AS IsIndexable  
  ,create_date  
  ,modify_date  
FROM sys.views;  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ6"></a> Come è possibile trovare tutte le entità che sono state modificate negli ultimi N giorni?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<n_days>` con valori validi.  
  
```  
USE <database_name>;  
GO  
SELECT name AS object_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE modify_date > GETDATE() - <n_days>  
ORDER BY modify_date;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ14"></a> Ricerca per categorie di tipi di dati LOB di una tabella specificata?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.table_name>` con nomi validi.  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS column_name   
    ,column_id   
    ,TYPE_NAME(user_type_id) AS type_name  
    ,max_length  
    ,CASE   
       WHEN max_length = -1 AND TYPE_NAME(user_type_id) <> 'xml'  
            THEN 1  
            ELSE 0  
     END AS [(max)]  
FROM sys.columns  
WHERE object_id=OBJECT_ID('<schema_name.table_name>')   
    AND ( TYPE_NAME(user_type_id) IN ('xml','text', 'ntext','image')  
         OR (TYPE_NAME(user_type_id) IN ('varchar','nvarchar','varbinary')  
         AND max_length = -1)  
        );  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ15"></a> Come è possibile visualizzare la definizione di un modulo?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.object_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 In alternativa, è possibile utilizzare la funzione `OBJECT_DEFINITION`, come illustrato nell'esempio seguente.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ19"></a> Come è possibile visualizzare la definizione di un trigger a livello di server?  
  
```  
SELECT definition  
FROM sys.server_sql_modules;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ16"></a> Come trovo le colonne di una chiave primaria per una tabella specificata?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.table_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,ic.index_column_id  
    ,key_ordinal  
    ,c.name AS column_name  
    ,TYPE_NAME(c.user_type_id)AS column_type   
    ,is_identity  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
INNER JOIN sys.columns AS c   
    ON ic.object_id = c.object_id AND c.column_id = ic.column_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 In alternativa, è possibile utilizzare la funzione `COL_NAME`, come illustrato nell'esempio seguente.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,key_ordinal  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ17"></a> Come trovo le colonne di una chiave esterna per una tabella specificata?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.table_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT   
    f.name AS foreign_key_name  
   ,OBJECT_NAME(f.parent_object_id) AS table_name  
   ,COL_NAME(fc.parent_object_id, fc.parent_column_id) AS constraint_column_name  
   ,OBJECT_NAME (f.referenced_object_id) AS referenced_object  
   ,COL_NAME(fc.referenced_object_id, fc.referenced_column_id) AS referenced_column_name  
   ,is_disabled  
   ,delete_referential_action_desc  
   ,update_referential_action_desc  
FROM sys.foreign_keys AS f  
INNER JOIN sys.foreign_key_columns AS fc   
   ON f.object_id = fc.constraint_object_id   
WHERE f.parent_object_id = OBJECT_ID('<schema_name.table_name>');  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ18"></a> Come trovare le autorizzazioni concesse o negate per un'entità specificata?  
 Nell'esempio seguente viene creata una funzione per restituire il nome dell'entità per la quale vengono verificate le autorizzazioni. La funzione viene richiamata nelle query seguenti. È necessario creare la funzione in ogni database nel quale si desidera verificare le autorizzazioni.  
  
```  
-- Create a function to return the name of the entity on which the permissions are checked.  
IF OBJECT_ID (N'dbo.entity_instance_name', N'FN') IS NOT NULL  
    DROP FUNCTION dbo.entity_instance_name;  
GO  
CREATE FUNCTION dbo.entity_instance_name(@class_desc nvarchar(60), @major_id int)   
RETURNS sysname AS  
BEGIN  
    DECLARE @the_entity_name sysname  
    SELECT @the_entity_name = CASE  
        WHEN @class_desc = 'DATABASE' THEN DB_NAME()  
        WHEN @class_desc = 'SCHEMA' THEN SCHEMA_NAME(@major_id)  
        WHEN @class_desc = 'OBJECT_OR_COLUMN' THEN OBJECT_NAME(@major_id)  
        WHEN @class_desc = 'DATABASE_PRINCIPAL' THEN USER_NAME(@major_id)  
        WHEN @class_desc = 'ASSEMBLY' THEN   
            (SELECT name FROM sys.assemblies WHERE assembly_id=@major_id)  
        WHEN @class_desc = 'TYPE' THEN TYPE_NAME(@major_id)  
        WHEN @class_desc = 'XML_SCHEMA_COLLECTION' THEN   
            (SELECT name FROM sys.xml_schema_collections  
              WHERE xml_collection_id=@major_id)  
        WHEN @class_desc = 'MESSAGE_TYPE' THEN   
            (SELECT name FROM sys.service_message_types WHERE message_type_id=@major_id)  
        WHEN @class_desc = 'SERVICE_CONTRACT' THEN   
           (SELECT name FROM sys.service_contracts  
              WHERE service_contract_id=@major_id)  
        WHEN @class_desc = 'SERVICE' THEN  
          (SELECT name FROM sys.services WHERE service_id=@major_id)  
        WHEN @class_desc = 'REMOTE_SERVICE_BINDING' THEN  
          (SELECT name FROM sys.remote_service_bindings  
             WHERE remote_service_binding_id=@major_id)  
        WHEN @class_desc = 'ROUTE' THEN  
          (SELECT name FROM sys.routes WHERE route_id=@major_id)  
        WHEN @class_desc = 'FULLTEXT_CATALOG' THEN  
          (SELECT name FROM sys.fulltext_catalogs WHERE fulltext_catalog_id=@major_id)  
        WHEN @class_desc = 'SYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.symmetric_keys WHERE symmetric_key_id=@major_id)  
        WHEN @class_desc = 'CERTIFICATE' THEN  
          (SELECT name FROM sys.certificates WHERE certificate_id=@major_id)  
        WHEN @class_desc = 'ASYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.asymmetric_keys WHERE asymmetric_key_id=@major_id)  
        WHEN @class_desc = 'SERVER' THEN   
             (SELECT name FROM sys.servers WHERE server_id=@major_id)  
        WHEN @class_desc = 'SERVER_PRINCIPAL' THEN SUSER_NAME(@major_id)  
        WHEN @class_desc = 'ENDPOINT' THEN   
             (SELECT name FROM sys.endpoints WHERE endpoint_id=@major_id)        
        ELSE '?'  
    END  
    RETURN @the_entity_name  
END;  
GO  
-- Return server-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc, major_id) AS entity_name   
    ,minor_id  
    ,SUSER_NAME(grantee_principal_id) AS grantee  
    ,SUSER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc   
FROM sys.server_permissions   
WHERE grantee_principal_id = SUSER_ID('public');  
GO  
-- Return database-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc , major_id) AS entity_name   
    ,minor_id  
    ,USER_NAME(grantee_principal_id) AS grantee  
    ,USER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc     
FROM  sys.database_permissions   
WHERE grantee_principal_id = DATABASE_PRINCIPAL_ID('public');  
GO  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ20"></a> Come è possibile determinare se una colonna viene utilizzata in un'espressione di colonna calcolata?  
 Prima di eseguire la query seguente, sostituire `<database_name>`, `<schema_name.table_name>`, e `<column_name`> con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS computed_column   
    ,class_desc  
    ,is_selected  
    ,is_updated  
    ,is_select_all  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.table_name>')  
    AND referenced_minor_id = COLUMNPROPERTY(referenced_major_id, '<column_name>', 'ColumnId')  
    AND class = 1;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ21"></a> Come individuare tutte le colonne utilizzate in un'espressione di colonna calcolata?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(d.referenced_major_id) AS object_name  
    ,COL_NAME(d.referenced_major_id, d.referenced_minor_id) AS column_name  
    ,OBJECT_NAME(referenced_major_id) AS dependent_object_name   
    ,COL_NAME(d.object_id, d.column_id) AS dependent_computed_column  
    ,cc.definition AS computed_column_definition  
FROM sys.sql_dependencies AS d  
JOIN sys.computed_columns AS cc   
    ON cc.object_id = d.object_id AND cc.column_id = d.column_id AND d.object_id=d.referenced_major_id       
WHERE d.class = 1  
ORDER BY object_name, column_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ22"></a> Come trovo le colonne che dipendono da un tipo definito dall'utente CLR specificato o un tipo alias?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido e `<schema_name.data_type_name>` con valido con Specificazione dello schema definiti dall'utente tipo CLR o nome del tipo alias con Specificazione dello schema. La query seguente richiede l'appartenenza al gruppo il **db_owner** ruolo o le autorizzazioni per visualizzare tutte le colonne dipendenti e alla colonna calcolata i metadati nel database.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,c.name AS column_name   
    ,SCHEMA_NAME(t.schema_id) AS schema_name  
    ,TYPE_NAME(c.user_type_id) AS user_type_name  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
    ,c.is_nullable  
    ,c.is_computed  
FROM sys.columns AS c  
INNER JOIN sys.types AS t ON c.user_type_id = t.user_type_id  
WHERE c.user_type_id = TYPE_ID('<schema_name.data_type_name>');   
GO  
  
```  
  
 La query seguente restituisce una vista ridotta e limitata delle colonne dipende da un tipo CLR definito dall'utente o un alias, ma il set di risultati è visibile per la **pubblica** ruolo. È possibile utilizzare questa query se si sono concesse le autorizzazioni REFERENCE per il tipo definito dall'utente ad altri utenti e non si dispone dell'autorizzazione per visualizzare i metadati degli oggetti che utilizzano il tipo creati da altri utenti.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,COL_NAME(object_id, column_id) AS column_name  
    ,TYPE_NAME(user_type_id) AS user_type  
FROM sys.column_type_usages  
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ23"></a> Come trovo le colonne calcolate che dipendono da un tipo definito dall'utente CLR specificato o un tipo alias?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido e `<schema_name.data_type_name>` con un tipo CLR definito dall'utente valido e qualificato a livello di schema o un nome di tipo alias.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS column_name  
FROM sys.sql_dependencies  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(object_id, 'IsTable') = 1;   -- exclude non-table dependencies  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ24"></a> Come è possibile trovare i parametri che dipendono da un tipo definito dall'utente CLR specificato o un tipo alias?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido e `<schema_name.data_type_name>` con un tipo CLR definito dall'utente valido e qualificato a livello di schema o un nome di tipo alias. La query seguente richiede l'appartenenza al gruppo il **db_owner** ruolo o le autorizzazioni per visualizzare tutte le colonne dipendenti e alla colonna calcolata i metadati nel database.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,NULL AS procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
UNION   
SELECT OBJECT_NAME(object_id) AS object_name  
    ,procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.numbered_procedure_parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY object_name, procedure_number, param_num;  
GO  
  
```  
  
 La query seguente restituisce una vista ridotta e limitata dei parametri che dipendono da un tipo CLR definito dall'utente o un alias, ma il set di risultati è visibile per la **pubblica** ruolo. È possibile utilizzare questa query se si sono concesse le autorizzazioni REFERENCE per il tipo definito dall'utente ad altri utenti e non si dispone dell'autorizzazione per visualizzare i metadati degli oggetti che utilizzano il tipo creati da altri utenti.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,parameter_id  
    ,TYPE_NAME(user_type_id) AS type_name  
FROM sys.parameter_type_usages   
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ25"></a> Come è possibile trovare i vincoli CHECK che dipendono da un tipo definito dall'utente CLR specificato?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido e `<schema_name.data_type_name>` con un nome di tipo definito dall'utente CLR valido, con Specificazione dello schema.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(o.parent_object_id) AS table_name  
    ,OBJECT_NAME(o.object_id) AS constraint_name  
FROM sys.sql_dependencies AS d  
JOIN sys.objects AS o ON o.object_id = d.object_id  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(o.object_id, 'IsCheckCnst') = 1; -- exclude non-CHECK dependencies  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ26"></a> Come individuare le viste, funzioni Transact-SQL e le procedure di Transact-SQL archiviate che dipendono da un tipo definito dall'utente CLR specificato o un tipo alias?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido e `<schema_name.data_type_name>` con un tipo CLR definito dall'utente valido e qualificato a livello di schema o un nome di tipo alias.  
  
 I parametri definiti in una funzione o una procedura vengono associati a schema in modo implicito. Di conseguenza, i parametri che dipendono da un tipo CLR definito dall'utente o un tipo alias possono essere visualizzati utilizzando il [Sys. sql_dependencies](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md) vista del catalogo. Le procedure e i trigger non sono associati a schema. Questo significa che le dipendenze tra qualsiasi espressione definita nel corpo della procedura o del trigger e un tipo CLR definito dall'utente o un tipo alias non vengono mantenute. Viste e funzioni definite dall'utente che dispongono di espressioni che dipendono da un tipo CLR definito dall'utente associate a schema o tipo alias vengono mantenute nel **Sys. sql_dependencies** vista del catalogo. Le dipendenze tra i tipi e le funzioni o le procedure CLR non vengono mantenute.  
  
 La query seguente restituisce tutte le dipendenze associate a schema nelle viste, nelle funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e nelle stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] per un tipo CLR definito dall'utente o un tipo alias specificato.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS dependent_object_schema  
  ,OBJECT_NAME(o.object_id) AS dependent_object_name  
  ,o.type_desc AS dependent_object_type  
  ,d.class_desc AS kind_of_dependency  
  ,TYPE_NAME (d.referenced_major_id) AS type_name  
FROM sys.sql_dependencies AS d   
JOIN sys.objects AS o  
  ON d.object_id = o.object_id  
  AND o.type IN ('FN','IF','TF', 'V', 'P')  
WHERE d.class = 2 -- dependencies on types  
  AND d.referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY dependent_object_schema, dependent_object_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ27"></a> Come individuare tutti i vincoli per una tabella specificata?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.table_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) as constraint_name  
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,OBJECT_NAME(parent_object_id) AS table_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
    ,is_ms_shipped  
    ,is_published  
    ,is_schema_published  
FROM sys.objects  
WHERE type_desc LIKE '%CONSTRAINT'   
    AND parent_object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ28"></a> Come individuare tutti gli indici per una tabella specificata?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.table_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ30"></a> Come è possibile trovare tutti gli oggetti che hanno un nome di colonna specificato?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<column_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id)  
FROM sys.columns  
WHERE name = '<column_name>';  
GO  
  
```  
  
 Oppure  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name   
    ,o.name AS object_name  
    ,type_desc  
FROM sys.objects AS o  
INNER JOIN sys.columns AS c ON o.object_id = c.object_id  
WHERE c.name = '<column_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ31"></a> Come individuare tutte le tabelle definite dall'utente in un database specificato?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido.  
  
```  
USE <database_name>;  
GO  
SELECT *   
FROM sys.tables;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ32"></a> Come individuare tutte le tabelle e indici partizionati?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(p.object_id) AS table_name  
    ,i.name AS index_name  
    ,p.partition_number  
    ,rows   
FROM sys.partitions AS p  
INNER JOIN sys.indexes AS i ON p.object_id = i.object_id AND p.index_id = i.index_id  
INNER JOIN sys.partition_schemes ps ON i.data_space_id=ps.data_space_id  
INNER JOIN sys.objects AS o ON o.object_id = i.object_id  
ORDER BY index_name, partition_number;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ33"></a> Come trovare tutte le statistiche su un oggetto specificato?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido e `<schema_name.object_name>` con un nome di tabella, vista indicizzata o funzione con valori di tabella valido.  
  
```  
USE <database_name>;  
GO  
SELECT name AS statistics_name  
    ,stats_id  
    ,auto_created  
    ,user_created  
    ,no_recompute  
FROM sys.stats  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ34"></a> Come individuare tutte le statistiche e le colonne delle statistiche su un oggetto specificato?  
 Prima di eseguire la query seguente, sostituire `<database_name>` con un nome valido e `<schema_name.object_name>` con un nome di tabella, vista indicizzata o funzione con valori di tabella valido.  
  
```  
USE <database_name>;  
GO  
SELECT s.name AS statistics_name  
    ,c.name AS column_name  
    ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ35"></a> Come individuare la definizione di una vista?  
 Prima di eseguire la query seguente, sostituire `<database_name>` e `<schema_name.object_name>` con nomi validi.  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 In alternativa, è possibile utilizzare la funzione `OBJECT_DEFINITION`, come illustrato nell'esempio seguente.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
