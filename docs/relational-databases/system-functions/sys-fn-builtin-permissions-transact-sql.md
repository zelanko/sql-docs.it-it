---
title: sys.fn_builtin_permissions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_builtin_permissions
- sys.fn_builtin_permissions_TSQL
- fn_builtin_permissions_TSQL
- sys.fn_builtin_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- compact permissions types
- viewing permission hierarchy
- hierarchies [SQL Server], permissions
- built-in permissions hierarchy [SQL Server]
- fn_builtin_permissions function
- permissions [SQL Server], hierarchy
- displaying permission hierarchy
- sys.fn_builtin_permissions function
ms.assetid: 704b1ad3-3534-4cf3-aff4-9fb70064b6cc
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 730508fca6b6f9d3e9515e9ec496971a4b758279
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68046517"
---
# <a name="sysfn_builtin_permissions-transact-sql"></a>sys.fn_builtin_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una descrizione della gerarchia delle autorizzazioni predefinite del server. `sys.fn_builtin_permissions`può essere chiamato solo su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]e restituisce tutte le autorizzazioni, indipendentemente dal fatto che siano supportate nella piattaforma corrente. La maggior parte delle autorizzazioni si applica a tutte le piattaforme, mentre alcune non si applicano a tutte le piattaforme. Ad esempio, non è possibile concedere autorizzazioni a livello di server per il database SQL. Per informazioni sulle piattaforme che supportano ogni autorizzazione, vedere [autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.fn_builtin_permissions ( [ DEFAULT | NULL ]  
    | empty_string | '<securable_class>' } )  
  
<securable_class> ::=   
      APPLICATION ROLE | ASSEMBLY | ASYMMETRIC KEY | AVAILABILITY GROUP  
    | CERTIFICATE | CONTRACT | DATABASE | DATABASE SCOPED CREDENTIAL    
    | ENDPOINT | FULLTEXT CATALOG | FULLTEXT STOPLIST | LOGIN      
    | MESSAGE TYPE | OBJECT | REMOTE SERVICE BINDING | ROLE | ROUTE    
    | SCHEMA | SEARCH PROPERTY LIST | SERVER | SERVER ROLE | SERVICE    
    | SYMMETRIC KEY | TYPE | USER | XML SCHEMA COLLECTION  
```  
  
## <a name="arguments"></a>Argomenti  
 DEFAULT  
 Quando viene chiamato con l'opzione predefinita (senza virgolette), la funzione restituirà un elenco completo delle autorizzazioni predefinite.  
  
 NULL  
 Equivale a DEFAULT.  
  
 *empty_string*  
 Equivale a DEFAULT.  
  
 **'**<securable_class>**'**  
 Quando viene chiamato con il nome di una classe di entità a protezione diretta, sys. fn_builtin_permissions restituirà tutte le autorizzazioni valide per la classe. <securable_class> è un valore letterale stringa che richiede virgolette. **nvarchar(60)**  
  
## <a name="tables-returned"></a>Tabelle restituite  
  
|Nome colonna|Tipo di dati|Regole di confronto|Descrizione|  
|-----------------|---------------|---------------|-----------------|  
|class_desc|**nvarchar(60)**|Regole di confronto del server|Descrizione della classe a protezione diretta.|  
|permission_name|**nvarchar(60)**|Regole di confronto del server|Nome dell'autorizzazione.|  
|tipo|**varchar(4)**|Regole di confronto del server|Codice abbreviato del tipo di autorizzazione. Vedere la tabella seguente.|  
|covering_permission_name|**nvarchar(60)**|Regole di confronto del server|Se non è NULL, corrisponde al nome dell'autorizzazione per la classe specifica, che implica altre autorizzazioni per tale classe.|  
|parent_class_desc|**nvarchar(60)**|Regole di confronto del server|Se non è NULL, corrisponde al nome della classe padre contenente la classe corrente.|  
|parent_covering_permission_name|**nvarchar(60)**|Regole di confronto del server|Se non è NULL, corrisponde al nome dell'autorizzazione per la classe padre specifica, che implica tutte le altre autorizzazioni per tale classe.|  
  
### <a name="permission-types"></a>Tipi di autorizzazione  
  
|Tipo di autorizzazione|Nome dell'autorizzazione|Si applica a entità a sicurezza diretta o classe|  
|---------------------|---------------------|-----------------------------------|  
|AADS|ALTER ANY DATABASE EVENT SESSION<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|AAES|ALTER ANY EVENT SESSION|SERVER|  
|AAMK|ALTER ANY MASK<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ADBO|ADMINISTER BULK OPERATIONS|SERVER|  
|AEDS|ALTER ANY EXTERNAL DATA SOURCE<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|AEFF|ALTER ANY EXTERNAL FILE FORMAT<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|AL|ALTER|APPLICATION ROLE|  
|AL|ALTER|ASSEMBLY|  
|AL|ALTER<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|AVAILABILITY GROUP|  
|AL|ALTER|ASYMMETRIC KEY|  
|AL|ALTER|CERTIFICATE|  
|AL|ALTER|CONTRACT|  
|AL|ALTER|DATABASE|  
|AL|ALTER<br /> **Applica t o**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|AL|ALTER|ENDPOINT|  
|AL|ALTER|FULLTEXT CATALOG|  
|AL|ALTER|FULLTEXT STOPLIST|  
|AL|ALTER|LOGIN|  
|AL|ALTER|MESSAGE TYPE|  
|AL|ALTER|OBJECT|  
|AL|ALTER|REMOTE SERVICE BINDING|  
|AL|ALTER|ROLE|  
|AL|ALTER|ROUTE|  
|AL|ALTER|SCHEMA|  
|AL|ALTER|SEARCH PROPERTY LIST|  
|AL|ALTER<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER ROLE|  
|AL|ALTER|SERVICE|  
|AL|ALTER|SYMMETRIC KEY|  
|AL|ALTER|USER|  
|AL|ALTER|XML SCHEMA COLLECTION|  
|ALAA|ALTER ANY SERVER AUDIT|SERVER|  
|ALAG|ALTER ANY AVAILABILITY GROUP<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|ALAK|ALTER ANY ASYMMETRIC KEY|DATABASE|  
|ALAR|ALTER ANY APPLICATION ROLE|DATABASE|  
|ALAS|ALTER ANY ASSEMBLY|DATABASE|  
|ALCD|ALTER ANY CREDENTIAL|SERVER|  
|ALCF|ALTER ANY CERTIFICATE|DATABASE|  
|ALCK|ALTER ANY COLUMN ENCRYPTION KEY<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ALCM|ALTER ANY COLUMN MASTER KEY<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ALCO|ALTER ANY CONNECTION|SERVER|  
|ALDA|ALTER ANY DATABASE AUDIT|DATABASE|  
|ALDB|ALTER ANY DATABASE|SERVER|  
|ALDC|ALTER ANY DATABASE SCOPED CONFIGURATION<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ALDS|ALTER ANY DATASPACE|DATABASE|  
|ALED|ALTER ANY DATABASE EVENT NOTIFICATION|DATABASE|  
|ALES|ALTER ANY EVENT NOTIFICATION|SERVER|  
|ALFT|ALTER ANY FULLTEXT CATALOG|DATABASE|  
|ALHE|ALTER ANY ENDPOINT|SERVER|  
|ALLG|ALTER ANY LOGIN|SERVER|  
|ALLS|ALTER ANY LINKED SERVER|SERVER|  
|ALMT|ALTER ANY MESSAGE TYPE|DATABASE|  
|ALRL|ALTER ANY ROLE|DATABASE|  
|ALRS|ALTER RESOURCES|SERVER|  
|ALRT|ALTER ANY ROUTE|DATABASE|  
|ALSB|ALTER ANY REMOTE SERVICE BINDING|DATABASE|  
|ALSC|ALTER ANY CONTRACT|DATABASE|  
|ALSK|ALTER ANY SYMMETRIC KEY|DATABASE|  
|ALSM|ALTER ANY SCHEMA|DATABASE|  
|ALSP|ALTER ANY SECURITY POLICY<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ALSR|ALTER ANY SERVER ROLE<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|ALSS|ALTER SERVER STATE|SERVER|  
|ALST|ALTER SETTINGS|SERVER|  
|ALSV|ALTER ANY SERVICE|DATABASE|  
|ALTG|ALTER ANY DATABASE DDL TRIGGER|DATABASE|  
|ALTR|ALTER TRACE|SERVER|  
|ALUS|ALTER ANY USER|DATABASE|  
|AUTH|AUTHENTICATE|DATABASE|  
|AUTH|AUTHENTICATE SERVER|SERVER|  
|BADB|BACKUP DATABASE|DATABASE|  
|BALO|BACKUP LOG|DATABASE|  
|CADB|CONNECT ANY DATABASE<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|CL|CONTROL|APPLICATION ROLE|  
|CL|CONTROL|ASSEMBLY|  
|CL|CONTROL|ASYMMETRIC KEY|  
|CL|CONTROL<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|AVAILABILITY GROUP|  
|CL|CONTROL|CERTIFICATE|  
|CL|CONTROL|CONTRACT|  
|CL|CONTROL|DATABASE|  
|CL|CONTROL<br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|CL|CONTROL|ENDPOINT|  
|CL|CONTROL|FULLTEXT CATALOG|  
|CL|CONTROL|FULLTEXT STOPLIST|  
|CL|CONTROL|LOGIN|  
|CL|CONTROL|MESSAGE TYPE|  
|CL|CONTROL|OBJECT|  
|CL|CONTROL|REMOTE SERVICE BINDING|  
|CL|CONTROL|ROLE|  
|CL|CONTROL|ROUTE|  
|CL|CONTROL|SCHEMA|  
|CL|CONTROL|SEARCH PROPERTY LIST|  
|CL|CONTROL SERVER|SERVER|  
|CL|CONTROL<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER ROLE|  
|CL|CONTROL|SERVICE|  
|CL|CONTROL|SYMMETRIC KEY|  
|CL|CONTROL|TYPE|  
|CL|CONTROL|USER|  
|CL|CONTROL|XML SCHEMA COLLECTION|  
|CO|CONNECT|DATABASE|  
|CO|CONNECT|ENDPOINT|  
|CORP|CONNECT REPLICATION|DATABASE|  
|COSQ|CONNECT SQL|SERVER|  
|CP|CHECKPOINT|DATABASE|  
|CRAC|Creare un gruppo di disponibilità<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|CRAG|CREATE AGGREGATE|DATABASE|  
|CRAK|CREATE ASYMMETRIC KEY|DATABASE|  
|CRAS|CREATE ASSEMBLY|DATABASE|  
|CRCF|CREATE CERTIFICATE|DATABASE|  
|CRDB|CREATE ANY DATABASE|SERVER|  
|CRDB|CREATE DATABASE|DATABASE|  
|CRDE|CREATE DDL EVENT NOTIFICATION|SERVER|  
|CRDF|CREATE DEFAULT|DATABASE|  
|CRED|CREATE DATABASE DDL EVENT NOTIFICATION|DATABASE|  
|CRFN|CREATE FUNCTION|DATABASE|  
|CRFT|CREATE FULLTEXT CATALOG|DATABASE|  
|CRHE|CREATE ENDPOINT|SERVER|  
|CRMT|CREATE MESSAGE TYPE|DATABASE|  
|CRPR|CREATE PROCEDURE|DATABASE|  
|CRQU|CREATE QUEUE|DATABASE|  
|CRRL|CREATE ROLE|DATABASE|  
|CRRT|CREATE ROUTE|DATABASE|  
|CRRU|CREATE RULE|DATABASE|  
|CRSB|CREATE REMOTE SERVICE BINDING|DATABASE|  
|CRSC|CREATE CONTRACT|DATABASE|  
|CRSK|CREATE SYMMETRIC KEY|DATABASE|  
|CRSM|CREATE SCHEMA|DATABASE|  
|CRSN|CREATE SYNONYM|DATABASE|  
|CRSO|CREATE SEQUENCE|SCHEMA|  
|CRSR|CREATE SERVER ROLE<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|CRSV|CREATE SERVICE|DATABASE|  
|CRTB|CREA TABELLA|DATABASE|  
|CRTE|CREATE TRACE EVENT NOTIFICATION|SERVER|  
|CRTY|CREATE TYPE|DATABASE|  
|CRVW|CREATE VIEW|DATABASE|  
|CRXS|CREATE XML SCHEMA COLLECTION|DATABASE|  
|DABO|ADMINISTER DATABASE BULK OPERATIONS<br /> **Si applica a**: [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].|DATABASE|  
|DL|DELETE|DATABASE|  
|DL|DELETE|OBJECT|  
|DL|DELETE|SCHEMA|  
|EAES|EXECUTE ANY EXTERNAL SCRIPT<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|EX|EXECUTE|DATABASE|  
|EX|EXECUTE|OBJECT|  
|EX|EXECUTE|SCHEMA|  
|EX|EXECUTE|TYPE|  
|EX|EXECUTE|XML SCHEMA COLLECTION|  
|IAL|IMPERSONATE ANY LOGIN<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|IM|IMPERSONATE|LOGIN|  
|IM|IMPERSONATE|USER|  
|IN|INSERT|DATABASE|  
|IN|INSERT|OBJECT|  
|IN|INSERT|SCHEMA|  
|KIDC|KILL DATABASE CONNECTION<br />**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|DATABASE|  
|RC|RECEIVE|OBJECT|  
|RF|REFERENCES|ASSEMBLY|  
|RF|REFERENCES|ASYMMETRIC KEY|  
|RF|REFERENCES|CERTIFICATE|  
|RF|REFERENCES|CONTRACT|  
|RF|REFERENCES|DATABASE|  
|RF|REFERENCES<br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|RF|REFERENCES|FULLTEXT CATALOG|  
|RF|REFERENCES|FULLTEXT STOPLIST|  
|RF|REFERENCES|SEARCH PROPERTY LIST|  
|RF|REFERENCES|MESSAGE TYPE|  
|RF|REFERENCES|OBJECT|  
|RF|REFERENCES|SCHEMA|  
|RF|REFERENCES|SYMMETRIC KEY|  
|RF|REFERENCES|TYPE|  
|RF|REFERENCES|XML SCHEMA COLLECTION|  
|SHDN|SHUTDOWN|SERVER|  
|SL|SELECT|DATABASE|  
|SL|SELECT|OBJECT|  
|SL|SELECT|SCHEMA|  
|SN|SEND|SERVICE|  
|SPLN|SHOWPLAN|DATABASE|  
|SUQN|SUBSCRIBE QUERY NOTIFICATIONS|DATABASE|  
|SUS|SELECT ALL USER SECURABLES<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|A|TAKE OWNERSHIP|ASSEMBLY|  
|A|TAKE OWNERSHIP|ASYMMETRIC KEY|  
|A|TAKE OWNERSHIP<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|AVAILABILITY GROUP|  
|A|TAKE OWNERSHIP|CERTIFICATE|  
|A|TAKE OWNERSHIP|CONTRACT|  
|A|TAKE OWNERSHIP|DATABASE|  
|A|TAKE OWNERSHIP<br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|A|TAKE OWNERSHIP|ENDPOINT|  
|A|TAKE OWNERSHIP|FULLTEXT CATALOG|  
|A|TAKE OWNERSHIP|FULLTEXT STOPLIST|  
|A|TAKE OWNERSHIP|SEARCH PROPERTY LIST|  
|A|TAKE OWNERSHIP|MESSAGE TYPE|  
|A|TAKE OWNERSHIP|OBJECT|  
|A|TAKE OWNERSHIP|REMOTE SERVICE BINDING|  
|A|TAKE OWNERSHIP|ROLE|  
|A|TAKE OWNERSHIP|ROUTE|  
|A|TAKE OWNERSHIP|SCHEMA|  
|A|TAKE OWNERSHIP<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER ROLE|  
|A|TAKE OWNERSHIP|SERVICE|  
|A|TAKE OWNERSHIP|SYMMETRIC KEY|  
|A|TAKE OWNERSHIP|TYPE|  
|A|TAKE OWNERSHIP|XML SCHEMA COLLECTION|  
|UMSK|UNMASK<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|UP|UPDATE|DATABASE|  
|UP|UPDATE|OBJECT|  
|UP|UPDATE|SCHEMA|  
|VW|VIEW DEFINITION|APPLICATION ROLE|  
|VW|VIEW DEFINITION|ASSEMBLY|  
|VW|VIEW DEFINITION|ASYMMETRIC KEY|  
|VW|VIEW DEFINITION<br />**Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|AVAILABILITY GROUP|  
|VW|VIEW DEFINITION|CERTIFICATE|  
|VW|VIEW DEFINITION|CONTRACT|  
|VW|VIEW DEFINITION|DATABASE|  
|VW|VIEW DEFINITION<br /> **Si applica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|VW|VIEW DEFINITION|ENDPOINT|  
|VW|VIEW DEFINITION|FULLTEXT CATALOG|  
|VW|VIEW DEFINITION|FULLTEXT STOPLIST|  
|VW|VIEW DEFINITION|LOGIN|  
|VW|VIEW DEFINITION|MESSAGE TYPE|  
|VW|VIEW DEFINITION|OBJECT|  
|VW|VIEW DEFINITION|REMOTE SERVICE BINDING|  
|VW|VIEW DEFINITION|ROLE|  
|VW|VIEW DEFINITION|ROUTE|  
|VW|VIEW DEFINITION|SCHEMA|  
|VW|VIEW DEFINITION|SEARCH PROPERTY LIST|  
|VW|VIEW DEFINITION<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER ROLE|  
|VW|VIEW DEFINITION|SERVICE|  
|VW|VIEW DEFINITION|SYMMETRIC KEY|  
|VW|VIEW DEFINITION|TYPE|  
|VW|VIEW DEFINITION|USER|  
|VW|VIEW DEFINITION|XML SCHEMA COLLECTION|  
|VWAD|VIEW ANY DEFINITION|SERVER|  
|VWCK|VIEW ANY COLUMN ENCRYPTION KEY DEFINITION<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|VWCM|VIEW ANY COLUMN MASTER KEY DEFINITION<br /> **Si applica a** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (da alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|VWCT|VIEW CHANGE TRACKING|OBJECT|  
|VWCT|VIEW CHANGE TRACKING|SCHEMA|  
|VWDB|VIEW ANY DATABASE|SERVER|  
|VWDS|VIEW DATABASE STATE|DATABASE|  
|VWSS|VIEW SERVER STATE|SERVER|  
|XA|EXTERNAL ACCESS ASSEMBLY|SERVER|  
|XU|UNSAFE ASSEMBLY|SERVER|  
  
## <a name="remarks"></a>Osservazioni  
 `sys.fn_builtin_permissions` è una funzione con valori di tabella che restituisce una copia della gerarchia di autorizzazioni predefinite. Questa gerarchia include le autorizzazioni implicite. Il `DEFAULT` set di risultati descrive un grafico aciclici diretto della gerarchia delle autorizzazioni, di cui la radice è (Class = Server, Permission = Control Server).  
  
 `sys.fn_builtin_permissions` non accetta parametri correlati.  
  
 `sys.fn_builtin_permissions` restituirà un set vuoto se viene chiamata con un nome di classe non valido.  
 
[!INCLUDE[database-engine-permissions](../../includes/paragraph-content/database-engine-permissions.md)]
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo public.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-all-built-in-permissions"></a>R. Elenco di tutte le autorizzazioni predefinite   
Usare `DEFAULT` o una stringa vuota per restituire tutte le autorizzazioni.   
```sql  
SELECT * FROM sys.fn_builtin_permissions(DEFAULT);
SELECT * FROM sys.fn_builtin_permissions('');  
```  
  
### <a name="b-listing-permissions-that-can-be-set-on-a-symmetric-key"></a>B. Elenco delle autorizzazioni che possono essere impostate in una chiave simmetrica   
Specificare una classe per restituire tutte le autorizzazioni possibili per la classe.   
```sql  
SELECT * FROM sys.fn_builtin_permissions(N'SYMMETRIC KEY');  
```  
  
### <a name="c-listing-classes-on-which-there-is-a-select-permission"></a>C. Elenco delle classi che includono un'autorizzazione SELECT   
  
```sql  
SELECT * FROM sys.fn_builtin_permissions(DEFAULT)   
    WHERE permission_name = 'SELECT';  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Gerarchia delle autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [CONCEDERE &#40;&#41;Transact-SQL](../../t-sql/statements/grant-transact-sql.md)   
 [CREAZIONE dello SCHEMA &#40;&#41;Transact-SQL](../../t-sql/statements/create-schema-transact-sql.md)   
 [DROP SCHEMA &#40;&#41;Transact-SQL](../../t-sql/statements/drop-schema-transact-sql.md)   
 [Autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys. fn_my_permissions &#40;&#41;Transact-SQL](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  


