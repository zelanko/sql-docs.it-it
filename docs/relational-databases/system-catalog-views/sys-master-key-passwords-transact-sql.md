---
title: proprietà sys.master_key_passwords (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
author: stevestein
ms.author: sstein
ms.openlocfilehash: 926acd9beb00102e19dbc2844e282d74bc890915
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752903"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Restituisce una riga per ogni password della chiave master del database aggiunta utilizzando la **sp_control_dbmasterkey_password** stored procedure. Le password utilizzate per proteggere le chiavi master vengono archiviate nell'archivio credenziali. Il nome della credenziale segue il seguente formato: #DBMKEY_<database_family_guid>_>_ random_password_guid<>. La password viene archiviata come segreto della credenziale. Per ogni password aggiunta utilizzando **sp_control_dbmasterkey_password**, è presente una riga in **sys.credentials**.  
  
 Ogni riga in questa visualizzazione mostra un **credential_id** e il **family_guid** di un database la cui chiave master è protetta dalla password associata a tale credenziale. Un join con **sys.credentials** nel **credential_id** restituirà campi utili, ad esempio il **create_date** e il nome della credenziale.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**credential_id**|**Int**|ID della credenziale alla quale appartiene la password. Questo ID è univoco all'interno dell'istanza del server.|  
|**family_guid**|**Uniqueidentifier**|ID univoco del database originale al momento della creazione. Questo GUID rimane invariato in seguito al ripristino o all'aggiunta del database, anche se il nome del database viene modificato.<br /><br /> Se la decrittografia automatica da parte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] della chiave master del servizio non riesce, utilizza l'family_guid per identificare le credenziali che possono contenere la password utilizzata per proteggere la chiave master del database. **family_guid**|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Viste catalogo sicurezza &#40;&#41;Transact-SQLSecurity Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQLTransact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
