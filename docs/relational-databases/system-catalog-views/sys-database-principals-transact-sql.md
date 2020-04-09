---
title: proprietà sys.database_principals (Transact-SQL) Documenti Microsoft
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: feed483cf3ee08c0652e55de51b1f73fc087ed39
ms.sourcegitcommit: 7ed12a64f7f76d47f5519bf1015d19481dd4b33a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80873117"
---
# <a name="sysdatabase_principals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Viene restituita una riga per ogni entità di sicurezza in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome dell'entità, univoco all'interno del database.|  
|**principal_id**|**Int**|ID dell'entità, univoco all'interno del database.|  
|**type**|**char(1)**|Tipo di entità:<br /><br /> A = Ruolo applicazione<br /><br /> C = Utente sul quale è stato eseguito il mapping a un certificato<br /><br /> E - Utente esterno da Azure Active Directory<br /><br /> G = Gruppo di Windows<br /><br /> K = Utente sul quale è stato eseguito il mapping a una chiave asimmetrica<br /><br /> R = Ruolo del database<br /><br /> S = Utente SQL<br /><br /> U = Utente di Windows<br /><br /> X - Gruppo esterno da applicazioni o gruppo di Azure Active Directory|  
|**type_desc**|**nvarchar(60)**|Descrizione del tipo dell'entità.<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|Nome da utilizzare quando il nome SQL non specifica uno schema. Restituisce Null per entità non di tipo S, U o A.|  
|**create_date**|**datetime**|Ora di creazione dell'entità.|  
|**modify_date**|**datetime**|Ora dell'ultima modifica dell'entità.|  
|**owning_principal_id**|**Int**|ID dell'entità proprietaria dell'entità corrente. Tutti i ruoli predefiniti del database sono di proprietà **di dbo** per impostazione predefinita.|  
|**sid**|**varbinary(85)**|ID di sicurezza (SID) dell'entità.  NULL per SYS e INFORMATION SCHEMAS.|  
|**is_fixed_role**|**bit**|Se è 1, questa riga rappresenta una voce per uno dei ruoli predefiniti del database, ovvero db_owner, db_accessadmin, db_datareader, db_datawriter, db_ddladmin, db_securityadmin, db_backupoperator, db_denydatareader, db_denydatawriter.|  
|**authentication_type**|**Int**|**Si**applica [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : e versioni successive.<br /><br /> Indica il tipo di autenticazione. Di seguito sono riportati i valori possibili e le relative descrizioni.<br /><br /> 0 : Nessuna autenticazione<br />1 : Autenticazione dell'istanza<br />2 : Autenticazione del database<br />3 : Autenticazione di Windows<br />4 : Autenticazione di Azure Active Directory|  
|**authentication_type_desc**|**nvarchar(60)**|**Si**applica [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : e versioni successive.<br /><br /> Descrizione del tipo di autenticazione. Di seguito sono riportati i valori possibili e le relative descrizioni.<br /><br /> NONE : Nessuna autenticazione<br />INSTANCE : Autenticazione dell'istanza<br />DATABASE : Autenticazione del database<br />WINDOWS : Autenticazione di Windows<br />EXTERNAL: Autenticazione di Azure Active Directory|  
|**default_language_name**|**sysname**|**Si**applica [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : e versioni successive.<br /><br /> Indica la lingua predefinita per questa entità.|  
|**default_language_lcid**|**Int**|**Si**applica [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : e versioni successive.<br /><br /> Indica l'identificatore LCID predefinito per questa entità.|  
|**allow_encrypted_value_modifications**|**bit**|**Si**applica [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] a [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]: e versioni successive, .<br /><br /> Elimina i controlli sui metadati di crittografia nel server nelle operazioni di copia bulk. Ciò consente all'utente di eseguire la copia bulk dei dati crittografati utilizzando Always Encrypted, tra tabelle o database, senza decrittografarli. Il valore predefinito è OFF. |      
  
## <a name="remarks"></a>Osservazioni  
 Le proprietà *PasswordLastSetTime* sono disponibili in tutte le configurazioni supportate di SQL ServerSQL Server, ma le altre proprietà sono disponibili solo quando SQL Server è in esecuzione in Windows Server 2003 o versione successiva e sono abilitati sia CHECK_POLICY che CHECK_EXPIRATION. Per ulteriori informazioni, vedere [Criteri password.](../../relational-databases/security/password-policy.md)
I valori del principal_id possono essere riutilizzati nel caso in cui i principali siano stati eliminati e pertanto non è garantito che siano in continuo aumento.
  
## <a name="permissions"></a>Autorizzazioni  
 Qualsiasi utente può visualizzare il proprio nome utente, gli utenti di sistema e i ruoli predefiniti del database. Per visualizzare altri utenti, è richiesta l'autorizzazione ALTER ANY USER o un'autorizzazione dell'utente. Per visualizzare i ruoli definiti dall'utente, è richiesta l'autorizzazione ALTER ANY ROLE o l'appartenenza al ruolo.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>A: elenco di tutte le autorizzazioni delle entità di database  
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
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>B: elenco di autorizzazioni per gli oggetti dello schema all'interno di un database  
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C: Elenco di tutte le autorizzazioni delle entità di database  
 Nella query seguente vengono elencate le autorizzazioni concesse o negate in modo esplicito alle entità di database.  
  
> [!IMPORTANT]  
>  Le autorizzazioni dei ruoli predefiniti `sys.database_permissions`del database non vengono visualizzate in . Pertanto, le entità di database potrebbero contenere ulteriori autorizzazioni non presenti in questo elenco.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: Elenco delle autorizzazioni per gli oggetti dello schema all'interno di un database  
 La query seguente `sys.database_principals` `sys.database_permissions` esegue `sys.objects` `sys.schemas` i join e per elencare le autorizzazioni concesse o negate a oggetti dello schema specifici.  
  
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
 [Principali &#40;&#41;del Motore di database](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [server_principals &#40;Transact-SQL&#41;ditransact-SQL](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [Viste catalogo sicurezza &#40;&#41;Transact-SQLSecurity Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Utenti del database indipendente - Rendere il database portabileContained Database Users - Making Your Database Portable](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Connessione al database SQL tramite l'autenticazione di Azure Active DirectoryConnecting to SQL Database By Using Azure Active Directory Authentication](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


