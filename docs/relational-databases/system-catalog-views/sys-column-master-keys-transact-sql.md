---
title: column_master_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ae8a4077c0fe4e3f6b7754b4fc53a401d03e355
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140063"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni chiave master del database aggiunta tramite il [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) istruzione. Ogni riga rappresenta una chiave master di colonna (CMK).  
    
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Il nome di CMK.|  
|**column_master_key_id**|**int**|ID della chiave master della colonna.|  
|**create_date**|**datetime**|Data che Creazione chiave master della colonna.|  
|**modify_date**|**datetime**|Data che ultima modifica della chiave master della colonna.|  
|**key_store_provider_name**|**sysname**|Nome del provider per l'archivio chiavi master della colonna che contiene la chiave CMK. I valori consentiti sono i seguenti:<br /><br /> MSSQL_CERTIFICATE_STORE - se l'archivio chiavi master della colonna è un certificato Store.<br /><br /> Un valore definito dall'utente, se l'archivio chiavi master della colonna è di tipo personalizzato.|  
|**key_path**|**nvarchar(4000)**|Un percorso di specifiche dell'archivio di chiave master della colonna della chiave. Il formato del percorso dipende dal tipo archivio chiave master della colonna. Esempio:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> Per un archivio chiavi master della colonna personalizzata, lo sviluppatore è responsabile della definizione è il percorso di una chiave per l'archivio chiavi master della colonna personalizzata.|  
|**allow_enclave_computations**|**bit**|Indica se la chiave master della colonna è l'enclave abilitato, (se le chiavi di crittografia di colonna, crittografate con la chiave master, possono essere usate per i calcoli all'interno di zone franche sicuri sul lato server). Per altre informazioni, vedere [Always Encrypted con enclave sicuri](../../relational-databases/security/encryption/always-encrypted-enclaves.md).|  
|**signature**|**varbinary(max)**|Una firma digitale **key_path** e **allow_enclave_computations**, prodotto utilizzando la chiave master della colonna, che fa riferimento **key_path**.|


  
## <a name="permissions"></a>Permissions  
 Richiede la **VIEW ANY COLUMN MASTER KEY** l'autorizzazione.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted &#40;Motore di database&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
