---
title: sys.database_principals (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_principals
- database_principals_TSQL
- sys.database_principals
- sys.database_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_principals catalog view
ms.assetid: 8cb239e9-eb8c-4109-9cec-0d35de95fa0e
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 512994ada852ea7807cc14ecd5b25d9acff56ffc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632682"
---
# <a name="sysdatabaseprincipals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Viene restituita una riga per ogni entità di sicurezza in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome dell'entità, univoco all'interno del database.|  
|**principal_id**|**int**|ID dell'entità, univoco all'interno del database.|  
|**type**|**char(1)**|Tipo di entità:<br /><br /> A = Ruolo applicazione<br /><br /> C = Utente sul quale è stato eseguito il mapping a un certificato<br /><br /> E = utente esterno da Azure Active Directory<br /><br /> G = Gruppo di Windows<br /><br /> K = Utente sul quale è stato eseguito il mapping a una chiave asimmetrica<br /><br /> R = Ruolo del database<br /><br /> S = Utente SQL<br /><br /> U = Utente di Windows<br /><br /> X = gruppo esterno da applicazioni o il gruppo di Azure Active Directory|  
|**type_desc**|**nvarchar(60)**|Descrizione del tipo dell'entità.<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|Nome da utilizzare quando il nome SQL non specifica uno schema. Restituisce Null per entità non di tipo S, U o A.|  
|**create_date**|**datetime**|Ora di creazione dell'entità.|  
|**modify_date**|**datetime**|Ora dell'ultima modifica dell'entità.|  
|**owning_principal_id**|**int**|ID dell'entità proprietaria dell'entità corrente. Tutte le entità, ad eccezione dei ruoli di Database devono essere proprietario **dbo**.|  
|**sid**|**varbinary(85)**|ID di sicurezza (SID) dell'entità.  NULL per SYS e INFORMATION SCHEMAS.|  
|**is_fixed_role**|**bit**|Se è 1, questa riga rappresenta una voce per uno dei ruoli predefiniti del database, ovvero db_owner, db_accessadmin, db_datareader, db_datawriter, db_ddladmin, db_securityadmin, db_backupoperator, db_denydatareader, db_denydatawriter.|  
|**authentication_type**|**int**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica il tipo di autenticazione. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> 0 : Nessuna autenticazione<br />1 : Autenticazione istanza<br />2 : Autenticazione del database<br />3 : Autenticazione di Windows|  
|**authentication_type_desc**|**nvarchar(60)**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Descrizione del tipo di autenticazione. Di seguito sono i valori possibili e le relative descrizioni.<br /><br /> NONE: Nessuna autenticazione<br />ISTANZA DI: Autenticazione istanza<br />DATABASE: Autenticazione del database<br />FINESTRE: Autenticazione di Windows|  
|**default_language_name**|**sysname**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica la lingua predefinita per questa entità.|  
|**default_language_lcid**|**int**|**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica l'identificatore LCID predefinito per questa entità.|  
|**allow_encrypted_value_modifications**|**bit**|**Si applica a**: da [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Elimina i controlli sui metadati di crittografia nel server nelle operazioni di copia bulk. Ciò consente all'utente di copia bulk di dati con Always Encrypted, tra le tabelle o database, senza la decrittografia dei dati. Il valore predefinito è OFF. |      
  
## <a name="remarks"></a>Note  
 Il *PasswordLastSetTime* proprietà sono disponibili in tutte le configurazioni supportate di SQL Server, ma le altre proprietà è disponibile solo quando viene eseguito SQL Server in Windows Server 2003 o versione successiva ed entrambe le opzioni CHECK_POLICY e CHECK_ SCADENZA sono abilitati. Visualizzare [criteri Password](../../relational-databases/security/password-policy.md) per altre informazioni.  
  
## <a name="permissions"></a>Permissions  
 Qualsiasi utente può visualizzare il proprio nome utente, gli utenti di sistema e i ruoli predefiniti del database. Per visualizzare altri utenti, è richiesta l'autorizzazione ALTER ANY USER o un'autorizzazione dell'utente. Per visualizzare i ruoli definiti dall'utente, è richiesta l'autorizzazione ALTER ANY ROLE o l'appartenenza al ruolo.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>R: Elenco di tutte le autorizzazioni delle entità di database  
 Nella query seguente vengono elencate le autorizzazioni concesse o negate in modo esplicito alle entità di database.  
  
> [!IMPORTANT]  
>  Le autorizzazioni dei ruoli predefiniti del database non sono incluse in sys.database_permissions. Pertanto, le entità di database potrebbero contenere ulteriori autorizzazioni non presenti in questo elenco.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>B: Elenco delle autorizzazioni per gli oggetti dello schema all'interno di un database  
 Nella query seguente viene creato un join di sys.database_principals e sys.database_permissions con sys.objects e sys.schemas per elencare le autorizzazioni concesse o negate agli oggetti di uno schema specifico.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C: Elenco di tutte le autorizzazioni delle entità di database  
 Nella query seguente vengono elencate le autorizzazioni concesse o negate in modo esplicito alle entità di database.  
  
> [!IMPORTANT]  
>  Le autorizzazioni dei ruoli predefiniti del database non sono incluse `sys.database_permissions`. Pertanto, le entità di database potrebbero contenere ulteriori autorizzazioni non presenti in questo elenco.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: Elenco delle autorizzazioni per gli oggetti dello schema all'interno di un database  
 La query seguente join `sys.database_principals` e `sys.database_permissions` al `sys.objects` e `sys.schemas` per elencare le autorizzazioni concesse o negate agli oggetti dello schema specifico.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Utenti di Database indipendente: rendere portabile un Database](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Connessione al database SQL con l'autenticazione di Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


