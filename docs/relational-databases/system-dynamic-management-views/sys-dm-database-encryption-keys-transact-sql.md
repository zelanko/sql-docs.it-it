---
title: metodo sys.dm_database_encryption_keys (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e716c826fd366fda4505b7fcf9ec8e3b756ec25
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531054"
---
# <a name="sysdm_database_encryption_keys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni sullo stato di crittografia di un database e sulle chiavi di crittografia a esso associate. Per altre informazioni sulla crittografia del database, vedere [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
 
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|database_id|**Int**|ID del database.|  
|encryption_state|**Int**|Indica se il database è crittografato o meno.<br /><br /> 0 = Nessuna chiave di crittografia del database presente, nessuna crittografia<br /><br /> 1 = Non crittografato<br /><br /> 2 = Crittografia in corso<br /><br /> 3 = Crittografato<br /><br /> 4 = Modifica chiave in corso<br /><br /> 5 = Decrittografia in corso<br /><br /> 6 = Modifica della protezione in corso. È in corso la modifica della chiave asimmetrica o del certificato usato per crittografare la chiave di crittografia del database.|  
|create_date|**Datetime**|Visualizza la data (in UTC) in cui è stata creata la chiave di crittografia.|  
|regenerate_date|**Datetime**|Visualizza la data (in UTC) in cui è stata rigenerata la chiave di crittografia.|  
|modify_date|**Datetime**|Visualizza la data (in UTC) in cui è stata modificata la chiave di crittografia.|  
|set_date|**Datetime**|Visualizza la data (in UTC) in cui la chiave di crittografia è stata applicata al database.|  
|opened_date|**Datetime**|Indica quando (in UTC) la chiave del database è stata aperta per l'ultima volta.|  
|key_algorithm|**nvarchar(32)**|Visualizza l'algoritmo usato per la chiave.|  
|key_length|**Int**|Visualizza la lunghezza della chiave.|  
|encryptor_thumbprint|**varbinary(20)**|Mostra l'identificazione digitale della crittografia.|  
|encryptor_type|**nvarchar(32)**|**Si**applica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : ( fino alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).<br /><br /> Descrive il componente di crittografia.|  
|percent_complete|**real**|Percentuale di completamento del cambiamento di stato della crittografia del database. In assenza di un cambiamento di stato il valore sarà 0.|
|encryption_state_desc|**nvarchar(32)**|**Si**applica [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] a : e versioni successive.<br><br> Stringa che indica se il database è crittografato o meno.<br><br>Nessuno<br><br>Unencrypted<br><br>Crittografato<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**Int**|**Si**applica [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] a : e versioni successive.<br><br>Indica lo stato corrente dell'analisi di crittografia. <br><br>0 - Non è stata avviata alcuna scansione, TDE non è abilitato<br><br>1 - Scansione è in corso.<br><br>2 - La scansione è in corso ma è stata sospesa, l'utente può riprendere.<br><br>3 - La scansione è stata interrotta per qualche motivo, è necessario un intervento manuale. Contattare il supporto tecnico Microsoft per ulteriore assistenza.<br><br>4 - La scansione è stata completata correttamente, TDE è abilitato e la crittografia è stata completata.|
|encryption_scan_state_desc|**nvarchar(32)**|**Si**applica [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] a : e versioni successive.<br><br>Stringa che indica lo stato corrente dell'analisi di crittografia.<br><br> Nessuno<br><br>RUNNING<br><br>SUSPENDED<br><br>ABORTED<br><br>Completo|
|encryption_scan_modify_date|**Datetime**|**Si**applica [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] a : e versioni successive.<br><br> Visualizza la data (in UTC) in cui è stato modificato lo stato dell'ultima analisi di crittografia.|
  
## <a name="permissions"></a>Autorizzazioni

On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], `VIEW SERVER STATE` richiede l'autorizzazione.   
Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Premium, `VIEW DATABASE STATE` richiede l'autorizzazione nel database. Nei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] livelli Standard e Basic è necessario **l'amministratore** del server o un account amministratore di Azure Active Directory.On Standard and Basic Tiers, requires the Server admin or an **Azure Active Directory admin** account.   

## <a name="see-also"></a>Vedere anche  

 [Funzioni e viste a gestione dinamica correlati alla sicurezza &#40;&#41;Transact-SQLSecurity-Related Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Crittografia dei dati trasparente &#40;&#41;TDE](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server Encryption](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Sql ServerSQL Server e le chiavi di crittografia del database &#40;i&#41;del motore di databaseSQL Server and Database Encryption Keys &#40;Database Engine&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Opzioni ALTER DATABASE SET &#40;Transact-&#41;SQL](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;transact-sqlSQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [CHIAVE di crittografia DI ALT DATABASE &#40;Transact-&#41;SQL](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  
