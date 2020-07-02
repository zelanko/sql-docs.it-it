---
title: sys. column_encryption_key_values (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c9c17ef0384d1b4ef1bc5534ffeffa8b2ba3d598
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718889"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>sys. column_encryption_key_values (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce informazioni sui valori crittografati delle chiavi di crittografia di colonna (chiavi CEK) create con la chiave di crittografia della colonna [Create Column](../../t-sql/statements/create-column-encryption-key-transact-sql.md) o l'istruzione [ALTER column Encryption Key &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md) . Ogni riga rappresenta un valore di un CEK, crittografato con una chiave master della colonna (CMK).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|ID di CEK nel database.|  
|**column_master_key_id**|**int**|ID della chiave master della colonna utilizzata per crittografare il valore CEK.|  
|**encrypted_value**|**varbinary(8000)**|Valore CEK crittografato con il CMK specificato in column_master_key_id.|  
|**encryption_algorithm_name**|**sysname**|Nome di un algoritmo utilizzato per crittografare il valore di CEK.<br /><br /> Nome dell'algoritmo di crittografia usato per crittografare il valore. L'algoritmo per i provider di sistema deve essere **RSA_OAEP**.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede l'autorizzazione **View any Column Encryption Key** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [CREAZIONE della chiave di crittografia della colonna &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [RILASCIARE la chiave di crittografia della colonna &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREAZIONE della chiave MASTER della colonna &#40;&#41;Transact-SQL](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Viste del catalogo di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys. column_encryption_keys &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys. column_master_keys &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys. Columns &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted con enclave sicure](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Panoramica della gestione delle chiavi per Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [Gestire le chiavi per Always Encrypted con enclave sicuri](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
