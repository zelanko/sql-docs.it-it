---
title: proprietà sys.credentials (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.credentials
- sys.credentials_TSQL
- credentials_TSQL
- credentials
dev_langs:
- TSQL
helpviewer_keywords:
- sys.credentials catalog view
ms.assetid: ea48cf80-904a-4273-a950-6d35b1b0a1b6
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f87378897256f8b4fae26b30263577bedede6175
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752885"
---
# <a name="syscredentials-transact-sql"></a>sys.credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-asdw-pdw-md.md)]

  Restituisce una riga per ogni credenziale a livello di server.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|credential_id|**Int**|ID della credenziale. Il nome è univoco nel server.|  
|name|**sysname**|Nome delle credenziali. Il nome è univoco nel server.|  
|credential_identity|**nvarchar(4000)**|Nome dell'identità da utilizzare, in genere corrispondente a un utente di Windows. Non è necessario che sia univoco.|  
|create_date|**datetime**|Ora di creazione della credenziale.|  
|modify_date|**datetime**|Ora dell'ultima modifica apportata alla credenziale.|  
|target_type|**nvarchar(100)**|Tipo di credenziale. Restituisce NULL per credenziali tradizionali e CRYPTOGRAPHIC PROVIDER per credenziali di cui è stato eseguito il mapping a un provider di servizi di crittografia. Per ulteriori informazioni sui provider di gestione delle chiavi esterni, vedere [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  
|target_id|**Int**|ID dell'oggetto a cui è stato eseguito il mapping della credenziale. Restituisce 0 per credenziali tradizionali e un valore diverso da 0 per credenziali di cui è stato eseguito il mapping a un provider di servizi di crittografia. Per ulteriori informazioni sui provider di gestione delle chiavi esterni, vedere [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).|  

## <a name="remarks"></a>Osservazioni  
Per le credenziali a livello di database, vedere [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede `VIEW ANY DEFINITION` l'autorizzazione o `ALTER ANY CREDENTIAL` l'autorizzazione. Inoltre, all'entità non `VIEW ANY DEFINITION` deve essere negata l'autorizzazione.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [Credenziali &#40;&#41;del Motore di databaseCredentials &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Viste catalogo sicurezza &#40;&#41;Transact-SQLSecurity Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Principali &#40;&#41;del Motore di database](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
